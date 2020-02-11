## jQuery
- 一套 javascript 的 library
- 優點：做好不同瀏覽器的支援
```javascript
// jQuery 語法
    require('https://code.jquery.com/jquery-1.12.4.min.js');
    $(document).ready(function(){   // $()就是選東西
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
-[You might not need jQuery](http://youmightnotneedjquery.com/)
-[webfont](https://www.justfont.com/)
