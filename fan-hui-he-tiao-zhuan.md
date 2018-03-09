**return，break，continue**

> break和continue只使用在循环体内

### **标签**

任何表达式都可以用标签来标记，为一个表达式加标签，只需在表达式前加上所需标签即可

##### 格式

标识符加@  例如：abc@ 表达式

##### 用法

```
        listOf(1,2,3,4).forEach adb@{
            if (it==3) return@adb
            println(it)
        }
        println("函数尾")

        // 输出
        1
        2
        4
        函数尾
```

* break：跳转到标签后的循环体，执行循环体之后的代码
* continue：跳转到标签后的循环体，执行循环体的下一次循环
* return：允许从外层函数返回

> return在lambda表达式中使用需要注意。不加标签，直接返回到外层函数；加标签，返回到标签处

```
        listOf(1,2,3,4).forEach {
            if (it==3) return
            println(it)
        }
        println("函数尾")

        // 输出
        1
        2
```



