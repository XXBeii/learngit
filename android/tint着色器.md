
https://www.cnblogs.com/punkisnotdead/p/5139372.html

https://mp.weixin.qq.com/s?__biz=MzAxMTI4MTkwNQ==&mid=2650820326&idx=1&sn=7f741d29f156af6db7c37623f9e8ca4c&mpshare=1&scene=23&srcid=0209FiTmrQBs0PJHPJsY7brf#rd


Tint 是 Android5.0 引入的一个属性，它可以在Android5.0 系统上，对视图进行颜色渲染。

作用：Tint的存在一定程度上减少了我们对图片的需求以及apk的大小；比如背景选择器



## 一、一张矢量图适配所有颜色  

### 方法一：xml：

#### 1、简单使用tint属性：

src属性 引用的是同一个 shape图形,第一个没有使用tint，第二个使用tint属性，减少资源文件创建

```java
	<ImageView
	 	android:id="@+id/image1"
        android:id="@+id/bottom_tabs_item_img"
        android:layout_width="wrap_content"
        android:src="@drawable/shape_radian_bg"
        android:layout_height="wrap_content"
        />

    <ImageView
        android:id="@+id/image2"
        android:layout_width="wrap_content"
        android:src="@drawable/shape_radian_bg"
        android:layout_height="wrap_content"
        android:tint="#f09"
        />
```
     当然src属性也可以使用图片资源如：对图片进行着色（矢量图）

#### 2、tint这个属性，是ImageView有的，它可以给ImageView的src设置，除了tint 之外，还有backgroundTint，foregroundTint，drawableTint,它们分别对应对背景、前景、drawable进行着色处理。

### 方法二：代码实现

```java
Drawable drawable = ContextCompat.getDrawable(this, R.mipmap.ic_launcher);
imageView.setImageDrawable(drawable);

Drawable.ConstantState state = drawable.getConstantState();
Drawable drawable1 = DrawableCompat.wrap(state == null ? drawable : state.newDrawable()).mutate();

drawable1.setBounds(0, 0, drawable.getIntrinsicWidth(), drawable.getIntrinsicHeight());
 DrawableCompat.setTint(drawable1,ContextCompat.getColor(this,R.color.colorAccent));

imageView1.setImageDrawable(drawable1);
```

DrawableCompat类：是Drawable的向下兼容类，我们为了在6.0一下兼容tint属性而使用的，有兴趣的看看源码哦，也是很简单的一个兼容类。

- wrap方法：使用tint就必须调用该方法对Drawable进行一次包装。
- mutate方法：（个人简单的理解就是类似于对象的深拷贝与浅拷贝），如果不调用该方法，我们进行操作的就是原drawable，着色之后原drawable也改变的，所有两个ImageView都会显示着色之后的drawable。调用mutate后会对ConstantState进行一次拷贝



二、一张图片实现 selector

