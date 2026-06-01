# Coding AI Agent Configuration (Resilience Loop)

## `[自用]` 對 OpenCode AI Agent 制定的設定檔。

### 檔案結構與說明

* **`coder-agent.md` (核心角色)**
  * 自主迭代的 agent workflow：Plan → Act → Reflect。
  * Agent 於需要時自動建立 `./temp/` 與 runtime state 檔案，用於隔離暫存與測試 artifacts。

* **`./SKILLS/devops-runtime.md` (技術執行技能)**
  * 對指令執行（如 `npm run dev`）採用背景運作，防止 Agent 卡死；內含 Windows / Unix 跨平台的進程管理（PID/Port）與檢查指令。

* **`./SKILLS/fullstack.md` (前後端整合技能)**
  * 前端：Framework-aware（框架與套件優先或 fallback 至 Vanilla）、排版與創意設計思考。後端：RESTful API、參數化查詢、安全錯誤處理、Schema 驗證。

* **`./SKILLS/mcp-governance.md` (工具使用技能)**
  * 外部工具控管，自動感知載入工具與長推理模型的調用優先級，防止 Agent 不正確使用工具或進行全域掃描。

* **`./SKILLS/security-runtime.md` (安全策略技能)**
  * 信任邊界、提示注入防禦、外部資料驗證，防止 Agent 執行隱藏指令或權限提升。

* **`MCP Tools` (常用 MCP 工具)**
  * [long-reasoning-mcp](https://github.com/harshpreet931/longReasoningMCP)
  * [neuromcp](https://github.com/AdelElo13/neuromcp)
  * [exa-multi-mcp](https://libraries.io/npm/exa-multi-mcp)
  * [duckduckgo-mcp-server](https://github.com/nickclyde/duckduckgo-mcp-server)

* **其他 MCP 工具**
  * [scrapling](https://github.com/D4Vinci/Scrapling)
  * [cloak-browser-mcp](https://npmx.dev/package/@devinwangd/cloak-browser-mcp)

* **`skills` (全域常用的技能)**
  * [code-review](https://github.com/awesome-skills/code-review-skill)

---

### opencode.json 配置

* 外部載入

```json
{
  "$schema": "https://opencode.ai/config.json",

  "instructions": [
    "https://raw.githubusercontent.com/ss-vip/coding-agent/main/coder-agent.md",
    "https://raw.githubusercontent.com/ss-vip/coding-agent/main/SKILLS/devops-runtime.md",
    "https://raw.githubusercontent.com/ss-vip/coding-agent/main/SKILLS/fullstack.md",
    "https://raw.githubusercontent.com/ss-vip/coding-agent/main/SKILLS/mcp-governance.md",
    "https://raw.githubusercontent.com/ss-vip/coding-agent/main/SKILLS/security-runtime.md"
  ]
}
```

* 其它 (請依 OpenCode 版本調整)

```json
{
  "$schema": "https://opencode.ai/config.json",

  "agent": {
    "build": {
      "temperature": 0.1,
      "permission": {
        "*": "allow",
        "skill": {
          "*": "allow"
        }
      },
      "tools": {
        "*": true
      }
    }
  },
  "default_agent": "build",
  "compaction": {
    "auto": true,
    "prune_tool_outputs": true,
    "strategy": "summarize",
    "threshold": 0.85
  },
  "watcher": {
    "ignore": [
      "node_modules/**",
      "dist/**",
      ".git/**",
      ".DS_Store",
      "Thumbs.db",
      "**/*.log",
      ".vscode/**",
      ".idea/**",
      ".env*",
      "coverage/**",
      ".wrangler/**",
      "__pycache__/**",
      "*.pyc",
      ".pytest_cache/**",
      "obj/**",
      "bin/**",
      "*.tsbuildinfo",
      ".vercel/**",
      ".netlify/**"
    ]
  },
  "plugin": [
    "opencode-timeout-continuer",
    "@franlol/opencode-md-table-formatter@latest"
  ]
}
```
