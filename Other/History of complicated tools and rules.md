[《零基礎的小明要如何成為前端工程師？》](https://medium.com/hulis-blog/frontend-engineer-guide-297821512f4e)

1. HTML, CSS, Javascript：基礎網頁架構，HTML 寫標籤、網頁內容，CSS 切板、美編，JS 製作動畫
2. jQuery：Javascript 的 Library，載入 jQuery 的封包後，就可以用比較簡潔的方式寫 JS
3. CSS preprocessor：CSS 預處理器，先用寫程式（使用變數、函數）的方式寫 SCSS/SASS/Less/Stylus 檔，再轉換成 CSS，修改共同變數時會比較方便
4. Post CSS：幫 CSS 加上重複的 prefix，讓 CSS 能適應不同的瀏覽器。整個流程像是 `SCSS -> CSS Preprocessor -> CSS -> Post CSS -> CSS with prefix`
5. Browserify：讓 JS 可以支援 `var function_name = require('./path')`，引入 library 時先定義名稱，避免造成變數上的混亂
6. gulp：task manager，批次執行 HTML, CSS, JS 轉換格式、壓縮的工具，就不用自己手動一個個慢慢做
7. Babel：將 ES6 的語法轉換成舊式語法，讓瀏覽器可以執行
8. Web pack：module bundler，將所有東西都視為資源，可以 require library, require css......，將所有物品一次打包。打包時可以用 plugin 來進行額外動作，像是進行 scss 的轉檔等等
9. Angular：確保 DOM 的同時後端資源也有更新，改變 state 或 UI 其中一個，都會造成另一個的改變
10. React：重新渲染時只畫必須改變的部分
> 只改變 state 就好，UI 就會自動跟著改變。

- - -

- [《跟著小明一起搞懂技術名詞：MVC、SPA 與 SSR》](https://medium.com/@hulitw/introduction-mvc-spa-and-ssr-545c941669e9)   
- [《前後端分離與 SPA》](https://blog.techbridge.cc/2017/09/16/frontend-backend-mvc/)   
- [《MVC是一個巨大誤會》](http://blog.turn.tw/?p=1539)

1. MVC：把 code 切開來，讓 HTMP 和 PHP 不會混在一起。更進一步來說，把資料和畫面顯示切開
- Wiki：
> MVC模式（Model-View-Controller）是軟體工程中的一種軟體架構模式，把軟體系統分為三個基本部分：模型（Model）、檢視（View）和控制器（Controller）。」

> Model 2 is a complex design pattern used in the design of Java Web applications which separates the display of content from the logic used to obtain and manipulate the content.
> In a Model 2 application, requests from the client browser are passed to the controller. The controller performs any logic necessary to obtain the correct content for display.

- 轉個彎日誌：現在經常被談到的其實是 Model 2，而不是 MVC，這兩者不一樣
> ### View
> Model 2: 不具有行為，只是等別人塞資料進去的模板（template）。  
> MVC: 具有監視Model的行為，並以此去改變呈現（presentation）。  
> ### Controller
> Model 2: 接收請求與參數，轉交給Model處理，再把結果（最新的資料）塞進View。  
> MVC: 接收請求與參數，轉交給Model處理。沒其他事了。
> ### Model
> Model 2: 接收Controller傳來的參數，回傳結果。  
> MVC: 接收Controller傳來的參數，將結果通知View。

- Huli：
> 首先，他把任何跟資料有關的操作都放到一個叫做 Model 的地方去，所以你要改任何跟資料有關的東西，都到那邊就對了。  
> 再來，他也把所有跟顯示畫面有關的東西都放到其他地方去，我們就叫做 View 吧，View 裡面用一個 template 來塞入資料，不做任何跟資料有關的處理。  
> 如此一來，他就把資料跟畫面顯示這兩者切開了，並且讓開頭那段 PHP code 把這兩者連接起來，先去 Model 拿資料，再把資料塞入 View 裡面輸出。那這個「連接兩者」的角色，就叫做 Controller 吧！

2. Ajax（Asynchronous JavaScript and XML）
- 在 Ajax 出現前，資料更新透過 Form 傳遞，必須換頁。但 Ajax 發明後，一方面將資料丟到後端，呼叫 Server 的 API 並且拿資料(成功 or 失敗)回來，另一方面，前端不刷新換頁，直接用 JavaScript 更改畫面，比較能增進使用者體驗

3. SPA（ Single Page Application，單頁式應用）；MPA（Multiple Page Application）
- 將一部份後端的工作搬到前端上面，不管後端發生了什麼事，都在同一個頁面上，用 JS 做出頁面變動
- 如果音樂播放網站是用 MPA 的話，每去一個新的網址就會把整個頁面換掉，那你的網頁播放器就會中斷了，這是完全沒辦法接受的事。所以唯一的解法就是：播放器永遠都在頁面上，只有其他部分的內容換掉，這一切都是在前端用 JavaScript 來處理的。

4. SSR：解決 SPA 的 SEO 問題
- SPA 的搜尋問題：內容不會一開始就寫好，要透過 JS 處理才會出現，但這樣可能會導致搜尋引擎找不到內容，使得 SEO 變差
- SSR：初始頁面（第一個頁面）直接從 Server Side render，搜尋引擎就能抓到東西，之後的動作再由 JS 來進行

5. PWA（Progressive Web App）：讓 Web 用起來、看起來都像 app，沒有網路時也能使用部分功能

6. 小結
- Huli
> MVC 就是因為 code 變得越來越亂，所以將職責區分清楚的一種設計模式。SPA 就是因為想增進使用者體驗，而出現的一種在前端利用 Ajax 達成不換頁的方法。SSR 就是因為要解決 SPA 的 SEO 問題而出現的解法。