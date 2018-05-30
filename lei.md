## 类

以关键字**class**声明，可有一个主构造函数和多个次构造函数，构造函数由**constructor**声明。主构函数前若没有可见修饰符和注解则可省略，且主构函数没有函数体，初始化由**init**代码块实现。

> 类中代码执行顺序：主构 -&gt; 类中属性初始化和init代码块（两者按类中顺序执行） -&gt; 次构

```
// constructor可省略
class One constructor(name: String) {

    // 次构造函数，需实现主构函数
    constructor(age: Int) : this("cc") {
        this.age = age
        println("次构 constructor age=$age")
    }

    constructor(name: String, age: Int) : this(name) {
        this.age = age
        println("次构 constructor name=$name age=$age")
    }

    val address ="first 属性 name=$name address=本地".also(::println)

    init {
//        Variable 'age' must be initialized
//        println("first init name=$name age=$age")
        println("first init name=$name")

    }

    var age = 1

    var sex: String = "second 属性 name=$name sex=男".also(::println)

    init {
        println("second init name=$name age=$age")
    }
}
```

输出

```
----------------------init name--------------------------------
first 属性 name=hh address=本地
first init name=hh
second 属性 name=hh sex=男
second init name=hh age=1
----------------------init age-------------------------------
first 属性 name=cc address=本地
first init name=cc
second 属性 name=cc sex=男
second init name=cc age=1
次构 constructor age=15
----------------------init name age--------------------------------
first 属性 name=kk address=本地
first init name=kk
second 属性 name=kk sex=男
second init name=kk age=1
次构 constructor name=kk age=30
```



### 抽象类

类和成员都可以声明为抽象的，用关键字**abstract**声明，抽象成员不能实现

可以用抽象成员覆盖一个非抽象开放成员

```
open class Animal() {

    open val color: Int = 0

    constructor(age: Int) : this()

    open fun eat() {
        println("Animal---------eat")
    }

    open fun speak() {
        println("Animal--------speak")
    }
}


abstract class Cat : Animal() {

    override fun speak() {
    }

    fun run() {}

    abstract override fun eat()
}
```



