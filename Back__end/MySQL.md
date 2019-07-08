## 資料庫基礎
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

## Table 表格基礎
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


## 語法簡介
- CRUD，(create, read, update, delete)
- select (選取)
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
- insert (插入)
```sql
INSERT INTO `table_Name`(col_1 , col_2) VALUES ( 'context' , 2 )
```

- update (更新)
```sql
UPDATE `table_Name` SET col_Name1="abc" , col_Name2 = 2 WHERE id_Number = 5
```

- delete (刪除)
    - 有時候為了避免誤刪，會增加 is_Delete 的 boolean 標籤，如果要刪掉就把值設成1，讓資料看不到
```sql
DELETE FROM `table_Name` WHERE id_Number = 5
```

- 函式
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

  - 非函式條件：between、in、like
```sql
SELECT * FROM `comments` WHERE id in (1,2,3) /*  搜尋 id=1 or 2 or 3 的寫法  */
SELECT * FROM `comments` WHERE content LIKE "%h%" /*  搜尋有 h 字元的資料，找 h 開頭用 h%  */
```

- JOIN：合併表格
    - [參考資料](https://www.w3schools.com/sql/sql_join.as)
    - inner join 取交集
    ```sql
    SELECT table1.id, table1.content, table2.username FROM table1, table2 WHERE table1.id = table2.id
    SELECT comment.id, comment.content, users.nickname FROM comment JOIN users ON comment.user_id = users.id /*  建議用這個  */
    ```
    - left join 取左邊全部，右邊有交集才會放進去
    - right join 取右邊全部
    - full order join 取聯集

- 第一正規化 First normal form
1. 欄位只能有一個值
2. 消除意義相同的欄位
3. 決定主鍵