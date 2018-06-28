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

    // B<Int>赋值给B<Number>
    fun testFX(b: com.example.kotlin.d623.B<Int>) {
        var vb: com.example.kotlin.d623.B<Number> = b

        println("b---${b.getT()}============vb----${vb.getT()}")
    }

    // C<Number>赋值给C<Float>
    fun testFX(c: com.example.kotlin.d623.C<Number>) {
        c.setP(1.0)
        var vc: com.example.kotlin.d623.C<Float> = c
    }

    fun testFX(b: com.example.kotlin.d623.B1<Int>) {
    // 报错，required：B1<Number>，founed：B1<Int>
    var vb: com.example.kotlin.d623.B1<Number> = b
    }

//输出
b---1============vb----1
```

> T是一个协变的类型参数，P是一个逆变的类型参数

### 类型投影

* 使用处型变：类型投影
* 星投影

类型投影：在使用时声明型变，

```
class Tom<T>(var v:T) {

    fun getT():T{
        return v
    }

    fun setT(t:T){
        v=t
    }
}


class House {

    fun change( old:Tom<Any>, new:Tom<Any>){
        new.v=old.getT()
    }


    fun change1( old:Tom<in Any>, new:Tom<out Any>){
        old.v=new.v
    }
}

    @Test
    fun testD628(){
    // 报错 required：Tom<Any>，founed：Tom<String>/Tom<Int>
        House().change(Tom<String>(),Tom<Int>())

        val old = Tom<Any>("a")
        val new = Tom<Int>(1)
        House().change1(old, new)

        println("--testD628--${old.v}")
    }

    // 输出
    --testD628---1
```

星投影：



#### 泛型函数：声明时类型参数要放在函数名称之前。使用时需在函数名后指定具体类型参数

```
fun <E> setE(e: E) :Boolean{
        return e is Int
   }
    
println("----old.setE<Int>(1)---${old.setE<Int>(1)}----")

// 输出
true
```

#### 泛型约束：指定参数类型可能类型的范围

约束上界：在类型参数加冒号**:**指定上界，默认值为Any?，多个上界用where语句，且多个上界中只有一个是类

```
    fun <U> setU(u: U) where U : Int,
                             U : Comparable<Int> {
    }
```

#### 类型擦除：泛型的类型安全检测只在编译期，运行时不会保留类型实参的任何信息



