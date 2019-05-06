[《零基礎的小明要如何成為前端工程師？》](https://medium.com/hulis-blog/frontend-engineer-guide-297821512f4e)

1. FrontPage & DreamWeaver：基礎網頁架構，簡單的 HTML & CSS
2. jQuery：Library
3. CSS preprocessor (SCSS → CSS) & Post CSS (CSS → 加上 pre fix 的 CSS)
4. Browserify
5. gulp：task manager
6. Javascript ES6
7. Web pack：module bundler
8. React：
>只改變 state 就好，UI 就會自動跟著改變。


[《跟著小明一起搞懂技術名詞：MVC、SPA 與 SSR》](https://medium.com/@hulitw/introduction-mvc-spa-and-ssr-545c941669e9)   
[《前後端分離與 SPA》](https://blog.techbridge.cc/2017/09/16/frontend-backend-mvc/)   
[《MVC是一個巨大誤會》](http://blog.turn.tw/?p=1539)

1. MVC：把 code 切開來，讓 HTMP 和 PHP 不會混在一起。
> #### Wiki：
> MVC模式（Model-View-Controller）是軟體工程中的一種軟體架構模式，把軟體系統分為三個基本部分：模型（Model）、檢視（View）和控制器（Controller）。」

> #### 轉個彎日誌：
> ### View
> Model 2: 不具有行為，只是等別人塞資料進去的模板（template）。  
> MVC: 具有監視Model的行為，並以此去改變呈現（presentation）。  
> ### Controller
> Model 2: 接收請求與參數，轉交給Model處理，再把結果（最新的資料）塞進View。  
> MVC: 接收請求與參數，轉交給Model處理。沒其他事了。
> ### Model
> Model 2: 接收Controller傳來的參數，回傳結果。  
> MVC: 接收Controller傳來的參數，將結果通知View。

> #### Huli：
>首先，他把任何跟資料有關的操作都放到一個叫做 Model 的地方去，所以你要改任何跟資料有關的東西，都到那邊就對了。  
>再來，他也把所有跟顯示畫面有關的東西都放到其他地方去，我們就叫做 View 吧，View 裡面用一個 template 來塞入資料，不做任何跟資料有關的處理。  
>如此一來，他就把資料跟畫面顯示這兩者切開了，並且讓開頭那段 PHP code 把這兩者連接起來，先去 Model 拿資料，再把資料塞入 View 裡面輸出。那這個「連接兩者」的角色，就叫做 Controller 吧！

2. Ajax（Asynchronous JavaScript and XML）
> 在 JavaScript 裡面可以非同步的去呼叫 Server 的 API 並且拿資料回來，在 Ajax 出現之前，你要把資料帶過去都必須透過 Form 的方式，一定要換頁。可是有了 Ajax 以後，不換頁也能跟 Server 溝通。

> **利用 Ajax 跟後端同步資料，並且在前端用 JavaScript 更改畫面**，所以你無論做什麼操作都不會換頁，也可以保證前後端的資料是同步的。

3. SPA（ Single Page Application，單頁式應用）；MPA（Multiple Page Application）
>如果音樂播放網站是用 MPA 的話，每去一個新的網址就會把整個頁面換掉，那你的網頁播放器就會中斷了，這是完全沒辦法接受的事。所以唯一的解法就是：播放器永遠都在頁面上，只有其他部分的內容換掉。而這一切都是在前端用 JavaScript 來處理的。

4. SSR：解決 SPA 的 SEO 問題

5. PWA（Progressive Web App）