扩展可实现无需继承即可为类扩展新功能或者像装饰者模式效果

扩展是静态解析的，并没有真正改变这个类。意味着扩展函数调用时是由调用者类型决定而不是运行时计算的结果

```
package com.example.kotlin

import com.example.kotlin.pojo.BlackDog

/**
 * Created by cc on 2017/12/29.
 *
 * function :
 */

val testA = "123"

fun BlackDog.jump() {
    println("扩展$testA")
}

 var blackDog = BlackDog()
 blackDog.jump()

// 输出
扩展123
```



