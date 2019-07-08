# 基礎計算機概論
## 軟體工程師分類
- Desktop
- WEB
- Mobile
---
## 網頁名詞介紹
- ip位置：地址
- 網址：域名（地名、建築物名等）
- DNS：將域名轉換成ip位置，電腦只看得懂ip。google
- 網頁：一個瀏覽器看得懂的檔案（HTML），由瀏覽器顯示出來。常用編輯器像sublime，vscode，atom
> Q: 為什麼網頁會跑掉？   
> A: 瀏覽器讀取程式碼的標準、要求不同，有時候會造成不符的狀況
-----
- 內網：像是公司、住家，會分配到不同的虛擬ip
- 外網：家裡的電腦在對外時，會共用一個ip
- vpn：像是先連到學校內部，再用學校ip連到其他地方
---
- Session：以登入來說，在網站後端，會有session id（亂碼）和內容（用戶名）
- cookie：瀏覽器存資料的地方
- 登入後 → server回傳response，要求瀏覽器內放入id（如h9wr03j0）→ 瀏覽下一頁、發送request時，瀏覽器會自動帶上id值 → server查詢後找到資料，確定身分。
- 有點像是申請（登入）、確認（登入成功）、發放識別證（cookie紀錄id）的概念

---

## 網路基礎概念
- 訊息來源、訊息目的地、三次的前置作業（確認收發功能正常）
- 標準化訊息格式、分為header ／ body、用狀態碼標準化結果、用動詞標準化動作
- 不同代號、不同格式、有些不一定要經過確認、沒有地址也可以
- Protocol 協定：一套標準，像一套資料交換模式等等
---
- HTTP是什麼：一套協定
- Client、Server、Request：按右鍵 → 檢查 ／ Windows按 F12就可以看背後運作內容
    1. 瀏覽器傳 HTTP Request 給 Server
    2. Server 傳 response 回來，被瀏覽器解讀顯示
    3. 其他：可以載軟體 Charles 來看 request 等資訊

- DNS ：把 domain name 翻譯成 ip
    1. client 發送 request 問 DNS Server 某網址是哪
    2. DNS 給答案

- 瀏覽器是什麼：一個程式。沒有瀏覽器也可以開網頁、發 request 給 Server 等等。像可以在CLI當中先 npm install request，然後用這個封包去載網頁（可以拿下原始碼，但沒有瀏覽器翻譯會是純文字檔）

- Header 與 Body ： request 與 response 都分成這兩種，前者發額外資訊，後者是額外內容

- HTTP Method
    - GET 與 POST：前者是請求資料，後者是提交資訊（送去對面）
    - PUT：取代原本內容的整個東西，PATCH 是只改某一部份，不會蓋掉全部
    - DELETE：刪除資源
    - OPTION：支援哪些方法

- HTTP 狀態碼
    - 1xx ：要進行一些處理
    - 2xx ：成功。201 OK，204 成功但沒有回傳任何東西
    - 3xx ：重新導向。301 永久改變，302 暫時改變
    - 4xx ：失敗（client）
    - 5xx ：伺服器錯誤。503 伺服器過載

- 網路的層級：
    1. OSI，共七層。實體層、資料鏈結層 ／ 網路層 ／ 傳送層 ／ 會談層、表現層、應用層
    2. TCP / IP，四層。鏈結層（實體電纜等） ／ 網路層（IP） ／ 傳送層（TCP、UDP） ／ 應用層（HTTP）
- IP地址
    1. IPv4 ：32 位元，8 位元為一單位，用二進位 = 2 ^ 8 ，因此用十進位表示的話，有四個數字、每個數字在 0 - 255 之間
    2. IPv6 ：解決 IPv4 不夠用的問題。128位元，使用八組數字
- 不同的IP
    1. 固定ip：不會變、可以直接連過去。Server 一定有固定ip
    2. 浮動ip：個人用不需要固定 ip，也可以避免駭客攻擊等等
    3. 虛擬ip：內網相互連結用的ip，外面連不過來

- Port：連接埠（段口），接在ip後面，例如210.224.5.10 : 443，選擇在同個 ip 下的不同要求（服務）
    1. 測試時常用：3000、4000、8080
    2. 預設：443

- TCP 與 UDP：傳輸層的協議，確定連結的順利性、穩定性（是否雙方都能收到回應）
    1. TCP：比較穩定、可靠的連結，大部分建立在這上面。TCP 的三次握手用來建立連結（A傳B、B傳A、A回復B）
    2. UPD：比較快速，像視訊就需要快速傳輸

- API（Application programming interface）應用程式介面：用來交換資料。分為使用 API ／ 提供 API，像我們就要用作業系統的 API 來要資訊，串接某網站的 API 來拿資料、新增資料
    - API ／ Web API：最常見的就是HTTP API
    - SDK（Software development kit）：裡面有做好的API

- 資料格式
    1. 純文字與自定義格式：很自由的寫，但也要自定義function
    2. XML（Extensible Markup Language）：很像 HTML，<body>標籤格式</body>
    3. JSON（JavaScript Object Notation）：最普遍、和 javascript 很接近
        - JSON.parse( document.json ) 把 json 檔轉成 js 字串
        - JSON.stringify( obj ) 把 js 字串轉成 json 格式

- 網路交換資料
1. SOAP（Simple Object Access Protocol）：現在很少用，底層透過XML格式進行交換
2. 其他HTTP API（json 類型）：大多數API
3. 自定義交換資料：可以不用HTTP

- RESTful：不是協定，只是一種風格，方便統一格式、不會造成工程師間的混淆   

|    功能    |    指令    |       路徑        |      動作     |
| ---------- | --------- |-------------------|---------------|
| 新增使用者  |  ：POST   |  /new user        |  /users      |
| 刪除使用者  |  ：DELETE |  /delete user     |  /users/:id  |
| 查詢使用者  |  ：GET    |  /users_data/:id  |  /users/:id  |
| 使用者列表  |  ：GET    |  /users_list      |  /users      |
| 更改使用者  |  ：PATCH  |  /update_user     |  /users:id   |

-----

## 網頁攻擊
- DoS （Denial of Service）攻擊：資源有限，若有一個人一直發request給server，server就沒有心力處理其他人的request
- DDoS 攻擊：很多台電腦同時連到伺服器，伺服器會變很慢或掛掉（用木馬操控電腦）
- DNS攻擊：讓DNS Server忙不過來，DNS沒辦法告訴你伺服器在哪，所以就連不上
- 木馬與盜帳號
    - 木馬程式：駭客可以遠端操控電腦，像是偷資料、成為DDOS攻擊群
    - 暴力破解：像是用字典檔，裡面有常見的密碼組合

-----

## 程式語言概述
- [什麼是程式語言](http://it-easy.tw/assembly-language/)
- 自然語言：人類用
- 高階語言：常見的程式語言，需要用編譯器(compiler)或直譯器(interpreter)來轉換成機器看得動的程式碼
    - 程序導向語言：照一般邏輯慢慢寫
    - 物件導向語言：用「物件」觀念設計，抽象描繪物件、然後再組合物件使用。物件導向的特性為封裝(encapsulation)、繼承(inheritance)、多型(polymorphism)
    - 編譯器 compile：將原始語言編譯成目的語言，翻譯機的概念
- 低階語言：電腦本身的語言，無法進一步抽象
    - 第一代：機器語言，01組合，電腦直接看得懂的東西
    - 第二代：組合語言，很接近電腦底層，一個指令只做一兩件事
- 逆向工程
    - 從機器語言推回到組合語言：反組譯 disassembly
    - 模仿程式驗證邏輯
    - [人人都會的 apk 反編譯 by huli](http://huli.logdown.com/posts/661513-android-apk-decompile)

-----

## 網頁程式工具
- 前端：看得到的東西，HTML（網頁結構與內容）、CSS（外觀）、JavaScript（程式相關，像邏輯、表單、運算），Ajax
- 後端：看不到的動作，資料庫、Server等等
- 好用工具：chrome dev tool（只改client端的檔案，無法改到server端）
- 瀏覽器 → request → 傳給server → 存取資料庫 → respond
- Client / Server
- 資安概念：SQL Injection、XSS、CSRF

-----

## 演算法
- 衡量演算法的指標：時間複雜度、空間複雜度
- 二分搜尋法：例如要查數列間是否有某數字，先將數列排序過，然後從中間一直往下切，再下去找，可以節省逐次搜尋的時間
- 排序法
    1. 選擇排序法：從還沒排序的數字中找出最小的，移到最左邊
    2. 泡沫排序法：從左到右兩兩比較，比較大往右移（往右浮上去），做到剩下最後一個數字
    3. 插入排序法：將每個數字依次插入到適合的位置
    4. 合併排序法：將數列切成左右兩端，排序好再合併。
    Example：
    9,1,5,2,8,6 先切兩半，然後繼續切並排好，會變成1,9／5，2,8／6。1比5小，排上去，5比9小，再排上去，所以排出1,5,9，另一邊相同。
    接著，從兩個數列最左邊開始算，像有1,5,9和2,6,8。1和2比，1最小拿下來；5和2比，2拿下來……依此類推。
    5. 快速排序法：挑選基準點，比它小排左邊，比它大排右邊，重複操作
- 待閱筆記
- 待閱影片 時間複雜度(11min)   複雜度分析(33min)

-----

## 其他
- Curl
    1. curl 網址 > file_name：發送 GET 的 request ，把網頁資料抓下來（並存到某個檔案中）
    2. curl -I 網址：只要header、不要body
    3. 發 POST 資料
- ping：看看是不是能連上某個地方
- talnet：測試某個 POST 有沒有開，偵測某個部分是否壞掉。用來上 PTT
- nslookup：解析 ip 地址有哪些
- 電腦儲存單位
    - bit：只能存0／1
    - byte：1 byte = 8 bit
    - kilobyte：1 kb = 1024 (2^10)  bytes
    - Megabyte：1 MB = 1024 kb
    - Gigabyte：1 GB = 1024 MB
    - TB：1 TB = 1024 GB
    - PB、EB ......

