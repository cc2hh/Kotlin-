通过**operator**修饰的成员函数或扩展函数可以重载预定义的操作符

#### 一元操作符

| 表达式 | 对应函数 |
| :---: | :---: |
| +a | a.unaryPlus\(\) |
| -a | a.unaryMinus\(\) |
| !a | a.not\(\) |
| a++（++a） | a.inc\(\)（++在前，则先使用后计算；反之，则先计算后） |
| a--（--a） | a.dec\(\)（--在前，则先使用后计算；反之，则先计算后） |

#### 二元操作符

| a+b或a+=b | a.plus\(b\)或a.plusAssign\(b\) |
| :---: | :---: |
| a-b 同上 | a.minus\(b\) |
| a\*b 同上 | a.times\(b\) |
| a/b 同上 | a.div\(b\) |
| a%b 同上 | a.rem\(b\) |
| a..b | a.rangTo\(b\) |
| a in b或a !in b | b.contains\(a\)或!b.contains\(a\)  **注意：参数顺序反的** |
| a\[i\]或a\[j\]=b | a.get\(i\)或a.set\(j,b\) |
| a\(i\) | a.invoke\(i\) |
| a==b或a!=b | a?.equals\(b\)?:\(b===null\)或!\(a?.equals\(b\)\)?:\(b===null\)相等性 |
| a&gt;b或a&gt;=b | a.compareTo\(b\)&gt;0或a.compareTo\(b\)&gt;=0 |
| a&lt;b或a&lt;=b | a.compareTo\(b\)&lt;0或a.compareTo\(b\)&lt;=0 |

#### 属性委托操作符

provideDelegate，getValue和setValue

#### 中缀表示法



