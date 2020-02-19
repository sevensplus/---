## Javascript
### 基本類型
- 比較熟悉的 Javascript 基本數據類型有五種：`undefined, boolean(true/false), number, string, null`。比較的有兩種，`bigInt, symbol`，symbol 是 EMCA6 新定義。

### 引用類型
- 引用類型是什麼？一類對象所具有的屬性和方法。
  - 一種數據結構，將數據與功能組織在一起，類似於其他程式語言的「類」
  - 包含 Object 類型，Array 類型，Date 類型，RegExp 類型，Function 類型，基本包裝類型（Boolean, Number, String），單體內置對象（Global, Math）
  - 引用類型參考自[重学Javascript之引用类型](https://juejin.im/post/5d662428e51d456206115a37)

### js 常見的執行環境
- 瀏覽器：可以用 `document` 選取 html 的 DOM 節點，可以用 fetch，發 request 等等
- node.js：可以控制檔案（讀寫電腦裡的檔案），可以架 http 環境
- 比較：和 `Node.js` 相比，瀏覽器的規則比較多，像是有同源政策的規定，會自己過濾、篩掉一些回覆，讓我們沒辦法直接拿到第一手資料。因此，為了去因應瀏覽器的規則（就是跨網域的問題），才需要執行像 `CORS`、 `JSONP` 的動作。


-----

## ES6
ES6 是什麼：ECMA Script 是一套標準、規範，就像規格說明書。2015年發布第六版，因此ES6 = ES2015

### 變數宣告
1. const：如果設定為常數（ '123' ）的話，值不能改變；但object的值可以變動（儲存的記憶體位置沒有改變，只是在現在的位置上塞進新的東西）
2. let 和 var 的差別： let 的生存範圍只在一個 block { } 裡面，var 在整個 function 裡面（如果 function 裡面有 if 、 for 等等 block ，let 只能在一個block裡面， var 不限）
3. 下層的函式如果在裡面找不到變數，可以往上層（函式外面）找，但上層不能走進下層找

### 字串工具
1. 用 ` 括起來可以直接寫換行字串
2. 要寫字串、變數、函式混合的字串時，可以寫成 `this is comibation of ${ variable }  and ${  function()  }`

### 解構
把 array、obj 的東西拿出來解構，當成變數。
1. 解構陣列
    - `var [fir, sec ] = arr`，會自動對應到 arr 前兩項
    - `var [fir, sec, thir] = [1, 5, 7]` 會自動對應變數
2. 解構物件
    - `var {name, address} = obj`，會直接把物件中對應的項目裝進來，塞入需要的變數中。基本上就是同時進行變數宣告、變數值設定的動作
    - 也可以雙層解構，用 `var {family{father}}` 的方式取物件（name）。（物件型態為 `obj = {family: {father: name}}`）
3. 函式參數解構
```javascript
function deposition ({a, b}) {return (a, b)}
deposition ({a:1; b:2} ) // 可以直接取出值
```

### 展開運算子
1. 陣列展開
    - `arr = [ 4 , 5 , 6 ]`，若用`[ 1, 2 ,    ... arr   , 3 ]`，能直接展成` [1, 2, 4, 5, 6, 3]`，相當於把 `[]` 拿掉
    - 如果直接讓` arr = arr2` 的話，兩個陣列會指向同樣位置，展開就能存到不同記憶體。物件也一樣
2. 物件展開
    - 把 `{}` 拿掉，例如 `obj3 = {...obj1; c:3}`，就把obj 1的內容丟進去
    - 後面的會取代掉前面的，若 obj 1 裡面也有 c 的值， c 會被取代成 3、被後面的值蓋掉
3. 函式參數展開
        - `function test ( ...arr ) 會等於 function test (4, 5, 6)`

### 反向展開 （把東西集合起來）rest parameter
1. 陣列
    - `var [first, ...rest] = arr`，陣列剩下的東西會被丟進 rest 裡，並成為陣列
    - 特別注意 `...rest` 一定要在最後
2. 物件
    - 跟陣列一樣，`var {a , ... rest} = obj`，如果 a 不寫 rest 就會是整個物件
3. 函式
    - `function test (... args) { ... }` ，若 `test(1, 2)` 就會傳入陣列而不是兩個變數，這邊args沒有事先定義一個陣列，因此作用時會變成陣列

### 函式預設值
1. 函式
    - `function default (a=2, b=3) { ...... }`，如果變數沒有定義的話就會傳預設值
2. 解構
    - `const {a = 1, b = 2} = obj` ，如果 obj 裡面沒有可以解構的參數的話，就會被丟進預設值

### 箭頭函式
- `const test = (n) => { ... }` ，只有一個參數的話就 `const test n => { ... }`
  - `arr.filter(value => {return value >1})`
  - `arr.filter(value => value>1)`

-----

### Import & Export
1. 輸出檔：在 function、variable 前面加 export 就可以了
    - 可以用大括號寫在一起，`export {function as new_name, variable}`，並改掉輸出名字
    - `export default function ......`
2. 輸入檔：`import { name }  from  './utils.js'`
    - 用 `npx babel-node index.js` 來跑測試（輸入檔）
    - `import {function as new_name, variable }` 可以再次改掉輸入東西的名字
    - `import * as utils form './document'`，全部一起輸入進來，各個被輸入函式、變數名就改為 utils.function

-----

### Babel：把比較新的語法，轉成比較舊、瀏覽器可以跑的語法
1. 到官網安裝，在CLI執行 npm install --save-dev  @babel/core @babel/node
2. 設定東西，npm install --save @babel/present-env，才能轉換語法
3. 使用這個套件，新開檔案touch  .babelrc，打開它 subl  .babelrc，裡面寫{  "present" :  [ " @babel / present-env " ]  }，就可以跑了

-----

### class
```javascript
// 舊的語法
function calculator(){
    ...
}
calculator.prototype.input = function(){
    ...
}

// 新的
function calculator(){
    constructor(){
        ...
    }
    work(){
        this.text = ""
    }
}
```