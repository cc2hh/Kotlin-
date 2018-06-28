声明属性用**var**表示可变；用**val**表示只读。

> 只读不允许自设setter访问器

用法类似**java**，对象名.属性

```
fun test(){
    var dog=Dog(1)
    val name=dog.name
    }
```

可自定义访问器，改变其可见性、注解和实现等，但getter访问器可见性不能改成**private**

### 幕后字段

不能直接声明字段，自动提供的幕后字段可用**field**标识符在访问器中引用，且只能在属性的访问器中使用**field**标识符

```
    var name: String = "dog123"
        set(value) {
            if (value == "") field = "cc"
        }
```

### 幕后属性

类似**java**中的封装思想，防止某些属性直接被外部使用，只为外部提供该属性的使用方法，当然也可提供get，set方法实现同样效果

```
class BlackDog() : Dog(1) {

    var address: String
        get() = this.address
        set(value) {}

    override fun eat() {
    }

    private var _sex: Int? = null

    var sex: Int=0
        get() {
            if (_sex == null) {
                _sex = 0
            }
            return _sex ?: throw AssertionError("aa")
        }
//        set(value) {
//            if (value >= 0) _sex = value
//        }

    fun getSex(): Int? {
        return _sex
    }
}


// 测试
    @Test
    fun testUse() {
        var dog = Dog(1)
        val name = dog.name
        println("-----name------$name")

        var blackDog = BlackDog()
        blackDog.sex = 2
        println("------sex------${blackDog.getSex()}")
        println("------sex------${blackDog.sex}")
    }

// 输出
-----name------dog123
------sex------null
------sex------0
```

### 编译器常量

使用**const**标记为常量

* 必须在顶层或在Object中
* 不能有自定义的getter
* 用String或原生类型初始化

```
// 顶层
package com.example.kotlin.pojo

/**
 * Created by cc on 2018/5/24.
 *
 * function :
 */

const val PI:Int=1123

abstract class Cat : Animal() {

    override fun speak() {
    }

    fun run() {}

    abstract override fun eat()
}

// Object
package com.example.kotlin.pojo

/**
 * Created by cc on 2018/5/29.
 *
 * function :
 */
object Obj {
    const val PI:Int=1123
}
```

### 延迟初始化

用**lateinit**标记延迟，非空属性不再必须在构造函数中初始化了

* 只用于非空属性
* 非原生类型（String可以）

> 如果在没有初始化时使用一个延迟属性，会报一个特定异常UninitializedPropertyAccessException

可通过在延迟属性的引用上使用**.isInitialized**方法检测该属性是否已初始化了

```
    lateinit var today: String

    @Test
    fun testLateInit() {
        today = "cc"
        println("------lateinit------${this::today.isInitialized}")
    }

// 输出
------lateinit------true
```



