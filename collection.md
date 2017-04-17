------------
out in 协变？

----------

####集合
可变(MutableList,MutableSet,MutableMap)和不可变(List,Set,Map)
如果不可变(只读)指向一个可变的,还是只读
```
val b = mutableListOf(1,2,3)
 b.add(6)
 println(b.filter { it>2 })
 println(b.requireNoNulls())
 println(b.none { it==6 })
 println(b.firstOrNull())
 println(b.first())
 println(b.first { it>2 })
 println(b.last { it>2 })
 list同，查询方法
 val h = hashMapof("a" to 1,"b" to 2)
```


#### 区间
in !in  ..
IntRange LongRange CharRange可迭代
```
for(i in 1..10){

}
for(i in 10 downto 1){}

for(i in 1..10 step 2)

for(i in 1 util 10) //[1,10)
```

#### 智能转换
- is  !is检查是否符合类型
- 原则：能保证变量在检查和使用之间不可变时候能智能转换
- 不安全的转换操作符号 as ,如果转换是不可能的会抛出异常
- 安全的转换操作符号 as?,转换失败的时候返回null

#### 相等
- 引用相等，即是否指向同一个对象 === !==
- 结构相等，用equal检查，== != 会翻译成equal
  a==b 会翻译成 a?.equal(b)?:(b===null)
  如果a为null,检查b和null是否引用相等
- 与null比较时候 a==null会自动翻译成a===null，所以不必优化
