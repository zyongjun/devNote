#### **selector**
```StateListDrawable drawable = new StateListDrawable();
   Drawable selected = context.getResources().getDrawable(R.drawable.woman_icon_select);
   Drawable unSelected = context.getResources().getDrawable(R.drawable.woman_icon_default);
   drawable.addState(new int[]{android.R.attr.state_pressed},
           selected);
   drawable.addState(new int[]{-android.R.attr.state_pressed},
           unSelected);
   tv.setCompoundDrawablesWithIntrinsicBounds(null, drawable, null, null);
   ```
   
   Android.R.attr.state_presses前面加负号代表xml中android:state_pressed="false"
   
#### **shape**
```int strokeWidth = 5; // 3dp 边框宽度
       int roundRadius = 15; // 8dp 圆角半径
       int strokeColor = Color.parseColor("#2E3135");//边框颜色
       int fillColor = Color.parseColor("#DFDFE0");//内部填充颜色
   
       GradientDrawable gd = new GradientDrawable();//创建drawable
       gd.setColor(fillColor);
       gd.setCornerRadius(roundRadius);
       gd.setStroke(strokeWidth, strokeColor);
   ```