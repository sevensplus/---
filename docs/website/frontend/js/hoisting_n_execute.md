## Hoisting
> 什麼是 hoisting：一個 javascript 的運行規則。在開始執行前，函式、變數會通通宣告一次，但不賦值。全部預先 run 過一輪後開始真正跑程式碼，若要賦值，必須執行到那行才有動作

### 為什麼需要 hoisting
如果沒有 hoisting，假設 A 呼叫 B，A 一定要在 B 前面。但如果 A, B 交互呼叫的話，就沒有辦法執行
 
### hoisting 的運作方式
- 先編譯，後執行
- 宣告提升，賦值不提升
- 編譯
    - 當進入一個環境（進入 function 就會產生一個環境），就會產生一個 EC（xecution Context，執行環境），裡面儲存相關資訊。這個 EC 會一層層堆疊起來（用 stack 方式，先進後出），最下面是 Global EC，最上面是當下這個。如果東西執行完，當前的 EC 就會被丟掉。
    - EC 裡面會有各種 VO（Variable object），宣告的變數、函式、參數都在裡面。參數會被直接丟進去，沒指派是 undefined；裡面的函式接著丟進 VO，名稱重複就覆蓋掉，權重高；裡面的變數最後丟進去，宣告並新增 undefined，如果已存在，則沒影響，權重最低

### 引用
- LHS 引用(Left hand side)，只在乎記憶體位置在哪裡，可能要進行賦值動作。`var a = 6`
- RHS(Right hand side)，只看值是多少，要使用。`console.log(a)`

-----

## Scope
### 什麼是 Scope
- scope 類似於變數的活動範圍，活動範圍外就無效。外層的（活動範圍大）能夠進入內層，但內層的（活動範圍小）出不去。
- 實際使用上：從內往外找，如果找到 global scope 還是沒有就會出現錯誤
- 作用域分類
  - 靜態作用域（static scope，lexical scope，語彙範疇，詞法作用域），js 是這種。作用域和呼叫位置無關，作用域宣告的時候就決定了
  - 動態作用域（dynamic scope）：變數值在執行的時候才被決定

### 範例
```javascript
var a = 100
function test() {
  var a = 200
  echo()
}
function echo() {
  console.log(a)
}
test();  // 100
```

-----

## EC（Execution Context，執行環境）
- 三大元素：VO(Variable Object)，scopeChain，this
- EC裡面，一般變數放 VO（Variable Object），函式的變數放 AO（Activation Object），AO 比 VO 多了 argument（參數）一項。
- ``

### 範例
```javascript
var v1 = 10
function test() {
  var vTest = 20
  function inner() {
    console.log(v1, vTest) //10 20
  }
  return inner
}
var inner = test()
inner()

// 1. 進入 global EC
globalEC = {
  VO: {
   v1: undefined,
   inner: undefined,
   test: function 
  },
  scopeChain: globalEC.VO
}

// 2. 執行程式碼，進入 test EC
// glocalEC > VO > v1 = 10
testEC = {
  AO: {
    arguments,
    vTest: undefined,
    inner: function
  },
  scopeChain: 
  	[testEC.AO, test.[[Scope]]]
  = [testEC.AO, globalEC.scopeChain]
  = [testEC.AO, globalEC.VO]
}

// 3. 執行 test 程式碼，進入 inner EC
// testEC > AO > vTest = 20
innerEC = {
  AO: {
    arguments
  },
  scopeChain:
  [innerEC.AO, inner.[[Scope]]]
= [innerEC.AO, testEC.scopeChain]
= [innerEC.AO, testEC.AO, globalEC.VO]
}

// 4. 執行完 inner、執行完 test、到最後一行前
testEC = {
  AO: {
    arguments,
    vTest: 20,
    inner: function
  },
  scopeChain: 
  	[testEC.AO, test.[[Scope]]]
  = [testEC.AO, globalEC.scopeChain]
  = [testEC.AO, globalEC.VO]
}

globalEC = {
  VO: {
   v1: 10,
   inner: function,  // function inner(){...}
   test: function 
  },
  scopeChain: globalEC.VO
}

// 5. 最後一行，進入inner 並執行
// 要輸出 兩個參數，innerEC.AO 沒有就往上找，testEC.AO 還是沒有再往上
innerEC = {
  AO: {
    arguments
  },
  scopeChain:
  [innerEC.AO, inner.[[Scope]]]
= [innerEC.AO, testEC.scopeChain]
= [innerEC.AO, testEC.AO, globalEC.VO]
}
```

-----

### Temporl Dead Zone
- TDZ 是什麼：針對 let 和 const，雖然有提升動作，但沒有初始化變成 undefined，所以還是存取不到。在提升到實際賦值的這段時間，就是 TDZ

### 範例
```javascript
console.log(a); // 輸出 function a(){}，函式提升權重大於變數，會蓋掉
var a;
function a(){};

funcion test(v){
    console.log(v);
    var v = 3;
}
test(5); // 5
```

### 參考資料   
- [我知道你懂 hoisting，可是你了解到多深？](https://github.com/aszx87410/blog/issues/34)
- [虚拟机随谈（一）：解释器，树遍历解释器，基于栈与基于寄存器，大杂烩](https://rednaxelafx.iteye.com/blog/492667)
- [About compilation phase](https://github.com/getify/You-Dont-Know-JS/issues/1375)
- [You Don't Know JS: Scope & Closures](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch1.md#enginescope-conversation)
- [ECMA-262-5 in detail. Chapter 3.2. Lexical environments: ECMAScript implementation.](http://dmitrysoshnikov.com/ecmascript/es5-chapter-3-2-lexical-environments-ecmascript-implementation/)
- [Understanding V8’s Bytecode](https://medium.com/dailyjs/understanding-v8s-bytecode-317d46c94775)
- [Note 4. Two words about “hoisting”.](http://dmitrysoshnikov.com/notes/note-4-two-words-about-hoisting/)  
- [JavaScript系列文章：变量提升和函数提升](https://www.cnblogs.com/liuhe688/p/5891273.html)
