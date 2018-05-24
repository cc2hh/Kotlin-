* 与**java**不同，被覆盖方法和属性也需要用**open**显式声明，并且只有基类才能声明，覆盖方法用**override**声明

* 在基类中没有显示声明的函数，不能在子类中覆盖
* 覆盖的成员本身是**open**的，若需要修改为不可被覆盖则需要添加**final**修饰该成员

> val 可被覆盖为var，反之则不可以

```
open class Animal(){

    // 可被覆盖属性
    open val color: Int = 0

    constructor(age:Int):this()

     // 可被覆盖方法
     open fun eat(){}
     
     // 可被覆盖方法
     open fun speak(){}

     // 不可被覆盖方法
     fun run(){}
}

open class Dog: Animal {
    // 被覆盖属性
    override var color: Int=1

    constructor(age:Int):super()
    constructor(name:String):this(1)

    // 覆盖基类方法
    override fun eat() {
        super.eat()
    }

    // 覆盖基类方法
   final override fun speak() {
        super.eat()
    }
    // 不是覆盖方法，参数不同
    fun run(speed:Int){}

}

class BlackDog:Dog(1){
    // 覆盖基类方法
    override fun eat() {
        super.eat()
    }
    
    // 不能覆盖speak方法，已被修改为
}
```



