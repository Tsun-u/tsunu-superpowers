# tsunu-superpowers

通用的 Codex 與 Claude Code 流程紀律框架。涵蓋程式開發、內容製作、研究、日常協作等多種任務類型。

Fork 自 [superpowers](https://github.com/obra/superpowers) v5.1.0 的設計精神，完全獨立實作，不依賴原版。

## 設計原則

- **組合式架構**：框架定義流程骨架，特化 skill 是可獨立觸發的模組，兩者榫卯結合
- **任務分流**：根據任務性質（嚴謹/混合/創意）決定流程強度，不一刀切
- **框架是安全網，不是官僚**：已有特化 skill 且任務明確時，不強制走完整流程
- **全正體中文**：skill 內容、產出文件全部使用正體中文和台灣技術術語
- **能力導向協作**：優先使用宿主原生子代理；環境有 Switchboard 等通道時才啟用跨 session 協作

## 任務性質三分法

| 性質 | 流程強度 | 範例 |
|------|---------|------|
| 嚴謹 | 完整（思考→計畫→驗收標準→執行→驗證） | 程式開發、教學影片、研究論文 |
| 混合 | 需求確認 + 核心步驟 + 品質驗證 | AI 算圖、社群貼文 |
| 創意 | 自由發揮 | 閒聊、遊戲 |

## Skill 清單（13 個）

### 流程骨架

| Slug | 名稱 | 職責 |
|------|------|------|
| `entry` | 超能力入口 | 入口路由，確保 skill 被觸發 |
| `triage` | 任務分流 | 判斷任務性質，決定流程強度 |

### 通用流程

| Slug | 名稱 | 職責 |
|------|------|------|
| `brainstorm` | 思考整理 | 需求探索和設計 |
| `plan` | 擬定計畫 | 設計 → 實作計畫 |
| `execute` | 執行計畫 | 四種模式：本 session / 子代理 / 跨 session / 混合並行 |
| `acceptance` | 驗收標準 | 先定義「怎樣算做好」再動手 |
| `verify` | 完成驗證 | 宣稱完成前必須跑驗證 |
| `debug` | 系統排查 | 系統化問題排除 |

### 協作與審查

| Slug | 名稱 | 職責 |
|------|------|------|
| `collaborate` | 夥伴協作 | 原生子代理與選用的跨 session 協作規範 |
| `review` | 同儕審查 | 任何產出的審查流程 |

### 收尾與工具

| Slug | 名稱 | 職責 |
|------|------|------|
| `deliver` | 交付收尾 | 任務收尾和交付 |
| `worktree` | 隔離工作區 | git worktree 隔離 |
| `write-skill` | 撰寫技能 | 元技能：撰寫新 skill |

## 安裝

### Codex

本 repo 同時是可直接加入的 Codex Git marketplace：

```bash
codex plugin marketplace add Tsun-u/tsunu-superpowers --ref main
codex plugin add tsunu-superpowers@tsunu
```

Codex 不載入 `hooks/` 內的 Claude SessionStart hook；skill 會依 Codex 的 plugin 與 skill 機制觸發。

### Claude Code

透過 local marketplace 安裝：

```bash
# 確認 local-plugins marketplace 已註冊
claude plugin marketplace list

# 安裝
claude plugin install tsunu-superpowers@local-plugins

# 驗證
claude plugin details tsunu-superpowers@local-plugins
```

## 與現有特化 Skill 的銜接

現有特化 skill 保留在原位（project-level 或 user-level），透過在 SKILL.md frontmatter 加上 `tsunu-superpowers:` 標注區塊接入框架：

```yaml
---
name: my-skill
description: ...
tsunu-superpowers:
  任務性質: 嚴謹
  模組:
    - name: 步驟一
      獨立: true
    - name: 步驟二
      依賴: [步驟一]
---
```

框架看到標注後，知道可以只觸發其中一個模組，也知道依賴關係。

## 更新

修改 skill 內容後：

```bash
# 1. 更新 marketplace 來源
# 2. 重裝 plugin
claude plugin uninstall tsunu-superpowers@local-plugins
claude plugin install tsunu-superpowers@local-plugins
```

## 授權

MIT License（詳見 [LICENSE](LICENSE)）。

設計精神 fork 自 [superpowers](https://github.com/obra/superpowers)（MIT License），完全獨立實作。
