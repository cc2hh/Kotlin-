使用的基本类型有：数字，字符，布尔，数组和字符串

* ## 数字

同**java**类似，但是没有隐式转换。例：Int 不能隐式转换成Long

类型                占位数

Double             64

Float                32

Long                64

Int                    32

Short               16

Byte                 8

> 不支持八进制

数字常量可添加下划线 **\_ **，使其易读

```
    val num = 100_000_110
    val socialSecurityNumber = 999_99_9999L
    val hexBytes = 0xFF_EC_DE_5E
    val bytes = 0b11010010_01101001_10010100_10010010
```

当使用非空引用或泛型时，会把数字装箱，装箱后有相等性也有同一性（跟教程不一样，待查）

```
    fun numEquals(v: View) {

        val a = 100
        val aa: Int? = 100
        println("a= = =a:${a === a}")
        println("a= = =aa:${a === aa}")

        val b = a
        val c = a
        println("b = = = c:${b === c}")
        println("b = = c:${b == c}")

        val d: Int? = a
        val e: Int? = a
        println("d = = = e:${d === e}")
        println("d = = e:${d == e}")

    } 

//打印输出

 a= = =a:true
 a= = =aa:true
 b = = = c:true
 b = = c:true
 d = = = e:true
 d = = e:true
```

###### 显示转换

```
        val a = 100

        val l: Long? = 1 // 静态检测
        val ll: Long? = a.toLong() // 显示转换Long方法
```

数字类型都有相应的数字类型显示转换方法，额外还有字符类型转换方法toChar\(\)

> 运算符会有重载做适当转换 val a = 1L+3

浮点数的一个注意点，逻辑运算符的变量为非静态浮点数时，运算符为浮点数实现不符合标准的equals与compareTo，会导致：

* 认为NaN与其自身相等
* 认为NaN比包括正无穷大在内的其他任何元素都大
* 0.0大于-0.0

> NaN 是Not a Number的缩写，非数字值的特殊值，用于处理计算中出现的错误情况

```
@Test
fun addition_isCorrect() {
val a = 0.0 // 静态为浮点数
val b = -0.0
println(a == b)
testEquals(a, b)
}

fun testEquals(a: Any, b: Any) {
// 这时a为Any并非静态浮点数
println("testEquals:${a == b}")
}
// 输出
true
testEquals:false
```

* ## 字符

用关键字**char**表示，不能直接当作数字

```
    fun testChar() {
        val c = '1'
        assertEquals(c, 1)
    }
    // 输出
    Expected :java.lang.Character<1> 
    Actual   :java.lang.Integer<1>
```

* ## 布尔

用关键字**Boolean**表示，值只有**true**和**false**

* ## 数字

用关键字**Array**表示，自带**get**与**set**函数和**size**属性，以及一些成员函数

```
class Array<T> private constructor() {
    val size: Int
    operator fun get(index: Int): T
    operator fun set(index: Int, value: T): Unit

    operator fun iterator(): Iterator<T>
    // ……
}
```

* 使用arrayOf\(\)库函数创建数组，arrayOfNulls\(\)创建元素都为空的数组。通过**\[\]**获取元素

```
    @Test
    fun testArray() {
//        val array = arrayOf(1, 2, 3)
        val array=arrayOfNulls<Int>(5)
         val temp=array[0]
        for (item in array) {
            println(item)
        }
    }
   // 输出
null
null
null
null
null
```

* 使用构造函数Array\(\)创建数组，第一个参数为数组大小，第二个参数为一个初始化函数

```
        val ac: Array<Int?> = Array(2, { it })
        for (item in ac) {
            println(item)
        }
        // 输出
        0
        1
```

> 与java的数组不同，不是型变的，即不能把Array&lt;String&gt; 赋值给Array&lt;Any&gt;，可以使用Array&lt;out Any&gt;

* 使用不装箱的专门类创建数组，如：intArrayOf\(\)-&gt;IntArray，IntArray不是Array的子类，没有继承关系

```
val arrInt: IntArray = intArrayOf(1, 2, 3)
```

* ## 字符串

用关键字**String**表示，是不可变的。可用**\[\]**获取其元素。有2种类型的字面值：转义字符串和原生字符串。通过trimMargin\(\)函数去除前导字符

```
    @Test
    fun testString() {
        // 转义字符串
        val str = "qw\nop\n"
        println(str[0])
        for (item in str) {
            print(item)
        }

        // 原生字符串
        val strT = """
    fun testChar() {
        val c = '1'
        assertEquals(c, 1)
    }

    ?my name is cc
    ?are you ok
    ?how old are you
    !!? please
        """.trimMargin("?")

        println(strT)

    }
    // 输出
q
qw
op
    fun testChar() {
        val c = '1'
        assertEquals(c, 1)
    }

my name is cc
are you ok
how old are you
    !!? please
```

> 基础类型使用可空引用时，会被装箱



