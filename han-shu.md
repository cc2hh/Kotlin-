#### 函数声明

用关键字**fun**声明函数

#### 用法

成员之间可直接调用，使用对象调用时用点操作符

```
class B707 {

    var name = run()

    fun run(age: Int = 1) {

    }

    class b707 {
        var v = B707().run()
    }
}
```

##### 参数

使用Pascal表示法：name **: **type，

* 参数之间用逗号分隔
* 必须显式声明类型
* 可设置默认值

覆盖方法时若参数有默认值，则覆盖方法不能设置默认值，用原方法的默认值

##### 命名参数

调用函数时使用命名的函数参数

```
class C707 {

    fun eat(age: Int = 1, name: String, sex: Boolean) {}

    fun speak(age: Int=1,vararg v:String){
    }
}

-----------测试----------------
        C707().eat(sex = false, name = "CC")
        C707().eat(12, "CC", false)
        C707().eat(12, name = "CC", sex = false)
        C707().speak(2,"CC", "HH", "EE")
        C707().speak(v = *arrayOf("CC", "HH", "EE"))
```

命名参数之间使用时可以换位置，但所有的位置参数必须放在第一命名参数之前

可变参数（vararg）的命名参数需要用星号修饰

> java中不能使用命名参数是由于java字节码不一定保留参数名称

#### 函数的返回

默认无返回就是返回Unit

```
    fun read() {}
    // 等价于
    fun read(): Unit {}
```



