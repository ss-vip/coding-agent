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
  - `hermes/SOUL.md`：放 `$HERMES_HOME/SOUL.md` 全域生效（POSIX 預設 `~/.hermes/`；Windows 原生預設 `%LOCALAPPDATA%\hermes\`，可用 `HERMES_HOME` 覆寫）。
  - `hermes/skills/workflow-plus/` 放 `$HERMES_HOME/skills/workflow-plus/`。
  - yolo 模式：以啟動參數 `--yolo` 或環境變數 `HERMES_YOLO_MODE=1` 啟用並加入自動加載技能：

```yaml
skills:
  auto_load:
    - workflow-plus
```

* **opencode**
  - `opencode/AGENTS.md`：放 global `~/.config/opencode/AGENTS.md` 全域生效。
  - `opencode.jsonc`（V2 格式，V1 向前相容讀取）加入以下權限控制：

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

* **other**
  - `other/AGENTS.md`：通用核心（Language、Personality、Intent defaults、Simplicity、Verify、Safety Net、Temp、Memory Protocol），供其他 agent 使用。
  - 放置到各工具的全域指令檔位置，以各工具官方文件為準，例如：
    - Claude Code：`~/.claude/CLAUDE.md`。
    - Codex：`~/.codex/AGENTS.md`。
    - Gemini CLI：`~/.gemini/GEMINI.md`。
    - TraeCode：Settings → Rules 的 user_rules。
    - ZCode：`~/.zcode/AGENTS.md`。
