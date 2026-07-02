# Spec-Driven Development Skill

[English](README.en.md) | 繁體中文

這是一個給 AI coding agent 使用的 **Spec-Driven Development (SDD)** skill。它的目的不是讓 agent 直接 vibe coding，而是先把需求、Feature 邊界、規格、架構、任務、實作與測試寫成可追蹤文件，讓任何 agent 或人類都能接手。

本 skill 目前包含三種模式：

- **Goal Mode**：整個 project/goal 全自動。先寫完所有 Feature specs，再全局規劃與批次實作。
- **Auto Mode**：單一 Feature 自動。Step 0/2/3 是主要確認點，之後自動完成。
- **Detailed Mode**：詳細手動。每一步都停下來給使用者確認。

同時內建 **Lean SDD (Lean Spec-Driven Development)**：只做最小但正確的需求、架構、任務與實作，避免過度工程，但不省略安全、驗證、資料保護、accessibility 與 spec-traced tests。

---

## 使用方法

### 1. 啟動 skill

當使用者提出類似以下需求時，agent 應使用本 skill：

- 「我想做一個 app」
- 「幫我規劃這個專案」
- 「幫我寫 PRD / spec」
- 「把這個功能拆成任務」
- 「用自動模式完成」
- 「用 goal mode 幫我整個做完」
- 「我要最小可行但完整的實作」

### 2. 一律先做 Step 0

不管使用者最後要哪個模式，都先執行 **Step 0 - Epic**，把大目標拆成 Features。

Step 0 完成後，必須詢問使用者選模式：

```text
請選擇執行模式：
- goal mode：先寫完所有 Feature specs，再全自動批次規劃與實作
- auto mode：一次處理一個 Feature，Step 2/3 確認後自動完成
- detailed mode：每一步都停下來確認
```

### 3. 依模式執行

選定模式後，agent 依照對應流程執行，並在完成後建立使用者語言的說明文件：

```text
.specify/final-explanation.md
```

如果使用者用中文提出需求，說明文件就用中文；如果使用者用英文，說明文件就用英文。

---

## 三種模式

### Goal Mode

適合整個專案或大目標，例如「幫我做一個 SaaS」、「幫我做一個遊戲」、「幫我完成整個系統」。

流程：

1. Step 0 建立 `epic.md`
2. 對所有 Features 先跑 Step 2 + Step 3，產生每個 Feature 的 `spec.md`
3. 建立 `.specify/spec-pack.md`
4. 建立 `.specify/project-blueprint.md`
5. 依 Feature dependency 順序，全自動跑 Step 4-9
6. 所有 Features 完成後建立 `.specify/final-explanation.md`

Goal Mode 的重點是：**先看完整專案需求，再開始規劃與實作**，避免前面 Feature 做完後，後面才發現 API、資料模型、模組架構要大改。

### Auto Mode

適合單一 Feature 或小型需求。

流程：

1. Step 0 建立或更新 `epic.md`
2. 使用者選 `auto mode`
3. Step 2 建立 `spec.md` 並讓使用者確認需求
4. Step 3 補齊 clarification 並讓使用者確認假設
5. Step 4-9 自動完成
6. 完成後建立或更新 `.specify/final-explanation.md`

Auto Mode 只有遇到重大風險才停下來問，例如：

- 新外部依賴或付費服務
- 破壞性 migration
- 大型重構
- 安全、權限、隱私決策
- spec 衝突且 AI 無法安全假設

### Detailed Mode

適合教學、審核、嚴格控管流程。

流程：

Step 0 到 Step 9 每一步都會停下來給使用者確認，使用者輸入 `continue` / `next` 後才進下一步。

---

## 階段說明

### Step 0 - Epic

目的：把大目標拆成可交付的 Features。

會做：

- 理解整體 project goal
- 切分 Feature
- 定義每個 Feature 的 scope / out of scope / dependency
- 排定交付順序

主要產出：

- `.specify/epic.md`

### Step 1 - Constitution

目的：建立專案治理原則。

會做：

- 定義 coding style
- 定義測試要求
- 定義安全、效能、accessibility 原則
- 定義 AI 可以自行決定什麼、什麼需要使用者核准

主要產出：

- `.specify/memory/constitution.md`

### Step 2 - Specify

目的：把單一 Feature 寫成清楚的需求規格。

會做：

- 寫 overview、problem statement、goals
- 寫 user stories
- 寫 acceptance criteria
- 寫 functional requirements
- 寫 non-goals 與 deferred scope
- 套用 Lean SDD，移除 speculative scope

主要產出：

- `.specify/specs/NNN-feature-name/spec.md`

### Step 3 - Clarify

目的：補齊模糊需求與假設。

會做：

- 找出 happy path、error states、edge cases
- 補 permissions、data lifecycle、integration 問題
- 對不確定事項做最小安全假設
- 記錄 clarifications 與 assumptions

主要產出：

- 更新 `.specify/specs/NNN-feature-name/spec.md`

### Step 4 - Checklist

目的：檢查 spec 品質。

會做：

- 檢查需求是否完整、明確、可測試
- 檢查 UX 狀態是否完整
- 檢查 API / integration 格式是否明確
- 檢查 security / permission / data handling
- 檢查 Lean SDD，找出過度工程與 speculative scope

主要產出：

- `.specify/specs/NNN-feature-name/checklists/requirements.md`
- `.specify/specs/NNN-feature-name/checklists/ux.md`
- `.specify/specs/NNN-feature-name/checklists/api.md`
- `.specify/specs/NNN-feature-name/checklists/security.md`
- `.specify/specs/NNN-feature-name/checklists/minimalism.md`

### Step 5 - Plan

目的：把 spec 轉成專案藍圖與技術計畫。

會做：

- 建立 Project Structure
- 建立 Module Map
- 建立 Workflow Map
- 設計 API contracts
- 設計 workflow stage contracts
- 設計 data model
- 決定 tech stack
- 用 Lean Planning Ladder 避免不必要模組、依賴與抽象

主要產出：

- `.specify/specs/NNN-feature-name/plan.md`
- `.specify/specs/NNN-feature-name/data-model.md`（需要資料模型時）
- `.specify/specs/NNN-feature-name/research.md`（需要技術研究時）
- `.specify/specs/NNN-feature-name/contracts/`（需要 API / event / workflow contracts 時）

### Step 6 - Analyze

目的：跨文件一致性檢查。

會做：

- 檢查 spec 是否都有 plan 對應
- 檢查 plan 是否有無需求支撐的 orphan components
- 檢查 data model 是否覆蓋需求
- 檢查 API / workflow contracts 是否完整
- 檢查 Module Map / Workflow Map 是否完整
- 檢查 Lean SDD 違規，例如單一實作 interface、無需求 cache、不必要 dependency

主要產出：

- `.specify/specs/NNN-feature-name/analysis.md`

### Step 7 - Tasks

目的：把 plan 拆成可執行任務。

會做：

- 依 Module Map 分組
- 依 Workflow Map 分組
- 每個 task 都要對應 requirement / module / workflow / contract / data
- 做 Task Pruning Pass，刪除 speculative scaffolding

主要產出：

- `.specify/specs/NNN-feature-name/tasks.md`

### Step 8 - Implement

目的：依 tasks.md 實作。

會做：

- 先讀 Project Structure / Module Map / Workflow Map
- 在正確模組與資料夾中實作
- 重用既有 codebase patterns
- 避免未核准新 dependency
- 避免單一實作 abstraction
- 完成 task 後標記 `[DONE]`

主要產出：

- 實際程式碼變更
- 更新 `.specify/specs/NNN-feature-name/tasks.md`
- 必要時更新 `plan.md` 的 Implementation Notes

### Step 9 - Test

目的：用測試驗證 implementation 是否符合 spec。

會做：

- 建立 acceptance criteria coverage map
- 撰寫 unit / integration / acceptance tests
- 跑測試
- 修復 failing tests
- 更新 epic feature status

主要產出：

- `.specify/specs/NNN-feature-name/test-report.md`
- 完成範圍時建立或更新 `.specify/final-explanation.md`

---

## Goal Mode 專案級文件

### `.specify/spec-pack.md`

用途：Goal Mode 的跨 Feature 規格總覽。

包含：

- 每個 Feature spec 狀態
- 跨 Feature 決策
- 共用角色、資料、流程、contracts
- 衝突與解法
- deferred scope
- execution order

### `.specify/project-blueprint.md`

用途：Goal Mode 的全局專案藍圖。

包含：

- 全局 Project Structure
- Global Module Map
- Global Workflow Map
- Shared Data Model
- Shared Contracts
- Execution Plan

### `.specify/final-explanation.md`

用途：給使用者看的完成說明。

包含：

- 完成內容
- 如何使用
- 主要功能
- 專案結構
- 測試結果
- 延後範圍
- 後續建議

---

## Lean SDD 原則

Lean SDD = **Lean Spec-Driven Development**。

核心規則：

1. 現在不需要的，不做
2. codebase 已經有的，重用
3. native / stdlib 能解的，不自造
4. 已安裝 dependency 能解的，不新增 dependency
5. 一個既有 module 能負責的，不新增 module
6. 一個清楚 task / contract 能描述的，不拆成 ceremony
7. 只有在 spec 真的需要時，才新增架構、依賴、任務或程式碼

但不能省略：

- trust-boundary validation
- auth / authorization
- security controls
- data-loss protection
- migration safety
- accessibility basics
- spec-traced tests

---

## Skill 檔案結構

```text
.
|-- README.md
|-- LICENSE
|-- .gitignore
|-- .gitattributes
`-- spec-driven-development/
    |-- SKILL.md
    |-- references/
    |   |-- goal-mode.md
    |   |-- step0-epic.md
    |   |-- step1-constitution.md
    |   |-- step2-specify.md
    |   |-- step3-clarify.md
    |   |-- step4-checklist.md
    |   |-- step5-plan.md
    |   |-- step6-analyze.md
    |   |-- step7-tasks.md
    |   |-- step8-implement.md
    |   `-- step9-test.md
    `-- templates/
        |-- constitution-template.md
        |-- spec-template.md
        |-- plan-template.md
        `-- tasks-template.md
```

---

## Attribution

Some workflow concepts reference [github/spec-kit](https://github.com/github/spec-kit).

## License

MIT. See [LICENSE](LICENSE).
