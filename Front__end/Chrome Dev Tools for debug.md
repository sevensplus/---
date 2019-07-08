## [《chrome 網頁除錯功能大解密》](https://www.udemy.com/share/1010Q2BkIYdlpVQHw=/)
### 基礎使用
- 使用 chrome 編輯器
    - 如何開啟
        - 右鍵 → 檢查
        - 選單 → 更多工具 → 開發人員工具
    - 美化：啟用「開發人員實驗工具」的功能，然後到 `Setting` 裡面 `allow UI theme`，安裝完就可以了

- 切換載具樣式：按左上方第二個圖示（Element 隔壁），可以切換成iphone、ipad 的介面，模擬在手機、平板上的尺寸、顯示狀況、排版等等（有些網站分成手機版和pc版，不同載具上的格式略有不同）

- 常用 Chrome 插件：
    - Type sample：檢視網頁上的字體和文字大小
    - Dimensions：檢視網頁上元素間的距離
    - Pesticide for Chrome：顯示區塊元素或行內元素，檢視網頁排版
    - Wappalyzer：顯示網頁中使用了那些前端、後端技術

- 補充資料
    - [Chrome官方文件](https://developers.google.com/web/tools/chrome-devtools/?hl=zh-tw)
    - [Gitbook 上的 Chrome Devtool 手冊](https://legacy.gitbook.com/book/leeon/devtools/details)

---

### 開發人員工具
- Element：可以觀看、修改 HTML、CSS 檔，即時顯示結果，但寫完不能直接覆蓋原檔案，要再複製、貼回去。按 CSS 右上角的路徑可以在 Source 裡面開啟檔案
    - 修改內容
        - HTML：(1)直接按兩下修改屬性　(2)按右鍵新增屬性　(3)拖拉物件改變位置
        - CSS：(1)點一下新增、修改屬性　(2)Transition可以調整變化速率
    - 搜尋內容：
        - HTML 快捷鍵，MAC：`Cmd + F`　／　Windows：`Ctrl + F`
        - CSS 搜尋：左上角的 `filter` 空格
        - 可以用指定 CSS 中的 `.class 、 #id 、 label > class` 搜尋

- Network：按重新整理（或 `CMD + R ／ Ctrl + R `）後，可以看到網頁大小，還有跑出這個網頁要花多久時間。如果花費時間太久，可以檢視各個組成元件（如JS檔、圖片檔）的大小、耗費時間，再決定壓縮哪一部份。這邊也可以模擬不同頻寬跑起來的狀態

- Timeline：按右鍵或左上角的紀錄鍵，執行後關閉，會顯示資訊。可以拉不同範圍來檢視較長或較短的時間段，以及該時間段中執行的東西
    - FPS：一秒鐘有多少張圖片來做渲染，越多張畫面越順
    - CPU
    - Scription：處理JS的事情、執行程式。Rendering：接受到訊息後為動作做準備。Painting：重繪（執行）。

- Profile：偵測耗損的CPU。  
[Timeline 和 Profile 的官方文件](https://developers.google.com/web/updates/2016/12/devtools-javascript-cpu-profile-migration)

---
### 其他

- 測試
    - 不同樣態：CSS `filter` 隔壁有 `active、hover、focus、visited、focus-within` 的選項，勾選後會顯示事件發生後的樣式。舉例來說，可以用來修改滑鼠點擊時的畫面
    - 動畫：右上方 show console → animation → 控制進度條看分鏡結果

- 開啟網頁伺服器：新增 `web server for chrome` → 可以模擬、偵測網頁內容 → 手機要使用的話要連跟電腦相同的 wifi

---
### Debug
- Console 除錯
    - 直接在瀏覽器上執行，有問題會發出警告
    - 用 `console.table` 來顯示物件資料
    - 用 `console.time、SetTimeout、console.timeEnd` 計算程式運行所花費的時間

- Event 除錯：
    - 將右邊視窗選取 `Event Listeners` 檢視綁定事件
    - 在左邊選擇 `Resource` ，到右方視窗用 `Watch` 監聽變數

- Source 右側狀態列
    - `Watch`：偵測變數
    - `Call stack`：如果進入 function 慢慢執行的話，可以看到現在位置、外層函式位置。有時候 function 會一層包一層，這個欄位可以清楚看到每一層的位置
    - `Scope`：看全域變數和區域變數、區域函數
    - `XHR Breakpoint`：偵測到特定關鍵字就會下斷點
    - 本文左下角的按鈕可以將程式碼格式化，排成方便閱讀的形式

- 斷點除錯：
    - 開啟 `Resource`，選取行數增加斷點，運行程式（程式會停在斷點上，繼續執行就走到下一個斷點），然後在右邊視窗用 `watch` 監看變數。不用 `watch` 的話，也可以直接將滑鼠移到斷點上面的程式碼，會顯示已執行的變數內容 
    - 右上角的圖示列功能
        - 第一個圖示（三角形播放鍵）：走到下一個斷點
        - 第二個（半圓弧）：走到下一行，可以看比較詳細的步驟變化
        - 第三、第四個圖示：進入、跳出 function，可以詳細執行每一行 function，前兩個都是一次執行完整個程式內容
        - 第五個：打開後會關閉所有斷點（暫時屏蔽起來），方便看整體效果，除錯時再關掉讓斷點回來
        - 第六個（暫停）：選取後可以除錯，執行時會有警告

- 偵測 HTML 標籤屬性的變更、移除：點 `Element` 文件的那行 → 按右鍵 → break on → 選擇偵測條件 → 加入狀況後按 `Resource` → 可以從 `DOM Breakpoints` 檢視 → 執行功能（觸發條件）後， `Resource` 會偵測到狀況，畫面暫停 → 可以按按鈕讓它運行
    - subtree modification：子元素變更
    - attribute modification：屬性變更
    - node removal：被刪除
