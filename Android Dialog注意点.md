1，去掉dialog内容外的灰色阴影。

Dialog.getWindow().clearFlags( WindowManager.LayoutParams.FLAG_DIM_BEHIND);
注：如果你使用的api为14，那么还可以使用：
Dialog.getWindow().setDimAmount(0);


2，点击dialog内容外区域弹窗不消失。
在dialog.show()。之前调用dialog.setCanceledOnTouchOutside(false);

3,用Activity使用Dialog样式来实现。
我们可以自定义Dialog样式来实现不同的Dialog，但是很多情况下我们习惯直接用activity来实现不同样式的dialog，只要在清单文件中注册theme为Dialog即可，例如：
<activity
    android:name="com.example.androidtest.MyDialogActivity"
    android:theme="@android:style/Theme.Holo.Light.Dialog"> </activity>

在这种情况下实现点击Dialog周围空白处该Dialog不消失有两种方法：
方法一：
activity本身已经提供了setFinishOnTouchOutside()方法来实现功能。

MyDialogActivity.this.setFinishOnTouchOutside(false);
其中MyDialogActivity为用来实现Dialog样式的Activity的名字

方法二：
自定义style，让activity使用我们自定义的theme：
在res\values\styles.xml文件中定义自己的Dialog theme：
<resources>
    ……    <style  name = "MyDialogTheme" parent = "@android:style/Theme.Holo.Light.Dialog">
        <item name="android:windowCloseOnTouchOutside">false</item>
    </style>
    ……</resources>

 在AndroidManifest.xml文件中使自己的activity使用该theme：
 <activity
    android:name="com.example.androidtest.MyDialogActivity"
    android:theme="@style/MyDialogTheme" > </activity>

 即可实现点击Dialog外空白处Dialog不消失


 注意：
Android4.0以上AlertDialog，包括其他自定义的dialog，在触摸对话框边缘外部，对话框消失。
可以设置这么一条属性，当然必须先AlertDialog.Builder.create()之后才能调用这两个方法
方法一：
setCanceledOnTouchOutside(false);调用这个方法时，按对话框以外的地方不起作用。按返回键还起作用
方法二：
setCancelable(false);调用这个方法时，按对话框以外的地方不起作用。按返回键也不起作用
