## CSS Preprocessor
### CSS 預處理器是什麼
CSS 預處理器可想像成轉譯的機器，我們用一般寫程式的規則（if, for, var）寫 CSS，寫完後丟進去，預處理器就會把內容轉成原生 CSS。
不用預處理器絕對沒問題，只是預處理器的好處是：可以用比較方便、直觀的方式寫 CSS。如果要寫重複性很高的 CSS，用預處理器會比較方便，修改時也比較容易。   CSS 預處理器主要有以下三種
- Scss / Sass
- Less
- Stylus

---
### 使用方式
```cmd
npm install -g sass
```

### 範例
```Scss
// Scss範例
// 設定通用變數
$color = blue; // 宣告共同的變數
.box{
    background: $color; // 套進去
}
.box2{
    background: $color;
}

// Nesting 巢狀
// 可以有階層的直接寫下去
.box{
    background:yellow;
    .item{
        background:red;
        .object{
            background:green;
        }
    }
}

// parent
// 簡化寫 box__title，box__content 的程序
.box{
    &__title{     // & 對應到的是 .
        width:100px;
    }
    &__content{
        font-size:16px;
        &--disable{     // 這邊 & 對應到的是上一層，會變成 .box__content--disable{}
            display:none;
        }
    }
}

// Mixin (function)
@mixin border-radius($radius){
    -webkit-border-radius:$radius*2;  // 可以進行變數運作
            border-radius:$radius;
}

.card{
    @include border-radius(10px);
}

// 也可以用import
```

---

### Post CSS
- 轉成 CSS 之後幫你加上東西，像有些東西瀏覽器不支援，利用這個就可以自動加上需要的東西
- Autoprefixer
- cssnext
