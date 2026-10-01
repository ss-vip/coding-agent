# Coding Agent Configuration

## `[自用]` 對 Hermes-Agent/OpenCode V2/FreeBuff CLI 制定的設定檔。

### 功用說明

* **核心及政策**
  - 人格、語言及行為規範、執行模式（Vibe/Production）、工具安全、DevOps、完成定義 (DoD)。
  - 自主迭代工作流 INTENT → EXECUTE → VERIFY → REFLECT（意圖→執行→驗證→反思）。
  - 使用 `./temp/` 目錄隔離所有暫存檔案、腳本、測試產物，同時確保寫入專案根目錄 `.gitignore`。
  - 進度記憶使用 `./temp/memory.md`（平行任務用 `temp/memory/<task-id>.md`）給各 agent 閱讀接手。

### 載入方式（請依照實際環境路徑處理）

* **freebuff**
  - `freebuff/.AGENTS.md`：放 global `~/.AGENTS.md` 全域生效。

* **hermes**
  - `hermes/SOUL.md`：放 global `~/.hermes/SOUL.md` 全域生效。
  - `hermes/skills/workflow-plus/` 放 `~/.hermes/skills/workflow-plus/`。
  - config 或啟動參數使用 `yolo` 模式，並且加入自動加載技能：

```yaml
skills:
  auto_load:
    - workflow-plus
```

* **opencode**
  - `opencode/AGENTS.md`：放 global `~/.config/opencode/AGENTS.md` 全域生效。
  - config 加入以下權限控制：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "permissions": [
    // yolo 全開：只覆寫 base policy 的兩處 ask，其餘沿用預設 allow；危險操作只靠 AGENTS.md 自律
    { "action": "read", "resource": "*.env*", "effect": "allow" },
    { "action": "external_directory", "resource": "*", "effect": "allow" }
  ]
}
```
