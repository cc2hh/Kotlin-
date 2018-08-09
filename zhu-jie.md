#### 注解声明

注解是将元数据附加到代码的方法，用**annotation**修饰符声明

元注解标注来指定注解的附加属性：

* **@Target**，指定该注解标注的元素可能的类型（类、函数、属性、表达式等）
* **@Rentention**，指定该注解是否存储在编译后的class文件中；运行时是否通过反射可见（默认都为true）
* **@Repeatable**，允许在单个元素上多次使用相同的该注解
* **@MustBeDocumented**，指定该注解是公有API的一部分，并且应该在生成的API文档中显示的类或方法的签名中

```
@Target(AnnotationTarget.CLASS, AnnotationTarget.FUNCTION, AnnotationTarget.VALUE_PARAMETER,
        AnnotationTarget.EXPRESSION,AnnotationTarget.FIELD,AnnotationTarget.CONSTRUCTOR,
        AnnotationTarget.PROPERTY_SETTER)
// 默认值RUNTIME，都为true；SOURCE都为false；BINARY只存储，不反射
@Retention(AnnotationRetention.SOURCE)
@Repeatable
@MustBeDocumented
annotation class A809 {

}
```

#### 用法

在Target中指定有的类型才能对应使用，例如若没有AnnotationTarget.CLASS声明，则不能对class使用该注解

> 主构中的参数无需AnnotationTarget.VALUE\_PARAMETER声明也能使用；次构和函数的参数则需要声明才能使用

```
@A809
class B809 @A809 constructor(@A809 val name: String) {
    @A809
    fun read(): Int {
        print("read")

        return (@A809 1)
    }

    var age:Int=1
    @A809 set

}
```

#### 构造函数

注解仅能有主构且可以带参数，参数必须**val**修饰

```
// 声明注解
@Target(AnnotationTarget.CLASS)
annotation class Q809(val width: String, val t: A809) {}

// 使用
 @Q809("QQ", A809())
 class IA809 {}
```

允许的参数类型：

* 对应java 的原生类型（Int等）
* String（字符串）
* 类（String::class等）
* 枚举
* 注解
* 以上类型的数组

> 不能有可空类型，JVM不支持将null作为注解属性的值存储

如果参数为另一注解，则参数注解不用@修饰；当类作为参数时，使用KClass声明参数

```
@Target(AnnotationTarget.CLASS)
annotation class W809(val f: KClass<String>, val fo: KClass<out Any>, val foo: KClass<*>) {}


@W809(String::class, String::class, String::class)
class IB809 {}
```

#### lambda表达式

注解被应用于生成表达式体的invoke\(\)方法

#### 注解使用处目标

当对属性或者主构参数进行标注时，对应的元素在java中会生成多个，所以需要精确指定该元素的生成

```
class C809(@field:A809 val name: String,// 标注 java 字段
           @param:A809 val age: Int,    // 标注 java 构参
           @get:A809 val sex: Float)    // 标注 java get函数
```

支持使用处目标的完整声明：

* file ，
* field ，字段
* param ，构参
* setparam ， 属性set参数
* get ， 属性get
* set ， 属性set
* property ， 对java不可见
* receiver ， 扩展函数或属性的接受者参数
* delegate ， 为委托属性存储其委托实例的字段

使用相同的语法标注整个文件，把带目标file的注解放在文件顶部

```
@file:JvmName("B809")
package com.example.kotlin.d8.d809
```

对同一目标有多个注解，在目标后面使用方括号**\[\]**包含所有注解，注解之间用空格分隔

```
@Target(AnnotationTarget.FIELD)
annotation class E809

class D809(@field:[A809 E809] val name: String)
```

标注扩展函数

```
fun @receiver:Fancy String.myExtension() { ... }
```

> 若不指定使用处目标，则按照Target声明的注解类型来标注，若注解类型有多个适用，则使用以下顺序适用标注：param -&gt; property -&gt; field

#### Java注解

与Java注解完全兼容。Kotlin使用Java注解：

* 需要使用命名参数来传递参数（Java注解中参数无序）；特殊情况，参数名为**value**时，无需使用命名参数
* 数组作为注解参数，需使用字面值（names = \["abc", "foo", "bar"\]）或arrayOf\(\)方法（names = arrayOf\("abc", "foo", "bar"\)）
* 访问注解实例的属性，注解实例的值会作为属性暴露给Kotlin



