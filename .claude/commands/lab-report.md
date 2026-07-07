---
description: 產出實驗室或特定學生的 AI 進度摘要報告(存成可編輯的 .md + .docx)
argument-hint: [學生姓名,留空=全實驗室總報告]
---

為 ANG Lab 研究室進度儀表板產出 AI 摘要報告。使用者指定的對象:$ARGUMENTS(若為空,產出全實驗室報告)。

## 步驟

### 1. 抓取資料

從 Firestore 讀取全部資料(公開讀取,無需金鑰):

```bash
curl -s 'https://firestore.googleapis.com/v1/projects/ang-lab-tracker/databases/(default)/documents/labkv?pageSize=300'
```

若回傳含 `nextPageToken`,用 `&pageToken=<token>` 續抓。依每份文件的 `fields.type.stringValue` 分類:

| type | 內容 | 重要欄位 |
|---|---|---|
| `student` | 學生 | name, level, tier, tracks[](文件 ID 去掉 `student_` 前綴=學生 id) |
| `project` | 專案 | owner, name, stage, status, milestone, deadline, blocker |
| `log` | 週報 | owner, date, mood, project, plan[], planDone[], done, block, next |
| `checklist` | 檢核勾選 | owner, checks{檢核項id:布林} |
| `customchecks` | 自訂檢核項 | owner, items[{id,dim,t}] |
| `plans` | 待辦計畫 | owner, items[{id,t,added}] |

沒有 `type` 欄位的文件(`lab_students` 等)是舊備份,忽略。

### 2. 代碼對照

- level:undergrad=大學部、master=碩士、phd=博士
- tier:U1 入門期/U2 上手期/U3 專題期/G1 定位期/G2 建置期/G3 產出期/G4 收束期/D1 探索期/D2 深化期/D3 領導期
- mood:ok=順利、behind=稍有落後、blocked=卡關、discuss=需要討論
- 專案 status:todo=未開始、active=進行中、blocked=卡關、review=待審、done=完成
- 檢核項維度 dim:skill=研究技能、project=專案進度、citizen=實驗室成員
- 各年資的預設檢核項定義在 `index.html` 的 `CHECKS` 常數(依 checklist 的勾選 id 對照出項目文字);達成率=已勾/(該年資可見項目+自訂項目)
- 升級門檻:達成率 ≥ 80%

### 3. 產出報告

**特定學生**(依 $ARGUMENTS 用姓名比對,找不到時列出所有學生姓名請使用者選):

1. **基本資料**——姓名、學制年資階段、負責領域
2. **檢核進度**——三維度達成率、距離 80% 升級門檻還差哪些項目(列出未完成項)
3. **專案現況**——每個專案的站點/狀態/里程碑/期限/卡點
4. **週報回顧**——按時間列出重點;分析 mood 趨勢(連續卡關?多久沒交?)
5. **待辦計畫**——目前追蹤中的項目,標注加入日期(擱置超過 14 天特別標記)
6. **AI 觀察與建議**——最重要的一節,要具體可執行:
   - 進度評估(相對年資階段的預期,超前/符合/落後)
   - 風險提醒(卡關、長期未動的計畫、週報中斷)
   - 給學生的下一步建議(3–5 點,具體到可以直接做)
   - 給老師的建議(需要介入或討論的點)

**全實驗室**(無參數):總覽表(每人一列:年資/達成率/專案數/卡關/最新週報)→ 每位學生 3–5 行短評 → 實驗室層級觀察(共同卡點、需要開會討論的事項)。

### 4. 存檔(可編輯文件)

存到專案的 `reports/` 資料夾(已加入 .gitignore,不會公開到 GitHub):

```bash
mkdir -p reports
# 1. Markdown 版(可編輯)
#    reports/<對象>_<YYYY-MM-DD>.md
# 2. Word 版:先產生同內容的 HTML(含 <meta charset="utf-8">,標題/表格用標準標籤),再:
textutil -convert docx reports/<對象>_<日期>.html -output "reports/<對象>_<日期>.docx"
# 轉完刪掉中間的 .html
```

完成後告訴使用者兩個檔案的完整路徑,並附上報告的重點摘要(3–5 句)。
