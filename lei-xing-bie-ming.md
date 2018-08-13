为现有的名称提供替代名称，别名

##### 缩短较长泛型类型

```
// 声明
typealias persionSet = Set<Persion>
typealias  tSet<T> = Set<T>

// 使用
    fun read(a: Set<Persion>) {
        a.forEach { println(it.toString()) }
    }

    fun <T> speak(a: tSet<T>) {
        a.forEach { println(it.toString()) }
    }
```

##### 函数类型提供别名

```
typealias MyHandler = (Int, String, Any) -> Unit

typealias Predicate<T> = (T) -> Boolean
```

##### 内部类和嵌套类

```
class A {
    inner class Inner
}
class B {
    class Inner
}

typealias AInner = A.Inner
typealias BInner = B.Inner
```

> 别名不会新引入一个类型，等效于相应底层类型，可互相替换使用
>
> ```
> // 测试
>  val b813 = B813()
>
> ------------别名变量传全名参数---------------------
>  val a: persionSet = setOf(Persion("CC", 18))
>  b813.read(a)
>
> ------------全名变量传别名参数---------------------
>  val b: Set<Persion> = setOf(Persion("HH", 16))
>  b813.speak(b)
>  
>  // 输出
> Persion(name=CC, age=18)
> Persion(name=HH, age=16)
> ```



