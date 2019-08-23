- 測試網頁工具：JMeter

- 網路基礎知識
    - TCP / IP
    - OSI 七層
    - DNS
    - 三次握手
- 資料庫基礎知識
    - ACID
    - 1 NF 正規化
- 系統架構基礎知識
    - Load balance
    - replication

## 網路基礎知識
- 網路如何運作的？
    - OSI 七層協定  [參考解說](https://www.zhihu.com/question/24002080)
    - TCP / IP 四層協定
        - 下層---鏈結層、網路層、傳送層、應用層---上層
        - 從上往下傳過去、再從下往上回傳
        - Ethemet、IP、UDP/TCP、HTTP

- IP、DNS、網域
- IP(Internet Protocal)
    - 網路層
    - 192.168 或 10.0 開頭的是內網，內網表示在從一個網路、同一個 wifi 底下，只有裡面用戶才能用這個 ip 連過去，稱為虛擬ip
    - 外網 ip，又稱為固定 ip，可以順著 ip 查到電信公司的機房位置，公司才能再進一步和用戶對起來
- TCP / UDP 
    - TCP：保證建立一個可靠連線，資料一定傳送得到，因此傳送速度比較慢，例如 Broswers
    - UDP：傳送速度快，但不一定傳得到，像是音樂串流、網路電話等
    - TCP 三次握手：目的是建立穩定連線 [參考一](https://github.com/jawil/blog/issues/14) [參考二](https://notfalse.net/7/three-way-handshake)
- 網域：就是網址，花錢買的
- DNS：由網域找到 ip 位置

- 網站背後：有伺服器，伺服器就是一台電腦，只是有裝伺服器的程式
- 虛擬空間(只有存取空間，沒有主機的操控權，一台電腦可以切出很多個不同空間，租給不同人，就像 ftp)
- 虛擬主機(一台實體主機上有很多個虛擬主機，可以視為 cloud ，和實體主機類似，只是資源和他人共享，有點像是一個程式一樣，可遷移性、機動性高，也最普遍)
- 實體主機(自己有一台完整的主機)

- 怎麼管理伺服器？
- SSH：透過 cmd 操作 SSH 指令，連到遠端的主機下指令
- 遠端桌面

- VPN：先連到一台主機，再連到外面
    - 內網、翻牆

- 伺服器網路架構
- NAT(Network address translation)
    - 內網互相溝通，外網看不到，出去、進來都要經過 NAT

- Load balance 負載均衡
    - 把流量平均分到機器中
    - 永遠要有備案、有兩台以上機器
- high availability

- 快取 cache(redis, memcache)：存在記憶體裡面的 database，用 key value 來存
    - 舉例：讀短網址
      讀取短網址：request -> load balance -> cache <-> DB(slave, read) (如果找不到 cache 的話，就會直接進去 db，然後再把拿到的資料存回 cache)
      生產短網址：request -> load balance -> DB(master) -> DB(slave) -> backup db -> cache
      -[循序漸進理解 Cache](https://blog.techbridge.cc/2017/06/17/cache-introduction/)
```php
<?php
header('Cache-Control: max-age=15') // 15 秒之內會抓(之前的)暫存檔案，不會重新整理
?>
<a href="/path/cache.php"> ... </a>
```


- Database replication(備源)
    - 讀寫分離，先存到一台中，再存到另外其他台，有點像是備份
    - Master：存取用
    - Slave：讀取用

##　購買網域
- GoDaddy 買網域
- 網域和伺服器串起來
- ip server 網域串起來
- digitalocean 買虛擬主機
- AWS，雲端主機，第一年免費
- [實際架站教學 10:00後](https://www.youtube.com/watch?v=w6MN-N2OFTg)
- [架站文章](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04)

- localhost v.s. server
- port：端口

## 其他
- 單元測試、整合測試、模擬使用者測試
    - [Cypress](https://www.cypress.io/)
- hash table
- [面試想問的問題](https://www.ptt.cc/bbs/Soft_Job/M.1539503272.A.2B3.html)
- DevOps
- 