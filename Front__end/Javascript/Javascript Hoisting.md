### Hoisting
《[我知道你懂 hoisting，可是你了解到多深？](https://github.com/aszx87410/blog/issues/34)》摘要
- Hoisting 是什麼：變數宣告提升。
    - 簡單來說，就像是在跑程式碼前把變數、函式先宣告一次（就像 `var a`），但不會執行賦值動作。在全部提升後才會開始執行程式碼，然後進行賦值等動作。
    - function 的宣告也會提升，而且優先權大於變數
```javascript
console.log(a); // function a(){}
var a;
function a(){};

funcion test(v){
    console.log(v);
    var v = 3;
}
test(5);
/* 結果是 5，可以拆解為
var v
var v
v = 5
console.log(v)
v = 3 */
```
- 為什麼我們需要 Hoisting
    - “ for mutual recursion & generally to avoid painful bottom-up ML-like order”
    - 遞迴函式的需要
```javascript
function a(n){
    ......
    b(n);
}

function b(m){
    ....
    a(m);
}
```
延伸資料
[Note 4. Two words about “hoisting”.](http://dmitrysoshnikov.com/notes/note-4-two-words-about-hoisting/)  
[JavaScript系列文章：变量提升和函数提升](https://www.cnblogs.com/liuhe688/p/5891273.html)

- Hoisting 是怎麼運作的
- Execution Context(EC，執行環境)
    - 「當你進入一個 function 的時候，就會產生一個 EC，裡面儲存跟這個 function 有關的一些資訊，並且把這個 EC 放到 stack 裡面，當 function 執行完以後，就會把 EC 給 pop 出來。」by huli
    ![image](https://user-images.githubusercontent.com/2755720/49352096-5d706b80-f6f1-11e8-82fe-8fbff9004184.png)
    - 「每個 EC 都會有相對應的 variable object（以下簡稱 VO），在裡面宣告的變數跟函式都會被加進 VO 裡面，如果是 function，那參數也會被加到 VO 裡」
    - 進入 EC 時，東西放進 VO 的順序
        1. 參數會直接被放進去，沒有值就是 undefined
        2. function 的宣告一樣是新增屬性，值是建完後回傳的東西。有同名的就覆蓋掉
        3. 變數的話，新增一個屬性並設 undefined，如果已經有，值不會被改變

- JS 引擎怎麼運作的
    - 編譯與直譯
    - 先編譯，後執行
    - LHS(Left hand side)，只在乎記憶體位置在哪裡，要賦值；RHS(Right hand side)，只看值是多少，要用

- Temporl Dead Zone
    - 「let 與 const 也有 hoisting 但沒有初始化為 undefined，而且在賦值之前試圖取值會發生錯誤。」


延伸參考資料   
[虚拟机随谈（一）：解释器，树遍历解释器，基于栈与基于寄存器，大杂烩](https://rednaxelafx.iteye.com/blog/492667)
[About compilation phase](https://github.com/getify/You-Dont-Know-JS/issues/1375)
[You Don't Know JS: Scope & Closures](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch1.md#enginescope-conversation)
[ECMA-262-5 in detail. Chapter 3.2. Lexical environments: ECMAScript implementation.](http://dmitrysoshnikov.com/ecmascript/es5-chapter-3-2-lexical-environments-ecmascript-implementation/)
[Understanding V8’s Bytecode](https://medium.com/dailyjs/understanding-v8s-bytecode-317d46c94775)
