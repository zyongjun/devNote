###### 如何实现图形随touch绘制的状态
1. action down 获取起点  初始化path
2. action move 根据起点和当前位置完成path路径 invalidate
3. ondraw 中绘制path到画布上
4. action up 根据path的路径创建图形缓存，reset path


###### Math.atan2(y2-y1,x2-x1)  计算(x1,y1)  (x2,y2)两点间的夹角，是弧度
转换成角度 Math.atan2(y2-y1,x2-x1)*180/Math.PI
1. 计算一定偏角与指定长度处的座标
```
double theta = Math.atan2((double) (tipY - tailY), (double) (tipX - tailX));
double x1 = tipX - arrowLength * Math.cos(theta+Math.toRadians(45.0d));
double y1 = tipY - arrowLength * Math.sin(theta+Math.toRadians(45.0d));
```


###### Paint
setStyle  Paint.FILL Paint.STROKE  Pain.STROKEANDFILL
setStrokeJoin 绘制矩形时候的角的效果 Pain.Join.BEVEL  Pain.Join.MITER Paint.Join.ROUND
setStrokeCap 末端  Pain.Cap.BUTT  Pain.Cap.ROUND Pain.Cap.SQUARE

setStrokeMiter  style 为stroke 或STROKEANDFILL时候，角的效果
