# Git 新手指南

這是一份給 Git 新手看的筆記，目標是用最少必要觀念，學會把專案放到 GitHub、更新版本、開分支和建立 Pull Request。

建議照順序閱讀。

## 目錄

1. [Git 基本流程](README.md)  
   從開啟 PowerShell、設定 Git、建立 repository，到第一次 `add` / `commit` / `push`。

2. [Git Clone 與 .gitignore](clone-and-gitignore.md)  
   學會把 GitHub 上的專案下載到本機，以及哪些檔案不應該上傳。

3. [Commit 前的檢查流程](check-before-commit.md)  
   使用 `git status` 和 `git diff` 檢查修改內容，避免盲目 commit。

4. [Commit 訊息怎麼寫](commit-message.md)  
   學會寫清楚的 commit message，不要只寫 `update`、`fix`、`123`。

5. [Branch、PR、Merge 的基本流程](branch-and-pr.md)  
   學會開分支、push 分支、建立 Pull Request，最後合併回 `main`。

---
 
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

## 下一步

如果已經會基本的 `add` / `commit` / `push`，可以繼續看：

- [Git Clone 與 .gitignore](clone-and-gitignore.md)
- [Commit 前的檢查流程](check-before-commit.md)
- [Commit 訊息怎麼寫](commit-message.md)
- [Branch、PR、Merge 的基本流程](branch-and-pr.md)