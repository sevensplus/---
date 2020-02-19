## Javascript & Website
### 使用重點
1. 介面：如何用 js 改變介面
2. 事件：如何監聽事件、做出反應
3. 資料：如何和伺服器交換資料

## 在瀏覽器中執行 js
1. 直接在將 `js程式碼` 寫在 `HTML` 裡面， `<script> javascript code </script> `
2. 將 `HTML` 連結到外面的 `.js` 檔，`<script src="./index.js"> </script>`
3. 和 `node.js` 比起來，瀏覽器支援的語法較少

-----

### Selector
- `querySelector`：輸入參數和 `CSS` 選擇器相同，只會選到符合的第一個元素
- `querySelectorall`：選符合的所有元素
- `getElementsByClassName`：`ClassName` 直接放進去就可，不用像 `CSS` 選取時要用 `.Name`
- `getElementById`：注意：指令裡面沒有 `s`，`id` 是唯一
- `getElementsByTagName`：常放在 `body` 下方，因為文件由上而下執行，如果上面沒執行過，就無法被定義進去。會把所有符合的元素抓進去，組成特殊形態的陣列

```HTML
<script>
const elements = querySelector('#a');

// 改 CSS 方法一
// 直接用 js 語法改 CSS 內容，注意用 . 的方式選取，後方不能有 - 所以要換大寫或用刮號包起來["padding-top"]
elements.style.paddingTop = '20px';  


// 改 CSS 方法二
// 先寫內容再改 class
<style>
.active{
    background : blue;
}
</style>

<div class='active'></div>
element.classList.add('active')
element.classList.remove('ClassName')
element.toggle.add('ClassName')  // 開關，開變關，關變開
</script>
``` 

-----

### 插入與刪除元素
- `removeChild`：刪掉某元素下層的東西，`element.removeChild(document.querySelector('name'))`
- `appendChild`
```html
    <script>
    const element = document.querySelector('#block');
    const item = document.createElement('div');
    item.innerText = '123';
    
    const item = document.createTextNode('123');
    element.appendChild(item)
    </script>
```    

- - -

### 改變內容
- 先用 `querySelector` 選好物件，再用 `element.innerText = 'new messenger'`
- 如果物件下面有其他東西，會全部不見被取代掉
- `innerHTML`：抓出標籤底下的所有東西，包含裡面的標籤等等
- `outerHTML`：和 `innerHTML` 相似，連自己也會抓起來

-----

### 創建按鈕
```html
<script>

    document.querySelector('.add-btn').addEventListenr('click',
    function(){
        const btn=document.querySelector('button')
        btn.setAttribute('data-value',num)
        btn.innerText = num
        num++
        document.querySelector('.outer').appendChild(btn)
    })

</script>
```

-----

### 事件監聽
```html
<script>
const element = document.querySelector('#block');
windows.addEvenListener('keyDown', function) 
element.addEvenListener('click', function(e){
    document.querySelector('body').classList.toggle('active')
}
)  
    
// 參數放  1.觸發事件  和  2.後續動作(callback function，沒事時先去做其他動作，一旦觸發再 call back 來執行這個動作)
// windows 表示在畫面的任何一個地方
// e 裡面有很多資料，像是按下哪個鍵、按的位置等等

</script>
```

-----

### 表單處理
```html
<form class='form'>
    <div>
    name: <input name='user'>
    </div>
    <div>
    password: <input name='password' type='password'>
    </div>

    <input type='submit'>
</form>
<script>
    const element = document.querySelector('.form');
    windows.addEvenListener('keyDown', function) 
    element.addEvenListener('submit', function(e){
        alert('submit')
        e.preventDefault() // 阻止預設行為，可以用來驗證表單，阻止超連結或物件送出等等
    }
    ) 
</script>

<script>
    const element = document.querySelector('.form');
    const input  = document.querySelector('input[name=password]');
    const input2 = document.querySelector('input[name=certified]');
    element.addEvenListener('submit', function(e){
        if(input.value !== input2.value){
            e.prevenDefault()
        }
        }
    ) 
</script>

```

- - -

## 事件傳遞機制
- 點到下層時，上層也被點到，也會被觸發
- 先往下捕獲，再往上冒泡
- `e.stopPropagation` 阻止往上傳遞 
- `e.stopImmediatePropagation` 阻止所有事件立刻的傳遞
- 先在按鈕上加上 `data-value = "...."`，再用 `e.target.getAttribute('data-value')` 拿到資料，可以用來寫迴圈

```html
<script>

function addEvent(className){
    document.querySelector(classname)
     .addEventListener('click',function(){
         console.log(className)
     },false)   // false會放在冒泡階段，true會在捕獲階段
}

</script>
```

- 如果用 `for` 迴圈對一系列的物件做事件監聽，不能輸出i，因為在跑完一圈時，i的值被固定成最終值了。通常會對各物件加屬性輸出
- `e.target.getAttribute('屬性名')`

-----

### Event delegation
把事件觸發條件安裝在上層，下層不管怎麼動都會被包住、觸發條件
```html
<script>

    document.querySelector('.outer').addEventListenr('click',
    function(e){
        if(e.target.classList.contains['btn']{
            alert(e.target.getAttribute('data-value'))
        })
    })

</script>
```

- - -

### 在瀏覽器上儲存資料
- 最早的方式：cookies
    - 小型文字檔，會自動帶到 server
    - 檢查 → application → storage → cookies
    - 檢查 → network → header → cookies
- Local storage
    - 檢查 → application → localstorage
    - 只能存字串
- session storage：一段期間內的
    - 不同分頁無法共用，只存在一個分頁下面
    - 其他用法都和 local storage 一樣

- - -

### 資料交換（網頁和伺服器的溝通）
- 用 node.js 和用瀏覽器發 request 的差別：node.js 是直接向 server 溝通，拿到第一手資料；瀏覽器做為一個中介者，是跑瀏覽器上的 js → 瀏覽器 → 瀏覽器的作業系統 → server 這樣一個流程，中間有第三者的介入，因此也會受到瀏覽器本身的一些限制
- 第一種：
form：我要到這個頁面，然後帶著這些參數過去。瀏覽器會發送東西過去，走到新頁面，帶上&xxx=ooo的東西等等，然後 response 直接被瀏覽器解析顯示在新的頁面
    - 每次都要換頁
- 第二種：
ajax(asynchronous javascript and xml)：回傳資料時，瀏覽器會把 response 給 js。

``` javascript
const request = new XMLHttpRequest()
//第一種寫法
request.onload = function(){
    if (request.status >= 200 && request.status < 400) {......}
}

//另一種監聽方式
request.addEventListener('load',function(){
if () {...}
})

request.onerror = function(){
    ...
}
request.open('GET','http://google.com',true)
request.send
```

- 第三種：
JSONP：json with padding。src、img不受同源政策影響。
先定義function，然後用 script裡面寫 src 連到 js ，設定好 function 拿到資料後再到`<script>`裡面寫東西，躲避同源規範

-----

### DOM 流程
### 捕獲（Event capture）與冒泡（Bubble）
DOM 樹除了像族譜外，也可以想像成一棟大樓，越大、越資深的人（或說元素）住在越低層，越小、與年輕的就住比較高。我們要到某個人，就要一層層爬樓梯上去問，找到後再爬下來，上樓的過程就像捕獲，下樓則是冒泡。   
另外特別注意，DOM 是由上往下長的（族譜那樣），用大樓來比喻只是比較好懂而已，方向不太準確。

-----

### 其他
- Same origin policy 同源協定：相同網域、相同domain就是同源，別人的瀏覽器通常都和你不同源。有相同協定、相同port、主機位置才能拿到東西，不同源的request會被擋掉
[《輕鬆理解Ajax與跨來源請求》](https://blog.techbridge.cc/2017/05/20/api-ajax-cors-and-jsonp/)
- CORS 跨來源（跨網域）資源共用的限制目的：安全性考量
- 單向傳送資料：在信件裡面放入很小、透明的圖片，一旦打開就會發request到某網址要求圖片，就可以追蹤開信狀況
- client side rendering ：動態產生，檢視原始碼不會看到任何東西
