## CSS
> CSS 是什麼：Cascading Style Sheets，階層式樣式表，用來調整網頁的美編和動畫

### CSS 寫在哪裡
1. 直接寫在 html 的標籤裡面。  
```CSS
<div style = "background:yellow" >
```  
2. 在html的 `head` 裡面單獨寫 `style` 的標籤。  
```CSS
<style> .classname { background : pink } </style>
```  
3. 另外開一個CSS檔案連接出去。  
```CSS
<link　rel = "stylesheet"　href = "./fileNameAndPath"　/>
```

-----
## CSS Selector：用來選取改動項目的方式
### 最常用 Selector
- 選`id` 與 `class`： `id` 必須是唯一的，不能重複。`class` 可以重複，一個標籤可以有很多個 `class`，不同標籤也可以有一樣的 `class`。

```CSS
#idName {
    ...
}
.className{
    ...
}
```

- 標籤：會選到所有標籤（所有的div都會被選取）  

```CSS
div{ background : yellow }
```
- 選符合多個規則的元素

```CSS
div.class1.class2 {   
    ...
}
/* 連接處不能有空格 */
```

- 選取底下元素

```CSS
/* 去到下兩層的div */
.lv1 > div > div{
    ...
}
/* 選取 lv1 底下所有的div，空格代表選底下所有的東西 */
.lv1 div {
    ...
}
```

- nth-child：選取第幾個物件

```CSS
/* 可以填first-child、last-child，裡面的數字可以填even、odd、2n、4n-1等等 */
div:nth-child(3){
    ...
}
/* 這個selector會從後面看回來，先看順序再看標籤。先選第4個元素，再看是不是class2，不是就不會回傳東西 */
.class .class2:nth-child(4){
    ...
}
```

- Pseduo-classes：假的狀態（不會一直存在的狀態，某些條件才能觸發）。  
Debug 時可以按右鍵 → 檢查 → styles → Toggle element state 切換顯示狀態，不然看不到內容

```CSS
/* 對不同狀態做出設定，像hover是滑鼠移上去時改變狀態 */
span: hover{
    ...
}
```

- pseudo element：`before` & `after`

```CSS
/* 會在標籤前面貼上一個元素 */
.price:before{
    content:"要裝的內容，像$、NTD等等"
}

<div　class="price"　data-id="NTD" > 1000 </div>

/* 會把值抓出來用 */
.price ::before{
    content:attr(data-id)
}
```

-----

### 較少用的技巧

- 選旁邊（`+`）或全部（`~`）：必須要在同一層才有用。可以用在不選第1個元素、但要選後面元素的情況

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

- Universal Selector：`*` ，選取html所有的內容。   

```CSS
* { color : blue }
```

-----

### Selector 權重判斷  
- 當不同指令衝突時，會看加權總分做計算；權重大有效，同分時後面的指令有效。權重比 ` id > class > label` 
- 每個指令可以換算成得分，分數計算為 `!important * 10000 + inline style * 1000 + id * 100 + class * 10 + tag`
    - 如 `#idName .class1` 的得分就是 `100 + 10 = 110`
    - 如果選擇同一個物件，但另一個指令只選 `span`，只拿到 `1` 分，就會被前面的壓過去。

|最重       |重|中等|輕|最輕|
|----------|---|---|---|---|
|!important|inline-style|id|class|element tag|
|           |            |  |psuedo-class|psuedo-element|
|           |            |  |attribute|  |

<br/>

|選取方式       |說明                |舉例                        |權重數       |
|--------------|--------------------|----------------------------|------------|
|!important    |加在 CSS 後面       |`div{ color:red !important; }`| 1,0,0,0,0  |
|inline style  |寫在 Html 裡面的樣式 |`<div style="color:red">`   | 0,1,0,0,0  |
|id            |                    | `#id_name`                 | 0,0,1,0,0  |
|class         |                    | `.class_name`              | 0,0,0,1,0 |
|psuedo-class  |偽類                 | `:nth-child(), :link, :hover ...`| 0,0,0,1,0 |
|attribute     |屬性選擇器           | `[type="checkbox"], [attr] ...`| 0,0,0,1,0  |
|element       |html標籤元素         | `div, span, ul, ol, li ...` | 0,0,0,0,1  |
|psuedo-element|偽元素               | `::before, ::after, ...`    | 0,0,0,0,1  |

---
### [CSS Diner](https://flukeout.github.io/) 小遊戲筆記

- Level 3：
> `ul#long`　selects `<ul id="long">`
- Level 4：
> `p strong`　selects all `<strong>` elements that are inside of any `<p>`
- Level 5：
> `#cool span`　selects all `<span>` elements that are inside of elements with `id="cool"`
- Level 7：
> `ul.important`　selects all `<ul>` elements that have `class="important"`
> `#big.wide`　selects all elements with `id="big"` that also have `class="wide"`
- Level 9：
> `p, .fun`　selects all `<p>` elements as well as all elements with `class="fun"`   
> `a, p, div`　selects all `<a>, <p>, <div>` elements
- Level 11：
> `ul.fancy *` selects every element inside all `<ul class="fancy">` elements.
- Level 12：
> `p + .intro` selects every element with `class="intro"` that directly follows a `<p>`
- Level 13：
> `A ~ B` selects all `<B>` that follow a `<A>`
- Level 14：
> `A > B` selects all `<B>` that are a direct children `<A>`
- Level 16：
> `span:only-child` selects the `<span?` elements that are the `only child` of some other element.
> `ul li:only-child` selects the only `<li>` element that are in a `<ul>`
- Level 19：
> Selects the children from the bottom of the parent. This is like nth-child, but counting from the back!
> `:nth-last-child(2)` selects all second-to-last child elements.
從後數回來
- Level 20：
> `span:first-of-type` selects the first span in any element.
- Level 21：
> `.example:nth-of-type(odd)` selects all `odd` instances of a the example class.
- Level 22：
> `p span:only-of-type` selects a `<span>` within any `<p>` if it is the only `<span>` in there.
- Level 24：
> `div:last-of-type` selects the last `<div>` in every element.
> `p span:last-of-type` selects the last `<span>` in every `<p>`
- Level 25：
> `div:empty` selects all empty `<div>` elements.
- Level 26：
> `:not(#fancy)` selects all elements that do not have `id="fancy"`
> `div:not(:first-child)` selects every `<div>` that is not a first child.
> `:not(.big, .medium)` selects all elements that do not have `class="big"` or `class="medium"`.
- Level 27：
> `a[href]` selects all a elements that have a `href="anything"` attribute.
> `[type]` selects all elements that have a `type="anything"` attribute

- Level 28：
> `[value]` selects all elements that have a `value="anything"` attribute.
> `a[href]` selects all a elements that have a `href="anything"` attribute.
> `input[disabled]` selects all input elements with the `disabled` attribute

- Level 29：
> `input[type="checkbox"]` selects all checkbox input elements.

- Level 30：
> `.toy[category^="Swim"]` selects elements with class `toy` and either `category="Swimwear` or `category="Swimming"`.

- Level 31：
> `img[src$=".jpg"]` selects all images display a `.jpg` image.

- Level 32：
> `img[src*="/thumbnails/"]` selects all image elements that show images from the `"thumbnails"` folder.
> `[class*="heading"]` selects all elements with "heading" in their class, like `class="main-heading"` and `class="sub-heading"`