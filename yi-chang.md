所有异常类都是Throwable的子类，并且都有消息，堆栈回溯信息以及可选的原因

可以使用throw主动抛出异常；使用**try{}**表达式捕获异常，在catch\(e:Exception\){}处理异常，finally\(\)总会执行

```
val a = try {
        1
    } catch (e: Exception) {
        2
    } finally {
        3
    }
    
    //输出
    try
    finally
    1 
```

> catch块可以有零到多个，但catch和finally至少得有一个

try表达式的返回值无异常时是try块中最后一个表达式的值；发生异常时则是catch块最后一个表达式的值；finally不影响返回值

#### 受检异常

没有受检异常，即没有Java中这样代码Appendable append\(CharSequence csq\) throws IOException;

```
    interface B808 {
    // 报错
        fun test() throw Exception
    }
```

#### Nothing类型

throw表达式返回类型为Nothing，该类型没有值，表示永远不能到达的代码位置，即不会返回

```
   fun read() :Nothing{
        throw IOException()
    }
```

> 可空变体Nothing?，该类型有一个可能值null，当使用null来默认初始化变量时，变量会推断为Nothing?
>
>     val x = null           // “x”具有类型 `Nothing?`



