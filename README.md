# Spec-Driven Development Skill

[English](#english) | [中文](#中文)

## English

[Jump to 中文](#中文)

A reusable AI skill for creating specs from a structured project development
workflow. It helps an agent move from a project idea to feature decomposition,
requirements, planning, task breakdown, implementation, and spec-traced testing.

This skill is designed around one principle: the specification is the source of
truth. Each step produces or updates durable documents so another AI agent or
human contributor can continue the work without relying on hidden context.

### File Structure

```text
.
|-- README.md
|-- LICENSE
|-- .gitignore
|-- .gitattributes
`-- spec-driven-development/
    |-- SKILL.md
    |-- references/
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

### Key Files

- `spec-driven-development/SKILL.md` - skill entry point, trigger description,
  workflow overview, and gate rules.
- `spec-driven-development/references/` - detailed instructions for each SDD
  step.
- `spec-driven-development/templates/` - reusable document templates generated
  during the workflow.
- `.gitattributes` - keeps text files normalized with LF line endings.
- `.gitignore` - excludes local generated artifacts such as `.specify/`, caches,
  logs, and environment files.
- `LICENSE` - MIT license.

### Attribution

Some workflow concepts reference
[github/spec-kit](https://github.com/github/spec-kit).

### License

MIT. See [LICENSE](LICENSE).

---

## 中文

[跳轉至 English](#english)

這是一個可重用的 AI skill，用於根據結構化專案開發流程製作 spec。它會引導
agent 從專案想法開始，依序完成 Feature 拆解、需求規格、澄清、檢查清單、
技術規劃、交叉分析、任務拆解、實作，以及根據規格追蹤的測試驗證。

這個 skill 的核心原則是：規格文件是唯一真相來源。每個步驟都會產生或更新
可保存的文件，讓另一個 AI agent 或人類開發者可以接手，而不必依賴隱藏在
對話中的上下文。

### 檔案架構

```text
.
|-- README.md
|-- LICENSE
|-- .gitignore
|-- .gitattributes
`-- spec-driven-development/
    |-- SKILL.md
    |-- references/
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

### 主要檔案

- `spec-driven-development/SKILL.md` - skill 入口、觸發描述、流程總覽與
  gate 規則。
- `spec-driven-development/references/` - 每個 SDD 步驟的詳細操作說明。
- `spec-driven-development/templates/` - 工作流中會使用到的文件模板。
- `.gitattributes` - 將文字檔換行統一為 LF。
- `.gitignore` - 排除 `.specify/`、快取、log、環境變數檔等本機產物。
- `LICENSE` - MIT 授權。

### 概念來源

部分工作流概念參考自 [github/spec-kit](https://github.com/github/spec-kit)。

### 授權

MIT。詳見 [LICENSE](LICENSE)。
