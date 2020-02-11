### Event loop
- 程序 process：有點像程式，例如瀏覽器每個分頁都是一個程序，可以開工作管理員看
- thread：執行緒，process 下會有很多 thread(★重要★)，執行動作的單位
- 瀏覽器跑 javascript 的時候是 single thread，一次做一件事，要有東西來跑非同步的東西，這個機制的一個元素叫Event loop
    - Call stack, Callback Queue
- [event loop by Philip roberts](https://vimeo.com/96425312)
- 當 api 被觸發、callback queue 裡面有東西，event loop 會先執行完 call stack(目前已經堆積的東西)，再把 callback queue(新的工作)放進 call stack 裡面，然後一直循環檢查，call stack 永遠會優先於 callback queue

---

### Javascript 執行：先編譯，後執行
### 執行環境 EC (Execution Context)
- 三元素：VO(Variable Object)，scopeChain，this

- EC（Execution Context）裡面，一般變數放 VO（Variable Object），函式的變數放 AO（Activation Object），AO 裡面有 argument。

```javascript
// 範例
var v1 = 10
function test() {
  var vTest = 20
  function inner() {
    console.log(v1, vTest) //10 20
  }
  return inner
}
var inner = test()
inner()
```
1. 進入 global EC
```javascript
globalEC = {
  VO: {
   v1: undefined,
   inner: undefined,
   test: function 
  },
  scopeChain: globalEC.VO
}
```
2. 執行程式碼，進入 test EC
```javascript
testEC = {
  AO: {
    arguments,
    vTest: undefined,
    inner: function
  },
  scopeChain: 
  	[testEC.AO, test.[[Scope]]]
  = [testEC.AO, globalEC.scopeChain]
  = [testEC.AO, globalEC.VO]
}
```
3. 執行 test 程式碼，進入 inner EC
```javascript
innerEC = {
  AO: {
    arguments
  },
  scopeChain:
  [innerEC.AO, inner.[[Scope]]]
= [innerEC.AO, testEC.scopeChain]
= [innerEC.AO, testEC.AO, globalEC.VO]
}
```
4. 執行 inner
```javascript
```

