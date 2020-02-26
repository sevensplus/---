## CORS
### 跨來源 HTTP 請求
> 當使用者代理請求一個不是目前文件來源，例如來自於不同網域（domain）、通訊協定（protocol）或通訊埠（port）的資源時，會建立一個跨來源 HTTP 請求（cross-origin HTTP request）。(by MDN)

也就是說，如果在網頁中用網址嵌入其他網站資源（像是 youtube 的影片、音檔等等），而不是網站本身有的資源（例如同個資料夾底下的東西），就會產生跨來源請求。在安全考量下，跨來源請求是不被允許的，因為有所謂的同源政策（Same-Origin policy），這時候雖然有成功發出 request、對方網站有給予 response，但 response 會被瀏覽器攔截。

-----

### 什麼是 CORS
CORS 是 Cross-Origin Resource Sharing，跨來源資源共用。簡單來說，就是為了處理上面的問題，讓大家可以拿到不同網域之間的資源所發展出的一套運作方式。

### 運作規則
CORS 工作的方式就是增加 HTTP Header，讓 Server 提供一些描述訊息，給瀏覽器審閱。而 get 以外的請求方法，瀏覽器必須要有 preflight 預檢定。當 server 認可之後，再發送真正的請求。

-----

### Request
Request 分成簡單請求和預檢請求兩種，如字面上的意思，前者不會觸發預檢，不用先確認一次是否能夠近進行通訊，會直接執行動作；後者則會先進行如 OPTION 動作的預檢。以下說明這兩種的分類標準
- 簡單請求（simple request）
  - 僅允許下面三種方法：get、head、post
  - 僅允許 user-agent 自動設定的 header（connection，user-agent），或以下的 CORS-safelisted request-header
  - 沒有 event listener 被註冊到發出請求的 XMLHttpRequestUpload 上
  - 沒有 ReadableStream 被上傳
- 預檢請求（preflighted request）：劃歸條件和上面相反
  - 包含 PUT、DELETE、CONNECT、OPTIONS、TRACE、PATCH
  - 設定下面以外的 header 會被劃到這類
  - content-type 指派三種選項外的值也會

下面是關於各種 request(from client)、response(from server) 的 header 整理，摘錄自 MDN。

|CORS-safelisted request-header|value  |
|------------------|------|
| Accept           |       |
| Accept-Language  |       |
| Content-Language |       |
| Content-Type     |1. application/x-www-form-urlencoded <br>2. multipart/form-data<br>3. text/plain  |
| Last-Event-ID    |       |
| DPR              |       |
| Save-Data        |       |
| Viewport-Width   |       |
| Width            |       |

<br>

|HTTP request headers          |value                      |
|------------------------------|---------------------------|
|Origin                        |url，請求來源               |
|Access-Control-Request-Method |預檢用，說明後續用的實際方法 |
|Access-Control-Request-Headers|預檢用，說明下次會帶的 header|

<br>

|response header               |value  |
|------------------------------|------|
|Access-Control-Allow-Origin   |* (means all)<br> url (specific website)|
|Access-Control-Expose-Headers |       |
|Access-Control-Max-Age        |       |
|Access-Control-Allow-Credentials|true       |
|Access-Control-Allow-Methods  |       |
|Access-Control-Allow-Headers  |       |

-----

### 怎麼避開同源政策、拿到資料

-----
參考資料
- [跨來源資源共用（CORS） by MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/CORS)
- [伺服器端存取控制（CORS） by MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Server-Side_Access_Control)
- [輕鬆理解 Ajax 與跨來源請求](https://blog.techbridge.cc/2017/05/20/api-ajax-cors-and-jsonp/)
