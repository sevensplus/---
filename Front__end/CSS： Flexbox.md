## [Flexbox Froggy](http://flexboxfroggy.com/)
### 物件對齊
#### 橫向對齊
-  **`justify-content:flex-start`**：橫向對齊（單排）
    - `flex-start`：對齊前面
    - `flex-end`：對齊底部
    - `center`：置中
    - `space-between`：水平均分，兩側置底。物件--空白--物件--空白
    - `space-around`：水平均分，兩側留白。空白--物件--空白--物件--空白


#### 垂直對齊
- **`align-items:center`**：垂直對齊（單排）
    - `flex-start`：對齊上方
    - `flex-end`：置底
    - `center`：垂直置中
    - `baseline`： Items display at the baseline of the container
    - `stretch`：Items are stretched to fit the container


- 單個物件改變
    - `.className { `**`align-self:flex-start`** `}`
    - 選項和 `align-item` 一樣，`align-item` 是改變所有物件，`align-self` 只改變單個


- **`align-content:flex-start`**：垂直對齊（多排），決定行間的排列方式
    - `align-content` 決定 **行間** 的排列，`align-item` 是決定 **物件** 間（items as a whole）的排序。如果只有一行，`align-content` 會沒有用
    - `flex-start`：向上排列
    - `flex-end`：向下排列
    - `center`：置中
    - `space-between`：垂直均分，兩側無空白
    - `space-around`：垂直均分，兩側留白
    - `stretch`：Lines are stretched to fit the container.


---


### 物件排序
- **`flex-direction:row`**：改變整排狀態，正排、倒著排、橫排、直排
    - `row`： 物件水平排列，1--2--3--空白--
    - `row-reverse`：物件從底部反過來排，--空白--3--2--1
    - `column`：物件垂直排列
    - `column-reverse`：從下往上排
    - 範例：要排出3--2--1--空白--
```CSS
pond {
    flex-direction:row-reverse;  // 位置反過來
    justify-content:flex-end;  // 開頭變結尾
}
```


- **`order`**：直接指定某物件的順序，所有物件預設都是0，指定 >0 會到最右， <0 會到最左
    - `.yello { order:2 }`


---


### 其他
- **`flex-wrap:nowrap`**：換行
    - `nowrap`：放在在同一行
    - `wrap`：超過的放到下一行
    - `wrap-reverse`：Items wrap around to additional lines in reverse.

- **`flex-flow:row wrap`**：結合 `flex-direction` 和 `flex-wrap`的指令，將兩個動作合而為一


