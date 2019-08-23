## CSS 預處理器(CSS Preprocessor)
- 主要有三種
    - Scss / Sass
    - Less
    - Stylus
- 功用：可以讓使用者用更簡化、更直觀的方式寫 CSS，然後丟進預處理器，預處理器會將程式碼轉換成原生 CSS
- 用寫程式的方式寫 CSS
    
```cmd
npm install -g sass
```

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
.box3{
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
    -webkit-border-radius:$radius*2;  // 可以做運作
            border-radius:$radius;
}

.card{
    @include border-radius(10px);
}

// 也可以用import
```

## Post CSS
- 轉成 CSS 之後幫你加上東西，像有些東西瀏覽器不支援，利用這個就可以自動加上需要的東西
- Autoprefixer
- cssnext
