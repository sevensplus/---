HTML（HyperText Markup Language）：超文本標記語言，會有很多標籤

- ```<!DOCTYPE HTML>```放在第一行，表示用的是最新的HTML版本
- ```<head>``` 放網頁的基本屬性
- ```<meta >```放在 head 裡面，因為這個標籤沒有內容（兩個標籤之間不會夾東西，只會標屬性），所以可以不用加第二個標籤，直接用 / 關閉。  
例如 ```<meta charset = " utf8 "/ >```
- ```<title> ```網頁標題，會顯示在瀏覽器分頁標籤  
-----
- ```<body>``` 網頁內容
- ```<!-- 註解-->``` 會被忽略不顯示，放備註，兩條橫線間不用加空格
- ```<h1><h2><h3><h4><h5><h6>``` 字體從大到小，放網頁主標題、副標題等等
- ```<p>``` 放段落文字，和 h1~h6 搭配使用
- `<img>`放圖片。`alt`是圖片無法顯示（像網址掛掉）出現的替代文字；`title`是滑鼠移到圖片時出現的文字；`src`是 source，放圖片來源。例如
```html
<img　alt = "替代文字"　title = "標題"　src ="網址" > 
```
-----
- ```<pre>``` 保留完整格式，例如空行時，html會將多個空白表示成一個，`pre`可以維持原狀
- ```<br>``` 換行，加不加 `/` (slash) 關閉都可以
- ```<div>``` 將內容分段、分區，由於div會自動換行，通常用在段落間的大範圍區分
- ```<span>``` 和 `div` 用途一樣，但 `span` 不會換行，因此用在一個段落間，要特別標註某幾個字、某幾句的時候
----
- ```<ul>``` 無排序清單，列點表示。例如
```html
<ul>　
<li>第一行</li>　
<li>第二行</li>
</ul>
```
- ```<ol>``` 排序清單，用法和 ul 相同，會顯示數字1. 2. 3. 表示
- ```<li>``` 清單項目
-----
表格
```HTML
<table>　
<tr><td>橫向第一列第一格</td>　<td>第一列第二格</td></tr>
<tr><td>橫向第二列第一格</td>　<td>第二列第二格</td></tr>　</table>
```
- ```<table>``` 表格大標籤
- ```<tr>```（table row）橫向列標籤
- ```<td>```（table cell）每格標籤
- ```<th>```（table header）如果要有表格標題，可以把第一列的 td 改成 th，會顯示粗體
-----
表單
```HTML
<form>　
<div>　欄位一：<input　type = "種類" />　</div>
<div>　欄位二：<input　type = "種類" />　</div>
<div>　性別：
<input　type = "radio"　name = "gender"　id = "M" /> <label for "M"> 男性 </label>
<input　type = "radio"　name = "gender"　id = "F" /> <label for "F"> 女性 </label>　</div>
<input　type = "submit"　value = "提交／送出表單 "/>　</div>
</form>
```

- `<input> `決定輸入類型，加`div`會分行。輸入的`type` 有 `text、password、email、date、radio（單選）、checkbox（複選）`等等。在 `radio` 和 `checkbox` 當中，不同選項的標籤中要指定 `name` 才會形成一個group，另外加入 id label 的話，文字會和選項綁在一起，按文字也可以選到該選項
-----

- `<a>` 錨點、超連結，可以連到外面網頁，或該網頁中某個地方（像網頁底層）。標籤中有兩個屬性：
    - `target` 表示要不要另開分頁，self 是直接在原有分頁開啟，_blank是另外開一個新的。  
    - `href`（hypertext refernce）表示連結地址，可以放網址或標籤。連到其他位置時，要在 h1~h6 等標籤中加入 `id = "p1"` 的位置，再寫`href =  # p1` 連過去。
```html 
<a　href = "網址"／#位置　target ='_blank' > 超連結名稱 </a>
```

- `<iframe　src = "網址"　width = "寬度，100%等"　height = "高度" >` 把別人的網頁鑲嵌進來，但有些網頁會拒絕被嵌入、存取
-----

語義化元素：不會改變網頁外觀，跟 div 很像，但讓其他人看 html 程式碼時更直觀、更好懂
- ```<header>```
- ```<nav>``` 導覽列
- ```<section>```
- ```<article>```
- ```<aside>```
- ```<main>``` 網頁的主要元素
- ```<footer>``` 網頁底端（像copyright、liscence）
-----
Escape 跳脫（讓某些符號不經過轉換，直接呈現在網頁上）
```
(1) < ：用&lt表示
(2) > ：&gt
(3) & ：&amp
```
------
SEO（Search Engine Optimization）搜尋引擎優化：幫搜尋引擎理解你的網頁、更好抓到資料  
- 在`meta`設定`keyword`和`description`。例如：
```html
<meta　name="keywords"　content="關鍵字">
<meta　name="description"　content="描述">
```
- 在meta設定og（Open Graph Protocal），通常是FB在用，可以去FB偵錯工具檢視效果。例如：
```html
<meta　property="og:title"　content="標題名">
```
- JSON-ld（JSON for Linking Date），通常是google在看，就是寫一段JSON資料當作簡介。
```html
<script type="application/ld+JSON>  {......}  </script>
```
- `robots.txt`（直接在網址後面加上去），給爬蟲機器看的檔案。進去可以看到allow/disallow，Sitemap是網站地圖、跟搜尋引擎說要爬哪些網站

- 跟搜尋引擎說有哪些翻譯成不同語言、但相同內容的網頁
```html
<link　rel = "alternate"　hreflang="語言"　href ="網址"/>
``` 
- 寫給不同網站特定資料方便讀取
```html 
<meta　property="al:ios:app_name"　content="名字">　／　<meta property="twitter:app:id:ipad"　name=""　id="">
``` 
- Google Search Console ：可以看網站流量等資料
