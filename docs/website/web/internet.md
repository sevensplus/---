## 網路基礎
### 網頁名詞介紹
- ip位置：地址
    - 外網：像是公司、住家，會分配到不同的虛擬ip
    - 內網：家裡的電腦在對外時，會共用一個ip。彼此間可以互相連結，但外面的人進不來
    - vpn：像是先連到學校內部，再用學校ip連到其他地方
- 網址：域名（地名、建築物名等）
- DNS：將域名轉換成ip位置，電腦只看得懂ip。google
- 網頁：一個瀏覽器看得懂的檔案（HTML），由瀏覽器顯示出來。常用編輯器像sublime，vscode，atom
> Q：為什麼網頁會跑掉？   
> A：瀏覽器讀取程式碼的標準、要求不同，有時候會造成不符的狀況

---

### 網路基礎概念
- 訊息來源、訊息目的地、三次的前置作業（確認收發功能正常）
- 標準化訊息格式、分為header ／ body、用狀態碼標準化結果、用動詞標準化動作
- 不同代號、不同格式、有些不一定要經過確認、沒有地址也可以
- Protocol 協定：一套標準，像一套資料交換模式等等

---

### 瀏覽器是什麼
瀏覽器是一個程式。沒有瀏覽器也可以開網頁、發 request 給 Server 等等。像可以在CLI當中先 npm install request，然後用這個封包去載網頁（可以拿下原始碼，但沒有瀏覽器翻譯會是純文字檔）

---

### HTTP是什麼：一套協定
- 怎麼看網路背後運作內容（client, server 的溝通）：按右鍵 → 檢查 ／ Windows按 F12
    1. 瀏覽器傳 HTTP Request 給 Server
    2. Server 傳 response 回來，被瀏覽器解讀顯示
    3. 其他：可以載軟體 Charles 來看 request 等資訊
- DNS ：把 domain name 翻譯成 ip
    1. client 發送 request 問 DNS Server 某網址是哪
    2. DNS 給答案
- Header 與 Body ： request 與 response 都分成這兩種，前者發額外資訊，後者是額外內容

### HTTP Method
- GET 與 POST：前者是請求資料，後者是提交資訊（送去對面）
- PUT：取代原本內容的整個東西，PATCH 是只改某一部份，不會蓋掉全部
- DELETE：刪除資源
- OPTION：支援哪些方法

### HTTP 狀態碼
- 1xx ：要進行一些處理
- 2xx ：成功。201 OK，204 成功但沒有回傳任何東西
- 3xx ：重新導向。301 永久改變，302 暫時改變
- 4xx ：失敗（client）
- 5xx ：伺服器錯誤。503 伺服器過載

-----

### 網路層級
1. OSI，共七層。實體層、資料鏈結層 ／ 網路層 ／ 傳送層 ／ 會談層、表現層、應用層
2. TCP / IP：四層
    - 鏈結層（實體電纜等）
    - 網路層（IP）
    - 傳送層（TCP、UDP）：確定連結的順利性、穩定性（是否雙方都能收到回應），這兩種協議略有不同
        - TCP：比較穩定、可靠的連結，大部分建立在這上面。TCP 的三次握手用來建立連結（A傳B、B傳A、A回復B）
        - UPD：比較快速，像視訊就需要快速傳輸
    - 應用層（HTTP）
    - TCP 與 UDP：傳輸層的協議，

### IP
#### IP地址
1. IPv4 ：32 位元，8 位元為一單位，用二進位 = 2 ^ 8 ，因此用十進位表示的話，有四個數字、每個數字在 0 - 255 之間
2. IPv6 ：解決 IPv4 不夠用的問題。128位元，使用八組數字
#### 不同的IP
1. 固定ip：不會變、可以直接連過去。Server 一定有固定ip
2. 浮動ip：個人用不需要固定 ip，也可以避免駭客攻擊等等
3. 虛擬ip：內網相互連結用的ip，外面連不過來

### Port 
連接埠（段口），接在ip後面，例如210.224.5.10 : 443，選擇在同個 ip 下的不同要求（服務）
    1. 測試時常用：3000、4000、8080
    2. 預設：443

-----

### 網路交換資料
1. SOAP（Simple Object Access Protocol）：現在很少用，底層透過XML格式進行交換
2. 其他HTTP API（json 類型）：大多數API，通常用 RESTfUL 格式
3. 自定義交換資料：可以不用HTTP

### 資料格式
1. 純文字與自定義格式：很自由的寫，但也要自定義function
2. XML（Extensible Markup Language）：很像 HTML，<body>標籤格式</body>
3. JSON（JavaScript Object Notation）：最普遍、和 javascript 很接近
        - JSON.parse( document.json ) 把 json 檔轉成 js 字串
        - JSON.stringify( obj ) 把 js 字串轉成 json 格式

---

### 網頁攻擊
- DoS （Denial of Service）攻擊：資源有限，若有一個人一直發request給server，server就沒有心力處理其他人的request
- DDoS 攻擊：很多台電腦同時連到伺服器，伺服器會變很慢或掛掉（用木馬操控電腦）
- DNS攻擊：讓DNS Server忙不過來，DNS沒辦法告訴你伺服器在哪，所以就連不上
- 木馬與盜帳號
    - 木馬程式：駭客可以遠端操控電腦，像是偷資料、成為DDOS攻擊群
    - 暴力破解：像是用字典檔，裡面有常見的密碼組合

-----

## 其他
- Curl
    1. curl 網址 > file_name：發送 GET 的 request ，把網頁資料抓下來（並存到某個檔案中）
    2. curl -I 網址：只要header、不要body
    3. 發 POST 資料
- ping：看看是不是能連上某個地方
- talnet：測試某個 POST 有沒有開，偵測某個部分是否壞掉。用來上 PTT
- nslookup：解析 ip 地址有哪些