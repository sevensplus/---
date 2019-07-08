# Javascript
## Module
- 其他人寫好的功能，可以將程式集中修改，不用重複改同樣的東西
    1. var use = require ( 'module_name' ) 引入模組（模板、配件）
    2. use . moduleFuctName來使用這些功能
    3. 要用自己寫的 module 時，通常會用到路徑，像 require( ' ./myModule ' )

- 自己寫Module
    1. 寫完 funciont funcName {......} 之後，要加入 module.exports  =  funcName ，才能把檔案輸出出去。這邊寫什麼（也可以寫陣列、直接給內容），輸入require就會讀到什麼。
    2. 如果想要指令包，輸出時就寫成一個物件，像obj { funcOne : _____  ,  funcTwo : _____ }。另一種寫法是module.funOne = ______ ，在第二種中，module預設是一個空物件
---
## NPM（Node Package Manager）
- NPM是什麼：Module（套件）倉庫，可以載別人寫好的，也可以分享自己的

- 怎麼裝
    1. 到npm網站上搜尋工具，頁面有github連結
    2. 在CLI中執行 npm install npmName
    3. 安裝完後，現在的位置上會多出一個module的資料夾
    4. 用npm install npmName --save 會把npm資料寫進package.json（索引列表）的dependency裡面，--save --dev是寫到 devDependency，代表只有開發時用到，正式環境不會用到。另外 npm 5 之後 --save 就成為預設選項了

- 多人專案時
    1. npm init，跟git init很像。會多一個package.json檔案，會用來記錄裝過
    的npm內容
    2. 之後commit時，就可以把npm資料砍掉（等於是放入.gitignore裡面），不用打包資料庫上傳，不然檔案會很大
    3. 其他人下載完git檔後，再用npm install，電腦會用package.json的檔案自動安裝需要npm

- Package.json
    1. 裡面有一欄 script ，可以在裡面加入自己的指令 " start " : " node project.js " ,
    2. 在 CLI 中使用 npm run instruct_name，可以直接執行該指令

---

Yarn
- yarn是什麼：和npm類似，fb開發，比較新也比較快

- 怎麼用
    1. 官網下載，CLI中用 yarn -v 查看安裝狀態
    2. yarn init 安裝索引，yarn add yarnName 安裝工具，一樣會預設記錄到索引裡面
    3. yarn run start 進行某指令

程式測試
- 最基礎： console.log ( function (n) === '  ' ) ，自己一條條慢慢試
- 進階：Jest

- Jest
    1. 把 jest 套件裝好
    2. 建立一個測試檔，touch index.test.js，然後打開（用subl?）
    3. var repeat（檔案輸出的名稱） = require ( '  ./ 被測試的檔案名稱 ' )，把檔案灌進來
    4. test ( ' 程式過程與結果描述 '  ,
    function () {　expect (　repeat (輸入參數)　)　.toBe (預期結果)　} )
    5. 測試多項，可以用 describe (　'想說的話' , function {  test1 ......test n  }　) 包起來，結果會比較好看
    6. 把 package.json 裡面， script 中加入 "test" : "jest"，只測單一檔就改 " jest index.test.js "
    7. npm run test，系統會自動去找專案底下對應的jest檔案，然後進行測試。因為 jest 不是電腦原生指令，直接下jest不會有反應。比較新的版本有npx，才可以用 npx jest 執行。

- 小結：程式寫完 → module.export = ______ 輸出 → 建立測試檔
    - var 測試名稱 = require( './ 被測試檔' ) 載入資料 → 用 test 工具寫過程
    - 回到CLI，更改describe內容 → 用npm run jest 測試

TDD （Test-Driven Development ）測試驅動開發：先寫測試，一邊測試一邊寫程式

ECMA Script：一套標準、規範，就像規格說明書

- 2015年發布第六版，因此ES6 = ES2015

- 變數宣告：var、let、const
    1. const：如果設定為常數（ '123' ）的話，值不能改變；但object的值可以變動（儲存的記憶體位置沒有改變，只是在現在的位置上塞進新的東西）
    2. let 和 var 的差別： let 的生存範圍只在一個 block { } 裡面，var 在整個 function 裡面（如果 function 裡面有 if 、 for 等等 block ，let 只能在一個block裡面， var 不限）
    3. 下層的函式如果在裡面找不到變數，可以往上層（函式外面）找，但上層不能走進下層找

- 字串工具
    1. 用 `  ` 可以直接寫換行字串
    2. 要寫字串、變數、函式混合的字串時，可以用 `   ` 一起輸出，例如：
    ` this is comibation of ${ variable }  and ${  function ( )  }`

- 解構工具：把 array、obj 的東西拿出來解構，當成變數。
    1. 解構陣列
        - var [ fir , sec ] = arr，會自動對應到 arr 前兩項
        - var [ fir , sec , thir ] = [ 1 , 5 , 7 ] 會自動對應設變數下去
    2. 解構物件
        - var { name , address } = obj，會直接把物件中對應的項目裝進來，塞入需要的變數中
        基本上就是同時進行變數宣告、變數值設定的動作
        - 也可以雙層解構，用 var { family { father } } 的方式取物件（name）
        （物件型態為 obj = {   family : { father : name }   }）
    3. 函式參數解構
        - function deposition ( { a , b } ) {  return  ( a , b )  }
        deposition ( { a : 1  ;  b : 2 } ) 就可以直接取出值

- 展開運算子
    1. 陣列展開
        - arr = [ 4 , 5 , 6 ]，若用[ 1, 2 ,    ... arr   , 3 ]，能直接展成 [ 1 , 2, 4,5,6 , 3 ]，相當於把[ ] 拿掉
        - 如果直接讓 arr = arr2 的話，兩個陣列會指向同樣位置，展開就能存到不同記憶體。物件也一樣
    2. 物件展開
        - 把{ } 拿掉，例如 obj 3 = {  ...obj1  ;  c : 3  }，就把obj 1的內容丟進去
        - 後面的會取代掉前面的，若 obj 1 裡面也有 c 的值， c 會被取代成 3、被後面的值蓋掉
    3. 函式參數展開
        - function test ( ...arr ) 會等於 function test ( 4 , 5 , 6 )

- 反向展開 （把東西集合起來）rest parameter
    1. 陣列
        - var [ first ,   ...rest   ] = arr，陣列剩下的東西會被丟進 rest 裡，並成為陣列
        - 特別注意...rest 一定要在最後
    2. 物件
        - 跟陣列一樣， var { a ,  ... rest  } = obj，如果 a 不寫 rest 就會是整個物件
    3. 函式
        - function test ( ... args ) { ... } ，若 test ( 1 , 2 ) 就會傳入陣列而不是兩個變數，這邊args沒有事先定義一個陣列，因此作用時會變成陣列

- 函式預設值
    1. 函式
        - function default (  a = 2 , b=3  ) { ...... }，如果變數沒有定義的話就會傳預設值
    2. 解構
        - const { a = 1 , b = 2 } = obj ，如果 obj 裡面沒有可以解構的參數的話，就會被丟進預設值

- 箭頭函式
    1. 原本的函式：function test (n) { .... }
        - 箭頭函式：const test = (n) => { ... } ，只有一個參數的話就 const test n => { ... }
    2. 原本的指令 arr. filter (   function (value) { return value >1 }   )
        - 箭頭函式 arr. filter (   value => { return  value >1 }   )   ／  arr.filter (value  =>  value>1 )

- Import & Export
    1. 輸出檔：在 function、variable 前面加 export 就可以了
        - 可以用大括號寫在一起，export {  function as new_name , variable   }，並改掉輸出名字
        - export default function ......，import 就直接輸入名稱，不用加{ }
    2. 輸入檔：import { 名稱 }  from  '  ./names  '
        - 用npx babel-node index.js 來跑測試（輸入檔）
        - import {  function as new_name , variable  } 可以再次改掉輸入東西的名字
        - import * as   utils   form ' ./document  '，全部一起輸入進來，各個被輸入函式、變數名就改為 utils.function

- Babel：把比較新的語法，轉成比較舊、瀏覽器可以跑的語法
    1. 到官網安裝，在CLI執行 npm install --save-dev  @babel/core @babel/node
    2. 設定東西，npm install --save @babel/present-env，才能轉換語法
    3. 使用這個套件，新開檔案touch  .babelrc，打開它 subl  .babelrc，
    裡面寫{  "present" :  [ " @babel / present-env " ]  }，就可以跑了

- 其他 ES6 語法
    1. Map
    2. Set
    3. Symbol

## class
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