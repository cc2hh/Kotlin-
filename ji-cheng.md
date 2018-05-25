* ### 继承

kotlin中所有类都有一个基类**Any**，一个类只能继承一个基类

```
Any并不是java中的Object，只有equals()、hashCode()和toString()函数
```

用冒号“**:”**声明继承，所有类都默认是final的，若要成为基类，需用**open**修饰。

* 子类有主构，则继承时必须实现基类构造函数，子类的次构遵循类规则必须实现子类主构

* 子类没有主构，则子类的次构必须用**super**直接实现基类构造函数或用**this**间接实现另一次构（已实现基类构造函数）

* 子类可实现任意基类构造函数

```
/* 有主构子类 */


// 带空参主构基类
open class Animal(){

    constructor(age:Int):this()
}

// 实现主构子类
class Dog(): Animal() {

    constructor(age:Int):this()
}

// 实现次构子类
class Dog(): Animal(1) {

    constructor(age:Int):this()
}
```

```
/* 无主构子类 */

// 基类
open class Animal{

constructor(age:Int)
}

// 子类
class Dog: Animal {

// super直接实现
constructor(age:Int):super()
// this间接实现
constructor(name:String):this(1)
}
```

* ### 抽象类

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



