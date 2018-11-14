
https://blog.csdn.net/asd199205/article/details/72841053

https://blog.csdn.net/honjane/article/details/78699002


android:inputType //设置文本的类型，用于帮助输入法显示合适的键盘类型
android:imeOptions //设置右下角IME动作与编辑框相关的动作，如actionDone右下角将显示一个“完成”，而不设置默认是一个回车符号.下面会详细说明.


我们在使用EditText中有时候会限制输入框中输入的文本类型,或者当弹出软键盘时,出现的是比较合适的输入法.如:我们在扣扣时,弹出的软件盘显示的就是数字,当输入密码时,右下角编辑框显示的是"完成",点击即会关闭软键盘.其实这也就是inputType和imeOptions属性来实现的,inputType属性可以指定键盘的类型,而imeOptions指定键盘右下角显示的Action.下面我们就来实现EditText使用过程中的小细节.

### 1.这个类似QQ登录输入框

第一个EditText(用户名)的inputType设置的是text,imeOptions设置的是actionNext(下一个).第二个EditText(密码)的inputType设置的是textPassword,imeOptions设置的是actionDone(完成).当输入完用户名,点击键盘action下一个,会跳到密码输入框,当输入完密码后,点击键盘action完成,软键盘就会隐藏.


```xml
 <EditText
     android:id="@+id/et_user_name"
     android:layout_width="match_parent"
     android:layout_height="wrap_content"
     android:hint="请输入用户名..."
     android:imeOptions="actionNext"
     android:inputType="text"
     android:textColor="@color/black" />
 
 <EditText
     android:id="@+id/et_password"
     android:layout_width="match_parent"
     android:layout_height="wrap_content"
     android:hint="请输入密码..."
     android:imeOptions="actionDone"
     android:inputType="textPassword"
     android:textColor="@color/black" />

```

#### 注意:这里需要注意的是,如果想让键盘显示Action,需要inputType和imeOptions结合使用才可以,只使用imeOptions是不会有效果的.只会显示默认的换行action.(不同手机的输入法不一样,可能显示的会有点小差别)

### 2.接下来我们看一下inputType可以接受的参数:

我们可以使用android：inputType属性指定要用于EditText对象的键盘类型.例如,如果你希望用户输入电子邮件地址，则应使用textEmailAddress输入类型.以下是输入类型常见的值:

值 | 含义 | 
----|------|
"text" |普通文本键盘
"textEmailAddress"| 带有@字符的普通文本键盘
"textUri" |带有/字符的普通文本键盘.
"number" |基本数字键盘.
"phone" |电话样式键盘.
"datetime" |时间日期.
"date" |日期.

android：inputType还允许指定某些键盘行为,例如是否大写所有新单词或使用自动完成和拼写建议等功能.以下是定义键盘行为的一些常见输入类型值:

值 | 含义 | 
----|------|
"textCapSentences" |普通的文本键盘,大写每个新句子的第一个字母.
"textCapWords" |大写每个单词的正常文本键盘.适合标题或人名.
"textAutoCorrect" |正常文本键盘,可纠正拼写错误的字词.
"textPassword" |这个就和设置password="true"是一样的效果.以原点的形式显示输入的文本.
"textMultiLine" |普通文本键盘,允许用户输入包含换行符的长字符串（回车符）.


### imeOptions参数
 当需要指定键盘action时,需要和inputType结合使用才会有效果,下面就来看下imeOptions可以接受的参数:

值 | 对应常量 | 含义 | 
----|---- |------|
actionUnspecified | EditorInfo.IME_ACTION_UNSPECIFIED | 未指定
actionNone  | EditorInfo.IME_ACTION_NONE | 没有动作
actionGo  | EditorInfo.IME_ACTION_GO | 去往
actionSearch | EditorInfo.IME_ACTION_SEARCH  | 搜索
actionSend | EditorInfo.IME_ACTION_SEND  | 发送
actionNext  | EditorInfo.IME_ACTION_NEXT | 下一个
actionDone  | EditorInfo.IME_ACTION_DONE | 完成
actionPrevious | EditorInfo.IME_ACTION_PREVIOUS | 上一个
flagNoFullscreen | EditorInfo.IME_FLAG_NO_FULLSCREEN | 请求IME输入法永远不要进入全屏模式 
flagNavigatePrevious | EditorInfo.IME_FLAG_NAVIGATE_PREVIOUS | 类似IME_FLAG_NAVIGATE_NEXT， 表明这里有后退导航可以关注的兴趣点
flagNavigateNext | EditorInfo.IME_FLAG_NAVIGATE_NEXT | 表明这里有前进导航可以关注的兴趣点，类似IME_ACTION_NEXT，不过允许IME输入多行且提供前进导航。 
flagNoExtractUi | EditorInfo.IME_FLAG_NO_EXTRACT_UI | 请求IME输入法不要显示额外的文本UI  
flagNoAccessoryAction | EditorInfo.IME_FLAG_NO_ACCESSORY_ACTION | 和一个Action结合使用表明在全屏输入法中不作为可访问性按钮  
flagNoEnterAction | EditorInfo.IME_FLAG_NO_ENTER_ACTION | 多行文本将自动设置了该标志位，执行Action时为换行效果，如果未设置，IME输入法将把Enter按钮自动替换为Action按钮  
flagForceAscii | EditorInfo.IME_FLAG_FORCE_ASCII | 请求IME输入法接受ASCII字符的输 



#### 在代码中通过editText.setOnEditorActionListener方法添加相应的监听，因为有些action是需要在代码中添加具体的相关操作的


```java
EditText editText = (EditText) contentView.findViewById(R.id.editText);
          editText.setOnEditorActionListener(new OnEditorActionListener() {
               @Override
               public boolean onEditorAction(TextView v, int actionId,
                         KeyEvent event) {
                    if (actionId == EditorInfo.IME_ACTION_SEARCH) {
                         Toast.makeText(getActivity(), "1111111",Toast.LENGTH_SHORT).show();
                    }
 
                    return false;
               }
          });
```




