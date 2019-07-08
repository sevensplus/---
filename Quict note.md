## hw6 作業檢討
可以用語意化標籤
- nav：navigation bar，選單列，裡面可以放list（ul 和 li）
- main(IE 11不支援)，h1，p
- footer

## JS補充
- Hoisting 變數宣告提升
- 目的：在宣告function之前就使用它
- 每個作用域都會提升，在 function 裡面也會
    - function 直接提到最前面
    - 變數宣告階段會提上去，但賦值階段不會
    - 如變數已經存在就不會提升

- let 不能重複宣告，let 和 const 的宣告是temperal dead zone
    - 會提升但是會寫 a is not defined
    1. function 裡面，宣告 parameter (放入的參數)，變成undefined
    2. function 提升，放到第一步下面
    3. 同一個 scope 裡面變數還沒宣告的話，宣告提升

- 預解析


- call back function
事情好了跟我說
1. func__1
2. func__2 (func__1){
    ......
    ...拿response
    func__1(response)
}
東西拿回來再丟回去、執行func__1

func__2( func__1(data){
    ......
} ) {
    ......
}


- setTimeout(cb,time)
幾秒後執行這個function

- GET v.s. POST
cmd + curl 網址：直接發 get request 給網址

- [《Inside look at modern web browser》](https://developers.google.com/web/updates/2018/09/inside-browser-part1)


CPU = 工人
GPU 一開始為了繪圖相關，對某些運算效能（繪圖、平行運算）更好，等於對某些類型加速的CPU
Process 程序、進程(中國翻譯)
Thread 執行緒、線程(中國)
- chrome setting - 更多工具 - 工作管理員 - 程序id
- process,thread,program
一個browser裡面有很多process，用IPC溝通
每個tab都有一個process，一個掛掉其他不會掛，各自獨立，不會拿到其他tab的資料
chrome會限制process量

display:none 不佔位子，直接排出去
visibility:invisible 看不到但是佔位子

dom tree
套用節點
排版
圖層

ES5 / ES6
const obj = { a : 10 }
obj.a = 20 可以改，存的位置不會變
obj.b = 10 就不行，變成一個新的位置了
生存範圍：let以區塊為準(if  for 也是一個block)，var以function為準

this的困難問題

arrow function var add = (a,b) => { ... }

var arr.filter(n => n*2) 只有一個參數，可以把大括號省略

template string 可以多行

解構陣列：照順序取
arr = [1,2,3]
var [sec,fir] = arr
var [, , third] = arr
sec = 1
fir = 2

潛拷貝

== 比陣列或是比物件的話，是比記憶體位置，就算存的東西一樣業不會相等

《淺談RESTful HTTP》
[資料來源 by Triton Ho](https://github.com/TritonHo/slides/blob/master/Taipei%202016-04%20talk/RESTful%20API%20Design-tw-2.1.pdf)

《輕鬆理解 Ajax 與跨來源請求》
[資料來源 by Huli](https://blog.techbridge.cc/2017/05/20/api-ajax-cors-and-jsonp/)
- Ajax (Asynchronous JavaScript and XML)：非同步運行
- XMLHttpRequest

``` javascript
var request = new XMLHttpRequest();
request.open('GET', `https://api.twitch.tv/kraken/games/top?client_id=xxx`, true);
request.onload = function() {
  if (request.status >= 200 && request.status < 400) {
  
    // Success!
    console.log(request.responseText);
  }
};
request.send();
```




