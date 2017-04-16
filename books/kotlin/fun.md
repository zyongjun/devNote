-----------------
高阶函数有参数怎么传：
答：可以通过高阶参数之前的参数传入

?请注意，如果一个函数接受另一个函数作为最后一个参数，lambda 表达式参数可以在 圆括号参数列表之外传递。 参见 callSuffix 的语法。
----------------


#### 高阶函数
以函数作为函数的参数或者返回值的函数
```
fun <T> h(a:T,trans:(T)->Unit){
  trans(a)
}
```

#### lamda表达式
```
{x:Int,y:Int->x+y}
```
语法
1.{}包着
2.->分隔参数和函数体，类型可选
```
{x,y->x+y}
```

#### 匿名函数
lamda表达式不方便指定返回类型，一般不必要，如果需要显示表示返回类型，可以使用匿名函数：
fun(x:Int,y:Int):Int{

}
返回类型能够从上下文推断也可以省略
上面的示例可以这样调用：
```
h(2){
    fun(a:Int){
        println("====$a")
    }
}
```

#### 闭包
lamda、匿名函数、局部函数、对象表达式可以访问其闭包，即外部作用域中的变量和修改

####带接收者的函数字面值
>sum:Int.(other:Int)->Int

```
fun t(b:Test.() ->Unit){
    val t= Test()
    t.b()
}

class Test(){
    fun a(i:Int = 5){
        println("=========$i")
    }
}
调用
t{
     a(2)
 }
```
如果需要一个带接受者的函数字面值后面使用
```
val sum = fun Int.(other:Int):Int = this+other
```