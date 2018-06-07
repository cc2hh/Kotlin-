扩展可实现无需继承即可为类扩展新功能或者像装饰者模式效果

* 扩展是静态解析的，并没有真正改变这个类。意味着扩展函数调用时是由调用者类型决定而不是运行时计算的结果
* 当扩展函数有同样成员函数时，会调用成员函数

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



