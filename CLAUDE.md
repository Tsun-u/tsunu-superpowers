# tsunu-superpowers

通用的 Codex 與 Claude Code 流程紀律框架。涵蓋程式開發、內容製作、研究、日常協作等多種任務類型。

## 開發原則

- 全正體中文，使用台灣技術術語
- skill 目錄與 frontmatter 名稱使用英文 slug；正文以中文名稱搭配 slug 交叉引用（例：思考整理（`brainstorm`））
- 共用 skill 不寫死宿主工具名稱；Codex 與 Claude Code 的差異以能力偵測處理
- 組合式架構：框架管流程，特化 skill 是可獨立觸發的模組
- 框架是安全網，不是官僚——任務明確時不強制走完整流程

## 目錄結構

```
skills/
├── entry/        — 超能力入口：入口路由
├── triage/       — 任務分流：判斷任務性質
├── brainstorm/   — 思考整理：brainstorming
├── plan/         — 擬定計畫：writing plans
├── execute/      — 執行計畫：含子代理/switchboard/並行模式
├── acceptance/   — 驗收標準：先定義怎樣算做好
├── verify/       — 完成驗證：宣稱前必須驗證
├── debug/        — 系統排查：系統化問題排除
├── collaborate/  — 夥伴協作：switchboard 基礎規範
├── review/       — 同儕審查：產出審查
├── deliver/      — 交付收尾：任務收尾
├── worktree/     — 隔離工作區：git worktree
└── write-skill/  — 撰寫技能：元技能
```
