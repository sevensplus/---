## 物件導向(面向對向，Object Orientation，OOP)
- 放在物件裡面是 method，外面是function
- class：類別；object：物件
    - 類別是藍圖，沒有 instance；物件是實體
- 資料與行為在一起

```php
//這是設計圖
class Dog(){ 

    function __construct($name){ 
        // 建構子，初始化，控制預設放進來的參數設定
        // javascript 的預設函式名稱是 constructor
        $this->name = $name
    }

    function hello(){
        echo "I'm a dog";
    }

    // class 內的函式或變數可以設定為 private, public, protected
    // private 不能在函式外呼叫，又稱為封裝，Encapsulation
    // public 是預設值、可以在外面呼叫
    // protected 很像 private，但繼承的東西也可以用
    // static 靜態方法 v.s. method : static 不是屬於這個 instance，而是屬於 class 的。所以會用 Class__name::static__name 呼叫。會存在 class 裡面被共用，不會隨著增加 children 被複製很多份

    public function action()
        echo $this->hello(); // this：指現在運行的這個東西
    }
}

class Aniamal(){
    ...
}

class Dog extends Animal {
    // 繼承上面(Animal)的東西
    // 可以複寫掉繼承來的東西
    public function yoyo(){
        parent::parent__function__name(); // 呼叫 parent 裡面的函式
        // 在 js 裡面用 super.action 去改程式碼
    }
}

$dog = new Dog();  // 把設計圖做出東西來，叫做實體(Instance)
$dog -> hello();  // 呼叫方法

```

參考資料
- 《深入淺出物件導向分析與設計》
- 《物件導向基礎：何謂類別(Class)？何謂物件(Object)？》(https://blog.miniasp.com/post/2009/10/01/OOP-Basis-What-is-class-and-object-ANSWER)
