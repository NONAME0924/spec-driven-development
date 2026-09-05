# GPT-6 Astra 工作流程審查與最佳化

查閱日期：2026-09-05。目標模型：GPT-6 Astra。
[繁體中文使用說明](../README.md) | [English guide](../README.en.md)

## 官方依據

Astra 官方指南指出，模型對 skill／AGENTS.md 中的衝突更敏感，可能因此提早停下；
也建議清楚交代自主程度、分工時機及適量驗證。本次據此整理指令優先順序、
核准邊界與完成條件。[GPT-6 Astra 指南](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra)

Skill 官方文件建議精準描述觸發範圍、逐步載入內容，並明定輸入與輸出。因此，
主文件只保留共用規則與入口，階段細節留在 references。
[Build skills](https://learn.chatgpt.com/docs/build-skills)

AGENTS.md 是專案指引的載入入口。本倉庫原本沒有實體檔案；新檔只說明維護這個
skill 倉庫的方法，不要求維護者把修改 skill 本身當成軟體專案跑完 SDD。
[AGENTS.md 官方說明](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

以下具體流程調整是本倉庫的設計判斷，不是 OpenAI 規定的 SDD 流程。

## 審查結果與修正

| 原本問題 | 本次修改 | 預期改善 |
|----------|----------|----------|
| 主文件、各步驟、Goal 及模板反覆定義等待規則，且互相衝突 | 核准政策集中於 SKILL.md，步驟以連結引用 | 減少自動模式中途無故停問 |
| Goal 要先寫全部 specs，但 Step 2/3 寫死等待回覆 | 明確以模式表決定停止點 | Goal 可以完成整個 spec sweep |
| 說明文件／模板混入固定層級、套件、效能數字及三個檔案核准限制 | 模板改成必要欄位；範例不等於需求 | 減少無需求的架構、檔案與治理規定 |
| Step 4 要求尚未設計的內部 API schemas，Step 6 要求尚未產生的 tasks | Step 4 看需求；Step 5 定 schema；Step 6 查 schema；Step 7 查 tasks | 消除步驟之間的前置條件循環 |
| 每個故事至少三條 AC、每個 AC 都要新增測試 | 穩定 AC ID 加適合的驗證證據；可重用測試 | 保留可追蹤性，減少湊數與重複測試 |
| 功能個別通過就可能結束整個 Goal | 增加組裝後跨 Feature 流程驗證 | 找出共享介面和完整流程的缺陷 |
| 續作需重新閱讀大量文件，已完成 Feature 不許更新 | epic 增加精簡 Execution State；變更後重開受影響驗證 | 保留核准、進度與有效證據，避免過時 PASS |
| 只要求 specs 也可能被推進到實作 | 明確文件／規劃／實作交付邊界 | 避免未要求的程式碼與錯誤完成條件 |
| 無明確分工條件 | 對獨立任務定義輸入、輸出、寫入擁有權與整合責任 | 可利用平行工作，又不破壞全局對齊 |
| 中英文 README 仍描述舊規則 | 同步模式、階段輸入輸出、每份文件用途 | 使用方法與實際指令一致 |

保留三種模式、Step 0 後的模式確認、Auto 的 Step 2/3 需求關卡、Goal 全部 specs
先完成、模組／流程架構、完整介面格式，以及使用者語言的完成說明。
已選模式不重問選項；使用者明確略過確認時，以該指示為準。

## 如何使用得更好

描述「要交付什麼、哪些是必要功能、現有專案限制、如何算完成」。
整個專案選 Goal，單一 Feature 精簡回報選 Auto，想看各階段詳細判斷與產出選 Detailed。
Detailed 與 Auto 都只固定確認 Step 0、2、3；Step 1、4–9 自動完成，詳細報告不增加核准關卡。
只要文件就明說「只寫 specs」，不需要再次確認就明說略過 Step 0 關卡。

大型 Goal 可讓不同 agent 草擬獨立 specs 或處理不同模組；共用契約由一個 owner
負責，主 agent 完成對齊與整合。這是工作分配原則，skill 不會創造環境中不存在的工具。

模型設定與 Markdown 指令是不同層次。本次沒有更改模型或 reasoning effort。
若另行遷移 API，官方建議通常保留原有效 effort；原為 none／minimal 才從 low
開始比較。不要把所有工作一律設為最高 effort。
[官方遷移指引](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-6-astra)

## 驗證與效果界線

首次 Astra 最佳化時，16 份 skill 指令／reference／template，換行正規化後由 3,045 行縮為 778 行；
UTF-8 文字量約減少 65%。主 SKILL.md 由 314 行縮為 136 行。
這是文件大小比較，不是 token、速度或品質的實測提升。

已進行獨立 agent 的五個情境模擬，發現並修正 Goal 文件交付的完成條件衝突，
再由該 agent 針對修正處複查確認。
更多維護情境見 [評估案例](workflow-evaluation.md)。情境推演不等於真的建立並測試
範例應用，也沒有量測 Astra 前後的成功率、延遲或費用。

21 份 Markdown 的 UTF-8、程式碼區塊、71 個本地連結與標題錨點檢查通過，
git diff --check 通過。入口的名稱與 description 結構檢查通過，description 為
374 字元。Skill-creator 的 quick_validate.py 因缺少 PyYAML 未能執行；本次替代
檢查針對現有兩欄位格式，不宣稱等同完整 YAML parser 或官方 validator。

要量測效能，應讓修改前後版本在相同模型設定、工具權限、範例專案與驗收條件下
各跑多次，比較完成率、非必要詢問次數、耗時、token、無需求檔案／依賴數及缺陷。
本次不宣稱已「最大化」模型效能，改善的直接證據是規則衝突減少與指令體積縮小。
