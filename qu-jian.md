区间以rangTo\(\)表示并配合 **in / !in **使用。

* 可用于任何**可比较**类型（继承Comparable的类）
  > 系统已扩展了
  >
  > ```
  > public operator fun <T: Comparable<T>> T.rangeTo(that: T): ClosedRange<T> = ComparableRange(this, that)
  > ```

* 对于原生类型有优化使用方式，使用操作符 **.. **表示（替换rangTo\(\)）

```
for (i in 1..4) {
    print("$i")
 }
 
// 等同

for (i in 1.rangeTo(4)) {
    print("$i")
}
```

整型区间（IntRange、LongRange、CharRange）是可以**迭代**的

部分常用方法

* downTo，倒序迭代，包括最后一位数
  ```
  for (i in 4 downTo 1) print(i)

  //输出 
  4321
  ```
* step，迭代步长，步长必须为正数，保证迭代方向不变
  ```
  for (i in 4 downTo 1 step 2) print(i)

  // 输出
  42
  ```

* until，正序，不迭代最后一位数
  ```
  for (i in 1 until 4) {
      print(i)
  }

  // 输出
  123
  ```



