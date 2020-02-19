## Javascript
### Module
Module 是什麼：其他人寫好的功能，可以將程式集中修改，就不用重複改同樣的東西。用法如下：
```javascript
var use = require ( 'module_name' )  //引入模組（模板、配件）
use . moduleFuctName // 使用功能
require(' ./myModule ') // 引入自己寫的 module
```
### 自己寫 module
```javascript
// 輸出 function
funcion func1() {
    ...
}
module.exports  =  func1

// 輸出多個物件
// 方法一
obj = { 
    funcOne:a,
    funcTwo:b
}
module.exports = obj

// 方法二
module.fun1 = a
module.fun2 = b
```

---

### NPM（Node Package Manager）
NPM是什麼：Module（套件）倉庫，可以載別人寫好的，也可以分享自己的
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

## Yarn
- yarn是什麼：和npm類似，fb開發，比較新也比較快
- 怎麼用
    1. 官網下載，CLI中用 yarn -v 查看安裝狀態
    2. yarn init 安裝索引，yarn add yarnName 安裝工具，一樣會預設記錄到索引裡面
    3. yarn run start 進行某指令

-----
## 程式測試
- 最基礎： console.log ( function (n) === '  ' ) ，自己一條條慢慢試
- 進階：Jest
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
