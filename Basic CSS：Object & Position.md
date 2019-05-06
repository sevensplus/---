## CSS Object & Position
### Box model
- Box 組成： `content、padding、border、margin`
- Box-sizing
    - 預設：`content-box` 
    - 調成`border-box`：會把 border、padding 包含在寬度裡面，不用自己另外算


### Display（物件形式）
- 不同物件有預設形式，但可以用 `display:inline` 強制更改
1. block
    - 例子： `div、h1、p`
    - 調什麼都可以，每個元素自己佔一行  
2. inline
    - 例子：`span、a`
    - 大家常常會說調寬高、上下邊距、 `padding` 沒用，不影響 `content`（元素本身）的位置。因為這些形式本來是預設在行內做效果，不會動到不同行之間，因此 `content` 不變。但背景會被撐開變大， `border` 位置也會改變

3. inline-block
    -  例子：`buttom、input、select`
    - 對內像 inline 可並排，對外像 block 可調寬高
    - `margin` 設成0，但是 inline-block 之間還是有空格？
        - `</div><div>` 之間不要換行
        - 在空行間下註解 `<!-- --!>`


### 物件定位
- Static & Relative  
1. 預設值是static  
2. 可以用`nth-child(n)`選定元素，將 `position:relative` ，就會相對於預定位置進行偏離
``` CSS
.box:nth-child(3){

position:relative;
top:-30px;
left:50px;

}
```
- Absolute & fixed：相對於瀏覽器做定位  
1. fixed：固定在瀏覽器、viewpoint的某個點，就算網頁上下滑動，該物件也不會移動  
2. Absolute

- z-index：調整圖層位置，數字越大代表越前面  

- sticky（`position:sticky`）：滾動時，如果到達某個位置，就會被黏住無法動彈  


### 其他指令

- 不是第幾個就隱藏起來

```CSS
.box:not(:fitst-child){
    display:none;
}


