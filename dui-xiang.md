对类做某些改动，不用继承

* 对象表达式
* 对象声明
* 伴生对象

#### 对象表达式

用一个**object**表达式来代表对象，适用于匿名类对象

```
open class A702(var aa: Int) {
    open fun eat() {
        println("---A702--eat----$aa--")
    }
}

--------------接口--------------------------

interface B702 {
}

-------------测试---------------------------

        val a702 = object : A702(20), B702 {
            override fun eat() {
                println("--testD702----eat--$aa--")
            }
        }

        a702.eat()

// 输出
--testD702----eat--20--
```

> 匿名对象可用于本地和私有作用域声明的类型；若用于公有则匿名对象的类型为其超类（**Any**是默认超类），添加的成员无法被匿名对象访问

```
    fun run() = object {
        var age = 1
    }

    // 私有
    private fun speak() = object {
        var age = 2
    }

    fun read() {
        // 本地
        val v = object {
            var a=1
        }

        // 正确
        v.a
        // 正确
        speak().age
        // 报错
        run().age
    }
```

#### 对象声明

跟类声明类似，用关键字**object**声明，不是一个表达式，不能用于赋值。使用时直接用名称

```
object Obe {
    object A {

    }

    fun getO(): String {
        return "POP"
    }
}

--------内部类------------

    inner class QQ {
    // 报错
        object PP{}
    }

--------函数--------------

    fun write(){
    // 报错
        object TT{}
    }        

--------测试--------------------

println("--Obe.getO==${Obe.getO()}----")    

// 输出
--Obe.getO==POP----
```

> 对象声明不能在函数和内部类中

#### 伴生对象

在类内部用关键字**companion**标记对象声明，名称可省略（使用时用**Companion**代表），伴生对象的成员可通过类名直接使用。如：单例模式

```
class C702 private constructor() {

    companion object {

        fun single(): C702 {
            return C702()
        }

        var age = 10

        fun setA(a: Int) {
            age = a
        }
    }

    val yoy = 1

}

 ---------测试--------------------------   

 val x = C702.Companion
 x.age

 println("--${C702.age}--${C702.single().yoy}--")
 
 // 输出
 --10--1--
```

> 一个类只能有一个伴生对象



### 差异





