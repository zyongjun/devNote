###### 如何实现图形随touch绘制的状态
1. action down 获取起点  初始化path
2. action move 根据起点和当前位置完成path路径 invalidate
3. ondraw 中绘制path到画布上
4. action up 根据path的路径创建图形缓存，reset path

#### 如何实现可回退的批注绘制
BaseShapeView  
1. parcelable
2. resetData
3. x,y,r,b
4. ondraw(Canvas canvas)
5. isfocus isvisible  shapeId
6. shapeAction

DrawingView
1. List<BaseShapeView> listRoot
2. currentIndex
----------------------
- 创建图形
  touch down  startx  starty
  touch up  create endx endY
  已经撤销部分清除掉 clearRedoSharpFromIndex（currentIndex）
  listRoot.add  currentIndex = size
  reset tmp virtual
 jumpShapeToTopLayer
 showOriginShape  currentShape = null

  invalidate


- 图形的显示
- 图形的移动

- 图形resize

- 图形焦点与点击


- 橡皮擦

- 回收

- 覆盖


- scale

- 图片拖动
- 缓存

---------
1. PathEffect

----------
###### Math.atan2(y2-y1,x2-x1)  计算(x1,y1)  (x2,y2)两点间的夹角，是弧度
转换成角度 Math.atan2(y2-y1,x2-x1)*180/Math.PI
1. 计算一定偏角与指定长度处的座标
```
double theta = Math.atan2((double) (tipY - tailY), (double) (tipX - tailX));
double x1 = tipX - arrowLength * Math.cos(theta+Math.toRadians(45.0d));
double y1 = tipY - arrowLength * Math.sin(theta+Math.toRadians(45.0d));
```


###### Paint
http://blog.csdn.net/abcdef314159/article/details/51720686

setStyle  Paint.FILL Paint.STROKE  Pain.STROKEANDFILL
setStrokeJoin 绘制矩形时候的角的效果 Pain.Join.BEVEL  Pain.Join.MITER Paint.Join.ROUND
setStrokeCap 末端  Pain.Cap.BUTT  Pain.Cap.ROUND Pain.Cap.SQUARE

setStrokeMiter  style为stroke或STROKEANDFILL时候，角的效果
