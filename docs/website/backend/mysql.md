## 資料庫
- 資料庫系統：專門處理「資料」的程式
- 關聯式資料庫
  - 就像 excel 表格，可以用某一欄連結不同頁的資料
  - 正規化 Normalization
  - 操作工具：SQL(sequel)
  - MySQL、PostgreSQL、MongoSQL
- NoSQL(Not only SQL)(另一種資料庫格式)
  - 像是用 object 存
  - 結構比較彈性，要新增東西可以直接加，不用新增一整欄
- 協助管理資料庫的東西：phpMyAdmin、Adminer、Sequel Pro
  - 別人寫好的php檔案

- - - - -

### NoSQL (Not only SQL)
- SQL：關聯式資料庫；NoSQL，混用關聯式和非關聯式資料庫
- 沒有結構(schema)，不支援 `join`、標準的 SQL 語法，通常用 API 來做管理。
- 就像是存 JSON 進去 DB (database) 一樣，用 key-value 對應方式來存，資料調整較有彈性
- 可以水平擴充，增加伺服器節點、機器數量就能擴大容量，擴充方便，存大量資料時用到
- CAP 理論：通常選用兩種來設計，難以全部兼顧，多是 CP/AP
- Consistent 一致性：資料遲早會一致，因此放給各節點分別異動，最後再一起同步，可能會有時間差，這需要使用者自己解決遺失或衝突的問題
- Availability 可用性：
- Partition Tolerance 中斷容忍性：
- 例子：MongoDB

- - - - -

### MySQL
### Table 表格基礎
- table schema(表格結構)
  - (欄位)名稱
  - 型態(INT、TEXT)
  - 長度
  - 預設值、空值(能否為空)
  - 編碼與排序
  - 屬性(非負數等)
  - 索引 index：需要空間，但可以方便快速定位。有 index、primary index、unique index
  - A_I(auto increment)：數字自動增加，通常用在 id，保證遞增不重複，但可能不連續(有東西被刪掉就不連續)
  - 主鍵(PK，primary key)：不能為空、不能重複，最主要(判別)的欄位

- - -

### 語法簡介：CRUD，(create, read, update, delete)
### select (選取)
  - 一般情形下，字串不用反引號 ` `` ` 包住也沒關係，除非字串中有命令字元才會造成混亂
  - 指令用大寫表示，和其他文字做區隔
```sql
SELECT * FROM `table_Name`
SELECT * FROM table_Name WHERE user = `dd` AND id = 3
SELECT * FROM table_Name WHERE a = `a` OR b = `b`
SELECT id_Name AS new_Name FROM table_Name /* 選取的時候也改名 */
SELECT column_Name1 , column_Name2 FROM tables_Name ORDER BY ASC /* 升冪排序 */
SELECT * FROM datas LIMIT 30 OFFSET 10 /* 從第11個開始選取30筆資料 */
```


### insert (插入)
```sql
INSERT INTO `table_Name`(col_1 , col_2) VALUES ( 'context' , 2 )
```


### update (更新)
```sql
UPDATE `table_Name` SET col_Name1="abc" , col_Name2 = 2 WHERE id_Number = 5
```


### delete (刪除)
- 有時候為了避免誤刪，會增加 is_Delete 的 boolean 標籤，如果要刪掉就把值設成1，讓資料看不到
```sql
DELETE FROM `table_Name` WHERE id_Number = 5
```

### JOIN：合併表格
- [參考資料](https://www.w3schools.com/sql/sql_join.as)
- inner join 取交集
- left join 取左邊全部，右邊有交集才會放進去
- right join 取右邊全部
- full order join 取聯集
```sql
SELECT table1.id, table1.content, table2.username FROM table1, table2 WHERE table1.id = table2.id
SELECT comment.id, comment.content, users.nickname FROM comment JOIN users ON comment.user_id = users.id /*  建議用這個  */
```

- - - - -

### MySQL 內建函式
  - COUNT：看有幾筆資料
  ```sql
  SELECT COUNT(id) FROM `comments` 
  ```
  - SUM：加總欄位
  
  - AVG：欄位平均
  
  - CONCAT：把兩個欄位合併
 ```sql
SELECT CONCAT(id,names) FROM `comments`
 ``` 

### 非函式條件：between、in、like
```sql
SELECT * FROM `comments` WHERE id in (1,2,3) /*  搜尋 id=1 or 2 or 3 的寫法  */
SELECT * FROM `comments` WHERE content LIKE "%h%" /*  搜尋有 h 字元的資料，找 h 開頭用 h%  */
```

- - - - - 

## 第一正規化 First normal form
1. 欄位只能有一個值
2. 消除意義相同的欄位
3. 決定主鍵

- - - - -

## View
- 在資料庫當中建一張虛擬的、只供檢視的 table，phpMyAdmin 當中的檢視表
- 購物網站：一張 table 存商品（名稱、數量、價格），另一張 table 存訂單（使用者、訂購商品數量、價格），價格存兩次是因為可能有折扣
- 開放給外人、被限制的使用者用，就不用開放整個資料庫內容
- 結構不能直接操作、改變，但可以透過改 `query` 語法修改
- 缺點：不好維護

```SQL
CREATE VIEW view_name AS
    SELECT o.id, o.user_id, u.username, p.name, o.quantity*o.price as total 
    FROM order as o
    JOIN users as u on o.user_id = u.id
    JOIN products as p on o.product_id = p.id 
    ORDER BY o.id ASC
    
/* 以後要撈資料時 */
SELECT * FROM `view_name`
```

- - - - - 

## Stored Producer
- 就像是 sql 的 function
- 另一種函式寫法：在 php 裡面寫 function
- phpMyAdmin、database 裡面的預存程序可以看或編輯

```SQL
/* SQL 內建函式 */
SELECT SUM(price) FROM `order_detail`

/* 自訂函式 */
DELIMEITER //  /* 把結束符號從分號改成斜線，才不會在函式碼結束時，分號就被解讀成函式結束，造成錯誤 */
CREATE PROCEDURE function_name(id INT)
    BEGIN
        SELECT * FROM table_names WHERE user_id = id;
    END //
DELIMETER ;

/* 函式使用 */
CALL function_name(1)
```

- - - - - 

## Trigger
- 就像 hook 一樣，處理發生事件前、後要做什麼
- 用來監控變動、或是在改錯時調回來
- phpMyAdmin 中的觸發器

```SQL
DELIMITER //
CREATE TRIGGER tRrigger_name
    BEFORE UPDATE ON table_name /* 也有AFTER，資料類型又分成 OLD 或 NEW */
    FOR EACH ROW
BEGIN
    INSERT INTO trigger_name(product_id, name, price, action)
    VALUES(OLD.id, OLD.name, OLD.price, 'UPDATE') 
END
DELIMITER ;
```

- - - - - 

## Transaction
- 不可分割的 `query` 動作，例如轉帳，必須要一正一負，或是購物，要確保東西都有庫存
- 一次執行多筆動作時，如果包在同一個 transaction 裡面，就會一次執行，而不是一個個慢慢執行
- InnoDB 可支援此動作，MyISAM 不支援

```php
$conn->autocommit(FALSE);
$conn->begin_transaction();
$conn->query('UPDATE ... FROM ... WHERE ... ');  //動作一
$conn->query('UPDATE ... FROM ... WHERE ... ');  //動作二
$conn->commit();
```

```php
if ( ... ){
    $conn->rollback();
} else {
    $conn->commit();
}
```

- - - - - 

## ACID
- 為了確保 transaction 的正確性，要符合四項特性
    1. atomicity 原子性：最小運作單位，全有全無，動作一請成功或一起失敗
    2. consistency 一致性：資料一致，例如總數相同
    3. isolation 隔離性：不同 transcation 之間不能同時動作、有先後順序，否則會造成混亂
    4. durability 持久性
- [一致性的概念](https://www.zhihu.com/question/31346392)

- - - - - 

## Lock
- 避免 race condition，有兩方同時抵達、同時發出要求(例如搶購)，導致資料數量判斷有誤
- 執行 transaction 時將東西鎖起來，阻止其他人存取
- 有加 `where` 只會 lock row，否則會 lock all table

```php
$conn->autocommit(FALSE);
$conn->begin_transaction();
$conn->query('SELECT ... FROM ...  WHERE ... **for update** ');  //在結尾標註 for update
$conn->execute();
$result = $stmt->get_result();
if (...) {
    ...
}
$conn->commit();
$conn->close();
```
