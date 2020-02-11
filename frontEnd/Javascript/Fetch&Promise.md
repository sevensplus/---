## Fetch & Promise
### Fetch：新時代的 XML Http Request
```javascript
// 原始方法： XMLHttpRequest 方式
const request = new XMLHttpRequest();
request.onloan = function(res){
    ......
}

// Fetch 方式
fetch('網址')   // 直接打網址會用 Get 方式，是 Ajax，不換頁
  .then(function(res){
    console.log(res);
    let json_info = res.json();  // 把資料變成 json 格式
    let text_info = res.text();  // 把資料變成純文字
    return 123;
  })
  .then( result => {   // .then 會接收上一個函式的 return，然後拿來繼續操作。這個叫做 chaining，像 jQuery 也可以
      console.log(result);   // 會輸出123
  })
  .then( promise => {
      console.log(promise);   // 如果傳 promise 進去的化，會直接在裡面執行
  })
  .catch( err => {
      console.log('err',err);   // 要拿結果用 then，有錯誤要檢視用 catch
  })

const api = fetch('網址');   // api 結果的格式會是 promise，一種物件格式
api.then( var => {
    ...
  })
  .catch( var => {
      ...
  })


//  promise 
const doFitst = new Promise(function(resolve,reject){
    resolve(...);   // 成功的動作
    reject(...);   // 失敗的動作
})
doFirst.then( result => {
    console.log(result);  // 上面 resolve 傳什麼，這邊就會接收到什麼。當上面跑完，就會跳到這裡繼續工作
}).catch( err => {
    console.log(err);
})

// 多層call back 會長這樣
doFirst()
  .then( () => doSecond() )
  .then( () => doThird() )
.....

// 自己寫的 fetch
const get = function(url){
    return new Promise(
        (resolve,reject) => {  // 簡化的箭頭函式
            const request = new XMLHttpRequest();
            request.open('GET',url);
            request.onreadystatechange = function(){
                if(request.readyState == 4 && request.status == 200){
                    resolve(request.responseText);  // 成功後動作
                }
            }
            request.onerror = function(err){
                reject(err);   // 失敗後動作
            }
            request.send();
        }
    )
}
get('要放的網址').then(result=>{
    console.log(result);
}).catch(err=>{
    console.log(err);
})
```

- callback hell
### promise
- 標準化和非同步操作有關的程式碼，讓大家有統一的規範去呼叫
- 如果確定函式執行完後回傳的是 promise，就可以很確定的寫 `.then` 或 `.catch`
- 狀態
    - pending：還沒執行時
    - fulfilled：執行完
    - rejected：執行失敗
- Promise.all()
- polyfill：補丁，IE7 沒有fetch，polyfill 是模擬 fetch 的工具
- [待複習：call back function (第二期7-2：fetch & promise)](https://www.youtube.com/watch?v=Fwo5VUsIvd4)
    - 30:00，call back function

