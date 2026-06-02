---
name: 隔離工作區
description: 開始程式開發任務前，確保有隔離的工作環境。使用 git worktree 或 Agent tool 的 isolation 參數，避免影響主分支和其他 session 的工作。程式開發專用。
---

# 隔離工作區

程式開發任務開始前，確保工作環境是隔離的。不要在主分支上直接開發。

## 什麼時候需要

- 開始一個新功能或修 bug
- 執行實作計畫
- 任何會改動程式碼的任務

## 什麼時候不需要

- 只是讀程式碼、做分析
- 非程式開發任務
- 使用者明確說在主分支上做

## 兩種隔離方式

### Git Worktree

在同一個 repo 建立獨立的工作目錄，共享 git 歷史但各自有自己的 working tree。

```bash
# 建立 worktree
git worktree add .worktrees/<功能名稱> -b <分支名稱>

# 進入 worktree
cd .worktrees/<功能名稱>

# 完成後清理（合併或捨棄後）
cd <主 repo 根目錄>
git worktree remove .worktrees/<功能名稱>
git worktree prune
```

**注意事項**：
- 清理 worktree 前先 `cd` 回主 repo 根目錄
- 不要從 worktree 內部刪除自己
- 合併前確認測試通過
- 不要刪除還在被 PR 使用的 worktree

### Agent Tool 的 isolation 參數

派子代理時指定 `isolation: "worktree"`，系統自動建立隔離環境。

```
Agent({
  description: "實作功能 X",
  prompt: "...",
  isolation: "worktree"
})
```

子代理完成後，系統會回報 worktree 路徑和分支名稱。如果子代理沒有做任何變更，worktree 會自動清理。

## 分支命名

- `feat/<功能名稱>` — 新功能
- `fix/<問題描述>` — 修 bug
- `refactor/<範圍>` — 重構

## 和其他 skill 的關係

- **擬定計畫**（`plan`）產出的計畫會指定要用隔離工作區
- **執行計畫**（`execute`）開始前應該先確認工作區就位
- **交付收尾**（`deliver`）負責清理工作區
