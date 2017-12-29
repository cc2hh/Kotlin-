使用关键字**package**表示，通常位于源文件顶部

```
package com.example.kotlin

...

class MainActivity : AppCompatActivity() {

...

override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        ...
}

...

}
```

### 导入

有些包会默认导入到源文件中，根据平台不同还会导入额外的包

* jvm

```
import java.lang.*
import kotlin.jvm.*
```

* js

```
import kotlin.js.*
```

可以导入具体文件的全包名，也可导入文件作用域，如果文件名冲突，可以使用关键字**as**为文件在本地重命名

```
import android.support.v7.app.AppCompatActivity  // 全包名
import java.lang.*  // 作用域

// 重命名
import com.example.kotlin.pojo.Person
import com.example.kotlin.bean.Person as PersonB

    fun testPackage(){
        val personP= Person()
        val personB= PersonB()
    }

// 不重命名
import com.example.kotlin.pojo.Person

    fun testPackage(){
        val personP= Person()
        val personB= com.example.kotlin.bean.Person()
    }
```

除类文件外还可导入：

* 顶层函数和属性
* 对象声明中的函数和属性
* 枚举常量



文件TestFun.kt

```
package com.example.kotlin

/**
 * Created by cc on 2017/12/29.
 *
 * function :
 */

val testA = "123"
```

对象声明TestObj

```
package com.example.kotlin

/**
 * Created by cc on 2017/12/29.
 *
 * function :
 */
object TestObj {
    fun test(){
    }
}
```

枚举常量

```
package com.example.kotlin

/**
 * Created by cc on 2017/12/29.
 *
 * function :
 */
enum class TestEnum {
    N , S , W , E
}
```

类Person

```
package com.example.kotlin.bean
// 对应导入
import com.example.kotlin.TestEnum
import com.example.kotlin.TestObj
import com.example.kotlin.testA

/**
 * Created by cc on 2017/12/20.
 */
class Person {

    fun testPackage(){
        // 顶层函数和属性
        testA
        // 对象声明中的函数和属性
        TestObj.test()
        // 枚举常量
        TestEnum.E
    }

}
```



> 没有import static，所有导入都用import



