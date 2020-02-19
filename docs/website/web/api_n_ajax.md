## API 與 Ajax 串接
### API 是什麼
`API（Application programming interface）`中文翻做應用程式介面。簡單來說，它為使用者與伺服器提供了一個框架，讓雙方可以在這個規矩下互動、交換資料。有時候，使用者想要向某網站的伺服器拿資料，可是伺服器不可能開放完整的資料庫，一方面有資安問題，另一方面資料太多會很複雜。於是雙方使用API，伺服器開放一部份權限，使用者在這個規則下，輸入特定的指令和伺服器溝通，拿到自己想要的東西。

舉例來說，比價網站就透過API，傳送使用者提供的條件給各大網站，然後獲得資訊，整理所有的結果給使用者，這個過程就是透過API。  

### RESTful API
不是協定，只是一種風格，方便統一交換格式、不會造成工程師間的混淆   

|    功能    |    指令    |       路徑        |      動作    |
| ---------- | --------- |-------------------|--------------|
| 新增使用者  |  ：POST   |  /new user        |  /users      |
| 刪除使用者  |  ：DELETE |  /delete user     |  /users/:id  |
| 查詢使用者  |  ：GET    |  /users_data/:id  |  /users/:id  |
| 使用者列表  |  ：GET    |  /users_list      |  /users      |
| 更改使用者  |  ：PATCH  |  /update_user     |  /users:id   |

---

### 什麼是 ajax
`Ajax` 的全名是 `Asynchronous Javascript and XML`，重點在於`非同步執行`。當程式碼比較複雜的話，如果堅持要同步、一行行執行的話，可能會在某一行卡住很久；因此，我們會使用 `Callback function`，當事情處理完後再回來繼續下一步，處理或等待的這段時間也可以去做其他事，這樣會比較有效率。

---

### 範例

```javascript
var web = "http://this.is.the.web.you.want.to.connect"
var clientId = "accessCode"

// 基本方式
var xhr = new XMLHttpRequest();
xhr.open("GET", web, tru);
xhr.setRequestHeader('client-id',clientId)
xhr.send();

xhr.onreadystatechange = function(){
  if (this.readyState === 4 && this.status === 200){
    var data = JSON.parse(this.responseText);
    ......
  }
}
```
```javascript
//jQuery方式
function getData(cb){

  const web = "網址放這";
  const cliendId = "id碼";

  $.ajax({
    url: web,
    success: (response) => {
      cb(null, response); //回傳拿到的東西
    },
    error:(err) => {
      cb(err);    
    }   
  })
}

getData( (err,response) => {
  if (err) {
    console.log(err)
  } else {
    const streams = data.streams;
    const $row = $('.row');
    for (const stream of streams){
      $row.append(getColumn(stream));
    }
  }
})

function getColumn(data){
  return ...
}

```
