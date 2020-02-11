### Closure
[所有的函式都是閉包：談 JS 中的作用域與 Closure](https://github.com/aszx87410/blog/issues/35)
- 作用域：scope
    - 外面的變數進得去，裡面的變數出不來
    - 作用域鍊：從最裡面、自己的函式先找，然後往外找，global scope 還是找不到的話就會錯誤
    - 靜態作用域，lexical scope，語彙範疇，詞法作用域，js 是這種。相對而言的是動態作用域（dynamic scope）
```javascript
var a = 100
function test() {
  var a = 200
  echo()
}
function echo() {
  console.log(a)
}
test();  // 100，「靜態作用域是在 function 被「宣告」的時候就決定了，而不是 function 被「執行」的時候。」
```

- 閉包：closure
```javascript
function test() {
  var a = 10;
  function inner() {
    console.log(a);
  }
  return inner;
}
var inner = test();
inner();  // 10


function getWallet() {
  var my_balance = 999
  return {
    deduct: function(n) {
      my_balance -= (n > 10 ? 10 : n) // 超過 10 塊只扣 10 塊
    }
  }
}
var wallet = getWallet()
wallet.deduct(13) // 只被扣 10 塊
my_balance -= 999 // Uncaught ReferenceError: my_balance is not defined
// 成功把 my_balance 關在 wallet 裡面，外面的動作動不到它


for(let i=0; i<=4; i++) {
  btn[i].addEventListener('click', function() {
    alert(i)
  })
}
//  let 的特性：每跑一圈都會產生一個新的作用域，不用擔心 alert 的 i 都是 4
```
---

### closure
```javascript
function createCounter(){
    var count = 0;
    return function (){
        count ++;
        return count;
    }
}
var counter = createCounter(); // counter 是一個 function
console.log( counter() ); // 1
console.log( counter() ); // 2


// 放在 function 裡面的才會被 return、被執行
function createCounter(){
    var count = 0;
    count ++;
    return function (){
        return count;
    }
}
var counter = createCounter();
console.log( counter() ); // 1
console.log( counter() ); // 1


// 兩個是不一樣的東西
function createCounter(){
    var count = 0;
    count ++;
    return function (){
        return count;
    }
}
var counter1 = createCounter();
var counter2 = createCounter();
counter1();
counter1();
console.log( counter1() ); // 3
console.log( counter2() ); // 1


function arr(){
    return [1,2,3];
}
var a = arr();
var b = arr();
console.log(a === b); // false，不同的記憶體位子


// 相同的記憶體位置
var default_arr = [1,2,3];
function arr(){
    return default_arr;
}
var a = arr();
var b = arr();
console.log(a === b); // true
```