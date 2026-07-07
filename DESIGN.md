# ANG Lab 研究室進度儀表板 — 設計文件

> ANG Lab Progress Dashboard — Design Document
>
> 線上網址:https://chaowei0712.github.io/ang-lab-tracker/
> 程式庫:https://github.com/ChaoWei0712/ang-lab-tracker
> 資料庫後台:https://console.firebase.google.com/project/ang-lab-tracker/firestore

---

## 1. 系統概觀

單一 `index.html` 檔案的網頁應用程式,不需要後端伺服器:

- **前端**:純 HTML/CSS/JavaScript,無框架、無建置流程
- **托管**:GitHub Pages(push 到 `main` 分支後 1–2 分鐘自動部署)
- **資料庫**:Google Firebase Firestore(專案 ID:`ang-lab-tracker`),透過 REST API 直接讀寫
- **使用對象**:實驗室老師(PI)與學生,全實驗室共享同一份雲端資料

### 四大功能模組

| 模組 | 分頁名稱 | 用途 |
|---|---|---|
| 檢核項 | 我的檢核 My Checklist | 依年資階段列出應達成項目,打勾追蹤達成率 |
| 專案 | 我的專案 My Projects | 專案卡片:管線站點、狀態、里程碑、期限、卡點 |
| 週報 | 週報進度 Weekly Updates | 每週回報:狀態、完成事項、卡點、下週計畫 |
| 總覽 | 全實驗室總覽 Lab Overview | 老師視角:全體學生進度、卡關與週報警示 |

另有「使用說明 Guide」分頁(中英雙語操作教學)。

---

## 2. 設計流程(開發歷程)

依 git 版本紀錄整理,每一步都經過本機實測後才部署:

### 第 1 步:建立基本應用(`d763e4b`)
- 單檔網頁應用,含檢核清單、專案板、週報時間軸、PI 總覽
- 年資分級:大學部 U1–U3、碩士 G1–G4、博士 D1–D3,各階段有預設檢核項
- 三大領域(tracks):AI 開發、訊號處理、動物飼養
- 通行碼閘門保護

### 第 2 步:修復通行碼問題(`b1f1e1b`、`66293f6`、`94dea0b`)
- 發現探測文件 ID `__gate_probe__` 是 Firestore 保留格式,驗證永遠失敗(HTTP 400)
- 改名為 `gate_probe`;`LAB_PASSCODE` 清空避免原始碼洩露密碼
- 最終決定改為免密碼直接使用,Firestore 規則開放 `labkv` 集合讀寫

### 第 3 步:雙語化與自訂領域(`3d3d039`)
- 全站中英對照:標題、分頁、所有檢核項、表單、狀態、表格
- 標題加入英文 "ANG Lab Progress Dashboard"
- 負責領域可自行新增(存入共享資料庫,全實驗室可選用,自動配色)
- 新增「使用說明 Guide」分頁

### 第 4 步:週報選項化(`bdfff7e`)
- 本週狀態四選一:順利/稍有落後/卡關/需要討論(彩色標籤)
- 關聯專案下拉選單(只列自己的專案)
- 下週計畫改為從「未完成檢核項+專案里程碑」勾選,依個人進度安排
- 修 bug:身分選擇改存本機 localStorage,避免全實驗室互相覆蓋

### 第 5 步:模組交互連動(`547e8b2`)
- 週報回報「已完成」的計畫 → 對應檢核項自動打勾、更新達成率
- 週報選「卡關」+關聯專案 → 專案自動標卡關並回填卡點;回報「順利」自動解除
- 專案卡片顯示該專案最近一次週報的日期與狀態標籤

### 第 6 步:結構化資料庫(`4206f6e`)
- 原本所有資料壓成 JSON 字串存在少數幾份文件,後台無法查詢
- 改為「一筆記錄=一份文件」,欄位對應輸入格(詳見第 4 節)
- 舊資料自動搬移,舊格式文件保留作備份

### 第 7 步:待辦計畫延續(`dee6d8c`)
- 下週計畫改為持續追蹤的待辦清單(`plans_<學生id>` 文件)
- 未勾選完成的項目自動延續到下一次週報,勾選「已完成」送出後才移除
- 可按 × 直接移除(更改計畫);挑選區自動排除已在追蹤中的項目
- 勾完成時照樣自動同步檢核項打勾

---

## 3. 模組交互關係圖

```
檢核項 ←──自動打勾──────┐
   │                     │
   └─未完成項目────→ 週報「下週計畫」勾選
                         │
專案里程碑 ──────────────┘
   ↑
   ├─卡關連動(狀態+卡點)── 週報「本週狀態」
   └─卡片顯示最新週報日期+狀態標籤
                         │
全實驗室總覽 ←─狀態標籤+紅字警示─┘
```

- 紅字警示條件:專案卡關、或超過 9 天沒有更新週報
- 升級門檻:單一年資檢核項達成 ≥ 80%,由老師於學期評核確認

---

## 4. 資料庫結構(Firestore)

集合:`labkv`,每份文件有 `type` 欄位供查詢篩選。

| 文件 ID 格式 | type | 欄位 |
|---|---|---|
| `student_<id>` | `student` | name, level, tier, tracks[] |
| `project_<id>` | `project` | owner, name, stage, status, milestone, deadline, blocker, links[] |
| `log_<id>` | `log` | owner, date, mood, project, plan[], planDone[], done, block, next, link |
| `checklist_<學生id>` | `checklist` | owner, checks{檢核項id: 布林} |
| `customchecks_<學生id>` | `customchecks` | owner, items[{id, dim, t}] |
| `plans_<學生id>` | `plans` | owner, items[{id, t, added}](待辦計畫,完成即移除) |
| `track_<id>` | `track` | label, short, color |
| `lab_students` 等 | (無) | 舊版 JSON 格式,保留作備份 |

### 常用查詢範例(Firebase Console → 查詢建立工具)

- 所有週報:`type == log`
- 某學生的週報:`type == log` 且 `owner == <學生id>`
- 卡關中的專案:`type == project` 且 `status == blocked`

### 欄位值代碼對照

- `level`:undergrad(大學部)/ master(碩士)/ phd(博士)
- `tier`:U1–U3 / G1–G4 / D1–D3
- `mood`(週報狀態):ok(順利)/ behind(稍有落後)/ blocked(卡關)/ discuss(需要討論)
- `status`(專案):todo / active / blocked / review / done
- `stage`(管線):文獻 → 背景 → 方法 → 實驗設計 → 結果討論

---

## 5. 儲存層設計

程式碼中的三層自動切換(`index.html` 內 storage adapter 區段):

1. **Claude 平台**:`window.storage`(整包 JSON)
2. **自行部署 + `FIREBASE_PROJECT` 已設定**:Firestore REST API,結構化文件
3. **兩者皆無**:localStorage(僅本機示範用)

重點函式:

- `dbLoadAll()`:列出整個 `labkv` 集合(分頁),依 `type` 分派到記憶體狀態
- `dbSaveStudent / dbSaveProject / dbSaveLog / dbSaveChecklist / dbSaveCustomChecks / dbSaveTrack`:單筆寫入
- `migrateLegacy()`:偵測到沒有結構化資料但有舊 JSON 時,自動搬移(一次性)
- 個人設定(目前身分 `lab_me`)存 localStorage,不進雲端,避免互相覆蓋

Firestore 安全規則(現行):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /labkv/{doc} {
      allow read, write: if true;
    }
  }
}
```

> 注意:目前資料庫完全開放,任何知道專案 ID 的人都可讀寫。實驗室內部工具可接受;若要加回通行碼,把 `index.html` 第 411 行 `LAB_PASSCODE` 填入密碼即可重新啟用閘門(規則同步改回 gate 驗證)。

---

## 6. 修改與部署流程

```bash
# 1. 編輯 index.html 後存檔(Cmd+S)
git add index.html
git commit -m "說明這次改了什麼"
git push
# 2. 等 1–2 分鐘 GitHub Pages 自動部署
# 3. 瀏覽器 Cmd+Shift+R 強制重新整理
```

驗證習慣:

- 改完先跑 `node --check` 確認 JS 語法
- 本機 `python3 -m http.server` 起伺服器實測(測試時攔截 `saveKey`/`dbSave*`,避免測試資料寫進真實資料庫)
- push 後用 `curl` 確認 GitHub Pages 已部署新版

---

## 7. 已知事項與待辦

- [x] 待辦計畫延續功能:已完成並部署(`dee6d8c`)
- [ ] 舊版 `lab_*` JSON 備份文件可在確認穩定後手動刪除
- [ ] 自訂領域目前只能新增、不能刪除
- [ ] 自訂檢核項只有單語(無中英對照欄位)
- 資料庫為完全開放讀寫,如需保護可重新啟用通行碼(見第 5 節)
