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
