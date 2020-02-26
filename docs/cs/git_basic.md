# Git
## Git
> Q：`Git` 的用途？  
> A：版本控制！有時候在做專案時，可能會有不同分枝，這時候就可以用 Git 管理。如果版本做壞了，可以復原回到前幾次的狀態；也可以開發不同部分，最後再一起整合起來。

> Q：`Github` 是什麼？  
> A：線上可以放 `Git repository` 的地方，讓很多人同時協作

---

## 基本指令
|  指令                   | 說明                              |  範例                                 |
|------------------------|-----------------------------------|---------------------------------------|
| git init               | 初始化                             |                                      |
| git clone SSH          | 把網路上的專案抓下來                |                                       |
| git status             |檢視版本狀況，staged是被版本控制，untracked是不加入|                          |
| git add                |加入版本控制                        |git add file_name，git add . 把全部加入 |
| git rm --cached        |檔案可以把原本被控制的移出來         |                                       |
| git commit             |建新版本                           | -m"  "(message)                       |
| git commit --amend     |更改commit名稱                     |                                       |
| git reset HEAD^        |回到上一個commit版本   |--hard：commit、改過的東西的都不要了。--soft：預設值，拋棄commit但是改過的東西還在（取消存檔但是沒還原）|
| git log                |看歷史資料                         |git log --oneline：看前七碼就好（較簡潔）  |
| git checkout           |回到過去版本                       |git checkout 版本號，git checkout master 回來最新版，或走到其他branch  |
| git checkout --file.txt|把某個檔案復原到上次commit狀態      |                                         |
| git chechout -b new_fold_name |開新branch同時轉移過去      |                                         |
| .gitignore             |忽略某些東西                   |touch .gitignore → vim .gitignore → 把要忽略的檔案名打進去存檔。這個檔案本身要加入版本控制中  |
| git commit -am 'version_3'|綜合add和commit的指令，但新檔案無法commit，要先add加入，才能對所有東西下指令| |
| git diff               |看這次和上次的差別                  |                                         |
| git commit -m'' --no-verify|跳過eslint檢查                 |                                         |
|                        |commit 流程     |git add 將檔案加入版本控制 → git status 檢視 → git commit -m "version_2" 建立新版本|

---

## Branch指令 
|  指令                      | 說明                              |
|---------------------------|-----------------------------------|
| git branch new_branch_name|建立branch                         |
| git branch -m             |名稱，更改名字                      |
| git branch -v             |看有哪些branch，會顯示branch以及裡面最後一個修改的commit  |
| git branch -d name        |刪掉branch                          |
| git checkout branch_name  |切換到分支資料夾                     |
| git merge branch_b  |合併分支，把另一個(b)併進來（現在位於a）。如果檔案有衝突 → git status → 手動更改（用vim進入更改） → git commit -am "new"  |
| git checkout branch_name  |可以透過這個抓遠端的branch            |

---

## 抓 repository 更新檔
|  指令                                                     | 說明                                         |
|-----------------------------------------------------------|----------------------------------------------|
| git remote add upstream(update_repo_name) http://...(url) | 加入專案原始來源的版本控制                     |
| git remote -v                                             | 查看版本控制來源                              |
| git pull upstream master                                  | 抓下更新檔案                                  |


---

## Github 操作  
|  指令                       | 說明                                             |
|-----------------------------|-------------------------------------------------|
| git remote add origin 網址  |增加一個遠端的repository，新增一個remote叫做origin  |
| git push -u origin master   |把東西放到origin上的某個branch，master是branch的名稱、可自訂，-u可以省略  |
| git pull origin master      |把上面的更新抓下來                                 |
| git clone SSH網址           |把別人的專案載下來，也可以在網頁上直接按Fork複製到自己那邊|

> Q：Hook?  
> A：像是偵測事件發生等等。例如在commit前做一些檢查

---
## 進階  
### rebase
-  re-base，「重新定義分支的參考基準」，一般分支都是從 master 長出來的。rebase 就是把另外一條線當作基準，然後合併進去。假設現在有 cat, dog, master，前兩者是同時從 master 長出來的。如果在 cat 執行 `git rebase dog`，現在的線就變成 master-dog-cat。不過並不是直接剪下貼上就好，而是貼上、發現新東西、執行指向 rebase_item 的新 commit 。
- 如果不改到其他人檔案，誰 rebase 誰先後順序沒差，只是被 rebase 的人因為被當成基準，commit 會排在比較前面（比較舊）
- rebase 後怎麼復原

|  指令                       | 說明                                             |
|-----------------------------|-------------------------------------------------|
|`git reset HEAD^ --hard`    |回上一個`commit`，可是 rebase 不是新建立一個 commit，如果要合併（被入贅）的對象有兩個commit，就會蓋好兩個新 commit，這方法不能保證回到原本狀況|
|`git reflog`                |翻找之前的紀錄，找 rebase 的指令狀態，然後 `git reset event_number --hard` 重置回去，重置 `checkout: moving from master to been_rebash_br` 這列物件 |
|`git reset ORIG_HEAD`       |這個會記錄危險動作之前的位置（merge、reset 都算）  |

### stash
- 一個分支沒做完，要先存檔去做其他事，就用 stash 先打包起來
- untracked 的東西沒辦法被 stash，要加 -u

|  指令                       | 說明                                             |
|-----------------------------|-------------------------------------------------|
|`git status`  |看一下狀態|
|`git stash`   |東西打包起來|
|`git stash list`  |檢查打包的東西，可以打包很多次，跟 commit 一樣|
|`git stash pop stash@{2}`  |撿回某次的東西來做。用 pop 就是指定某次，用完備份的 stash 就刪掉；沒指定就會用最晚的拿出來，`pop = apply + drop`|
|`git stash apply stash@{1}`|撿回來的另一個指令，但用這 stash 檔案不會被砍|
|`git stash drop stash@{0}`| 刪掉某個不要的 stash|

### pull-request
- fork：把專案複製到指定帳號下面，改完後用 pull request 和原作者互動。開 branch 的話，用 merge / rebase 合併
- pull request 流程
    1. fork project_a 到自己的 github 變成 project_b，clone project_b 回電腦修改
    2. add, commit, push to project_b
    3. 發 pull request

### cherry-pick
想要別人的分支，但不要所有的 commit，就用 `git cherry-pick yoyoyo 666666 whendr` 撈想要的過來用，可以同時撈多個，加上 `--no-commit` 就不會馬上合併

### tag
- 就是貼紙
- 輕量標籤（lightweight tag）：指向 commit，沒有其他多的資訊
    - 用法是 `git tag tag_name yo66yo(commit_code)`，如果不指定哪個，就貼到目前最近的一個commit
    - 通常是個人使用或暫時標記
- 附註標籤（annoted tag）
    - `git tag tag_name_yo 6666yo -a -m" say somethin here "`
    - 通常拿來標版本號
- 標籤和分支：一樣 40 位 SHA-1
    - 標籤不會移動
    - 分支隨 commit 移動
