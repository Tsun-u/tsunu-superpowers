---
name: worktree
description: 開始程式開發任務前評估是否需要隔離工作環境；使用 git worktree 或宿主提供的隔離能力，避免影響主分支與其他 session。程式開發專用。
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

### 宿主的子代理隔離能力

若宿主的子代理工具明確支援 worktree 或 isolation 參數，可使用該能力自動建立隔離環境。不要假設所有宿主都有相同參數；先以當前工具 schema 為準。

子代理完成後，確認宿主回報的 worktree 路徑、分支名稱與清理狀態。宿主沒有承諾自動清理時，不得假設 worktree 已被移除。

## 分支命名

- `feat/<功能名稱>` — 新功能
- `fix/<問題描述>` — 修 bug
- `refactor/<範圍>` — 重構

## 和其他 skill 的關係

- **擬定計畫**（`plan`）產出的計畫會指定要用隔離工作區
- **執行計畫**（`execute`）開始前應該先確認工作區就位
- **交付收尾**（`deliver`）負責清理工作區
