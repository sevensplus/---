## jQuery
### jQuery 是什麼
jQuery 是建立在 vanilla JS 底下的函式，目的也是相同的(都是要進行特定操作)，只是達成目的的手段不同(寫法不一樣)。vanilla JS 寫起來可能要一長串，但 jQuery 做了對照表，將一長串內容轉成比較簡短的敘述，因此我們就能用這種簡潔的方式來寫 js。
簡單講，jQuery 就是用另一套寫法來寫 javascript 而已，兩者間可以互換，有點像是文言文和白話文的差別，但 jQuery 寫出來的程式碼比較好懂，而且開發出來的時間在 vanilla JS 後面。

### 範例
```javascript
// jQuery 語法
    require('https://code.jquery.com/jquery-1.12.4.min.js');
    $(document).ready(function(){   // $() 是選取物件
        $('.class_name').append("<button class='hi'>hi<div/>");
        $('.class_name').click(function(){
            alert('yo');
        })
    })

    $(document).ready(function(){
        $('.class1').click(function(){
            $('.class2').fadeOut();  //動畫、漸層淡出，fadeIn 是出現;
            $('.class3').css('background','lightyellow');
            $('.a').attr('href','./path.php');
        })
    })

// vanilla JS 語法
document.addEventListener('DOMContentLoaded',function(){
    document.querySelector('.class__name').addEventListener('click',function(){
        alert('yo');
    })
})

```

其他資源
- [You might not need jQuery](http://youmightnotneedjquery.com/)
- [webfont](https://www.justfont.com/)
