## Javascript 運作原理
### 淺拷貝與深拷貝
[深入探討 JavaScript 中的參數傳遞：call by value 還是 reference？](https://github.com/aszx87410/blog/issues/30)
- call by value
    - 把變數傳進 function 的時候，將值複製一份過去
    ```javascript
    function test(a,b){
        var temp = a;
        a = b;
        b = temp;
        console.log(`a = ${a}, b = ${b}, temp = ${temp}`);
    }
    var x = 10;
    var y = 20;
    test(x,y); // x, y 不會變
    ```
- call by reerence
    - 傳進去的是真的 x, y，只是改叫 a, b 而已，改 a, b 也會改到 x, y 
- call by sharing
    - 指向同一個東西，但重新賦值的話，會生成新的東西
![image](https://user-images.githubusercontent.com/2755720/49351766-ea1a2a00-f6ef-11e8-8ea4-f6a04b5997be.png)


[[Javascript] 關於 JS 中的淺拷貝和深拷貝](http://larry850806.github.io/2016/09/20/shallow-vs-deep-copy/)
- 「淺拷貝只複製指向某個物件的指標，而不複製物件本身，新舊物件還是共用同一塊記憶體。但深拷貝會另外創造一個一模一樣的物件，新物件跟原物件不共用記憶體，修改新物件不會改到原物件。」


[[筆記] 談談JavaScript中by reference和by value的重要觀念](https://pjchender.blogspot.com/2016/03/javascriptby-referenceby-value.html)
- primitive value(boolean, string, number, null, undefined)：拷貝值
- object, array, function ：拷貝記憶體(by reference)

---
#### hoisting 和 closure 補 V8 編譯


---

### instance
- `A instanceof B`：判斷 A 是不是 B 的 instance
```javascript
console.log(Function instanceof Object); // true
console.log(Object instanceof Function); // true
```
