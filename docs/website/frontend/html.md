## HTML
### Html 是什麼
HyperText Markup Language，翻作超文本標記語言，通常由很多標籤組成。

### 網頁基本架構
- `<!DOCTYPE HTML>` 放在第一行，表示用的是最新的HTML版本
- `<head>` 放網頁基本屬性，`<body>`放 網頁主要內容

---

### DOM 是什麼
DOM 的全名是文件物件模型（`Document Object Model`），將（HTML）檔案蓋成一個有層級的架構，就像是一顆樹，或者是族譜那樣。在這棵 DOM 樹上，不同的節點就是樹上的枝葉、族譜上的成員。特別注意的是，結點是由上往下，跟族譜差不多；樹的概念剛好相反，是由下往上，這邊只用來比喻，沒有方向的意思在內（精確點就想像成以天空為土壤、從上往下長出來、倒立著的樹吧）。節點可以分成：
1. 元素節點 element
2. 文本節點 text
3. 屬性節點 attribute

元素節點就像大祖宗，可以包含其他兩個的標籤，像是 div、p 等。文本節點指的是內容，像真正會呈現在網頁上的 'Hello world'。屬性顧名思義，就是標籤的不同性質，其實就是將 HTML 換個方式描述。有了 DOM 樹，就可以用 `document.querySelector` 等方式，選想要的節點，然後進行各種操作。另外有 `BOM`，`Browser object model`，瀏覽器對象模型，是用 javascript 訪問瀏覽器的接口。<br>
最後，網頁從零到有的建構過程是：
1. 構建 DOM，蓋骨架
2. 從上到下、從左到右布局，將節點排列成一串，然後把各種屬性的東西對應好
3. 開始渲染，把東西放上去

-----

### 網頁屬性
- ```<meta >``` 放在 head 裡面，因為這個標籤沒有內容（兩個標籤之間不會夾東西，只會標屬性），所以可以不用加第二個標籤，直接用 / 關閉。  
例如 ```<meta charset = " utf8 "/ >```
- ```<title> ``` 網頁標題，會顯示在瀏覽器分頁標籤  

-----

### 常用內容
- ```<div>``` 最常用的標籤，將內容分段、分區。由於div會自動換行，通常用在段落間的大範圍區分
- ```<span>``` 和 `div` 用途一樣，但 `span` 不會換行，因此用在一個段落間，要特別標註某幾個字、某幾句的時候
- ```<h1><h2><h3><h4><h5><h6>``` 字體從大到小，放網頁主標題、副標題等等
- ```<p>``` 放段落文字，和 h1~h6 搭配使用
- `<img>` 放圖片。`alt`是圖片無法顯示（像網址掛掉）出現的替代文字；`title`是滑鼠移到圖片時出現的文字；`src`是 source，放圖片來源。例如
```html
<img　alt = "替代文字"　title = "標題"　src ="網址" > 
```

----
### 清單
```html
<ul>　
    <li> 第一行</li>　
    <li> 第二行</li>
</ul>
```

- ```<ul>``` 無排序清單，呈現時列點表示。用法是將 `ul` 當作容器，下層包覆 `li`。例如
- ```<ol>``` 排序清單，用法和 ul 相同，但列表顯示數字 `1. 2. 3.`
- ```<li>``` 清單項目

-----

### 表格
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

### 表單
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

- `<input> `決定輸入類型，用 `div` 包起來就會分行。輸入的 `type` 有 `text、password、email、date、radio（單選）、checkbox（複選）`等等。在 `radio` 和 `checkbox` 當中，不同選項的標籤中要指定 `name` 才會形成一個group，變成一組選項。另外加入 `id label` 的話，文字會和選項綁在一起，點選文字也可以選到該選項

-----

### 超連結
- `<a>` 錨點、超連結，可以連到外面網頁，或該網頁中某個地方（像網頁底層）。標籤中有兩個屬性：
    - `target` 表示要不要另開分頁，`self` 是直接在原有分頁開啟，`_blank`是另外開一個新的。  
    - `href`（hypertext refernce）表示連結地址，可以放網址或標籤。連到網頁其他位置時，要在標籤中加入 `id = "p1"` 等位置，再用 `href =  # p1` 連過去。
```html 
<a　href = "網址"　target ='_blank' > 超連結名稱 </a>
```

- `<iframe　src = "網址"　width = "寬度，100%等"　height = "高度" >` 把別人的網頁鑲嵌進來，但有些網頁會拒絕被嵌入、存取

-----

### 語義化元素
不會改變網頁外觀，跟 div 很像，但讓其他人看 html 程式碼時更直觀、更好懂
- ```<header>```
- ```<nav>``` 導覽列
- ```<section>```
- ```<article>```
- ```<aside>```
- ```<main>``` 網頁的主要元素
- ```<footer>``` 網頁底端（像copyright、liscence）

-----

### 其他
- ```<pre>``` 保留完整格式，例如空行時，html會將多個空白表示成一個，`pre`可以維持原狀
- ```<!-- 註解-->``` 會被忽略不顯示，放備註，兩條橫線間不用加空格
- ```<br>``` 換行，加不加 `/` (slash) 關閉都可以

-----

### Escape 跳脫
使用時機：為了讓某些符號不經過轉換，直接呈現在網頁上
```
(1) < ：用&lt表示
(2) > ：&gt
(3) & ：&amp
```

------

### SEO（Search Engine Optimization）搜尋引擎優化
目的：幫搜尋引擎理解你的網頁、更好抓到資料  
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
