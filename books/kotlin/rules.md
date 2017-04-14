#### kotlin 语法
==================
question:
- 泛型 in  , out  
- this::prop  两个冒号意思

------------------------
#### 对象表达式  也叫匿名对象
- 只能用在本地和私有作用域
- 如果用作公有函数的返回类型或者公有属性，那么类型会是匿名对象的超类或者any,新添加的成员无法使用

#### 对象声明

- 不是表达式不能用在语句的右边
- 是单例模式，使用的时候直接使用名称即可
- 不能声明在局部作用域（函数内）,可以嵌套在其他对象声明，---和非内部类（这个不能理解，好像不报错）

 ##### 伴生对象 （类内部的对象声明）
 - companion 关键字修饰对象声明，对象名存在时候可通过Myclass.x Myclass.name.x来访问对象中的属性
 - 如果省略对象名称，引用属性可以写成Myclass.x ,Myclass.Companion.name

 #### 对象表达式、对象声明的区分
- 对象表达式是在使用的地方立即执行及初始化的
- 对象声明是在第一次使用的时候初始化的，即延迟初始化。 而伴生对象相应的是在类被加载或者解析的时候被初始化的，和静态初始化的语义相匹配
  不过不是静态对象，仍是真实对象的实例成员，只是初始化的时间和静态语义相匹配

#### 类委托 （# 不能理解，是不是多此一举 #）
class Derived(b:Base):Base by b
这里的by表示b将在Derived内部存储，并且编译器将生成Base的所有方法并转发给b

#### 委托属性
只读的属性要有getValue方法：
operator fun getValue(thisRef:Any,property:KProperty< * >){}

可写的属性要有setValue方法：
operator fun setValue(thisRef:Any?,property:KProperty< * >,value:String){}

  - 延迟属性lazy
  ```
  val a：String by lazy{

  }
```
  - 可观察属性observable

  ```
  var a：String by Delegates.observable( "aa" ){
    prop,old,new->
    ...
  }
  ```

  被赋值后调用处理程序
  如果想在赋值前截获赋值并否决他
  var a:String by Delegates.vetoable("aa"){
    prop,old,new->
    new=="bb"
  }
  如果赋值"bb"会被否决，值还是old或初始值

  - 属性存储在map中
  ```
  class Testt(map:Map<String,Any>){
    val name:String by map
  }
  Test(mapOf("name" to "joe"))
```
  - 总结
  ReadOnlyProperty ReadWriteProperty
  > 委托属性原理：编译器会生成一个代理类型的隐藏属性，实际委托属性的get set代理给这个委托属性
    ```
      class C{
        var a:String by MyDelegates()
      }
    编译器生成的类似代码
    class c{
      val a$delegates = MyDelegates()
      var a:String
        get()=a$delegates.getValue(this,this::a)
        set(value:String)=a$delegates.setValue(this,this::a,value)
      }
    ```

    #### 提供委托 provideDelegate 1.1起才有的特性
  *没有测试 升级到1.1再测*
如果属性委托by右边对象的成员或扩展函数有provideDelegate操作符方法，那么创建委托对象的时候会通过该对象的provideDelegate方法生成委托对象，通过实现该方法，可以在创建委托属性前做些事情，如检查名字
class PDelegate<T>{
  operator fun provideDelegate(thisRef:T,prop:KProperty< * >):ReadOnlyProperty{
     //do somthing
    //创建委托
  }
}

class Test{
  val a:String by PDelegate()
}

------------------

#### 函数

- 中缀表示法
1. 成员函数或者扩展函数
2. 只有一个参数
3. infix修饰

```
infix Int.a(b:Int){

}
调用 1 a 2
相当于1.a(2)
```
- 默认参数
注意默认参数的重写不能带默认参数
- 命名参数
1.调用的时候使用参数名字来赋值，增加可读性
2.调用java函数不能用命名参数，因为java字节码并不总是保留函数参数的名称

- 可变参数 varargs
1.一般放在最后一个参数，或者后面的用命名参数调用或lamda
2.伸展<Spread>操作符号*,可在数组前加传入作为可变参数或者参数一部分展开

- 局部函数
函数中可以定义函数，内部的函数可以访问外部函数的局部变量
- 泛型函数的定义和调用
```
fun <T> f(t:T){

}
调用f<Int>(1)

对比类型泛型
class a<T>{

}
a<Int>()
```
