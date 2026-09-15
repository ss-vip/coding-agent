# Coding Configuration

## `[自用]` 對 OpenCode Build/Plan 模式制定的設定檔。

### 檔案結構與說明

* **`agent-plus.md` (核心 + 全部政策)**
  * 涵蓋語言治理、衝突解決優先級、執行模式（Vibe/Production）、行為護欄、工具安全、DevOps、記憶系統整合、完成定義 (DoD)。
  * 自主迭代工作流 INTENT → EXECUTE → VERIFY → REFLECT（意圖→執行→驗證→反思）。
  * Agent 在執行任務時，會建立 `./temp/` 目錄隔離所有暫存檔案、腳本與測試產物（Artifacts）；執行期狀態（phase/attempt/resume hook）改由 plugged.in 記憶系統（`memory_observe`）跨環境同步，不再寫本機狀態檔。
  * 已建立 `.gitignore` 將 `./temp/` 與 `.codegraph/` 排除於版本控制之外。

* **`MCP Tools` (常用 MCP)**
  * [codegraph](https://github.com/colbymchenry/codegraph)
  * [plugged.in](https://plugged.in/)
  * [huashu-chrome](https://github.com/alchaincyf/huashu-chrome)

* **`SKILL` (常用 skills)**
  * [agent-use-browser](https://github.com/ss-vip/hermes-agent-soul/tree/main/skills/agent-use-browser)

---

### opencode.json 配置

* 外部載入與設定檔 (請依 OpenCode 版本調整)

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "api-gateway": {
      "models": {
        "openai": {
          "name": "openai",
          "limit": {
            "context": 128000,
            "output": 8000
          }
        }
      },
      "name": "api-gateway",
      "npm": "@ai-sdk/openai-compatible",
      "options": {
        "baseURL": "https://your-gateway/v1",
        "headers": {
          "Authorization": "Bearer your-key"
        }
      }
    }
  },
  "mcp": {
    "codegraph": {
      "type": "local",
      "command": ["codegraph", "serve", "--mcp"],
      "enabled": true
    },
    "huashu-chrome": {
      "type": "local",
      "command": ["npx", "-y", "huashu-chrome", "mcp"],
      "enabled": true
    },
    "PluggedinMCP": {
      "type": "local",
      "command": ["npx", "-y", "@pluggedin/pluggedin-mcp-proxy"],
      "environment": {
        "PLUGGEDIN_API_KEY": "your-key"
      },
      "enabled": true
    }
  },
  "agent": {
    "plan": {
      "temperature": 0.2,
      "top_p": 0.9
    },
    "build": {
      "temperature": 0.2,
      "top_p": 0.9,
      "permission": {
        "*": "allow"
      }
    }
  },
  "compaction": {
    "auto": true,
    "keep": {
      "tokens": 8000
    },
    "buffer": 20000
  },
  "watcher": {
    "ignore": [
      "node_modules/**",
      "dist/**",
      ".next/**",
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
      ".venv/**",
      "venv/**",
      ".mypy_cache/**",
      "target/**",
      "build/**",
      "obj/**",
      "bin/**",
      "*.tsbuildinfo",
      ".vercel/**",
      ".netlify/**",
      "temp/**",
      ".codegraph/**"
    ]
  },
  "instructions": [
    "https://raw.githubusercontent.com/ss-vip/opencode-agent/refs/heads/main/agent-plus.md"
  ]
}
```
