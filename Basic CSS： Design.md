### CSS背景
- 背景  
(1)可以放圖片或直接填色彩  
(2)調整背景圖片大小、對齊位置，第一個參數對上下，第二個對左右  
(3)調整背景放置大小
(4)到chrome的檢查 → style 可以看


``` CSS
#box1{

background:rgba(121,210,210,0.8) no-repeat center center ;
background:#79D2D2 top left;
background:url(./file.jpg) bottom right;

background-size:200px 100px　　// 這邊改背景圖片大小
background-size:50% 50%
background-size:contain　　// 讓圖片剛好貼合
background-size:cover　　// 圖片會隨著瀏覽器視窗縮放

height:500px　　// 這邊是背景圖要放多大，如果這邊大於背景圖設定大小就會有留白
width:200px
}
```


- 邊框
``` CSS
#box1{

background:#79D2D2;

border:10px solid #3FBF7F;　　// 邊框是背景圖向外延伸，會動到元素位置（border → 元素外面多了一圈，整個變大 → 邊框對齊原本元素位置 → 元素被擠到中心，往右下移動）。可以改邊框樣式，像dashed/dotted/solid
border-radius:5px　　// 邊框角的弧度，50%會變成圓形

border-top: 10px solid pink;　　// 四個邊的顏色可以分開設
border-bottom: 10px solid transparent;
border-bottom: 10px solid transparent;
border-bottom: 10px solid transparent;
// 把背景的 width 和 height 設 0，然後有三邊設透明，就可以畫三角形

outline:5px solid green　　// outline 也是往外長出去，在 border 外面，但不會動到元素位置

}
```


- 留白
``` CSS
#box1{
width:100px;
height:100px;

padding:30px;　　// 內部留白，設定距離邊框的大小。背景寬和高不變，但會往外延伸出30px，物件變成130*130，物件內容對齊(30,30)
padding:20px 10px;　　// 上下留白值-左右留白值

margin:30px　　// 外部留白，不影響物件內容。背景仍是100*100，但現在對齊到(30,30)

}
```


- 文字屬性
``` CSS
#box1{

color:orange;　　// 文字顏色
font-size:20px;　　// 文字大小
font-weight:normal;　　// 文字粗細，normal/bold粗體/或100~900之間
font-family:"正黑體";　　// 字體

letter-spacing:1px;　　// 字與字之間的距離
line-height:1.5em;　　// 行高

text-align:center;　　// 對齊哪裡，center/right...，但多行就沒辦法，可以用padding撐開

work-break:break-word;　　
// 斷行，break-all會直接切開，break-word會照著字切，不會把單字分成兩成

white-space:nowrap;　　
// 如何處理空白。nowrap 是不要分開，永遠是同一行；pre-line 是換行；pre 是保留 html 原來的樣子

overflow:hidden;　　// 文字超出背景時的處理方法。hidden會直接被截斷，scroll是文字會變成可以滾動的拉軸，auto也是滾動
text-overflow:ellipsis;　　// 超出時會變成...

}
```


- 動畫 
``` CSS
#box1{

background:white;
color:orange;
width:200px;
height:100px;

transition: all 3s ease-in;　　// 花多少時間轉場、動畫樣式。transition要加在原本的box底下，如果加在box.hover下面，移上去有動畫，移出來就沒有

}

#box1.hover{

background:orange;
color:white;

cursor:pointer;　　// 滑鼠移上去會變換圖示，換成可以點的手

transform:scale(2);　　// transition可能會動到其他物件，但transform不會，只會改變自己
transform:rotate(180deg);　　// 旋轉
transform:translateX(20px,-50px);　　// 移動位置

position:absolute;
top:50%;
left:50%;
transform:translateX(-50%,-50%);　　// 可以讓物件置中

}
```


- 切版
    - 將畫面分區，用不同 `div` 切出不同版面
```CSS
#box1{

display:flex;　　// 把底下的元素排成左右
align-items: center;　　// 讓底下的元素置中對齊
vertical-align:; 　　// inline 元素怎麼和其他東西並排

}
```