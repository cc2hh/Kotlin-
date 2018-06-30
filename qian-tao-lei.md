类可以嵌套在其他类里

* 内部类，用关键字**inner**标识，使其能访问外部类的成员
* 匿名内部类，用对象表达式创建实例

```
class Q {

    private var a = 1
    var b = "?"

    fun getValue() {}

    class W {
        private var c = 2
//        var f = a

        fun foo() = c
    }

    inner class InE {
        private var d = a

        fun foo() = b
    }
}

class Num {

    fun setClick(h: H) {

    }

    fun setEnable(g: G) {

    }
}

interface H {

    fun getH()

    fun setH()
}

class G{
}

 @Test
    fun testD630() {
        val wf = com.example.kotlin.d630.Q.W().foo()
        val ef = com.example.kotlin.d630.Q().InE().foo()

        println("---testD630----$wf--------$ef")

        Num().setClick(object :H{
            override fun setH() {

            }

            override fun getH() {

            }
        })

        Num().setEnable(G())
    }


// 输出
---testD630----2--------?

```

> 内部类使用时需要用外部类的实例调用：Q\(\).InE\(\)，而普通嵌套类则直接用外部类即可：Q.W\(\)





