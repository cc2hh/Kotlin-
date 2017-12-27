# 基本类型

使用的基本类型有：数字，字符，布尔，数组和字符串

* #### 数字

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

> 运算符会有重载做适当转换 val l = 1L+3





