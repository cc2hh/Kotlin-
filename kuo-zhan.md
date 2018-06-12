扩展可实现无需继承即可为类扩展新功能或者像装饰者模式效果

* 扩展是静态解析的，并没有真正改变这个类。意味着扩展函数调用时是由调用者类型决定而不是运行时计算的结果
* 当扩展函数有同样成员函数时，会调用成员函数
* 支持扩展属性，但不能有初始化器
* 支持伴生对象扩展

```
package com.example.kotlin

import com.example.kotlin.pojo.BlackDog
import com.example.kotlin.pojo.Dog

/**
 * Created by cc on 2017/12/29.
 *
 * function :
 */

val testA = "123"

fun BlackDog.jump() {
    println("BlackDog扩展$testA")
}

fun Dog.jump() {
    println("Dog扩展$testA")
}


--------------------------------------------


    var blackDog = BlackDog()
    testEx(blackDog)

    fun testEx(dog:Dog){
        dog.jump()
    }

---------------------------------------------

// 输出
Dog扩展123

-------------------------------------------

open class Dog : Animal, Work {

   ...

    fun jump() {
        println("Dog成员函数$testA")
    }

    ...
}



// 输出
Dog成员函数123
```

### 扩展声明为成员

在一个类（如：A）内部声明另一个类（如：B）的扩展，其中A称为分发接受者，B称为扩展接受者

* 在扩展成员中可直接访问B中成员
* A和B中有相同成员时，优先调用B的成员，若要调用A的成员，使用限定的**this**语句
* 函数的分发对于A是虚拟的，对B是静态的
* **扩展函数内的函数是虚拟调用**

```
open class A {
    fun eat() {
        println("A.eat")
    }

    open fun run() {
        println("A.run")
    }
}

--------------------------------------------

open class A1 : A() {

    override fun run() {
        println("A1.run")
    }
}

----------------------------------------------

open class B {
    fun eat() {
        println("B.eat")
    }

    open fun A.write() {
        println("A.write")
        run()
        eat()
    }

    open fun A1.write() {
        println("A1.write")
        run()
        this@B.eat()
    }

    fun callPrint(a: A) {
        a.write()
    }

}

-----------------------------------------------

open class B1 : B() {

    override fun A.write() {
        println("B1==========A.write")
    }

    override fun A1.write() {
        println("B1==========A1.write")
    }
}

------------------------------------------------


    @Test
    fun testD612() {
        println("---------B().callPrint(A())---------")
        B().callPrint(A())
        println("---------B().callPrint(A1())---------")
        B().callPrint(A1())
        println("---------B1().callPrint(A())---------")
        B1().callPrint(A())
        println("---------B1().callPrint(A1())---------")
        B1().callPrint(A1())
    }


   // 输出
---------B().callPrint(A())---------
A.write
A.run
A.eat
---------B().callPrint(A1())---------
A.write
A1.run   // 扩展函数内的函数是虚拟调用
A.eat
---------B1().callPrint(A())---------
B1========A.write
---------B1().callPrint(A1())---------
B1========A.write
```



