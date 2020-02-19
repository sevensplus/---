## Javascript 常用指令

###  Array Method

|指令      |用法                                          |說明                                                              |
|---------|----------------------------------------------|------------------------------------------------------------------|
|concat   |`var arr3 = arr1.concat(arr2)`                |合併兩個 array                                                     |
|filter   |`var result = arr1.filter(a => a > 3)`        |篩選符合條件的元素。會輸出陣列                                       |
|find     |`var ans = arr.find(a => a > 1)`              |找符合條件的第一個元素，輸出值                                       |
|flat     |`arr1.flat()`                                 |將多層如 `[1, [2,3]]` 拉平                                           |
|includes |`var ans = arr.includes('something')`         |找有沒有，輸出 `true/false`                                         |
|indexOf  |`var ans = arr.indexOf('word',3)`             |找符合項目的位置，第二個參數填數字，像要找第三個符合的位置              |
|join     |`var str = arr.join( '---' )`                 |把 array 拼接成字串，預設用 `,` 拼，可以設定空白、其他符號等等           |
|push     |`arr.push(element)`                           |在陣列最後佳東西，就算是 `var arr2 = arr1.push`，也會改到原本的 arr1  |
|slice    |`var arr2 = arr1.slice(2,3)`                  |切分陣列，不會改到原本的。從第一個參數開始，第二個參數本身不算          |
|splice   |`arr.splice(1,0,element)`                     |插入或取代元素，第一個代表位置，第二個代表取代與否，取代 1，不取代 0    |
|reduce   |`var sum = arr.reduce( (arr, cur) => arr + cur )`|arr 表示過去結果，cur 表示現在的 element                          |

-----

### String Method

|指令     |用法                                           |說明                                                        |
|---------|----------------------------------------------|------------------------------------------------------------------|
|concat   |`var str1.concat('',str2)`                    |拼接兩個字串，第一個參數放連接的東西，像空格、逗點等等                 |
|include  |`let result = sentence.includes(str)`         |確認字串中是否包含另一個字串，輸出 `true/false`                      |
|indexOf  |`var result = sentence.indexOf(str)`          |同上，字串中是否包含某字母、某字串，是的話輸出位置，沒有輸出 -1        |
|match    |`var result = paragraph.match(/[A-Z]/g)`      |搜尋匹配的部分                                                     |
|slice    |`let str2 = str1.slice(1,2)`              |切割字串，第一個參數是開始處，包含在切割的內容內，第二個是結束，不包含在內，可以填負數，不改變原本字串 |
|split    |`let arr = str.split(',')`                    |將字串切割成 array                                                    |
|substring|`let str2 = str1.substring(1,2)`              |和 slice 類似                                                        |
|toLowerCase|`let str2 = str1.toLowerCase()`             |轉成小寫，轉大寫是 `toUpperCase`                                      |
|toString |`let str = item.toString()`                   |轉成字串                                                             |
|trim     |`let str_clean = str.trim()`                  |去掉前後空白                                                         |

-----

### 其他指令
|指令     |用法                                           |說明                                                              |
|---------|----------------------------------------------|------------------------------------------------------------------|
|parseInt |`let num = str.parseInt()`                    |轉成數字                                                           |
|getMonth |`let mon = new Date(12,30,2020).getMonth()`   |取得月份，轉換時月份會 -1。還有 `getDate, getYear, getMinutes, getHours`|
|setDate  |`date.setDate(31)`                            |設定時間                                                           |
|Date.now |`let start = Date.now()`                      |取得現在時間                                                       |
