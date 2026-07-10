# 實驗室技能庫草案 Skill Library Draft

> **怎麼編輯這份清單**
> - 每一列＝一項獨立技能。直接增刪列、改文字即可，改完告訴 Claude「依 SKILLS.md 實作」。
> - **必備**欄打 ★ 的是該階段升級前必須完成的核心技能；空白＝一般項。
> - **維度**：技能＝研究技能、專案＝專案進度、事務＝實驗室事務。
> - **領域**：通用＝所有人；AI／DSP／動物＝只有選該領域的學生會看到。
> - 「實驗技能模組」段落的技能不綁階段，綁**實驗類型**——學生參與哪種實驗（或專案掛載哪個模組）才會出現。

---

## 一、階段技能總表（依學制年資自動分配）

### 大學部 U1 入門期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 事務 | 通用 | 完成實驗室安全與環境訓練 | Complete lab safety & environment training |
| ★ | 事務 | 通用 | 建立實驗記錄本／開發日誌，每次都記錄 | Keep a lab notebook / dev log and record every session |
| ★ | 技能 | 通用 | 讀懂 1 篇指定文獻並口頭摘要 | Read 1 assigned paper and give an oral summary |
|   | 技能 | 通用 | 正確引用文獻、了解抄襲界線 | Cite sources correctly; understand plagiarism boundaries |
| ★ | 專案 | 通用 | 能說明所屬專案的目標與動機 | Explain your project's goal and motivation |
| ★ | 技能 | 動物 | 完成動物實驗倫理(IACUC)訓練，熟讀飼養 SOP | Complete IACUC training; know the husbandry SOP well |
| ★ | 技能 | 動物 | 在學長姊指導下正確操作基本實驗（保定、餵飼、清潔） | Perform basic animal procedures under supervision (restraint, feeding, cleaning) |
| ★ | 技能 | AI | 完成 Python 環境建置，跑通一份範例訓練程式 | Set up Python; run a sample training script |
| ★ | 技能 | DSP | 完成訊號擷取環境建置，讀入並畫出一段訊號 | Set up signal acquisition; load and plot a signal |

### 大學部 U2 上手期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能獨立完成核心技術並產出可重現數據 | Run core techniques independently with reproducible data |
| ★ | 技能 | 通用 | 會使用實驗室文獻／知識庫查資料 | Use the lab literature / knowledge base |
|   | 技能 | 通用 | 能把原始數據整理成可分析格式（試算表／程式） | Organize raw data into analyzable form |
| ★ | 專案 | 通用 | 負責專案中一個明確子任務 | Own a well-defined subtask in a project |
| ★ | 事務 | 通用 | 主動回報卡關，週報準時 | Report blockers proactively; weekly updates on time |
| ★ | 技能 | AI | 獨立完成一輪資料前處理→訓練→評估，並用 git 管理程式 | Complete a preprocess→train→evaluate cycle; use git |
| ★ | 技能 | DSP | 實作一種濾波／特徵抽取並驗證結果 | Implement a filter / feature extraction and validate it |
| ★ | 技能 | 動物 | 獨立執行飼養與基本取樣／量測，符合動物福祉規範 | Handle husbandry and basic sampling/measurement per welfare rules |

### 大學部 U3 專題期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能做小範圍文獻回顧（3–5 篇） | Conduct a small literature review (3–5 papers) |
| ★ | 技能 | 通用 | 能對自己數據做基本統計與判讀（敘述統計、t 檢定） | Basic statistics & interpretation (descriptive stats, t-test) |
| ★ | 專案 | 通用 | 獨立負責一個小子題並整理成果 | Own a small sub-topic and compile the results |
| ★ | 專案 | 通用 | 完成專題書面報告與海報／口頭報告 | Finish the capstone report and poster / oral presentation |
| ★ | 事務 | 通用 | 記錄本／程式可供後人接手 | Notebook / code ready for handover |
|   | 技能 | AI | 模型結果可重現（固定隨機種子、記錄超參數與版本） | Reproducible model results (seeds, hyperparameters, versions) |
|   | 技能 | DSP | 能對訊號處理流程做量化評估（如 SNR／準確率） | Quantitative evaluation of the signal pipeline (SNR / accuracy) |
|   | 技能 | 動物 | 能獨立完成一次完整實驗流程並記錄異常處理 | Run a full experiment independently; log anomaly handling |

### 碩士 G1 定位期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 完成題目文獻回顧，能畫出研究缺口 | Literature review; map the research gap |
| ★ | 技能 | 通用 | 能提出可驗證的研究假說 | Formulate a testable hypothesis |
| ★ | 技能 | 通用 | 掌握所屬領域全部核心技術 | Master all core techniques of your track |
| ★ | 專案 | 通用 | 完成背景綜整草稿與 proposal 雛形 | Draft the background synthesis and proposal outline |
| ★ | 事務 | 通用 | 數據／程式命名與版本符合實驗室規範 | Data / code naming and versioning follow lab conventions |
|   | 技能 | AI | 建立可重現的訓練 pipeline（資料版本、實驗追蹤） | Reproducible training pipeline (data versioning, experiment tracking) |
|   | 技能 | DSP | 能設計完整訊號處理流程並說明每一步依據 | Design a full signal chain and justify each step |
|   | 技能 | 動物 | 能規劃動物實驗分組與樣本數（含倫理考量） | Plan animal groups & sample sizes (incl. ethics) |

### 碩士 G2 建置期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能設計實驗：對照組、辨識與控制變因 | Design experiments: controls, identify & manage variables |
| ★ | 技能 | 通用 | 會做基礎統計檢定並正確解讀（ANOVA、迴歸等） | Run and interpret statistical tests (ANOVA, regression) |
|   | 技能 | 通用 | 能用統計軟體／程式完成分析（R／Python／SPSS） | Analyze data with statistical software (R / Python / SPSS) |
| ★ | 專案 | 通用 | proposal 定稿；建立實驗／開發系統 | Finalize the proposal; build the experiment / dev system |
| ★ | 專案 | 通用 | 產出初步或預試數據 | Produce preliminary / pilot data |
| ★ | 事務 | 通用 | 開始帶 1 位大學部 | Start mentoring one undergraduate |
|   | 技能 | AI | 完成 baseline 模型並有可比較的評估指標 | Baseline model with comparable metrics |
|   | 技能 | DSP | 完成訊號採集到分析的端到端 prototype | End-to-end prototype from acquisition to analysis |
|   | 技能 | 動物 | 完成預試(pilot)並依結果調整方案 | Finish the pilot study; adjust the plan |

### 碩士 G3 產出期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能將結果與文獻對照、寫出 discussion 論點 | Contrast results with literature; write discussion points |
|   | 技能 | 通用 | 能製作出版等級的圖表 | Produce publication-quality figures |
| ★ | 專案 | 通用 | 主要結果產出 | Produce the main results |
| ★ | 專案 | 通用 | 完成期中報告；投研討會摘要或海報 | Mid-term report; conference abstract or poster |
| ★ | 事務 | 通用 | 組會能主持自己題目的討論 | Lead your topic's discussion in group meeting |
|   | 技能 | AI | 完成消融／比較實驗，結果具統計意義 | Ablation / comparison experiments with significance |
|   | 技能 | DSP | 演算法在真實資料上驗證並量化效能 | Validate on real data with quantified performance |
|   | 技能 | 動物 | 完成正式實驗批次，數據品質達可分析標準 | Formal experiment batches with analysis-grade data |

### 碩士 G4 收束期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能獨立完成論文各章 | Write thesis chapters independently |
| ★ | 技能 | 通用 | 能回應審查／口委意見 | Respond to reviewer / committee comments |
| ★ | 專案 | 通用 | 論文撰寫與口試 | Thesis writing and oral defense |
|   | 專案 | 通用 | 投稿論文／專利／委託案結案 | Submit a paper / patent, or close an industry project |
| ★ | 事務 | 通用 | 完整交接（記錄、原始數據、SOP）給接手者 | Full handover (notes, raw data, SOPs) |

### 博士 D1 探索期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能自行提出研究方向與假說 | Propose research directions and hypotheses independently |
| ★ | 技能 | 通用 | 獨立完成完整文獻回顧與研究計畫書片段 | Full literature review and grant-proposal sections |
| ★ | 專案 | 通用 | 確立博士論文主軸與第一個子計畫 | Fix the PhD thesis axis and first sub-project |
| ★ | 事務 | 通用 | 穩定指導碩士／大學部日常研究 | Regularly mentor master / undergrad students |

### 博士 D2 深化期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能設計一整套實驗／開發策略 | Design a complete experimental / development strategy |
| ★ | 專案 | 通用 | 產出第一作者論文 | Publish a first-author paper |
|   | 專案 | 通用 | 主導一個委託案 | Lead an industry-commissioned project |
| ★ | 事務 | 通用 | 成為某項技術的實驗室內部負責人 | Become the lab's point person for a technique |

### 博士 D3 領導期

| 必備 | 維度 | 領域 | 技能 | English |
|---|---|---|---|---|
| ★ | 技能 | 通用 | 能協助審稿或撰寫計畫書 | Assist with peer review or grant writing |
|   | 專案 | 通用 | 第二篇第一作者論文／重要成果 | Second first-author paper / major output |
| ★ | 事務 | 通用 | 建立或維護實驗室某項 SOP 與訓練新人 | Establish/maintain a lab SOP; train newcomers |
|   | 事務 | 通用 | 能規劃與管理實驗室資源（耗材、儀器、時程） | Plan and manage lab resources (supplies, equipment, schedule) |

---

## 二、實驗技能模組（依參與的實驗／專案分配，不綁階段）

> 這是「參與不同實驗需要不同技能」的部分：每個模組對應一種實驗類型，
> 專案掛載模組後，參與該專案的學生清單會自動出現這些技能。
> 模組與內容都可以自由增刪，以下先依實驗室常見實驗草擬四個。

### 模組 A：動物採樣實驗 Animal Sampling

| 必備 | 技能 | English |
|---|---|---|
| ★ | 血液／體液採樣與樣本前處理 | Blood / fluid sampling and sample preparation |
| ★ | 生理數據量測（體溫、體重、心跳等） | Physiological measurements (temp, weight, heart rate) |
| ★ | 樣本編號、記錄與冷鏈保存 | Sample labeling, records and cold-chain storage |
|   | 採樣異常（動物緊迫等）的辨識與處置 | Recognize and handle sampling anomalies (animal stress) |

### 模組 B：聲音／訊號採集實驗 Audio & Signal Acquisition

| 必備 | 技能 | English |
|---|---|---|
| ★ | 錄音／感測設備架設與校正 | Set up and calibrate recording / sensing equipment |
| ★ | 依 SOP 完成現場採集並記錄環境條件 | Follow the acquisition SOP; log field conditions |
| ★ | 音檔／訊號檔案的整理與標註 | Organize and annotate audio / signal files |
|   | 採集品質即時檢查（雜訊、斷訊） | On-site quality checks (noise, dropouts) |

### 模組 C：AI 模型開發 AI Model Development

| 必備 | 技能 | English |
|---|---|---|
| ★ | 資料標註與標註品質控管 | Data annotation and annotation QC |
| ★ | 模型訓練、調參與實驗記錄 | Model training, tuning and experiment logging |
| ★ | 評估指標選擇與結果報告 | Choose evaluation metrics; report results |
|   | 模型交付／部署（打包、文件） | Model delivery / deployment (packaging, docs) |

### 模組 D：牧場／田間調查 Farm & Field Study

| 必備 | 技能 | English |
|---|---|---|
| ★ | 調查表／記錄表設計與試填 | Design and pilot survey / record sheets |
| ★ | 現場資料收集與當日回傳整理 | Collect field data; same-day upload and tidy-up |
|   | 與場方人員溝通協調 | Communicate and coordinate with farm staff |
