**this**表示当前接受者

* 在类的成员中，指代该类的当前对象
* 在扩展函数或带接受者的函数字面值中，指代点左侧的接受者对象

> 作用域为最内层包含其的接受者内

##### 限定this

访问外部作用域的**this**，需使用this@label形式，@label代表接受者对象

```
class A727 {

    inner class B727 {
        fun String.read() {
            // 调用最外层
            println("this@A727==${this@A727}")
            // 调用内部类层
            println("this@B727==${this@B727}")
            // 调用最内层
            println("this@read==${this@read}")
            // 直接调用
            println("this==$this")

            // 无接受者的lambda，this指代作用域对象（扩展函数）点左侧的接受者String
            val b = { _: Int -> "this==${this}" }
            println("Int---b(2)==${b(2)}")

            // 带接受者的函数字面值，this指代点左侧接受者Int
            val c = fun Int.(): String { return "this==$this" }
            println("Int---c(3)==${c(3)}")
        }

        fun speak() {
            "asd".read()
        }

    }


    fun opo() {
        TODO("考虑如何在外部使用在内部类声明的扩展函数")
    }

}

// 输出
this@A727==com.example.kotlin.d7.d727.A727@58d25a40
this@B727==com.example.kotlin.d7.d727.A727$B727@1b701da1
this@read==asd
this==asd
Int---b(2)==this==asd
Int---c(3)==this==3
```



