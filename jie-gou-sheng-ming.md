把一个对象解构成多个变量，变量可单独使用（在同样的作用域内）

* 解构成几个变量就需要对应的类声明几个component
* 任何表达式都能在解构声明右侧

##### 

##### 函数返回多个结果

把返回结果封装进一个数据类中，再函数调用处利用解构声明可直接得到结果对象

```
data class Result(val result: Int, val status: Status)
fun function(……): Result {
    // 各种计算

    return Result(result, status)
}

// 现在，使用该函数：
val (result, status) = function(……)
```

> 也可使用标准类Pair
>
> ```
>         fun run(name: String): Pair<String, Int> {
>                 return Pair(name, name.length)
>         }
>
>         // 测试
>         val a719 = A719()
>
>         val (name, speed) = a719.run("爱新觉罗·媚")
>
>         println("$name 的速度是 $speed")
>         // 输出
>         爱新觉罗·媚 的速度是 6
> ```

##### 

##### 使用map时

遍历一个map时，可直接得到key与value

```
for ((key, value) in map) {
    // 使用该 key、value 做些事情
}
```

> 标准库为我们实现了这样使用时，map需要的扩展
>
> ```
> operator fun <K, V> Map<K, V>.iterator(): Iterator<Map.Entry<K, V>> = entrySet().iterator()
> operator fun <K, V> Map.Entry<K, V>.component1() = getKey()
> operator fun <K, V> Map.Entry<K, V>.component2() = getValue()
> ```

---

使用下划线来表示不会使用的解构声明变量（同lambda中一样）

```
        val (name1, _) = a719.run("爱新觉罗·拉克丝")

        println("$name1 没有速度变量")
        
        // 输出
        爱新觉罗·拉克丝 没有速度变量
```

在lambda中使用解构声明

* 若具有Pair、Map.Entry或任何具有相应componentN类型的参数可通过括号中引入新参数来取代单个参数
  ```
  map.mapValues { entry -> "${entry.value}!" }
  map.mapValues { (key, value) -> "$value!" }
  ```

* 多个参数和解构声明的区别
  ```
  { a, b, c //-> …… } // 两个参数
  { (a, b, c) //-> …… } // 一个解构对
  { (a, b), c //-> …… } // 一个解构对以及其他参数
  ```

* 可以为解构的参数整体或单独指定类型
  ```
  map.mapValues { (_, value): Map.Entry<Int, String> -> "$value!" }

  map.mapValues { (_, value: String) -> "$value!" }
  ```





