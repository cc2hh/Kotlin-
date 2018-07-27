

判断两个对象相等

* 结构相等，用equals\(\)
* 引用相等，2个引用指向一个对象

##### 结构相等

用操作符**==**（**!=**）判断

```
    // == 会翻译成
    fun read(a: Int?, b: Int?): Boolean {
        return a?.equals(b) ?: (b === null)
    }
    
    // 测试
    println("c727.read(1, 1)${c727.read(1, 1)}---------(1 == 1)${1 == 1}")
    
    // 输出
    c727.read(1, 1)true---------(1 == 1)true

```

> a?.equals\(b\) ?: \(b === null\) 
>
> ?.



