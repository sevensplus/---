### Display（物件形式）  
(1) block。像是 `div、h1、p...` 調什麼都可以，通常會自己佔一行  
(2) inline。像是 `span、a` 調寬高沒用，調上下邊距沒用，因為這些本來是預設在行內做效果，不會動到不同行之間。特別注意的是 `padding`，調上下間距時元素位置不變，但背景會被撐開變大   
(3) inline-block。像是 `buttom、input、select`，對內像inline可並排，對外像block可調寬高


### 物件定位
- Static & Relative  
(1) 預設值是static  
(2) 可以用`nth-child(n)`選定元素，將 `position:relative` ，就會相對於預定位置進行偏離
``` CSS
.box:nth-child(3){

position:relative;
top:-30px;
left:50px;

}
```
- Absolute & fixed：相對於瀏覽器做定位  
(1) fixed：固定在瀏覽器、viewpoint的某個點，就算網頁上下滑動，該物件也不會移動  
(2) Absolute

- z-index：調整圖層位置，數字越大代表越前面  

- sticky（`position:sticky`）：滾動時，如果到達某個位置，就會被黏住無法動彈  
`
