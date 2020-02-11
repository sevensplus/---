### This
[淺談 JavaScript 頭號難題 this：絕對不完整，但保證好懂](https://blog.techbridge.cc/2019/02/23/javascript-this/)
[JavaScript深入之从ECMAScript规范解读this](https://github.com/mqyqingfeng/Blog/issues/7)
[鐵人賽：箭頭函式 (Arrow functions)](https://wcc723.github.io/javascript/2017/12/21/javascript-es6-arrow-function/)
- 物件之外的 this
    1. 嚴格模式底下就都是undefined
    2. 非嚴格模式，瀏覽器底下是window
    3. 非嚴格模式，node.js 底下是global
```javascript
function hello(){};
hello.call('要指派給 this 的值','function 原本的參數 1','參數 2'); // 更改 this 的方式一
hello.apply('this 的值',['參數 1','參數 2']); // 更改 this 的方式二
const myHello = hello.bind('my'); // 指派 this 的方式三，一旦 bind 之後 this 就不會再改變了

class Car {
  hello() {
    console.log(this);
  }
}
const myCar = new Car();
myCar.hello(); // myCar instance
myCar.hello.call('yaaaa'); // 把 this 更改為 yaaaa
```
```javascript
// Case 1
const obj = {
  value: 1,
  hello: function() {
    console.log(this.value)
  },
  inner: {
    value: 2,
    hello: function() {
      console.log(this.value)
    }
  }
}
  
const obj2 = obj.inner
const hello = obj.inner.hello
obj.inner.hello();  // obj.inner.hello.call(obj.inner) => 2
obj2.hello();  // obj2.hello.call(obj2) => 2
hello();  // hello.call() => undefined

// Case 2
var x = 10
var obj = {
  x: 20,
  fn: function() {
    var test = function() {
      console.log(this.x)
    }
    test()
  }
}
obj.fn(); // 被呼叫的方式是 test.call()，全域呼叫，所以是 10
```


[What's THIS in JavaScript ?[上]](https://kuro.tw/posts/2017/10/12/What-is-THIS-in-JavaScript-%E4%B8%8A/)
- this 代表的是 function 執行時所屬的物件，而不是 function 本身。
- this 與 function 在何處被宣告完全無關，而是取決於 function 被呼叫的方式
- this 指的是，當 function 執行時，這個 scope 的 owner
- 當 function 是某個物件的 method，this 指的就是上層物件
- 全域變數的上層物件就是 window

```javascript
var foo = function() {
  this.count++;
};
foo.count = 0;
for( var i = 0; i < 5; i++ ) {
  foo(); // 這邊加到的會是 window.count，全域變數 count，和 foo.count 無關
}
```


[What's THIS in JavaScript ? [下]](https://kuro.tw/posts/2017/10/20/What-is-THIS-in-JavaScript-%E4%B8%8B/)
- 預設綁定 (Default Binding)：預設綁定至 window
- 隱含式綁定 (Implicit Binding)
- 顯式綁定 (Explicit Binding)：透過 bind(), apply(), call() 綁定要的元素
- 「new」關鍵字綁定：`function (a) => { this.a = a; }`

- 這個 function 的呼叫，是透過 new 進行的嗎？ 如果是，那 this 就是被建構出來的物件。
- 這個 function 是以 .call() 或 .apply() 的方式呼叫的嗎？ 或是 function 透過 .bind() 指定？ 如果是，那 this 就是被指定的物件。
- 這個 function 被呼叫時，是否存在於某個物件？ 如果是，那 this 就是那個物件。
- 如果沒有滿足以上條件，則此 function 裡的 this 就一定是全域物件: window 或是 global，在嚴格模式下則是 undefined。


[this 的值到底是什么？一次说清楚](https://zhuanlan.zhihu.com/p/23804247)
```javascript
//  JS 的三種函數調用模式
//  第一種
func(p1, p2) // 等價於
func.call(undefined, p1, p2)

func() // 等價於
func.call(undefined) // 又可簡化為
func.call()
//  第二種
obj.child.method(p1, p2) // 等價於
obj.child.method.call(obj.child, p1, p2)
//  第三種
func.call(context, p1, p2) // 先不讲 apply，這種才是正常的調用形式
//  瀏覽器的規則中，當傳送的 context 是 null 或 undefined，會默認 window

//  其他
function fn (){ console.log(this) }
var arr = [fn, fn2]
arr[0]()
arr.0()
arr.0(arr) // this 就是 arr
```