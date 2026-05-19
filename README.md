# OpenCode AI Agent Configuration (Resilience Loop)

`自用` 對 OpenCode 優化的 AI Agent 設定檔。

## 檔案結構與說明

* **`coder.md` (核心角色)**
  * 規範思考模式（RIPER-5），回應須符合 `[Status]`, `[Decision Log]`, `[Action]`, `[Next]` 四段式結構。
  * 啟動時會自主建立 `./temp/` 目錄並自動寫入 `.gitignore`，排除非預期檔案或測試腳本污染專案。

* **`./devops-runtime/SKILL.md` (技術執行技能)**
  * 維運執行（如 `npm run dev`）採用背景執行，防止 Agent 卡死；內含 Windows / Unix 跨平台的進程管理（PID/Port）與檢查指令。

* **`./tool-governance/SKILL.md` (工具策略技能)**
  * 外部工具控管，自動感應到的工具與長推理模型的調用優先級，防止 Agent 亂開工具或進行全域程式庫掃描，節省 Token 成本。

* **`MCP Tools` (使用 npx 安裝 MCP 工具)**
  * long-reasoning-mcp
  * @gongrzhe/quickchart-mcp-server
