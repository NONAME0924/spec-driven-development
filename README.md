# Spec-Driven Development Skill

[English](README.en.md) | 繁體中文

**Lean SDD（Lean Spec-Driven Development）** 是給 AI coding agent 使用的規格驅動開發工作流程。它把需求、模組、流程、介面、任務與驗證連起來，讓產出具有完整的專案結構，同時避免不必要的文件與架構。

支援 Goal、Auto、Detailed 三種模式。這次已依 GPT-6 Astra 官方指南調整指令，但不綁定模型或修改你的模型設定。[最佳化說明](docs/astra-review.md)

## 使用方法

將本倉庫的 `spec-driven-development/` 作為一個 skill 安裝至使用工具支援的 skill 目錄；入口是大寫的 `SKILL.md`。已安裝時，可在支援的 agent 中明確呼叫：

```text
請使用 $spec-driven-development，幫我規劃並完成一個支出管理工具。
需要 CSV 匯入及每月統計，沿用目前專案技術。
```

提供目標、必要功能、限制，以及你要「只有文件」還是「包含實作」。一般小修正、程式解釋、code review 或維護 skill 本身，不會自動被要求走完整 SDD。

1. Agent 先檢查既有專案，再以 Step 0 建立或更新 Feature 拆分。
2. 拆分完成後，詢問你選 Goal、Auto 或 Detailed 模式。
3. 依選定模式處理，完成後以你的語言產生 `.specify/final-explanation.md`。

若一開始已選模式，Step 0 只確認拆分與該模式，不重問選項。你也可以明確要求略過這次確認。續作時沿用已記錄的模式、核准與有效文件。

```text
使用 Goal 模式，Step 0 拆分後直接繼續，不需要再次確認。
先完成所有 Feature specs，再統一規劃與實作。
```

只需要規格時：

```text
使用 Goal 模式，略過初始確認。
只完成預約系統的全部 specs 與跨規格對齊，不要實作。
```

## 三種模式

| 模式 | 適用範圍 | 確認點 | 後續執行 |
|------|----------|--------|----------|
| Goal | 整個專案 | Step 0 拆分與模式 | 全部 specs 先完成、對齊，再全局規劃與批次實作 |
| Auto | 選定的單一 Feature | Step 0、Step 2、Step 3 | Step 3 核准後自動完成 Step 4–9 |
| Detailed | 選定的單一 Feature，需要詳細說明 | Step 0、Step 2、Step 3 | 其餘階段自動完成，詳細呈現產出、判斷與驗證 |

Auto 與 Detailed 的 Step 2、3 預設分開確認；你可明確要求合併或略過。Detailed 的差別是說明較詳細，不是多設確認關卡：Step 1、4–9 都自動執行，不會因為呈現階段報告而等待回覆。

三種模式涉及無法合理推斷的核心需求或超出既有授權的動作才另外詢問。Step 8 超出授權的大改仍需確認；一般實作、設計調整或測試修復則自動處理。Goal 會自行處理一般假設。

「自動」仍以你要求的範圍為界；只要 specs 的請求不會一路變成實作，也不會為了宣布完成而偷偷刪除需求。

## 每個階段做什麼

下表的 Feature 文件均位於 `.specify/specs/NNN-feature-name/`。

| 階段 | 主要輸入 | 工作與產出 | 文件用途 |
|------|----------|------------|----------|
| [0 Epic](spec-driven-development/references/step0-epic.md) | 目標、現有專案 | `.specify/epic.md` | Feature 邊界、依賴、交付順序、模式及續作狀態 |
| [1 Constitution](spec-driven-development/references/step1-constitution.md) | 使用者限制、repo 指引與設定 | 重用或建立 `.specify/memory/constitution.md` | 跨 Feature 共用約束及來源；不憑空增加治理規定 |
| [2 Specify](spec-driven-development/references/step2-specify.md) | Feature 範圍 | `spec.md` | 使用者需求、非目標、可觀察的驗收條件與穩定 AC 編號 |
| [3 Clarify](spec-driven-development/references/step3-clarify.md) | 草稿規格、現有行為 | 更新 `spec.md` | 記錄回答、假設、依據及真正阻塞問題 |
| [4 Checklist](spec-driven-development/references/step4-checklist.md) | 澄清後規格 | `checklists/requirements.md` | 檢查完整、明確、一致與可驗證性 |
| [5 Plan](spec-driven-development/references/step5-plan.md) | 規格、repo、Goal 全局藍圖 | `plan.md` 及必要附屬文件 | 決定程式放哪裡、誰負責、流程怎麼串、介面格式與驗證方法 |
| [6 Analyze](spec-driven-development/references/step6-analyze.md) | 規格與技術設計 | `plan.md` 的 Analysis 區塊；複雜時拆為 `analysis.md` | 檢查需求、模組、資料、contracts 是否互相對得上 |
| [7 Tasks](spec-driven-development/references/step7-tasks.md) | 一致的計畫 | `tasks.md` | 依模組與流程分組，列出實際路徑、依賴及完成條件 |
| [8 Implement](spec-driven-development/references/step8-implement.md) | 規格、計畫、任務、程式 | 程式與適量測試，更新任務與計畫 | 實作可用結果，逐步驗證；一般實作不另行停問 |
| [9 Verify](spec-driven-development/references/step9-test.md) | 驗收條件、實作、測試環境 | `test-report.md`、更新 epic | 以實際證據確認結果，區分通過、失敗、未執行及阻塞 |

階段的目的保留，但有效文件可以重用，小型檢查可以合併處理。模板的欄位與範例不代表每次都要建立一樣的層級或檔案。

## UX、API 與其他文件

| 文件 | 什麼時候需要 | 主要內容 |
|------|--------------|----------|
| `checklists/ux.md` | UX 檢查值得獨立成檔 | 使用者流程與適用的 loading／empty／error／success 狀態、可及性 |
| `checklists/api.md` | 存在值得獨立檢查的整合介面 | 操作、權限、外部輸入輸出期待與相容性要求 |
| `checklists/security.md` | 功能涉及實際資料或存取風險 | 信任邊界、敏感資料、權限需求 |
| `checklists/minimalism.md` | 精簡檢查需要獨立紀錄 | 非必要範圍、重複規定與推測性複雜度 |
| `data-model.md` | 資料設計細節超出簡短 plan | 資料擁有者、欄位型別、必填、驗證、關聯、生命週期與遷移影響 |
| `research.md` | 有影響決策的技術未知事項 | 問題、官方來源、版本／日期、結論與未解問題 |
| `contracts/api-spec.json` | 需要新的 HTTP API schema | OpenAPI request／response／error schema、狀態碼與 auth |
| `contracts/events.md` | 有事件或訊息邊界 | producer／consumer、訊息 schema、傳遞與失敗語意 |
| `contracts/workflows.md` | API schema 無法完整表達多階段流程 | 各階段 owner、輸入格式、輸出格式、狀態變更及失敗輸出 |

小型領域檢查可以放在 `requirements.md` 的章節中，不必產生五份空表格。既有 API schema、資料定義保留原位置並用連結引用，避免兩份定義漂移。

**UX/API checklist 是需求品質檢查；實際介面格式在 Step 5 的 contracts。** 輸入輸出需有欄位、型別、必填／可選／null、驗證規則與錯誤格式；不能只有 JSON 範例。多階段 API、CLI、event、job 或 agent pipeline 都能用 workflow contracts 描述。

## Goal 的全局流程

```text
Step 0：拆分與模式確認
  -> Step 1：重用／建立共用原則
  -> 全部 Features 的 Step 2 + 3
  -> spec-pack 對齊 + 全部規格的 Step 4
  -> project-blueprint 全局技術規劃
  -> 各 Feature 的 Step 5–9
  -> 跨 Feature 整合驗證
  -> 使用者語言的完成說明
```

| 專案級文件 | 用途 |
|------------|------|
| `.specify/spec-pack.md` | 全部規格的索引、共用概念、跨規格決策、依賴順序與整合驗證證據 |
| `.specify/project-blueprint.md` | 全局資料夾結構、模組責任、流程、共用 contracts／data 的正式位置、實作順序 |
| `.specify/final-explanation.md` | 完成內容、使用方法、主要檔案、驗證結果與限制；只做文件時明確說明未實作 |

只有依賴與檔案擁有權允許時才平行工作。共用 contract 改變時，重新對齊受影響規格與設計；不重跑無關 Features。Feature 各自通過後，還要驗證整個專案串起來的流程。

## Lean SDD 與驗證

優先重用既有模組、平台能力與合適函式庫。有真實需求或框架邊界時才新增抽象，單一實作不再自動被判錯。保留必要的資料保護、權限檢查、可及性與驗證。

測試依修改風險安排：重用有效測試，改變重要行為時補測試；低風險文件可用檢查或可重現手動驗證。每個驗收條件要有適合的證據，未執行不能算通過。必要檢查通過後，只有新修改或未解疑慮才擴大測試。

## 維護與官方依據

- [AGENTS.md](AGENTS.md)：維護本 skill 倉庫的簡短指引。
- [SKILL.md](spec-driven-development/SKILL.md)：共用規則與階段入口。
- `references/`：按目前階段載入；`templates/`：按需使用。
- [Astra 審查與改善](docs/astra-review.md)：變更原因、依據與效果限制。
- [工作流程評估案例](docs/workflow-evaluation.md)：核准、範圍、續作及驗證情境。

官方參考：[GPT-6 Astra 指南](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra)、[Build skills](https://learn.chatgpt.com/docs/build-skills)、[AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)。查閱日期：2026-09-05。

## Attribution

工作流程概念參考 [github/spec-kit](https://github.com/github/spec-kit)；Lean SDD 吸收 [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) 的精簡與避免過度工程概念，依本流程需求改寫。

## License

MIT。見 [LICENSE](LICENSE)。
