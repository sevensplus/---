## Command Line
> Q：`Command Line` 是什麼？  
> A：文字型的操作視窗。我們現在看到的螢幕（資料夾、圖示等等）是圖形化視窗（Graphical User Interface），使用時點圖示進行操作。如果直接打程式碼進行操作，就可以用 `Command Line`。舉例來說，我們點擊資料夾進入某個位置，cmd 當中則是用 `cd` 來移動；我們在資料夾中按右鍵新增檔案，cmd 當中則用 `touch`。

> Q：那要怎麼使用？  
> A：Windows 到Cmder下載程式，或是直接用命令提示字元；Mac 則是搜尋terminal，或用iTerm2。

補充：[美化Terminal]()    [cmder介紹]()

---
### 基本操作
|  指令   |說明                             |  範例                      |
|---------|--------------------------------|----------------------------|
|pwd      |路徑位置                         |`cd ..`到上一層，`~` 代表`User/who` |
|ls       |列出所有檔案                     |                            |
|cd       |切換位置                         |                            |
|man      |看各個指令的內容                  |man ls                      |
|touch    |碰一下檔案，更改最後修改時間；或是建立檔案|                      |
|rm       |刪東西   |rmdir刪資料夾，mkdir建資料夾，rm-r資料夾底下東西全刪    |
|mv       |移動資料夾或改名                  |mv 檔案 路徑/名稱            |
|cp       |複製檔案                |cp 檔案 新檔案名，用-r可以複製資料夾    |
|vim(vi)  |文字編輯器 |`i/a/o`=insert，`esc`出去insert模式，`:q`整個出去，`:w`儲存    |
|cat      |印出內容，或是連接檔案             |                          |
|less     |分頁印出檔案                      |                          |
|date     |印出時間                          |                          |
|top      |印出所有process，看和電腦有關的資訊 |                          |
|grep     |抓關鍵字   |`grep 關鍵字 檔案`，會把被搜尋到的那行列出來         |
|wget     |下載檔案或網頁原始碼               |`wget 網址`                |
|curl     |測試、送出request                 |                           |
|node     |打這個可以直接在cmd裡面寫程式碼，打指令會回傳內容   |    |
|`>`      |redirection輸出或導向，像echo 123 > a.txt，將內容輸出到文件中並覆蓋，如果不覆蓋原本檔案用`>>`   |  |
|`|`      |pipe連結指令                     |                            |


---

## Git
> Q：`Git` 的用途？  
> A：版本控制！有時候在做專案時，可能會有不同分枝，這時候就可以用 Git 管理。如果版本做壞了，可以復原回到前幾次的狀態；也可以開發不同部分，最後再一起整合起來。

> Q：`Github` 是什麼？  
> A：線上可以放 `Git repository` 的地方，讓很多人同時協作

---

### 基本指令
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

### Branch指令  |
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

### Github 操作  |
|  指令                       | 說明                                             |
|-----------------------------|-------------------------------------------------|
| git remote add origin 網址  |增加一個遠端的repository，新增一個remote叫做origin  |
| git push -u origin master   |把東西放到origin上的某個branch，master是branch的名稱、可自訂，-u可以省略  |
| git pull origin master      |把上面的更新抓下來                                 |
| git clone SSH網址           |把別人的專案載下來，也可以在網頁上直接按Fork複製到自己那邊|

> Q：Hook?  
> A：像是偵測事件發生等等。例如在commit前做一些檢查

---
### Git進階指令  |
- rebase
- cherry-pick
- tag