#### 委托模式

有两个对象处理同一个请求，接受请求的对象将请求委托给另一个对象来处理。可不继承类而扩展功能（聚合）

```
interface I704 {
    fun getQ(): Int
}

-----------处理请求对象----------------

class A704 : I704 {
    override fun getQ(): Int {
        return 2
    }

}

------------接受请求对象----------------

class C704 {

    var a704 = A704()

    // 委托实现
    fun getQ(): Int {
        return a704.getQ()
    }
}

------------测试------------------

    fun testD704() {
       println("--testD704------${ C704().getQ()}")
    }

// 输出
--testD704------2
```

#### 委托属性

语法：**var**/**val**  属性名 **:** 类型 **by** 表达式

by 后面的表达式即为委托，属性若是**val**修饰，表达式则必须实现getValue\(\)，**var**修饰则还必须实现setValue\(\)，因为属性的get\(\)和set\(\)会被委托给上面两个方法。

getValue\(\)方法有两个参数：

* thisRef，被委托类，是自身类型或其超类
* property，属性名，是类型KProperty&lt;\*&gt;或其超类型

返回类型是属性类型或其子类型

setValue\(\)方法比getValue\(\)还额外多一个参数：

* value，赋与的值，是属性的类型或其超类

当实现两个方法时都需要**operator**修饰

---

适用于以下情况（不限于）：

* lazy（延迟属性），只在首次访问时初始化值
* observable（观察者属性），监听者能收到该属性的变更通知
* map（映射），多个属性存放在一个map中

```
var q703: String by B703()

----------委托类--------------------

class B703 {

    var _v: String? = null

    operator fun setValue(a703: A703, property: KProperty<*>, s: String) {
        println("设值")
        println("setValue 值：$s ，被委托类：$a703 ，属性名：$property")
        _v = s
    }

    operator fun getValue(a703: A703, property: KProperty<*>): String {
        println("获值")
        return "getValue  值：$_v ，被委托类：$a703 ，属性名：$property"
    }
}

-----------测试------------------------

        var a703 = A703()

        println(a703.q703)
        a703.q703 = "CC"
        println(a703.q703)

// 输出
获值
getValue  值：null ，被委托类：com.example.kotlin.d703.A703@14899482 ，属性名：property q703 (Kotlin reflection is not available)
设值
setValue 值：CC ，被委托类：com.example.kotlin.d703.A703@14899482 ，属性名：property q703 (Kotlin reflection is not available)
获值
getValue  值：CC ，被委托类：com.example.kotlin.d703.A703@14899482 ，属性名：property q703 (Kotlin reflection is not available)
```

> 委托可以不用具体类

```
var qq703: String by {

    }

------------------需实现扩展方法-------------------------------

 operator fun <R> Function<R>.setValue(a703: A703, property: KProperty<*>, s: String) {
    println("qq703")
}

 operator fun <R> Function<R>.getValue(a703: A703, property: KProperty<*>): String {
    return "123456"
}

-------------------测试------------------

        a703.qq703="789"
        println(a703.qq703)
// 输出
qq703
123456
```

##### lazy，延迟属性

只会在第一次调用get\(\)时计算并记录结果，以后调用时直接返回结果

```
    var w703: Int by lazy {
        var v = 2 + 2
        println("lazy" + v)
        v
    }

 -----------测试---------------

        println("-第一次-${a703.w703}")
        a703.w703 = 1
        println("-第二次-${a703.w703}")
// 输出
lazy4
-第一次-4
-第二次-4
```

> 默认情况lazy是同步锁的，一个线程计算，所有线程用一个值。也可以更改模式
>
> ```
> @kotlin.jvm.JvmVersion
> public fun <T> lazy(mode: LazyThreadSafetyMode, initializer: () -> T): Lazy<T> =
>         when (mode) {
>             LazyThreadSafetyMode.SYNCHRONIZED -> SynchronizedLazyImpl(initializer)
>             LazyThreadSafetyMode.PUBLICATION -> SafePublicationLazyImpl(initializer)
>             LazyThreadSafetyMode.NONE -> UnsafeLazyImpl(initializer)
>         }
> ```
>
> lazy表达式即为getValue\(\)方法，set方法无效，就算扩展了也不能更改其值。lazy&lt;out T&gt;只读的
>
>     operator fun <T> Lazy<T>.setValue(a703: A703, property: KProperty<*>, s: T) {
>     // 报错
>     //    value=s
>     }
>
>     public interface Lazy<out T> {
>         /**
>          * Gets the lazily initialized value of the current Lazy instance.
>          * Once the value was initialized it must not change during the rest of lifetime of this Lazy instance.
>          */
>         public val value: T
>         /**
>          * Returns `true` if a value for this Lazy instance has been already initialized, and `false` otherwise.
>          * Once this function has returned `true` it stays `true` for the rest of lifetime of this Lazy instance.
>          */
>         public fun isInitialized(): Boolean
>     }

##### observable，观察者属性

在对象类Delegates里

当给属性赋值时调用（赋值后执行），有三个参数：被赋值的**属性**，旧值，新值

```
    var e703: Boolean by Delegates.observable(true) { property, oldValue, newValue ->
        println("observable-----$property(oldValue,newValue)=($oldValue,$newValue)")
    }

 ---------------测试------------------

 a703.e703 = false
 println("a703.e703=${a703.e703}")

 // 输出
 observable-----property e703 (Kotlin reflection is not available)(oldValue,newValue)=(true,false)      
 a703.e703=false
```

表达式内固定返回 return@observable  即新值

> 当想拦截一个值并去除掉是可用 vetoable（赋值前执行）
>
> ```
>     var r703: Int by Delegates.vetoable(0) { property, oldValue, newValue ->
>         println("vetoable-------$property(oldValue,newValue)=($oldValue,$newValue)")
>         oldValue > newValue
>     }
>     
>  ---------测试-----------------
>  
>   a703.r703 = 1 
>   println("a703.r703=${a703.r703}")
>   
>   //输出
>   vetoable-------property r703 (Kotlin reflection is not available)(oldValue,newValue)=(0,1)
>   a703.r703=0
> ```

##### map，映射属性

常用与json解析或动态情况

```
class B705(map: Map<String, Any?>) {
    val name :String by map
    val old : Int by map
}

------------测试-----------------

        val b705 = B705(mapOf("name" to "CC", "old" to 18))
        println("b705.name=${b705.name}-------b705.old=${b705.old}")

// 输出
b705.name=CC-------b705.old=18
```

> Map是只读，所以委托属性只能是val，若要用var，需用MutableMap

局部变量也能声明委托

#### 翻译规则

委托实现的实现都生成辅助属性并委托给它

```
class C {
    var prop: Type by MyDelegate()
}

// 这段是由编译器生成的相应代码：
class C {
    private val prop$delegate = MyDelegate()
    var prop: Type
        get() = prop$delegate.getValue(this, this::prop)
        set(value: Type) = prop$delegate.setValue(this, this::prop, value)
}
```

> `this`引用到外部类`C`的实例而`this::prop`是`KProperty`类型的反射对象，该对象描述`prop`自身

#### 提供委托



