# Commit 前的檢查流程：git status + git diff

每次要 commit 之前，養成「先看再 commit」的習慣，可以避免誤上傳不該上傳的東西，也能讓 commit 訊息寫得更準確。

## git status：看「哪些檔案」變動了

```powershell
git status
```

這個指令會告訴你目前資料夾內，哪些檔案是：
- **Untracked（未追蹤）**：全新的檔案，Git 還沒記錄過
- **Modified（已修改）**：已經被 Git 追蹤過，但內容有變動
- **Staged（已加入暫存區）**：已經執行過 `git add`，準備要 commit 的檔案

> `git status` 只告訴你「哪些檔案變了」，不會告訴你「裡面具體改了什麼」——這就是 `git diff` 要做的事。

---

## git diff：看「具體改了什麼內容」

### 查看尚未 add 的修改
```powershell
git diff
```
會顯示目前所有已修改、但還沒 `git add` 的檔案，逐行列出新增、刪除的內容。

### 查看單一檔案的修改
```powershell
git diff README.md
```

### 查看已經 add 過、準備要 commit 的修改
```powershell
git diff --staged
```
> 這個很實用：執行 `git add .` 之後，可以用這個指令再次確認「等一下要 commit 的內容到底是什麼」，避免不小心把不該加的東西 commit 上去。

### 怎麼看懂 diff 的輸出
```diff
- 這是被刪除的內容（紅色，行首是 -）
+ 這是新增的內容（綠色，行首是 +）
```

> **小提醒**：diff 的內容如果很長，畫面會用類似看檔案閱讀器的模式顯示，按 `q` 可以離開，回到一般的終端機畫面。

---

## Commit 前的標準檢查流程

建議照這個順序，每次 commit 前都走一遍：

```powershell
# 1. 先看有哪些檔案變動
git status

# 2. 看看具體改了什麼內容，確認沒有改錯地方
git diff

# 3. 確認沒問題後，加入暫存區
git add .

# 4. 再次確認暫存區裡的內容是預期的
git diff --staged

# 5. 沒問題就可以 commit
git commit -m "清楚描述這次改了什麼"

# 6. 推上 GitHub
git push
```

> **為什麼要分兩次 diff（第 2 步跟第 4 步）？**
> 第 2 步是看「還沒加入暫存區」的修改，第 4 步是看「已經加入暫存區、即將被 commit」的內容。如果你 `git add .` 之後又手滑改了檔案，這兩次看到的內容可能不一樣，分兩次檢查比較保險。

---

## 常見情境

| 情況 | 該用什麼指令 |
|---|---|
| 想知道哪些檔案動過 | `git status` |
| 想知道某個檔案具體改了什麼 | `git diff 檔案名稱` |
| add 完想再確認一次內容 | `git diff --staged` |
| 想取消某個檔案的修改，回到上次 commit 的狀態 | `git restore 檔案名稱` |
| 想把某個已經 add 的檔案從暫存區移除（但保留修改） | `git restore --staged 檔案名稱` |

> `git restore 檔案名稱` 會把檔案內容還原到上次 commit 的狀態，未 commit 的修改會消失；`git restore --staged 檔案名稱` 只會取消暫存，不會刪掉修改。