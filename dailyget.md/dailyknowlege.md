## public resource
android资源默认是public的，想保护某些资源不背访问，可以创建res/values/public.xml
里面至少一行，没声明的都是private
<resources>
  <public name="hello" type="string"/>
</resources>

如果在library的build.gradle中添加resourcePrefix,所有资源都要以这个prefix开头
android{
....
  resourcePrefix 'myprefix'
}

## xlmns:tools:''http://schemas.android.com/tools''
####错误处理
tools:ignore  任意元素，值为任意lint错误ID，多个用逗号隔开
tools:targetApi 指定api版本，防止版本不适合报错
tools:locale 给resources指定语言区域,如es,防止语言检查报错
###视图预览  可以同时使用tools 和android定义属性值在一个控件中
tools:showIn 能预览显示在另一个include这个layout的布局
* tools:context 用于布局推断默认主题，可以省略包名，如.MainActivity,
  另外可以使android:onClick使用快捷方式直接在推断的容器中创建点击方式

### 资源压缩属性
首先要配置资源压缩脚本
release{
  shrinkResources true
  minifyEnable true
  progardFiles getDefaultProgardFile('progard-android.txt'),'progard-rules.pro'
}

tools:shrinkMode  safe or strict
当指定strict模式时候
tools:keep 指定保持的资源
tools:discard指定删除的资源
使用方式，创建一个带resources标签的xml,添加属性，多个值能用逗号隔开
