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
