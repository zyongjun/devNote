#### getDimension,getDimensionPixelOffset和getDimensionPixelSize的区别
##### **问题**
网上搜了下这3个方法：
resources.getDimension() 
resources.getDimensionPixelOffset()  
resources.getDimensionPixelSize() 

很多说前两个对dp和sp乘以密度做转化，px不会，后面的方法不不管是px,dp,sp都会乘以密度转化
#### **分析**
这三个方法分别调用了 
TypedValue.complexToDimension
TypedValue.complexToDimensionPixelOffset
TypedValue.complexToDimensionPixelSize

查看代码，最终都会这样调用
```
     final float value = complexToFloat(data);
    final float f = applyDimension(
            (data>>COMPLEX_UNIT_SHIFT)&COMPLEX_UNIT_MASK,
            value,
            metrics);
   ```   
        
 complexToDimension返回了applyDimension的返回值,为float
 complexToDimensionPixelOffset返回了applyDimensiond的值并强转为int
 complexToDimensionPixelSize返回了applyDimensiond的值并做了修正：
 
 ```
     final int res = (int)(f+0.5f);
     if (res != 0) return res;
     if (value == 0) return 0;
     if (value > 0) return 1;
     return -1;
 ```
 
看看TypeValue.applyDimension
``` 
 public static float applyDimension(int unit, float value,
                                       DisplayMetrics metrics)
    {
        switch (unit) {
        case COMPLEX_UNIT_PX:
            return value;
        case COMPLEX_UNIT_DIP:
            return value * metrics.density;
        case COMPLEX_UNIT_SP:
            return value * metrics.scaledDensity;
        case COMPLEX_UNIT_PT:
            return value * metrics.xdpi * (1.0f/72);
        case COMPLEX_UNIT_IN:
            return value * metrics.xdpi;
        case COMPLEX_UNIT_MM:
            return value * metrics.xdpi * (1.0f/25.4f);
        }
        return 0;
    }
```
 px直接返回
 sp*metrics.scaledDensity返回
 dp* metrics.density返回
 #### **验证**
```  float a1=getResources().getDimension(R.dimen.d_12);
    int a2=getResources().getDimensionPixelOffset(R.dimen.d_12);
    int a3=getResources().getDimensionPixelSize(R.dimen.d_12);
   
    float b1=getResources().getDimension(R.dimen.p_12);
    int b2=getResources().getDimensionPixelOffset(R.dimen.p_12);
    int b3=getResources().getDimensionPixelSize(R.dimen.p_12);
   
    float c1=getResources().getDimension(R.dimen.s_12);
    int c2=getResources().getDimensionPixelOffset(R.dimen.s_12);
    int c3=getResources().getDimensionPixelSize(R.dimen.s_12);
   
    Log.e("test", "getDimension= "+a1+", getDimensionPixelOffset="+a2+",getDimensionPixelSize="+a3);
    Log.e("test", "getDimension= "+b1+", getDimensionPixelOffset="+b2+",getDimensionPixelSize="+b3);
    Log.e("test", "getDimension= "+c1+", getDimensionPixelOffset="+c2+",getDimensionPixelSize="+c3);
```
打印如下：
```
   E/test: getDimension= 36.0, getDimensionPixelOffset=36,getDimensionPixelSize=36
   E/test: getDimension= 12.0, getDimensionPixelOffset=12,getDimensionPixelSize=12
   E/test: getDimension= 36.0, getDimensionPixelOffset=36,getDimensionPixelSize=36
```
 #### **结论**
三个方法的返回值大体一致，没什么差别，都可以使用dp,sp,px的dimen资源通过类型的不同对密度做转化
 resources.getDimension() 直接返回float   
 resources.getDimensionPixelOffset()  强转为int
 resources.getDimensionPixelSize() 传入不为0时候结果做了修正+0.5f再强转为int
实际使用中都可以差别不大