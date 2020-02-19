## React
### React 是什麼
- 官網：Javascript library for building user interfaces（是 UI library 不是框架，但搭其他東西，就算是框架了）
- FB 研發出來的東西。FB 規模大、UI 複雜，所以發展出這個東西去管理；但如果我們的產品沒那麼大，就不一定能體會到 React 的好處

### 為什麼要用 React
React 有點像是 jQery，兩個都是讓寫程式更方便的 library，不過著重的層面不太一樣。React 提供了一套解決方法，讓我們在處理某些情況時比較快速，若不用也沒問題，只是可能要花比較多心力。另外，React 是 facebook 開發拿來處理渲染問題的，但和 facebook 相比，我們處理的專案規模可能沒那麼大，未必能迅速地體會到 React 的方便之處

React 關注的問題是：資料改變和頁面渲染如何維持同步。我之前用過兩種方法，第一種方法是：將資料儲存起來，只要資料有任何變動，就將頁面全部重新渲染，但在資料量很大時，這作法會有效能上的疑慮。另一種方法是，不儲存資料，直接在頁面上進行改動。React 像是這兩種方法的折衷，React 會將資料儲存在 state 中，但在偵測到資料變更時，會先判定是哪一部份，然後進行部分的重新渲染

### 學習前的預備知識
- Webpack（前端的模組化）：用這個來打包，寫前端時才能用 node.js 裡面的 require、import 等（後端）功能。react 裡面有一個類似 webpack server 的東西，一存檔就會偵測到然後進行更新
- Class（物件導向）
- Component（組件化）：把每個東西切作成不同的 component，有點像是 html 裡面的切版。
- JSX（JS 跟 HTML 混著寫，用 babel 轉換）
- State（狀態與 UI 的對應）

---

### 快速搭建 react 環境
``` javascript
npx create-react my-app-name // 用 command line 下載環境封包
cd my-app-name 
npm install

// 方法一
npm start // 開始運行 react 環境。報錯的話跟著步驟走，這次遇到的情況是 eslint 衝除，先刪除 node_modules, package-lock.json, 然後用 npm install/ yarn。弄好後會自動開啟 localhost:3000，就可以用了

// 方法二
npm run build // 這個指令則是把東西打包好，但是會用絕對路徑去改寫裡面的東西（原本就是預設要放在 server 跑），所以還是會出現空白
python -m SimpleHTTPServer 8111 // 簡單蓋一個 server 起來，就可以存取到 index.html 裡面的東西了，或者手動把 / 改成相對路徑 ./
```
---

### 基礎觀念
### Virtual DOM
React 裡面，有 Real DOM tree 和 Virtual Dom tree(虛擬 DOM tree)，當有東西改變時，會用 key 去比較 Virtual DOM tree before/after，然後再到真正的 DOM tree 上面進行修改。因此，React 只會處理有變動的地方，不會一直 re-render，就沒有效能問題

### State v.s. Props
- state：component 內部的狀態，自己原生的資料
- props：從 parent 那邊得到的特性，有父子、parent/child 的概念。
- 以 component 的角度來看，state 是自己從零到有建造出來的，可以隨意改動；props 則是從別人那邊接收過來的，已經被固定好、無法改變。另外，child 沒有辦法直接改變 parent 的 state，而要 call parent 裡面的 function 去進行改動

### render
- Client side render：在瀏覽器上自己產生的，檢視原始碼時可能會看不到東西，因為是 js 後來才又加上去的。React 就是這種
- Server side render：像是 php echo 出來的東西，會從 server 那邊拿到一整套資料，response 裡面本來就有內容

### functional component
- 用 function 寫 component
- 如果要寫只有 render 的 component，可以用 `function component_name(props) { return (...) }` 來寫
- 可以再更簡化成 `const component_name = () => (......)`

### shouldComponentUpdate(nextProps, nextState)
- 決定 state 改變後要不要 call render function
- shallow compare（比記憶體位置） v.s. deep compare（慢慢比內容，耗時）

### Immutable Data
state 不能直接修改，只能清空重新指定，是為了拿來做比對，才能知道哪邊改變、需要重新渲染

---

### React 的生命週期
- Mounting
    - React 小書翻成掛載，是物件從零到有的產生過程，包含組件渲染、構造 DOM 元素、將元素塞入頁面
    - 就是經過 constructor，第一次 render、把東西放到 DOM 上面
    - 整體的執行流程
        - constructor()：初始化工作
        - componentWillMount()
        - render()
        - `componentDidMount()`
- Updating
    - 更新物件內容
    - shouldComponentUpdate(object nextProps, object nextState)：控制物件是否重新渲染
    - `componentDidUpdate(object prevProps, object prevState)`：重新渲染並把更新變更到 DOM 之後使用
- Unmounting
    - 將物件清除，刪除前會使用 `componentWillUnmount()`
---

## 範例
### 快速搭建一個 component
```javascript
// 原本 jQuery 會這樣寫
document.querySelector('#root').innerHTML = 
` <div>
    hi everyone
  </div> `

// React 版本這樣寫
import React, {Component} from React
class bio-asp extends Component {
  constructor() {
    super()  // 初始化程式碼
    this.state = {
      lab: 301
    }
  }

  render() {
    return (
      <div> hi everyone </div>
    )
  }
}
ReactDOM.render(
  <bio-asp />,  // 記得用 / 關起來
  document.querySelector('#root')
)
```
### 在 React 裡面使用 function
```javascript
class bio-asp extends Component {
  constructor() {
    super()
    this.state = {
      list = [1,2,3]
      num: 12,
      judge:true
    }
    this.click = this.click.bind(this)  // 沒用箭頭函式的話，要特別進行綁定動作
  }
  
  click(){
    this.setState({
      num: this.state.num + 1,
      newlist = [...this.state.list,Math.random()],
      judge = !this.state.judge
    })
  }
  auto_bind_function = () => { ... }  // 用 array function 寫就不用特別 bind 綁定

  render() {
    return (
      <div>
        {this.state.list}
      </div>
  }
}
```
### JSX 與 其他細節
```javascript
class bio-asp extends Component {
  constructor() {
    super()
    this.state = {
      judge:true
    }
  }
  
  render() {
    return ( 
      // 記得寫成 className 避免和 class ... extends Component 搞混，要用駝峰式命名
      // 用 { } 寫 JSX
      <div className={this.state.num}></div>

      // 用 state 裡面 true/false 的值做判斷，true 才會顯示
      { judge && <elements title={this.state.something}/> }  
      
      <ul>
        { this.state.list.map( 
          (item,index) => (<Item key={item}  index={index}> item </li>)
        )}

        { this.state.list.map( (item,index) =>
          React.createElement( Item, {
            ket:item,
            index,
            label:this.label
          }, null)  // 不同寫法但和上面效果一樣
          )
        }
      </ul>
    )
  }
}
```
### Parent and Child
```javascript
class bio-asp extends Component {
  constructor() {
    super()
    this.state = {
      num: 12
    }
    this.click = this.click.bind(this)
  }  
  click(){
    this.setState({
      num: this.state.num + 1,
    })
  }
  onDelete() = () => { ... }
  render() {
    return (
      <Item onclick={this.onDelete} index={this.state.num}/>
    )
  }
}
class Item extends Component {
  clickAgain = () => {
    const {onDelete,index} = this.props
    onDelete(index)
  }
  render() {
    const {index,label} = this.props  
    return (
      <li onClick={this.clickAgain}> index </li>
    )
    return this.props.judge ? <h1></h1> : null
  }
}

```

### life cycle 相關的內建函式
```javascript
class lifetime_example extends Component {
  constructor(){
    super()
    this.state = {
      num:0
    }
  }
  render(){
    return( <div> {this.state.num} </div> )
  }

  componentDidMount() {  // 設定自動變化，每隔一秒改一次
    const num = Math.random()
    this.timer = setInterval( () => {
      this.setState({
        title:num
      })
    }, 1000)
  }
  componentWillUnmount() {  // 把東西拿掉時清除乾淨，否則會報錯
    clearInterval(this.timer)
  }
  componentDidUpdate(prevProps, prevState) {  // 監控 state 變化，進行相對應的動作
    if (this.state.something >= 2 || this.state.something <5>){
      ......
    }
  }

}

```
-----
### React 使用注意
  - 一定要回傳一個元素。不能回傳兩個元素，一定要把元素包成一個，不想多寫一層的話，可以用空物件 <> </> 包起來
  - 也可以回傳 array
  - 和 Component 類似的東西：Fragment
  - React 創造出的 spa 頁面要怎麼分享給別人：在網址加上 hashtag（#hashtag）。用 addEventListener 監聽 hashchange，然後加上動作

```javascript
class test extends Component {
    render() {
        const {tab} = this.state
        return(
            <> 
            {a ? <div></div> : <span></span> } // 正確寫法
            {a ? <div> : <span> } // 不能這樣寫，因為要轉成 React.createElement，這樣寫會造成程式錯誤
            <a href={'#' + name}/> // 控制頁面間的跳轉
            {tab === 'condition1' && <Component1/>} // 符合條件就 render、輸出這個東西
            {tab === 'condition2' && <Component2/>}
            </>
        )
    }
}
```
-----
### React Router
- 一個 library，根據路徑去 render 不同的 component
- HashRouter v.s. BrowserRouter
```javascript
import {BrowserRouter as Router, Route, Link} from "react-router-dom"  
function example() {
  return (
    <Router>
      <Route exact path='condition1' component={test1}/>  了
      <Route exact path='condition2' component={test2}/>
      <Route exact path='condition3' component={test3}/>
    </Router>
  )
  // path 沒有寫成 exact path 的話，部分符合就算符合
}
```

- 參考資料：《程式導師實驗計畫》直播