- 基本操作
  - 不用宣告變數
  - 變數要用 `$` 開頭

```PHP
<?php // 環境設定
$a = "1"; //變數設定
$b = $_GET['username'];
$c = array(1,2,"3","4")

echo "<h1>123</h1>"; //輸出東西
echo $a . $b; //用 . 來拼接字串
echo $c[sizeof($c)-1] //用sizeof取長度

var_dump($c) //echo不能輸出array，只能輸出字串。var_dump會輸出type和value
print_r($c) //輸出array，但只會顯示value，沒有type

for ($i = 1; $i<3; $i++){
  ...
}

if ( isset($_GET['users']) ) {
  die('檢查一下'); //後面不會執行
} else {
  header('Location: index.php') // redirect 到其他地方，放網址也行
}

$conn->query("SET NAMES 'UTF8'");
$conn->query("SET time_zone = '+08:00'");

session_start(); //開始使用session
$_SESSION['user_id'] = $user_id;
session_unset();
session_destroy();

?>
```

- [參考資料](https://www.w3schools.com/php/php_mysql_select.asp)
