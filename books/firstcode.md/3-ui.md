###### layout_gravity
LinearLayout方向为水平时候，在垂直方向上起作用，垂直亦然
FrameLayout也可以使用来定位

###### RelativeLayout有用的属性使控件与相对对齐
layout_alignLeft 与控件左侧对齐
layout_alignTop
layout_alignRight
layout_alignBottom 类似

###### 百分比布局
PercentFrameLayout
PercentReleativeLayout
支持百分比宽高和margin
layout_widthPercent
layout_heightPercent
layout_marginPercent
layout_marginLeftPercent
layout_marginStartPercent
layout_marginRightPercent
layout_marginEndPercent
layout_marginTopPercent
layout_marginBottomPercent
源码解析和自定义PercentLinearLayout
http://blog.csdn.net/lmj623565791/article/details/46695347

原理:主要用到类PercentLayoutHelper PercentLayoutHelper.PercentLayoutParams
1.generateLayoutParams重写返回实现了PercentLayoutHelper.PercentLayoutParams接口的LayoutParams，这样可以通过getPercnetLayoutInfo返回PercentLayoutHelper.PercentLayoutInfo保存的percent信息

2.onMessure的时候通过PercentLayoutHelper的ajustChildren方法，遍历子view，给他们的PercentLayoutParams（margin,width,height的percent如果是的话）设置百分比，如果测量的值太小而且子view的w/h为wrap_content时候，对应的重置为wrap_content重新测量
3.onlayout中重置 宽高


###### recyclerview多列时候 列的宽度是自动分配的 这时候item的宽度应为match_parent

###### Recyclerview.ViewHolder getLayoutPosition和getAdapterPositon的区别
getLayoutPosition反应的是recyclerview中视图的位置，getAdapterPositon反应的是adapter中的位置。当数据改变通知视图改变的时候<16ms，这时候他们是不一致的。要等layout刷新，才能得到操作后的真正位置，除非通知使用的是notifyItemInsert(0)这种方法，他就能同时知道。
mRecyclerView.findViewHolderForLayoutPosition(myViewHolder.getLayoutPosition() - 1)可以查找到视图中对应位置的ViewHolder

###### Recyclerview.Adapter 的通知
在之前我们用 ListView 或者 GridView 的时候，通知适配器刷新是这样的：

adapter.notifyDataSetChanged();
但是当我们使用了更强大的 RecyclerView 之后，如果直接这样通知适配器刷新将不会显示动画效果。它会直接将所有的 item 重新绘制。

我们需要使用如下的方法来通知适配器刷新，这样 RecyclerView 才会显示对应的动画效果：

adapter.notifyItemInserted();
adapter.notifyItemChanged();
adapter.notifyItemMoved();
adapter.notifyItemRemoved();
adapter.notifyItemRangeChanged();
adapter.notifyItemRangeInserted();
adapter.notifyItemRangeRemoved();
Support Library 24.2.0 中添加了一个新的工具类DiffUtil
