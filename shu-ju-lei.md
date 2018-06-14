只保存数据的类，用关键字**data**声明

数据类为了确保一致性和有意义，必须满足：

* 主构至少有一个参数且所有参数都需用**var**或**val**修饰
* 不能声明为抽象、**open**、密封或内部的

特点，会为主构的所有参数自动生成：

* equals\(\) / hashCode\(\) 对
* toString\(\)
* componentN\(\) ，按主参顺序生成
* copy\(\)

在类体中声明的属性不会自动生成上述方法，若类的两个对象主构值一样，则视为相等

```
data class User(val name: String, val sex: Boolean) :Person(){

    var age: Int = 0
    
    fun callName():String{
        return name
    }
}

----------------------------------------------------

open class Person {

   final override fun toString(): String {
        return "Person"
    }

}

----------------------------------------------------

    @Test
    fun testD614() {
        val user = User("cc",true)
        val user1 = User("cc",true)

        user.age = 12
        user1.age = 24

        val copy = user.copy(sex=false)

        println("------${user.toString()}----------")
        println("------${copy.name}-----${copy.age}---${copy.sex}--")
        println("-user.age-${user.age}---${user.equals(user1)}---user1.age----${user1.age}----")
    }
   
   // 输出
------Person----------
------cc-----0---false--
-user.age-12---true---user1.age----24----
```

##### copy\(\)函数，改变对象某部分主构值，其余保持不变。类体中的属性保持初始值

数据类可用于解构声明

标准库提供了**`Pair`**和**`Triple`**`数据类`



