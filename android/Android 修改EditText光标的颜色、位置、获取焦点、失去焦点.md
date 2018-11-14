### 1、控制光标颜色

EditText有一个属性：textCursorDrawable，这个属性是用来控制光标颜色的。

例如：
```xml
android:textCursorDrawable="@null"
```
上面”@null”作用是让光标颜色和text color一样（默认的）。

如果想要修改一下光标的颜色和粗细：
先在资源文件drawable下，新建一个光标控制edit_cursor.xml文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
 
    <size android:width="1dp" />
 
    <solid android:color="#008000" />
 
</shape>

```
然后在EditText中添加属性：
```xml
android:textCursorDrawable="@drawable/edit_cursor"
```

### 2、修改光标位置

EditText 控件默认获取焦点的时候，插入光标是在第一个位置的，如果EditText中设置了文本，这个时候光标是在文本的最前面，而不是文本的最后。 

为了方便用户使用，需要把光标移动到文本最后，方便编辑。

此时用代码修改如下：
```java
EditText et = (EditText) findViewById(R.id.edit);
String text = "text";
et.setText(text);
et.setSelection(text.length());
```
注意：在调用setSelection方法时，如果里面的参数为0(即text.length长度为0时)会报错，请在使用前确认文本长度大于零。

### 3、EditText获得焦点

如果界面中含有多个EditText，在首次进入界面时，自动弹出软键盘，却不知道光标在何处。汗(⊙﹏⊙)

所以，最好呢在你想要编辑的第一个EditText中添加如下代码，用来获取焦点并且弹出软键盘：

```java
et.requestFocus();
et.setFocusable(true);
et.setFocusableInTouchMode(true);
InputMethodManager imm = (InputMethodManager) this
		.getSystemService(Context.INPUT_METHOD_SERVICE);
imm.showSoftInput(et, 0);
```
ok,此刻进入界面光标在你想要的位置，并且弹出了键盘，直接输入就可以编辑了呦。


### 4、EditText失去焦点
有些时候我们是不想让用户编辑我们的EditText的，此刻应该怎么办呢？一句代码解决：
```java
et.setEnabled(false);
```


