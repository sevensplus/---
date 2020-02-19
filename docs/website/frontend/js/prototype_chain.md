## 原型鏈 prototype

>#### [Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)

> new 出來的新物件中，有個別性質、也有共同性質（prototype），共同性質修改時，所創造之物件的性質都會變動
```javascript
function Dogs(name){
    this.name = name;  // 個別性質
}
Dogs.prototype = {species:"犬科"}  // 共同性質

let dogA = new Dogs('天天');
let dogB = new Dogs('樂樂');
console.log(dogA.name);  // 天天
console.log(dogA.species == dogB.species);  // true，都是犬科，而且有〈相同的記憶體位置〉
Dogs.prototype.species = "狗";  // dogA、dogB 兩個的性質都會被改到

```

-----

#### [从设计初衷解释 JavaScript 原型链](https://www.jianshu.com/p/a97863b59ef7)
```javascript
// 呈上
dogA.__proto__ == Dogs.prototype;  // true
dogA.__proto__.__proto__ = Dogs.prototype.__proto__ == Object.prototype;  // true
dogA.hasOwnProperty('species');  // false
dogA.__proto__.hasOwnProperty('species');  // true
Dogs.prototype.hasOwnProperty('species');  // true
dogA instanceof Dogs;  // true
dogA instanceof Object;  // true

dogA.__proto__ = Object.prototype;
dogA instanceof Dogs;  // false
```

-----

#### [該來理解 JavaScript 的原型鍊了](https://blog.techbridge.cc/2017/04/22/javascript-prototype/)

> 你有一個叫做 `Person` 的函數，就可以把 `Person` 當作 `constructor`，利用 `var obj = new Person()` 來 `new` 出一個 `Person` 的 `instance`，並且可以在 `Person.prototype` 上面加上你想讓所有 `instance` 共享的屬性或是方法
```javascript
// 方法一：把函式放在單獨的 function 中
function person(name){
    this.name = name;
    this.getName = function(){
        return this.name
    }
}
var nick = new person('nick');
var peter = new person('peter');
console.log( nick.getName === peter.getName ); // false，記憶體不同

//  方法二：把函式放在 prototype 中
function person(name){
    this.name = name;
}
person.prototype.getName = function(){
    return this.name;
}
var nick = new person('nick');
var peter = new person('peter');
console.log( nick.getName === peter.getName ); // true，記憶體不同

nick.getName === person.prototype.getName; // true
nick.getName === peter.getName; // true
nick.__proto__ === person.prototype; // true，會加上這個屬性

person.prototype.constructor === person; //true
nick.constructor === person; //true
nick.hasOwnProperty('constructor'); // false
nick.__proto__.hasOwnProperty('constructor'); // true
person.prototype.hasOwnProperty('constructor'); // true

//  其他
person.__proto__ === Function.prototype; // true
person.__proto__.__proto__ === Function.prototype.__proto__ === Object.prototype; // true
Function.prototype.__proto__.__proto__ === Object.prototype.__proto__; //null
Function.__proto__.__proto__ === Object.prototype; //true


Function.prototype === Function.__proto__; //true
Function.__proto__ === Object.__proto__; // true，是 ƒ () { [native code] }
Function.prototype === Object.__proto__; // true
Function.__proto__ === Object.prototype; // false
Object.prototype === Object.__proto__; //false
Object.__proto__ === Function.prototype; //true
Object.prototype; 
// 內容為 {constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}

console.log( nick.getName === person.prototype.getName ) // true
console.log( nick.getName === peter.getName ) // true
console.log( nick.__proto__ === person.prototype ) // true，會加上這個屬性
```

- new 的實際運作：`var nick = new person('nick')` 在幹嘛
    1. 創造出一個新的 obj，`var o = { ... }`
    2. 把 `o` 的 `__proto__` 指向 `person` 的 `prototype`，`obj.__proto__ = person.prototype`，繼承原型鍊
    3. 拿 `o` 當成 context，呼叫 person，最後回傳

- 原型鍊：當呼叫 `nick.getName` 的時候，會依照這個順序去找
    1. `nick` 的屬性裡面，就是 `nick.getName`
    2. 沒有的話，進入 `nick.__proto__ ( == person.prototype )`
    3. `nick.__proto__.__proto__ ( == person.prototype.__proto__ == Object.prototype )`
    4. `Object.prototype.__proto__ ( == null )`，原型鍊頂端

-----

參考資料
- [Javascripter 必須知道的繼承 ...](https://medium.com/@peterchang_82818/javascripter-%E5%BF%85%E9%A0%88%E7%9F%A5%E9%81%93%E7%9A%84%E7%B9%BC%E6%89%BF%E5%9B%A0%E5%AD%90-prototype-prototype-proto-object-class-inheritace-nodejs-%E7%89%A9%E4%BB%B6-%E7%B9%BC%E6%89%BF-54102240a8b4)
- [JavaScript. The Core.](http://dmitrysoshnikov.com/ecmascript/javascript-the-core/?source=post_page---------------------------)  
- [JavaScript's Pseudo Classical Inheritance diagram](https://kenneth-kin-lum.blogspot.com/2012/10/javascripts-pseudo-classical.html?showComment=1484288337339&source=post_page---------------------------#c1393503225616140233)
- [你懂 JavaScript 嗎？#19 原型（Prototype）](https://ithelp.ithome.com.tw/articles/10205313)
- [Object.prototype.__proto _ _](http://dmitrysoshnikov.com/wp-content/uploads/constructor-proto-chain.png)
- [理解 JavaScript 的原型链和继承 Table of Contents instanceof 引发的问题](https://blog.oyanglul.us/javascript/understand-prototype.html)
- [从proto和prototype来深入理解JS对象和原型链](https://github.com/creeperyang/blog/issues/9)
- [彻底理解JavaScript原型](http://www.imooc.com/article/2088)
- [JS 对象机制深剖——new 运算符](https://www.cnblogs.com/aaronjs/archive/2012/07/04/2575570.html)
- [理解JavaScript的原型链和继承](https://blog.oyanglul.us/javascript/understand-prototype.html)
- [Javascript 面向对象编程（一）：封装](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)
- [Javascript面向对象编程（二）：构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)
- [Javascript面向对象编程（三）：非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)
