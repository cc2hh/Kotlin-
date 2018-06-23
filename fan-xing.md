与**java**类似，可有类型参数，但**java**中的泛型是不型变的

```
// 类型参数T，名称随意取
class A<T>(t: T) {
    var v = t
}

class A1 : B<Int> {
    override fun getT(): Int {
        return 1
    }
}
```

## 型变

* 声明处型变
* 类型投影

只能读取的对象为生产者，只能写入的对象为消费者

> 生产者并不是不可变的，不能写入还有删除等操作。只读、只写是为了保证类型安全

#### 声明处型变

型变注解，并在类型参数声明处使用

* **out**，表示该对象只能读取，是生产者。例：Collection&lt;out E&gt;
* **in**，表示该对象只能写入，是消费者。例：Comparable&lt;in T&gt;

```
//声明处型变，生产者
interface B<out T> {
    fun getT(): T
    // 报错，不能写入T类型对象
    fun setT(t:T)
}

interface B1<Q> {
    fun getQ(): Q
}

//声明处型变，消费者
interface C<in P> {
    fun setP(p: P)
    // 报错，不能读取P类型对象
    fun getP(): P
}


    @Test
    fun testD623() {

        testFX(com.example.kotlin.d623.A1())
    }

    fun testFX(b: com.example.kotlin.d623.B<Int>) {
        var vb: com.example.kotlin.d623.B<Number> = b

        println("b---${b.getT()}============vb----${vb.getT()}")
    }

    fun testFX(b: com.example.kotlin.d623.B1<Int>) {
        // 报错，required：B1<Number>，founed：B1<Int>
        var vb: com.example.kotlin.d623.B1<Number> = b  
    }
    
//输出
b---1============vb----1
```

> T是一个协变的类型参数



