## Closure（閉包）
### 什麼是 Closure
> 在電腦科學中，閉包（英語：Closure），又稱詞法閉包（Lexical Closure）或函式閉包（function closures），是參照了自由變數的函式。這個被參照的自由變數將和這個函式一同存在，即使已經離開了創造它的環境也不例外。所以，有另一種說法認為**閉包是由函式和與其相關的參照環境組合而成的實體。**(wiki)

> 閉包（Closure）是 **函式（function）** 以及該函式被宣告時所在的 **作用域環境（lexical environment）** 的組合。(MDN)

### 特性
- 函式能存取外部變數
- Javascript 把函式當成物件，因此，函式可以成為另一個函式的參數 or 回傳值
- 函式被呼叫時，會創造一組新環境
- closure 能夠保留環境，即使外層已經回傳了，只要內層還在，就能夠抓到外層物件（內層會有 scope chain）

### 應用
- 模擬物件導向裡面的 private member，就不會被外部環境操作竄改
- 資料隔離，可以用同一個函式，產生不同的兩組數值。`var data1 = func1(); var data2 = func1()`


### closure 的例子：錢包
```javascript
function getWallet() {
  var my_balance = 999
  return {
    deduct: function(n) {
      my_balance -= (n > 10 ? 10 : n) // 超過 10 塊只扣 10 塊
    }
  }
}
var wallet = getWallet()
wallet.deduct(13) // 只扣 10 塊
my_balance -= 999 // 無效，外部存取不到，只能從內部改動
```

### 其他範例
```javascript
// 範例一
function test() {
  var a = 10;
  function inner() {
    console.log(a);
  }
  return inner;
}
var inner = test();
inner();  // 10

// 範例二
for(let i=0; i<=4; i++) {  // let：每跑一圈都會產生一個新的作用域，不用擔心 alert 的 i 都是 4
  btn[i].addEventListener('click', function(i) {
    alert(i)
  })
} 

// 範例三之一
function createCounter(){
    var count = 0;
    return function (){
        count ++;  // 放在 function 裡面的才會被 return、被執行
        return count;
    }
}
var counter = createCounter(); // counter 是一個 function
console.log( counter() ); // 1
console.log( counter() ); // 2

// 三之二
function createCounterAgain(){ 
    var count = 0;
    count ++;
    return function (){
        return count;
    }
}
var counter = createCounterAgain();
console.log( counter() ); // 1
console.log( counter() ); // 1

// 三之三
function createCounterThird(){
    var count = 0;
    return function (){
        count ++;
        return count;
    }
}
var counter1 = createCounterThird(); // 兩個不一樣
var counter2 = createCounterThird();
counter1();
counter1();
console.log( counter1() ); // 3
console.log( counter2() ); // 1

```

#### 參考資料
- [所有的函式都是閉包：談 JS 中的作用域與 Closure](https://github.com/aszx87410/blog/issues/35)
- [hoisting & Scope & EC](./hoisting_n_execute) 筆記
