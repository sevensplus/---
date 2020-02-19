```javascript
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

### javascript 小複習
```javascript
var state = {
  list = [1,2,3]
}
var newList = state.list // 指到同一個記憶體
newList.append(4)

newList // [1,2,3,4]
list // [1,2,3,4]
```
