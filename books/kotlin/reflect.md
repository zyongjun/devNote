

#### 反射

kotlin使用反射需要包kotlin-reflect.jar包，需要添加

#### 类引用
MyClass::class ,是KClass类型的值，与java的类引用不同，要得到java类引用，在KClass值上使用.java属性

自1.1起同样可以使用对象::class获取类的引用
val a:Shape = Rectangle()
a::class
可以获取精确类rectangle的类引用。

#### 函数的引用
1.  
```
fun a(){}

::a表示这个函数的引用，可以作为函数参数传递
```
作为参数传递，相当与()->unit的一个值

2. 如果限定类的函数或扩展函数的引用的引用，String::toFloat
