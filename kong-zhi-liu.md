控制流有四种操作符：**if,while,for,when**

* #### if

条件判断，在Kotlin中没有三元运算符（?:）用**if**来实现相同功能

```
    @Test
    fun testIf() {
        val max = 5
        val min = 1
        assertEquals(getMax(min, max), getMax(max, min))

    }

    // 类似三元运算符功能
    //    fun getMax(a: Int, b: Int) = if (a > b) a else b
    // 代码块最后表达式最为返回值
    fun getMax(a: Int, b: Int) {
        if (a > b) {
            a
        } else {
            b
        }
    }

    // 输出
    success
```

* #### while

同java一致

```
do {
  val y = retrieveData()
} while (y != null) // y 在此处可见
```

* #### for

类似java中的**foreach**，可以遍历提供迭代器的所有对象：

有成员函数或扩展函数**iterator\(\): Iterator&lt;T&gt;**，而**Iterator**对象需要函数next\(\)和函数hasNext\(\): Boolean

> 上述三个函数必须**operator** 修饰

    public operator fun iterator(): Iterator<T>

    ...

    // 迭代器接口
    public interface Iterator<out T> {
        /**
         * Returns the next element in the iteration.
         */
        public operator fun next(): T

        /**
         * Returns `true` if the iteration has more elements.
         */
        public operator fun hasNext(): Boolean
    }

使用withIndex\(\)函数可遍历索引

```
    @Test
    fun testArray() {

        val array = arrayOf(1, 2, 3)
        for ((index, item) in array.withIndex()) {
            println("$index->$item")
        }
    }
// 输出
0->1
1->2
2->3
```

* #### when

类似java里面的**switch**，分支选择

分支条件可用任何表达式；若有相同处理情况，用 **, **分割不同分支条件

可取代 **if-else-if** 模式

作表达式时必须覆盖所有情况，不能枚举所有情况时用**else**

```
    @Test
    fun testWhen() {

        var i: Int = 4
        val result = when (i) {
            0 -> "零"
            "2".toInt() -> "二"
            4 -> "四"
            6, 8 -> "六或八"
            10 -> {
                print("多条表达式")
                "十"
            }
            in 11..15 -> "在11和15之间，包括边界值"
            is Any -> "判断类型"
            else -> "无"
        }

        println("$i:$result")

        // if-else-if 模式
        when {
            i == 0 -> "零"
            i is Any -> "判断类型"
        }
        val bds = when {
            i == "4".toInt() -> "四"
            i in 6..8 -> "六和八之间"
            else -> "无"
        }
    }
```



