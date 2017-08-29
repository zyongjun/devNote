1.屏幕尺寸 对角线长度，单位寸
分辨率：手机屏幕像素点个数 720x1280
DPI PPI: 计算方法 对角线的像素个数/屏幕大小
独立像素密度 dp的换算方法：
###### DPI PPI标识单位尺寸上像素个数，以160dpi为标准（1dp为1px），320dpi单位物理尺寸像素个数是160dpi的两倍，故为1dp是2px

###### xml绘图
1. Bitmap
```
<?xml version="1.0" encoding="utf-8"?>
<bitmap
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:src="@[package:]drawable/drawable_resource"
    android:antialias=["true" | "false"]
    android:dither=["true" | "false"]
    android:filter=["true" | "false"]
    android:gravity=["top" | "bottom" | "left" | "right" | "center_vertical" |
                      "fill_vertical" | "center_horizontal" | "fill_horizontal" |
                      "center" | "fill" | "clip_vertical" | "clip_horizontal"]
    android:tileMode=["disabled" | "clamp" | "repeat" | "mirror"] />
```

2. shape
```
<?xml version="1.0" encoding="utf-8"?>
<shape    
    xmlns:android="http://schemas.android.com/apk/res/android"    
    android:shape=["rectangle" | "oval" | "line" | "ring"] >    
    <corners        //当shape为rectangle时使用
        android:radius="integer"        //半径值会被后面的单个半径属性覆盖，默认为1dp
        android:topLeftRadius="integer"        
        android:topRightRadius="integer"        
        android:bottomLeftRadius="integer"        
        android:bottomRightRadius="integer" />    
    <gradient       //渐变
        android:angle="integer"        
        android:centerX="integer"        
        android:centerY="integer"        
        android:centerColor="integer"        
        android:endColor="color"        
        android:gradientRadius="integer"        
        android:startColor="color"        
        android:type=["linear" | "radial" | "sweep"]        
        android:useLevel=["true" | "false"] />    
    <padding        //内边距
        android:left="integer"        
        android:top="integer"        
        android:right="integer"        
        android:bottom="integer" />    
    <size           //指定大小，一般用在imageview配合scaleType属性使用
        android:width="integer"        
        android:height="integer" />    
    <solid          //填充颜色
        android:color="color" />    
   	<stroke         //边框
      	android:width="integer"        
        android:color="color"        
        android:dashWidth="integer"        
        android:dashGap="integer" />
</shape>
```

3. layer-list

```
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="@[package:]drawable/drawable_resource" />
    <item android:drawable="@[package:]drawable/drawable_resource" />
    ......
</layer-list>

```

4. selector
```
<?xml version="1.0" encoding="utf-8" ?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <!-- 默认时的背景图片-->
    <item android:drawable="@drawable/pic1"/>
    <!-- 没有焦点时的背景图片 -->
    <item android:drawable="@drawable/pic1" android:state_window_focused="false"/>
    <!-- 非触摸模式下获得焦点并单击时的背景图片 -->
    <item android:drawable="@drawable/pic2" android:state_focused="true" android:state_pressed="true"/>
    <!-- 触摸模式下单击时的背景图片-->
    <item android:drawable="@drawable/pic3" android:state_focused="false" android:state_pressed="true"/>
    <!--选中时的图片背景-->
    <item android:drawable="@drawable/pic4" android:state_selected="true"/>
    <!--获得焦点时的图片背景-->
    <item android:drawable="@drawable/pic5" android:state_focused="true"/>
</selector>
```

selector设置不同状态下的文本颜色
```
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:color="#999" android:state_selected="true"/>
    <item android:color="#666" android:state_focused="true"/>
    <item android:color="#333" android:state_pressed="true"/>
    <item android:color="#000"/>
</selector>
```


###### android canvas layers
canvas.saveLayerAlpha
canvas.restore()
调用saveLayerAlpha之后，后续的drawxxxx操作都发生在新建的图层上，restore会将新图层合并到canvas默认图层上
