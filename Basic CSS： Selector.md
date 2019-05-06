## CSS（Cascading Style Sheets）階層式樣式表
### Selector
- Selector 寫法：selector { attribute : value; }
1. 直接寫在 html 的標籤裡面。  
```CSS
<div style = "background:yellow" >
```  
2. 在html的 `head` 裡面單獨寫 `style` 的標籤。  
```CSS
<style> div { background : pink } </style>
```  
3. 另外開一個CSS檔案再連接出去。  
```CSS
<link　　rel = "stylesheet"　　href = "./fileNameAndPath"　/>
```


-----


- Universal Selector：`*` ，選取html所有的內容。   
```CSS
* { color : blue }
```
- 標籤：會選到所有標籤（所有的div都會被選取）  
```CSS
div{ background : yellow }
```
- `id` 與 `class`： `id` 必須是唯一的，不能重複。`class` 可以重複，一個標籤可以有很多個 `class`，不同標籤也可以有一樣的 `class`。
```CSS
#idName {
    ...
}

.className{
    ...
}
```


-----


- 選取符合多個規則的元素
```CSS
div.class1.class2 {   
    ...
}
/* 連接處不能有空格 */

```
- 選取底下元素
```CSS
.lv1 > div > div{
    ...
}
/* 去到下兩層的div */


.lv1 div {
    ...
}
/* 選取 lv1 底下所有的div，空格代表選底下所有的東西 */
```
- 旁邊（`+`）或全部（`~`）：必須要在同一層才有用。可以用在不選第1個元素、但要選後面元素的情況
```CSS
.class1 + .class2{
    ...
}
/* 加號代表選取「旁邊」的東西，舉例來說，第1、3、4個都有class，只有第4個會被選到，因為第4個是「第3個旁邊的class」，可以想像成由上往下看 */

.class1 ~ .class2{
    ...
}
/* 旁邊（或後面）所有的標籤都會被選到，像第1、3、4個有class，3、4都會被選到 */
```
- Pseduo-classes：假的狀態（不會一直存在的狀態，某些條件才能觸發）。  
Debug 時可以按右鍵 → 檢查 → styles → Toggle element state 切換顯示狀態，不然看不到內容
```CSS
span: hover{
    ...
}
/* 對不同狀態做出設定，像hover是滑鼠移上去時改變狀態 */
```
- nth-child：選取第幾個物件
```CSS
div:nth-child(3){
    ...
}
/* 可以填first-child、last-child，裡面的數字可以填even、odd、2n、4n-1等等 */

.class .class2:nth-child(4){
    ...
}
/* 這個selector會從後面看回來，先看順序再看標籤。先選第4個元素，再看是不是class2，不是就不會回傳東西 */
```
- pseudo element：`before` & `after`
```CSS
.price:before{
    content:"要裝的內容，像$、NTD等等"
}
/* 會在標籤前面貼上一個元素 */


<div　class="price"　data-id="NTD" > 1000 </div>

.price ::before{
    content:attr(data-id)
}
/* 會把值抓出來用 */
```
----
- Selector的權重  
- 當不同指派間衝突時，` id > class > label` ，會看加權總分做計算

| !important | inline style | id數 | class數 | 標籤數 |
| ---------- | ------------ | ---- | ------ | ------ |
| 加在CSS檔案裡面 | 寫在HTML檔案標籤 |  |  |  |
