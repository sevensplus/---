## Bootstrap
- front-end component library
    - UI Library：有一套寫好的 CSS，直接套進 Class 就可以使用
    - 一些 js 的功能(換頁等等)
- 可搭配 Bootwatch


## 其他
```PHP
echo json_encode($row);  //用來將資料轉成 JSON 格式，方便前端工作
```


## 前後端溝通
```php
echo json_encode(array('info1' => 123, 'info2' => '456'))
```
```javascript
fetch (()=>{
    ......
}).then((res)=>{
    return res.json()
}).then((info)=>{
    ...... // 處理資料
})
```

---

## Cache
- 緩存、暫存，CPU、瀏覽器、Server side 都可能有
- 讀取：從記憶體、資料庫、硬碟(讀取速度快到慢)
- 當要求資料不用很精確(或隨時更新)的時候，可以把東西存起來隨時讓人讀取，就不用每次都拿一遍資料，比較有效率
- [循序漸進理解 HTTP Cache by huli](https://blog.techbridge.cc/2017/06/17/cache-introduction/)

---


## 資料結構 Data Structure
- 陣列 Array(數組)、鏈結串列 Linked List（鏈表）、堆疊 Stack（棧）、佇列 Queue（隊列）、樹 Tree
- Stack 堆疊：東西吃完把東西拿去放，東西從下往上放，拿取從上往下拿，先進後出
    - LIFO(Last in, First out) 後進先出
    - 執行 call back function 的原理
```javascript
stack.push(1);
stack.push(30);
stack.push(6);
stack.pop(); // 結果是 6
stack.pop(); // 結果是30
```
- Queue 佇列：先進先出
```javascript
queue.push(1);
queue.push(30);
queue.push(6);
queue.pop(); // 結果是 1
queue.pop(); // 結果是 30
```


---

## javascript

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