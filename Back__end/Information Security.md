# 資訊安全
## 密碼安全
- 若是直接將密碼存在資料庫中，一旦資料庫被盜取，密碼也會被拿走。因此，存進去的密碼會經過加密，即使資料庫被偷走，駭客也很難反推回原本密碼
- 加密方式：使用雜湊函數
    - md5：一個單向函數。只要輸入一樣、輸出就會一樣。由於無限的輸入對應到有限的輸出，一定會有重複，因此無法從結果反推輸出，重複的情況稱為碰撞
    - SHA256：比 md5 更安全，但也更耗時
    - 暴力破解法：找出各種雜湊處理後的結果，然後和有限的密碼值對應。為了處理這個問題，因此會加鹽(salting)，即自動產生一段亂碼加入
- 參考資料
    - [加密算法反向查詢](https://www.cmd5.com/)
    - [How Dropbox securely stores your passwords](https://blogs.dropbox.com/tech/2016/09/how-dropbox-securely-stores-your-passwords/)
    - [密码破解之王：Ophcrack彩虹表原理详解](http://www.ha97.com/4009.html)


## 網頁攻擊
### SQL Injection
- 設計不良的程式讓`輸入變成程式的一部份`，因此可以用特殊的構造來控制程式碼
    - 舉例：
        ```SQL
        SELECT * FROM users WHERE username = '`'or 1=1 ——`'and password=''
        ```

       - 帳號輸入時打 'or 1=1 ——
        - 第一個單引號會和前面的單引號組成一對，然後關閉帳號輸入框
        - 後面接著的 or 1=1 確保輸出是 true，
        - —— 表示註解，會讓程式忽略後面的指令
    - 解決方式：[prepare statement](https://www.w3schools.com/php/php_mysql_prepared_statements.asp)

    ```PHP
    <?php
    $stmt = $conn->prepare("SELECT infos FROM users WHERE username = ? AND password = ?");
    $stmt->bind_param("ss",$username,$password); // s = 放字串，兩個 s 就是擺兩個字串，i 是整數
    $stmt->execute();

    $stmt->store_result();
    $row = $stmt->num_rows();

    $stmt->bind_result($hash_password);
    $stmt->fetch();

    $result = $stmt->get_result();
    echo "錯誤訊息：" . mysqli_error($conn);

    if ($result->num_rows > 0){
        $row = $result->fetch_assoc();
    }
    ?>
    ```


### XSS(Cross site scripting) 跨站式腳本攻擊
- 讓輸入變成程式的一部份
    - 網頁名稱寫成 `<h1>hi</hi>`，會被解讀成 html
    - 留言板內容填入 <script>...</script>，就可以直接執行 js 程式碼，去改頁面、偷 cookie 等等
- 型態：
    - 儲存型(stored CSS)：存在資料庫結構
    - 反射型(reflected XSS)：把東西放在網址上
- 解決方式：escape 跳脫，把輸入內容轉成純文字，或限制特殊符號的輸入

    ```PHP
    echo htmlspecialchars($str,ENT_QUOTES,'utf-8');
    ```


### CSRF(Cross-site request forgery)跨站偽造請求：利用別人的權限去執行操作


- OWASP

參考資料
- [網路安全（Ruby on Rails實戰聖經）](https://ihower.tw/rails/security.html)
- [實戰演示如何利用 SQL 注入漏洞攻破 WordPress 網站](http://www.aqee.net/post/how-to-hack-a-wordpress-site-using-sql-injection.html)
- [SQL Injection 常見的駭客攻擊方法](http://www.puritys.me/docs-blog/article-11-SQL-Injection-%E5%B8%B8%E8%A6%8B%E7%9A%84%E9%A7%AD%E5%AE%A2%E6%94%BB%E6%93%8A%E6%96%B9%E5%BC%8F.html)
- [OWASP 2017 中文版](https://www.owasp.org/images/d/dc/OWASP_Top_10_2017_%E4%B8%AD%E6%96%87%E7%89%88v1.3.pdf)
