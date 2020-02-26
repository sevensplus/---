# Git
## 面試題整理 
- [參考來源 by 高見龍](https://gitbook.tw/interview)

### branch 分支是什麼
- 本質上只是一個 40 字元大小的檔案，就是 `HEAD` 指向的那個檔案 
- 就像檔案上面的標籤，刪掉分支只是把標籤撕掉，可是裡面的產品（文件、文件修改痕跡 commit）都不會消失
- 從過去 commit 開平行時空分支：`git branch my_new_branch 657fce7`

### HEAD 是什麼
- 一個位置
- `vim .git/HEAD`，會看到指向某分支、某個位置，像是 `refs/heads/master, refs/heads/car`，通常可以當目前所在位置標示來看
- detached Head 斷頭

-----

### git clone, git fetch, git pull
- `clone`：通常是專案開始時用，把 online project 抓一份到電腦裡。之後的更新會用下面兩個指令
- `fetch`：會先設端節點，然後比較兩邊差別，抓「對方有我沒有的」。通常是載一個專案下來玩，原作者更新時，把補丁載一下
- `pull`：`pull = fetch + merge`，載完順手合併
    - `git pull --rebase`，合併時學 rebase，就不會多出 commit

### git push origin master
- 把 master 推一份到 origin，在 origin 形成一份 master 分支
- 完整程式碼是 `git push origin master:set_origin_been_push_name`
- `git push -f features/my_branch`：只強制修改某分支，衝突通通以 origin 為主
- `git push -u origin master`，`-u` 是把 origin 設成 upstream，下次可以直接 `git push` 就好

### git diff
|  指令                     | 說明                                  |
|--------------------------|---------------------------------------|
|`git diff bjyx218 szdszd` |比較兩個 commit                         |
|`git diff szdrrr`         |比這個 commit 和目前 HEAD 所指 commit    |
|`git diff `               |比工作目錄和暫存區，執行 `git add` 之前，可以看看修正的內容|
|`git diff --cache`        |如果已經 `git add`，比目前暫存區與工作目錄|
|`git diff-tree HEAD --name-only -r --no-commit-id`|看一下變動的東西|

### 合併
- merge：先切回主分支，然後 `git merge side_brance`
- rebase：不會新增 commit，但其他合併方式的某些情況會多產生一個 commit
- 合併衝突的話，文字檔出去開檔案起來改，改完再 add, commit。圖片的話選一邊，`git checkout --ours file.png, git checkout --their file2.png`，輸入要的那邊

### git checkout SHA1, git reset SHA1, git revert SHA1
- `git checkout SHA1`：把 HEAD 移到指定 commit 並改狀態，但不移動分支，只有 HEAD 在走路。
- `git reset SHA`：把 HEAD 和分支都移過去到指定的 commit，用參數決定（舊 commit 沒有的）新檔案的去留
    - `--mixed` 留在工作目錄
    - `--soft` 目錄和檔案留在暫存
    - `--hard `丟掉變化
- `git revert SHA1`：產生新 commit 來取消舊動作，紀錄會變長

### .gitignore
只會對設定後的檔案有效，清釘子戶的話，用 `git rm --cached`

### 工作狀態切換
- `git commit` 先存檔，弄完再 `git reset` 拆掉 commit 繼續做
- `git stash `丟暫存，之後要回來

------

### 刪掉 develop 怎麼辦，刪掉 branch 怎麼辦，git reset --hard 刪掉 commit 了怎麼辦
刪掉 branch，等於撕貼紙，貼回去就好。洗掉刪除訊息找不到商品，回 reflog 找，什麼都有什麼都不少。刪 commit 一樣找到再 reset 回來


### 做完後悔了要復原：Reset, Revert, Rebase 
- Reset：移動位置去其他 commit
- Rebase：改 commit，刪 commit，調整 commit 順序，加入新 commit，無所不能
- Revert：產生新 commit 覆蓋舊 commit，反推 commit 的內容（要回到前幾次時），通常用在已經推出去的東西裡面

### 改 commit 不麻煩 
- 改 commit 名稱
    - `git commit --amend -m"new commit name"`：`--amend` 只能改最後一次
    - `git rebase -i names1` 進入互動模式，範圍從 `names1 - newest `commits，將 `pick cd82f29 add cat 1 `的 `pict` 改成 `reword`，最後改名字。取消的話用 `git reset ORIG_HEAD --hard`
- 砍掉某次 commit
    - `git revert SHA1`
- 合併多個 commit
    - `git rebase -i SHA1`，選 squash 繼續 rebase
- 反悔不 commit 了
    - `git reset master^, git reset HEAD^` 用相對的方式 ^ 搬到上一次，或是直接打代碼
        - `--mixed` 暫存丟掉，工作目錄檔案不丟，commit 拆出來的東西會丟到目錄
        - `--soft` 目錄、暫存都不丟
        - `--hard `通通丟掉
- 把某個檔案丟進最後一次 commit
    - `git add file, git commit --amend --no-edit`，`--no-edit` 指的是不編輯訊息

---
### git flow
- 五個常用 branch，master、develop 是長期定居戶
- master：穩定、隨時可上線的版本
- develop：開發用分支
- hotfix：上線產品出現問題時，從 master 複製一份過來，修改完合併回 master 和 develop
- release：develop 成熟後，把 develop 合併過來測試，測試完再合併回 master, develop
- feature：新增功能，從 develop 複製過來用的

### github flow
- 抓取遠端所有 tag
    - `$ git fetch -t origin`
- 從上一版本建立 branch (0.2.4 代表上一個版本)
    -`$ git checkout -b patch-1 origin/0.2.4`
- 把修正個 commit 抓到 patch-1 branch
    - `$ git cherry-pick commit_id`
- 打上新的 Tag 觸發 Deploy 流程
    - $ `git tag 0.2.5`
    - $ `git push origin 0.2.5`
- 將 patch 也同步到 master 分支
    - `$ git checkout master`
    - `$ git cherry-pick commit_id`
    - `$ git push origin master`

----

### 其他
- 想存空目錄：加上 `.keep` 檔案
- 想看東西誰寫的：`git blame file_name`
