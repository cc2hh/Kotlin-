用关键字**enum**声明，主要用于类型安全枚举，枚举常量是枚举类一个对象（实例），每个常量之间用逗号分隔

> 枚举常量和普通类成员应用分号分隔，常量必须放在普通成员之前

* 匿名类
* 实现接口

#### 匿名类

**枚举常量**能声明自己的匿名类，并实现或覆盖枚举类的方法。

```
enum class Color(c: Int) {

    Red(1) {
        override fun testB(): String {
            return "----testB--Red---"
        }

        override fun testV(): String {
            return "----testV--Red---"
        }
    },

    Black(2) {
        override fun testB(): String {
            return "----testB--Black---"
        }
    },

    White(3) {
        override fun testB(): String {
            return "----testB--White---"
        }
    };

    open fun testV(): String {
        return "----testV--Color---"
    }

    abstract fun testB(): String

}

----------测试--------------------------------------------------------

 Color.values().forEach { println("-----${it.testB()}----${it.testV()}") }
 
// 输出
---------testB--Red-----------testV--Red---
---------testB--Black-----------testV--Color---
---------testB--White-----------testV--Color---
```

#### 实现接口

枚举类可以实现接口，但不能继承类

```
enum class Math : Opear {

    Add {
        override fun getResult(a: Int, b: Int): Int {
            return a + b
        }
    },
    Multiply {
        override fun getResult(a: Int, b: Int): Int {
            return a * b
        }
    },
    Division {
        override fun getResult(a: Int, b: Int): Int {
            return a / b
        }
    }
}

----------测试--------------------------------------------------------

 val a = 6
 val b = 3
 Math.values().forEach { println("----$it($a,$b)==${it.getResult(a, b)}-----") }
 
 // 输出
 ----Add(6,3)==9-----
----Multiply(6,3)==18-----
----Division(6,3)==2-----
 
```

#### 

> 每个枚举常量都有名字（name）和位置（ordinal）属性

```
enum class Shape {

    Circle,Square,Triangle;

    val v:String="qwe"

}

---------测试-----------------------------------------------------

testShaper(Shape.Circle)

// 输出
----testD702---Square----false---ordinal==1--name==Square--

```



