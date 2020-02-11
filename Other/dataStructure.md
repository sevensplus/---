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
