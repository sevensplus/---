## React
### webpack 與 babel 前置作業
- 因為要用到 import, export，因此需要用 webpack 進行 js 檔案的處理，用瀏覽器開啟時才能執行。另外，有些瀏覽器不支援 ES6，因此要用 babel 轉成 ES5
- 安裝：`yarn add react react-dom @babel/preset-react`
- 其他前置作業：

```javascript
// webpack.config.js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.export = {
    entry:'./src/index.js',
    output: {
        path: path.join(__dirname,'/dist'),
        filename: 'bundle.[hash].js'  // 會自動產生 hash，變成檔案的一部份。只要檔案有變，hash 碼就會不同
    },
    module: {
      rules: [
        {
          test: /\.js$/,  // 把 .js 都進行 babel-loader 處理
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader'
          }
        }, {
          test: /\.css$/,
          loader: ['style-loader','css-loader']  // 順序很重要
        }
      ]
    },
    plugins: [
      new HtmlWebpackPlugin({
        template: './index.html'    // 處理匯入 js 檔案，檔名中有 hash 的問題
      })
    ]
}


// package.json
{
  ...
  "script": {
      "start":"webpack-dev-server --mode webpack --open --hot",   // 要記得先裝 webpack-dev-server, webpack, webpack-cli
      // 有 webpack-dev-server 之後，只要 js 檔案一更正，就會自動更新
      "build":"webpack --mode production"
  }
  ...
}


// .babelrc
{
  "presents": ["@babel/present-env","@babel/present-react"]
}
```

- 另一個建置環境的做法：`npx create-react-app dir_name`，會自動幫你蓋環境，然後 `npm run start`，server 就會自己跑起來

-----
### React 基礎操作
> React 是什麼：要改變畫面時，不直接改變畫面，而是改變物件的 state，state 一改變，畫面會自己 re-render，渲染出新的 UI 介面

```javascript
//  component & render function
import React, {Component} from 'react'
import ReactDOM from 'react-dom'

class title extends Component {
  render(){
    return (
      <h1> title </h1>
    )
  } 
}

class App extends Component {
  render(){
    return ( 
      <h1> something </h1>
      <title/> // 上面 title 的東西會被加進來 
    )
  }
} 
export default App


// JSX
class piece extends Component {
  render(){
    const name = 'yoyoyo'
    return (
      <h1 className="title"> something </h1>  // 加 class 要用 className
      <a href="www.goo.com"></a>

      <div className={name + '!!!'}></div>  // 用 { } 來表示 js 變數
      <div style={{ color:'red', fontSize:'20px'}}></div>  // font-size 會寫成 fontSize，也可以先定義 css = {size:'10px'}，再套進 stype = {css}
      <div onClick={ () => {
        alert('hello~')
      }}>click me</div> // 加 eventListener 的方法，form 是用 onsubmit
    )
  }
}


// add state
class content extends Component {
  constructor() {
    super()  // 初始化的動作
    this.state = {
      counter: 1
    }

    this.handleClick = this.handleClick.bind(this) // 要 bind 起來不然會報錯
    // this 的時候是呼叫時決定的，不是建立時決定的
  }

  handleClick(){
        this.setState({  // 改變 state 必須 call 這個
          counter: this.state.counter + 1
  }

  render(){
    return ( 
      <span onClick={this.handleClick}> button </span>
      <span>{this.state.counter}</span>

      <div onClinck={ () => {  // 箭頭函式可以用，但 function(){} 不行。箭頭函式的 this 會變成 function 定義時的 this 值，其他種在被呼叫時才會決定 this 值
        this.setState({
          counter: this.state.counter + 1
        }}>
      </div>

    )
  }
} 


// props
// 第一種寫法
class deliver extends Component{
  handleClick () {
    this.setState({
      counter: this.counter + 1
    })
  }

  render(){
    return (
      <div>
        <h1 onClick={this.handleClick}></h1>
        <receiver number={this.state.counter}/>
      </div>
    )
  }  
}


class receiver extends Component {
  render(){
    return (
      <h1>{this.props.number}</h1> 
    )
  } 
}

// 第二種寫法
class deliver extends Component{
  render(){
    return (
        <receiver>
          {this.state.counter}
        </receiver>
    )
  }  
}

class receiver extends Component {
  render(){
    return (
      <h1>{this.props.children}</h1>  // children 可以傳任意元素，可以是 component，或 Html 的元素等等都可以
    )
  } 
}

// 第三種寫法：functional component
function counter(props) {
  return (
    <div>{props.number}</div>
  )
}

function counter({ number }) {
  return (
    <div>{number}</div>
  )
}

const counter = ({ number }) => {
  return (
    <div>{number}</div>
  )
}


// Component 之間的溝通
// 不能直接改變 props，必須使用 parent 傳遞給你的 function
const title = (props) => {
  render (
    <h1 onClick={props.handleClick_deliver}>{props.text}</h1>  // 提取 handleClick，用 props.function_name 去呼叫 parent 中的 function
  )
}

class contents extends Component {
  constructor() {
    super()
    this.state = {
      counter:1    
    }
    this.handleClick = this.handleClick.bind(this)
  }

  handleClick(){
    this.setstate({
      counter: this.state.counter + 1
    })
  }

  render() {
    return(
      <title handleClick_deliver={this.handleClick} text={this.state.counter} />  // 把 handleClick 屬性賦值
    )
  }
}


// 寫 CSS
import styled from 'styled-components'
const header = styled.h1`
  color:red;
`


// 插入元素
import React, {Component} from 'react'
import ReactDOM from 'react-dom'
ReactDOM.render(<app/>, document.getElementById('root'))
ReactDOM.render(<app/>, document.querySelector('#root'))  // 用 render 去產出東西
document.querySelector('#root').innerHTML=` <app 裡面的內容> `  // 和上面相等

```
-----
### React 生命週期
```javascript
// 控制 component 出現與隱藏
// 第一種方法
class app extends Component {
  constructor() {
    super()
    this.state = {
      isShow:true    
    }
  }

  render() {
    const {isShow} = this.state
    return(
      {isShow && </title>}  // 當 isShow 為 true，才 render <title/>，類似 if 的語法
      <button onClick={ () => {
        this.setState({
          isShow: !this.state.isShow
        })
      }}>click me</button>
    )
  }
}

// 第二種方法
class title extends Component {
  constructor(props)) {
    super(props)  // 做好初始化，不做事可以不寫，但要用就都寫上去
  }
  render () {
    const {isShow} = this.props
    return (
      <h1 style={{
        display: isShow ? 'block' : 'none'
      }}> title </h1>
    )
  }
}


// shouldComponentUpdate
// 更改 state 後，會 call 這個 function，預設是 true
shouldComponentUpdate(nextProps, nextState){
  if (nextState.number == 3) return true;
  return false  // state 會改變，但不會 re-render，畫面不會動
}

class contexts extends Component {
  shouldComponentUpdate(nextProps, nextState){
    if (nextProps.num !== this.props.num) return true;
    return false
  }
}


// componentDidMount：state 初始化後的動作
// componentWillUnmount：清除沒用到的東西
class pieces extends Component {
  conponentDidMount() {  // 東西初始化後才會做事
    this.timer = setTimeOut( () => {
      this.setState({
        title: 'ya'
      })
    }, 2000)  // 過一下子後更改 state
  }

  componenetWillUnmount() {
    clearTimeout(this.timer)  // 如果 component 已經不在畫面上，就會把東西清掉
  }
}


//  componentDidUpdate：state 變更時呼叫
//  可以限定只有在某些 state 變動時動作
componentDidUpdate(prevProps,prevState) {
  if(prevState.num !== this.state.num) doSomeThing();
}
```

- 參考資料：[【Lidemy鋰學院-FE301】](https://www.lidemy.com/p/fe301-react) 課程