# Branch、PR、Merge 的基本流程

## 為什麼不要直接在 main 上改

到目前為止，你可能都是直接在 `main` 上面 commit、push。這在自己一個人練習時沒問題，但只要：

- 改一半發現方向錯了，想整個丟掉重來
- 同時想做兩件不相關的事（例如一邊修 bug、一邊寫新功能）
- 之後要跟別人協作

直接在 `main` 上改就會很麻煩——壞掉的話沒有「乾淨版本」可以退回去。

解法是：**開一個新的分支（branch）來改，改好沒問題了，再合併（merge）回 main。**

---

## branch 是什麼

你可以把 `main` 想成主線劇情，branch 就是你開的一條「平行世界」，在裡面怎麼改都不會影響到主線，直到你決定要合併回去。

### 建立並切換分支

```bash
git switch -c feature/login
```

這行做了兩件事：
1. 建立一個叫 `feature/login` 的新分支
2. 切換過去（之後的 commit 都會記錄在這個分支上）

（`-c` 是 create 的意思。新版 git 把「切換分支」獨立成 `switch`，比舊的 `checkout` 語意更清楚，後面都會用這個。）

常見命名方式：
```
feature/登入頁面
fix/修正選單bug
docs/新增安裝教學
```

### 查看目前在哪個分支

```bash
git branch
```

有 `*` 的就是你目前所在的分支。

### 切換回 main

```bash
git switch main
```

---

## 在分支上工作

切到分支後，平常怎麼用 git 就怎麼用，完全一樣：

```bash
git add .
git commit -m "feat: 新增登入頁面"
git push origin feature/login
```

第一次 push 一個新分支，要加上分支名稱（`origin feature/login`），讓遠端也建立同名分支。

---

## PR（Pull Request）是什麼

PR 不是 git 的指令，是 GitHub（或 GitLab 等平台）提供的功能。意思是：

> 「我在 `feature/login` 分支上改好了，請把這些改動合併進 `main`，麻煩看一下。」

流程：

1. push 分支到 GitHub 後，網頁上會出現「Compare & pull request」的提示
2. 點進去，選擇「從哪個分支 → 合併到哪個分支」（通常是 `feature/login → main`）
3. 寫標題和說明，講清楚這次改了什麼
4. 建立 PR

PR 的好處：
- 別人可以在合併前先看過你的改動、留言討論
- 留下一筆「這次改動為什麼存在」的紀錄
- 自己一個人開發也可以用，當作改動前的最後檢查

---

## Merge：合併回 main

PR 確認沒問題後，在 GitHub 上點「Merge pull request」，改動就會併回 `main`。

合併後，記得在自己電腦上同步：

```bash
git switch main
git pull
```

這樣本地的 `main` 才會跟遠端一致。

分支沒用了可以刪掉（保持乾淨，不是必須）：

```bash
git branch -d feature/login
```

---

## 整個流程串起來

```bash
# 1. 從 main 開新分支
git switch main
git switch -c feature/login

# 2. 開發、commit
git add .
git commit -m "feat: 新增登入頁面"

# 3. push 到 GitHub
git push origin feature/login

# 4. 到 GitHub 開 PR，請人 review（或自己看一次）

# 5. Merge 後，回到本地同步
git switch main
git pull
```

---

## 小結

- 不要直接在 `main` 上改，先開分支
- `git switch -c 分支名` 建立並切換分支
- PR 是「請求合併」的動作，發生在 GitHub 網頁上，不是 git 指令
- Merge 完記得 `git switch main` + `git pull` 同步本地
- 一個分支對應一件事，做完就可以合併、刪掉

這套「開分支 → 改 → PR → merge」的流程，是接下來跟別人協作時最基本的循環，先把這個走熟，之後遇到衝突（conflict）或更複雜的情境會再另外教。