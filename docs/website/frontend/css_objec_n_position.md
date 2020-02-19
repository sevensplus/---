## CSS Object & Position
### Display（物件形式）
- 不同物件有預設形式，可以用 `display:inline` 強制更改
1. block
    - 例子： `div、h1、p`
    - 調什麼都可以，每個元素自己佔一行
2. inline
    - 例子：`span、a`
    - 大家常常會說調背景高度(`height`)、上下邊距(`margin`)、 `padding` 沒用，不影響 `content`（元素本身）的位置。因為這些形式本來是預設在行內做效果，不會動到不同行之間，因此 `content` 不變。但調 `padding` 時背景會被撐開變大， `border` 位置也會改變
3. inline-block
    - 例子：`buttom、input、select`
    - 對內像 inline 可並排，對外像 block 可調寬高
    - `margin` 設成0，但是 inline-block 之間還是有空格？
        - `</div><div>` 之間不要換行
        - 在空行間下註解 `<!-- --!>`

-----

### Box model
- Box 組成： `content、padding、border、margin`
- 由於 Box 由好幾個東西組成，如果今天想指定物件的寬，就要計算` total width - padding - border `，相當不方便。因此，可以設定 `box-sizing` 進行自動修正
    - 預設值 `content-box`：這四個部分分開計算。指定 `width、height` 只會改變 `content` 部分的長寬。
    - 調成 `border-box`：會把 `border、padding` 包含在寬度裡面，`content` 的長寬就會等於 `width - 2 * (padding + border)`

-----

### 物件定位

- `static`：預設值，什麼事都不會改變。這時候 `top、right、bottom、left、z-index` 指令無效
- `relative`：相對定位，根據原本應該出現的位子去做改變。
    - 舉例來說，若 a 原本被安排到 (10,10)，當 `position:relative`，這時候 (10,10) 就會變成新的原點，後續調整會依照新的原點去做改變。
    - 元素的改變不會影響到其他元素

``` CSS
.box:nth-child(3){

position:relative;
top:-30px;
left:50px;
}
```

- `absolute`：雖然直接翻譯是絕對定位，但我覺得比較像相對定位，相對於（參考點）定位。如果往上找有發現不是 `static` 的元素，就會根據那個元素定位；沒有的話，就會相對於 `body` 定位
    - 要相對於某元素定位時，通常會將那個元素設定成 `position:relative`
    - 當元素被設定成 `absolute` 時，就會被抽離出原本的排序方式，自成另一套體系
- `fixed`： viewport 絕對定位（瀏覽器定位）。物件會被固定在瀏覽器（viewport）的某個位子，不管頁面上下捲動都不會改變。
- `z-index`：調整圖層位置，數字越大代表越前面
- `sticky（position:sticky）`：滾動時，如果到達（瀏覽器）某個位置，就會被黏住無法動彈。到達前是 `static`，到達後是`fixed`
- 小結：`static` 是不能改變的預設值，`fixed` 是絕對定位，會被釘在瀏覽器某個地方。`relative` 是相對於原本的預設位置去改變，`absolute` 是相對於某個錨點改變（`body` 或 上層非預設值的元素）。
