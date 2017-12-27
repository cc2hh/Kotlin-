## 基本语法

* #### 包

同Java类似，也用关键字 **package **，位于源文件顶部

```
package com.example.kotlin
```

* #### 函数

使用关键字**fun**，同java的int不同，使用Int

```
// 无返回值函数，Unit可以省略
fun test(name: String, age: Int):Unit {
    }

// 有返回值函数
fun test(name: String, age: Int):Boolean {
        return 1<2
    }
// 另一种形式，Boolean声明可以省略
 fun test(name: String, age: Int): Boolean = 1 < 2
```

* #### 变量

使用关键字**val**（只读）和**var**（可变），处于源文件不同位置，分为顶层变量和局部变量，同java的全局和局部对应

定义变量时就赋值可省略类型声明，顶层和局部都适用

```
    //    val ageL: Int = 0
    //    var ageR: Int = 0
    val ageL = 0
    var ageR = 0
```

顶层变量的赋值情况：

1. 在定义时就赋值
2. 使用关键字**lateinit**声明延迟赋值
3. 定义时不赋值，在**init{}**函数中赋值

三种情况必须实现一种

* #### 注释

同java一样，其中块注释可以嵌套

```
// 行注释

/*
* 块注释
*/
```

* #### 非空性

默认所有变量为非空，这样避免了java中常见的null异常。若需要可为空的变量，需在变量声明处的类型后面加“?”符号。

```
fun parseInt(str: String): Int? {
    // ……
}
```

* #### 类型检测和自动类型转换

使用关键字**is**进行检测，在检测后的作用域内变量会自动转换成检测后的类型

```
 fun getStringLength(any: Any): Int {
        if (any is String)
            return any.length
        else
            return -1
    }

//    fun getStringLength(any: Any): Int? {
//
//        return if (any is String)
//            any.length
//        else
//            null
//    }
```

* #### for循环

使用关键字**for**和**in**

```
    fun forUse() {
        val names = arrayOf("a", "b", "c")
        for (item in names) {
            println("name is $item")
        }
    }
```

> while 循环用法同java一样



