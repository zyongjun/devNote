###### FLAG
- Intent.FLAG_ACTIVITY_CLEAR_TOP 清除该activity上的activity
关于clear_top的使用方法在源码注释里写的很清楚：
   ```    /** If set, and the activity being launched is already running in the
           * current task, then instead of launching a new instance of that activity,
           * all of the other activities on top of it will be closed and this Intent
           * will be delivered to the (now on top) old activity as a new Intent.
           **/```
 如果当前栈里有这个activity的实例的话，会清除上面所有的activity并带上这个intent.
 
 举例：依次启动A、B、C、D，D带Intent.FLAG_ACTIVITY_CLEAR_TOP启动B的话，C和D都会被清除，而D会收到这个Intent.
 关于B会不会新建有两种情况：
 1. 当B是默认的standard（可以创建多个实例‘multiple’）模式下，B会被创建，Intent正是启动的Intent
 > 检测是否有某个Flag用解包的方式 
 > ```((Intent.FLAG_ACTIVITY_CLEAR_TOP & intent.getFlags()) != 0)```
 2. 不会新建的情况
    1) 当B是其他任意启动模式时候，都不会被新建，onNewIntent会被调用带有这个Intent
    2) standard模式下（其他模式查看上一条说明）设置了Intent.FLAG_ACTIVITY_SINGLE_TOP
效果同上。
 3. Intent.FLAG_ACTIVITY_CLEAR_TOP和Intent.FLAG_ACTIVITY_NEW_TASK结合比较有意思的一个点，
 当B是singleInstance的时候，可以把B带到栈顶而不会清掉C和D。在特定场景比如通知栏点击打开某个页面非常有用。

**遇到启动模式相应的问题一定要注意目标activtiy本来设置的lauchmode,因为lauchmode也会影响结果，
所以看到网上相关问题答案比较混乱，多种混用的话只能具体情况具体分析**
- Intent.FLAG_ACTIVITY_SINGLE_TOP:
```
    /**
     * If set, the activity will not be launched if it is already running
     * at the top of the history stack.
     */
```
- Intent.FLAG_ACTIVITY_NEW_TASK:

