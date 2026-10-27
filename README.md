# Coding Agent Configuration

**自用** Codex、OpenCode V2、FreeBuff、Hermes prompt 設定；以簡短規則統一工作方式，供不同工具／模型使用。

## 功能

- **語言與風格**：繁體中文、台灣用語；直接說明判斷與取捨，不假裝確定。
- **開發流程**：釐清目標 → 執行 → 驗證 → 回報；優先重用、最小修改與相關測試。
- **安全界線**：操作前確認目標與授權、保護秘密；依工具原生權限執法。
- **任務接續**：需要續作時，以 temp/ 內的簡短 Markdown 筆記交接；接手先核對實際程式狀態。

## 安裝

| 來源 | 目的地 |
| --- | --- |
| `codex/AGENTS.md` | `~/.codex/AGENTS.md` |
| `codex/skills/workflow-plus/` | `~/.agents/skills/workflow-plus/` |
| `opencode/AGENTS.md` | `~/.config/opencode/AGENTS.md` |
| `freebuff/.AGENTS.md` | `~/.AGENTS.md` |
| `hermes/SOUL.md` | `$HERMES_HOME/SOUL.md` |
| `hermes/skills/workflow-plus/` | `$HERMES_HOME/skills/workflow-plus/` |

- Codex 請成對安裝；既有 host 若使用 `~/.codex/skills/`，保留確認可載入的路徑，避免同名雙份。
- `other/AGENTS.md` 供其他工具使用，目的地依該工具規定。
- Hermes 的 HERMES_HOME 使用實際資料目錄；在 config.yaml 啟用 skill：

```yaml
skills:
  auto_load: [workflow-plus]
```

## 記憶

生成的記憶、計畫與心得草稿放 Git-ignored temp/；正式文件只在任務授權時更新。原生記憶維持工具自己的位置。

只有需要續作／換工具時才寫 `temp/memory/<task-id>.md`，內容自由、簡短，例如：

```markdown
# Task
修正登入導向
# State
repo/branch、目前進度與阻塞
# Checks
測試命令及結果；未測就明說
# Next
下一個具體步驟
```

清理時保留未完成任務；temp/ 不會自動同步或備份。
