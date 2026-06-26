# Git 新手指南
 
## 開啟 PowerShell
 
1. 按 `Win + X`
2. 選擇「終端機」（Windows 11）或「Windows PowerShell」（Windows 10）
3. 如果選單裡沒有看到，也可以按 `Win` 鍵，搜尋 `PowerShell`，再按 `Enter` 開啟
接下來的 Git 指令都在這個視窗裡輸入。
 
> **權限提醒**
> 一般安裝 Git 不一定需要系統管理員權限。如果之後執行指令時出現「權限不足」或 `Access Denied`，可以重新開啟 PowerShell：
> 搜尋 `PowerShell` → 右鍵 → 選擇「以系統管理員身分執行」
 
---
 
## 第一次設定與建立專案
 
### 1. 安裝 Git for Windows
```powershell
winget install --id Git.Git -e --source winget
```
 
### 2. 檢查是否安裝成功
```powershell
git --version
```
 
### 3. 設定名字與 Email
```powershell
git config --global user.name "你的GitHub名稱"
git config --global user.email "你的GitHub信箱"
```
 
### 4. 到 GitHub 建立 repository
1. 到 [https://github.com/new](https://github.com/new)
2. Repository name 輸入：`first-project`
3. 建議先**不要**勾選 `Add a README file`
4. 建立後會拿到類似這種網址：
```
https://github.com/你的GitHub名稱/first-project.git
```
 
### 5. 建立專案資料夾
```powershell
mkdir D:\first-project
```
 
### 6. 進入專案資料夾
```powershell
cd D:\first-project
```
 
### 7. 建立 README.md
```powershell
Set-Content README.md "# first-project"
```
 
> **編碼提醒**
> 如果之後 README.md 要寫中文，建議用 VS Code 開檔案編輯並存檔。VS Code 通常會用 UTF-8，比用 PowerShell 指令寫中文內容更不容易出現亂碼。
 
### 8. 初始化 Git 專案
```powershell
git init
```
 
### 9. 查看目前 Git 狀態
```powershell
git status
```
 
### 10. 加入檔案並建立第一次 commit
```powershell
git add .
git commit -m "Initial commit"
```
 
### 11. 綁定 GitHub repository
```powershell
git remote add origin https://github.com/你的GitHub名稱/first-project.git
```
 
### 12. 設定主要分支名稱為 main
```powershell
git branch -M main
```
 
### 13. 推上 GitHub
```powershell
git push -u origin main
```
> **注意**：第一次 push 時，可能會自動跳出瀏覽器要求登入 GitHub 並授權。這是正常的，照畫面登入並同意授權即可。授權完成後，回到終端機等待，它通常會自動繼續執行。
 
### 14. 用 VS Code 開啟專案
```powershell
code D:\first-project
```
如果 `code` 指令不能用，就手動用 VS Code 開啟 `D:\first-project`
 
### 15. 修改檔案，例如 README.md
建議修改完先按 `Ctrl + S` 存檔
 
### 16. 查看目前有哪些檔案被修改
```powershell
git status
```
 
### 17. 加入所有修改
```powershell
git add .
```
 
### 18. 建立版本紀錄
```powershell
git commit -m "這次改了什麼"
```
 
### 19. 推上 GitHub
```powershell
git push
```
 
### 20. 到 GitHub 頁面重新整理，確認檔案有更新
 
---
 
## 之後每次修改後
 
```powershell
git status
git add .
git commit -m "這次改了什麼"
git push
```
 
| 指令 | 說明 |
|---|---|
| `git status` | 查看目前 Git 狀態，例如哪些檔案被新增、修改或刪除 |
| `git add .` | 把目前資料夾內的所有修改加入暫存區，準備提交 |
| `git add README.md index.html` | 只把 `README.md` 和 `index.html` 這兩個檔案加入暫存區 |
| `git commit -m "..."` | 建立一筆版本紀錄，訊息要簡單描述這次改了什麼 |
| `git push` | 把本機的 commit 上傳到 GitHub |
 
---
 
## 開新 branch 的基本流程
 
### 1. 先確認目前狀態
```powershell
git status
```
 
### 2. 建立並切換到新 branch
```powershell
git switch -c feature/login-page
```
 
### 3. 修改檔案後，查看狀態
```powershell
git status
```
 
### 4. 加入修改
```powershell
git add .
```
 
### 5. 建立 commit
```powershell
git commit -m "Add login page"
```
 
### 6. 推上 GitHub
```powershell
git push -u origin feature/login-page
```
 
### 7. 到 GitHub 網頁上開 Pull Request
1. 推上去之後，到 GitHub 網頁的 repository 頁面
2. 會看到「Compare & pull request」按鈕，點下去
3. 確認內容沒問題後，點「Merge pull request」完成合併
4. 合併完成後，可以選擇刪除 `feature/login-page` 這個分支（GitHub 上會有按鈕）
### 8. 切回 main 前，先確認目前沒有未提交的修改
```powershell
git status
```
 
### 9. 切回 main
```powershell
git switch main
```
 
### 10. 把 GitHub 上最新的內容（剛剛合併的）拉回本機
```powershell
git pull
```
 
> **補充**：如果想在本機直接合併，不透過 GitHub 網頁的 PR，可以這樣做（新手建議先用上面 GitHub 網頁的方式，比較不容易出錯）：
> ```powershell
> git switch main
> git merge feature/login-page
> git push
> ```
 
### 小提醒
 
| 指令 | 說明 |
|---|---|
| `git status` | 查看目前哪些檔案被修改、新增或刪除 |
| `git switch -c <分支名稱>` | 建立並切換到新分支 |
| `git switch <分支名稱>` | 切換到已存在的分支 |
| `git pull` | 把遠端（GitHub）最新的內容同步到本機 |
 
> 合併完 PR 後，本機的 main 不會自動更新，記得要 `git pull` 一次。
