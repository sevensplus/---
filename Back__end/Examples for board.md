- 流程   
request → apache(server) → php → html → apache → response
- Apache 的工作
    1. 把 request 丟進 php 裡面
    2. 就像是一個 server、一個程式，專門用來處理 request 和 response

## 職缺頁面實作
### __實作架構__
1. 產品（頁面）規劃
    - 產品模式(前台、後台模樣，不同指令分別對應到不同的 php 檔)
    - 資料結構

2. 資料庫設定
    - 欄位設定(名稱，資料類型)
    - 到 phpMyAdmin 新增 data 結構

3. 寫前端頁面
    - 對於前端、後端頁面，先切出簡單的 html 和 CSS 版型

4. 連線進資料庫
```PHP
$serverName = 'localhost'; //關於資料庫的訊息
$userName = 'anonymous';
$password = 'secret';
$dbname = 'mentor';

$conn = new mysqli($serverName, $userName, $password, $dbname); //連線進資料庫
$conn->query('SET NAMES UTF8'); //設定編碼，防止亂碼


if ($conn->connect_error) {
  die("connection failed: " . $conn->connect_error);
}
```

5. 後端和資料庫連結
```PHP
//add.php
//這個是新增資料(送資料)的頁面
<form method="POST" action="./handleAdd.php"> //把東西傳出去後會連到外面的 php 檔
  <div>職缺名稱<input name="title"></div>
  <div>職缺薪資<input name="salary"></div>
...
  <div><input type="submit" value="送出"/></div>
</form>
```

```PHP
//handleAdd.php
//這個是資料送到的地方，下面是運行的東西
<?php

require_once('./conn.php');

$title = $_POST['title']; //把傳送的東西丟進變數
$salary = $_POST['salary']; 

$sql = "INSERT INTO jobs(title, salary) VALUES('$title','$salary') ";
$result = $conn->query($sql); //  " -> " 的用法就和 " . " 一樣

if ($result) {
  header('Location: ./admin.php')
} else {
  echo 'failed' . $conn->error;
}

?>
```

6. 前端撈取資料庫
```PHP
//index.php，前端頁面

<?php require_once('./conn.php')?> //在最前面放這行

<head></head>

<body>
    <?php
      $sql = 'SELECT * FROM jobs ORDER BY create_at DESC'; //依照某欄降冪排序
      $result = $conn->query($sql);

      if ($result->num_rows > 0){
        while( $row = $result->fetch_assoc() ){
          ?>      //第一種方式：先把php關掉來作業
              ... //工作中
          <?PHP   //工作完再開起來

          echo "<div class='job'>";//第二種方式：直接做
          echo "<h2 class=''job_title>" . $row['title'] . "</h2>";
          echo "<p class='job_salary'>" .  $row['salary'] . "</p>";
          echo "</div>";
        }
    }

    ?>
</body>
```
```PHP
//admin.php，後台頁面
//大致上和前台頁面一樣
<a href="./add.php">新增職缺</a>
<div class=""jobs>
    <?PHP
        if ($result->num_rows > 0){}
            while( $row = $result->fetch_assoc() ){
                echo "<div class='job'>";
                echo "<h2 class=''job_title>" . $row['title'] . "</h2>";
                echo "<p class='job_salary'>" .  $row['salary'] . "</p>";
                echo "<a class='job_link' href='./update.php?id=" .  $row['id'] . "'>編輯職缺</a>";
                echo "<a class='job_link' href='./delete/php?id=" .  $row['id'] . "'>刪除職缺</a>";
                echo "</div>";
            }
        }
    ?>
</div>
```

7. 編輯與刪除功能
```PHP
//delete.php，刪除功能
<?php

require_once('./conn.php');
$id = $_GET['id'];

$sql = "DELETE FROM jobs WHERE id = " . $id;

if ( $conn->query($sql) ){
    header('Location: ./admin.php');
 } else {
     echo "failed:" . $conn->error;
 }

?>
```

```PHP
//update.php，編輯職缺
<!DOCTYPE html>
<html>
<?php

require_once('./conn.php');
$id = $_GET['id'];

$sql = "SELECT * FROM jobs WHERE id = " . $id;
$result = $conn->query($sql);
$row = $result->fetch_assoc();

?>

<head></head>
<body>
    <h1>編輯職缺</h1>
    <a href="./admin.php">回到管理頁</a>
    <form method="POST" action="./handleUpdate.php">
        <div>職缺名稱：<input name='title' value="<?php echo $row["title"] ?>"/></div>
        <div>薪水範圍：<input name='salary' value="<?php echo $row["salary"] ?>"/></div>
        <input type="hidden" name="id" value="<? php echo $row["id"] ?>"/>
        <input  type="submit" value="送出"/>
    </form>
</body>
</html>
```

```PHP
//handleUpdate.php
<?php

$title = $_POST['title'];
$salary = $_POST['salary'];
$id = $_POST['id'];

$sql = " UPDATE jobs SET title = '$title' , salary = '$salary' WHERE id = '$id'" ;
$result = $conn->query($sql);

?>
```
8. 職缺到期日
9. 排序功能
10. 會員註冊、管理職缺
11. 審核職缺
