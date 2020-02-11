## API 與 Ajax 串接

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
  return `
    放 Html 和 js 混合檔 
  `
}

```
