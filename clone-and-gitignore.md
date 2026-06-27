# Git Clone 與 .gitignore
 
## git clone：把 GitHub 上的專案下載到本機
 
如果專案已經在 GitHub 上了，不需要重新 `git init`，直接用 `clone` 把整個專案（包含歷史紀錄）下載下來，並自動幫你連好 remote。
 
### 1. 找到專案的網址
在 GitHub 專案頁面，點綠色的「Code」按鈕，複製 HTTPS 網址，類似：
```
https://github.com/chiffon-0504/git.git
```
 
### 2. 切換到想要存放專案的資料夾
```powershell
cd D:\
```
 
### 3. 執行 clone
```powershell
git clone https://github.com/chiffon-0504/git.git
```
> 這會自動建立一個跟 repo 同名的資料夾（例如 `git`），裡面已經是完整的 Git 專案，remote 也設定好了，不用再手動 `git remote add origin`。
 
### 4. 進入資料夾就可以開始用
```powershell
cd git
git status
```
 
> **小提醒**：如果想下載到指定名稱的資料夾，可以在網址後面加上資料夾名稱：
> ```powershell
> git clone https://github.com/chiffon-0504/git.git my-folder-name
> ```
 
---
 
## git pull：更新已經下載的專案
 
如果專案已經 `clone` 到本機，之後 GitHub 上有新的更新（例如別人 push 了新的 commit，或自己在另一台電腦上更新過），可以在專案資料夾內執行：
 
```powershell
git pull
```
 
`git pull` 的意思是把 GitHub 上的新版本同步到本機。
 
> **注意**：
> - 第一次下載專案用 `git clone`
> - 之後要同步更新用 `git pull`
> - 如果本機有還沒 commit 的修改，建議先 `git status` 確認狀態，避免 `pull` 時發生衝突
 
---
 
## .gitignore：告訴 Git 哪些檔案不要追蹤
 
有些檔案不應該被上傳到 GitHub，例如：
- 程式套件資料夾（例如 Node.js 的 `node_modules`）
- 含有密碼或金鑰的設定檔（例如 `.env`）
- 編輯器或系統自動產生的檔案（例如 `.DS_Store`、`Thumbs.db`）

`.gitignore` 就是用來告訴 Git「這些檔案不用管」的清單。
 
### 1. 在專案根目錄建立 `.gitignore` 檔案
```powershell
code .gitignore
```
如果 `code` 指令不能用，也可以用記事本或 VS Code 手動建立這個檔案。
 
### 2. 寫入要忽略的項目
範例內容（依專案需求調整）：
```
# 套件資料夾
node_modules/
 
# 環境變數與機密設定
.env
 
# 系統自動產生的檔案
.DS_Store
Thumbs.db
```
 
### 3. 存檔後加入 commit
```powershell
git add .gitignore
git commit -m "Add .gitignore"
git push
```
 
> **注意**：`.gitignore` 只能擋住「還沒被 Git 追蹤過」的檔案。如果某個檔案之前已經 commit 過，加進 `.gitignore` 也不會自動移除它，需要額外執行：
> ```powershell
> git rm --cached 檔案名稱
> ```
> 然後再 commit 一次。
 
### 小提醒
 
| 情境 | 建議寫法 |
|---|---|
| 忽略某個資料夾 | `資料夾名稱/` |
| 忽略某個檔案 | `檔案名稱` |
| 忽略所有同類型檔案 | `*.log` |
| 忽略整個資料夾但保留特定檔案 | `資料夾名稱/*` 加上 `!資料夾名稱/檔案名稱` |
 
> 不同程式語言/框架通常有現成的 `.gitignore` 範本，可以直接搜尋「gitignore 範本 + 語言名稱」，或參考 [github/gitignore](https://github.com/github/gitignore) 這個官方範本庫。