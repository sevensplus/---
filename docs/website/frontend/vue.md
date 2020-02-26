# Vue basix
## template syntax 模板語法
### 賦值與屬性
- 雙括號 `{{ }}` 在 html 裡面插值
    - 可以放入 javascript 變數或程式碼
    - 不能放 `if`，要判定用三元運算子； `var a = ...` 這種也不行
    - 屬性中加入 v-once 為一次性賦值，後續改動不會造成頁面更新
- 用 `v-bind` 指定 attribute
    - 會強制把 attribute 名轉成小寫
    - 如果選項是 `null、undefined、false`，不會被渲染出來，所以想指定 `true` 時才會使用
    - 可以設定將變數指派 true/false，依據變數決定是否顯示 class，像是 `{ active : isActive}`；或指派到 data 中的 obj，obj 有多項，就會依據該項的 true/false 決定是否渲染項目，或是渲染指定的值；也可以指派到 computed 的 function

```html
<!-- 插值 -->
<span >{{ number + 1 }}</span> 
<span>{{ ok ? 'YES' : 'NO' }}</span> 
<span v-once>{{ message.split('').reverse().join('') }}</span> 

<!-- 設定 attribute -->
<div v-bind:id="dynamicId"></div>
<button v-bind:disabled="isButtonDisabled">Button</button>
<div v-bind:id="'list-' + id"></div>
<div v-bind:class="{ active: isActive }"></div>
<div v-bind:class="classObject"></div>
<!-- errorClass 永遠都會被渲染，activeClass 不一定，要看判定值表現 -->
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
<!-- 指定多項 css 項目，第二種寫法比較清楚 -->
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
<div v-bind:style="styleObject"></div>

<!-- 將連結與 url 值綁定 -->
<a v-bind:href="url">...</a>
```

### 指令
- 帶有 `v-` 的 attribute。當表達式的值改變，連帶產生影響（像用 `true/false` 開關控制元素的消失或出現）

```html
<!-- 判斷 -->
<p v-if="seen">现在你看到我了</p>

<!-- 監聽 -->
<a v-on:click="doSomething">...</a>

<!-- 縮寫：下面兩種相等 -->
<a v-bind:href="url">...</a>
<a :href="url">...</a>
<a :[key]="url"> ... </a>

<!-- 縮寫 again -->
<a v-on:click="doSomething">...</a>
<a @click="doSomething">...</a>
<a @[event]="doSomething"> ... </a>
```
-----

## Computed , Method, Watchers
### computed & method
- 如果頁面值要和 vue data 的值綁定，但無法直接呈現、必須經過計算的話，就採用這個方法，當 data 值變動，也會牽扯到 computed 和 method 的值，兩種方式就結果上來講非常類似
- 差別：__computed properties are cached based on their reactive dependencies__。再次請求時，如果 data 沒有改變，computed 會直接給上次結果，不會重複工作。但 method 每次會重新進行運算。

```html
<div id="example">
  <p>complicated and bad writing way: {{ message.split('').reverse().join('') }}</p>
  <p>better method: {{ reversedMessage }}</p>
</div>
```
```javascript
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    reversedMessage: function () { // this 指向 vm
      return this.message.split('').reverse().join('')
    }
  },
  methods: {
    reversedMessage: function () {
        return this.message.split('').reverse().join('')
    }
  }
})
```

### setter
- 個人理解：`getter` 是一般情況下自動生成 data，`setter` 是 data 特別指派時才會工作

```javascript
var vm = new Vue({ ...
  computed: {
    fullName: {
        get: function () { //getter
           return this.firstName + ' ' + this.lastName
        },
        // setter
        set: function (newValue) {
            var names = newValue.split(' ')
            this.firstName = names[0]
            this.lastName = names[names.length - 1]
        }
    }
  }
}

vm.fullName = 'John Doe' // setter 出來工作
```

### watched
- 用 watch 來監控 data 變化，並做出動作

```html
<div id="watch-example">
  <p>Ask a yes/no question:<input v-model="question"></p>
  <p>{{ ans }}</p>
</div>
```
```javascript
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    ans: 'I cannot give you an answer until you ask a question!'
  },
  watch: {
    question: function (newQuestion, oldQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      this.debouncedGetAnswer()
    }
  },
  created: function () {
    this.debouncedGetAnswer = _.debounce(this.getAnswer, 500)
  },
  methods: {
    getAnswer: function () {
      if (this.question.indexOf('?') === -1) {
        this.answer = 'Questions usually contain a question mark. ;'
        return
      }
      this.answer = 'Thinking...'
      var vm = this
      axios.get('https://yesno.wtf/api')
        .then(function (response) {
          vm.answer = _.capitalize(response.data.answer)
        })
        .catch(function (error) {
          vm.answer = 'Error! Could not reach the API. ' + error
        })
    }
  }
})
```

-----
## Component 組件
- `Vue.component` 的 data 必須是函數，不然資料之間不會獨立，會被串在一起

### 基礎範例

```html
<div id="components-demo">
  <button-counter name="counter1"></button-counter>
  <button-counter name="counter2"></button-counter>
  <button-counter name="counter3"></button-counter>
</div>
```
```javascript
Vue.component('button-counter', {
  props: ['name'],
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```

### Props
```html
<div id='blog-post-demo'>
  <blog-post
    v-for="post in posts"
    v-bind:key="post.id"
    v-bind:post="post"
  ></blog-post>
</div>
```
```javascript
new Vue({ // 母元素，傳遞 data 到 props
  el: '#blog-post-demo',
  data: {
    posts: [
      { id: 1, title: 'My journey with Vue', content:'...'},
      { id: 2, title: 'Blogging with Vue' , content:'---'},
      { id: 3, title: 'Why Vue is so fun',content:'~~~'}
    ]
  }
})

Vue.component('blog-post', { // 子元素
  props: ['post'],
  template: 
  `<div class="blog-post">
      <h3>{{ post.title }}</h3>
      <div v-html="post.content"></div>
    </div> `
})
```

### 監聽子元素
- 監聽 child 並改動 parent 的狀態，利用 `$emit(func_name,param)` 的方式將參數傳遞回上層

```html
<div id="blog-posts-events-demo">
  <div :style="{ fontSize: postFontSize + 'em' }">
    <blog-post
      v-for="post in posts"
      v-bind:key="post.id"
      v-bind:post="post"
      v-on:enlarge-text="postFontSize += $event"
      v-on:enlarge-text="onEnlargeText"
    ></blog-post>
  </div>
</div>
```
```javascript
new Vue({ // 父元素
  el: '#blog-posts-events-demo',
  data: {
    posts: [],
    postFontSize: 1
  },
  methods: { 
    onEnlargeText: function (enlargeAmount) { // 也可以用方法來處理 parent & child 的互動
      this.postFontSize += enlargeAmount
    }
  }
})

Vue.component('blog-post', { // 子元素，button 中傳入 $ emit 事件方法偵測觸發
  props: ['post'],
  template: `
    <div class="blog-post">
      <h3>{{ post.title }}</h3>
      <button v-on:click="$emit('enlarge-text', 0.1)"> 
        Enlarge text
      </button>
      <div v-html="post.content"></div>
    </div>
  `
})
```

------

## 條件渲染 v-if
- true 時渲染某組件，可以用 `if, else, else if`
- `v-if` 和 `v-show` 用法類似，前者會進行創建和銷毀，後者始終被放在 DOM 上，只是切換 `display` 狀態。所以，如果使用頻繁用 `v-show`，不頻繁用 `v-if`
- `v-for` 優先級高於 `v-if`，所以放在同一個物件上的話，每圈都會跑（執行所有 list），先跑完 `v-for` 再執行 `v-if` 判定。如果要先判定的話，把 `v-if` 放在 `v-for` 外圈
```html
<div v-if="Math.random() > 0.5"> Now you see me </div>
<div v-else>  Now you don't </div>
```

```
<div v-if="type === 'A'"> A </div>
<div v-else-if="type === 'B'"> B </div>
<div v-else> Not A/B </div>
```

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```

-----

## 列表渲染 v-for
- 渲染列表

```html
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} : {{ index }} : {{ item.message }}
  </li>
</ul>
```
```javascript
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

- 渲染單個物件的所有內容

```html
<div id="v-for-object" class="demo">
  <div v-for="(value, name, index) in object">
    {{ index }}. {{ name }}: {{ value }}
  </div>
</div>
```
```javascript
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
})
```
- 其他範例

```html
<li v-for="n in even(numbers)">{{ n }}</li>
```
```javascript
new Vue{
  data: {
  numbers: [ 1, 2, 3, 4, 5 ]
  },
  methods: {
    even: function (numbers) {
      return numbers.filter(function (number) {
        return number % 2 === 0
      })
    }
  }
}
```

### 事件偵測
- 變異方法 mutation method
  - `push()、pop()、shift()、unshift()、splice()、sort()、reverse()`
- 替換方法 replacing array
  - `filter()、concat()、slice()`
- 無法偵測直接指派的狀態，跟 React 不能直接指定 state 類似
  - `vm.items[indexOfItem] = newValue, vm.items.length = newLength`
  - 解決方法：`Vue.set(vm.items, indexOfItem, newValue), vm.items.splice(indexOfItem, 1, newValue)`

-----

## 事件處理 v-on
```html
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
```
```javascript
var example3 = new Vue({
  el: '#example-3',
  methods: {
    say: function (message) {
      alert(message)
    }
  }
})
example3.say('something') // 也可以直接在 js 中呼叫函式
```

### event modifier & key modifier
- event modifiet：處理 `event.preventDefault()` 之類的要求，可用方法有 `.stop, .prevent, .capture, .self, .once, .passive`
- key modifier：檢查按鍵詳情，可用的有 `.enter, .tab, .delete, .esc, .space, .up, .down, .left, .right`

```html
<input v-on:keyup.enter="submit">
<input v-on:keyup.page-down="onPageDown">
```

參考資源
- 程式碼摘錄自 [Vue 官方文檔](https://cn.vuejs.org/)
