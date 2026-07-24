# tsunu-superpowers

通用的 Codex 與 Claude Code 流程紀律框架，涵蓋程式開發、內容製作、研究與日常協作。

## 開發原則

- 全程使用符合台灣習慣的正體中文與技術術語。
- skill 目錄與 frontmatter `name` 使用英文 slug；正文以中文名稱搭配 slug 交叉引用，例如思考整理（`brainstorm`）。
- 維持單一共用 skill 來源；平台差異以能力偵測與條件式指引處理，不複製整套 skill。
- 尊重宿主的指令優先序、安全政策、工具名稱與權限模型，不宣稱 skill 能覆蓋系統或開發者指令。
- Codex 使用 `.codex-plugin/plugin.json`；Claude Code 使用 `.claude-plugin/plugin.json` 與 `hooks/`。
- Claude 專用 hook 不加入 Codex manifest。若新增跨平台 hook，必須分別驗證兩個宿主的格式。
- 框架是安全網，不是官僚；任務明確且已有特化 skill 時，不強制走完整流程。

## 目錄結構

```text
.codex-plugin/  — Codex plugin manifest
.claude-plugin/ — Claude Code plugin manifest
hooks/          — Claude Code session hook
skills/         — 兩個平台共用的 13 個 skill
```

修改後至少執行 Codex plugin validator 與所有 skill 的 quick validator；Claude 端的 manifest 與 hook 行為也不得被破壞。
