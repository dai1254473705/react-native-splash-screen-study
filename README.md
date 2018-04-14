#react-native 启动页
-------
###git地址
> 插件 ：[react-native-splash-screen](https://github.com/crazycodeboy/react-native-splash-screen#getting-started)

###声明
> 在学习过程中，用react-native-splash-screen 3.0.6（学习这个插件默认安装的版本）和react-native（0.54.2 也是默认安装的版本）一直出问题，直到换成react-native@0.51.0、react-native-splash-screen@3.0.1后才顺利进行，当前只做的Android版本的，下面将简单说下使用步骤（网上到处都能搜到，再次仅当做个人学习笔记）

###Android：
####一、初始化react-native项目
```
react-native init testSplash --version 0.51.0
```
####二、安装react-native-splash-screen
```
npm i react-native-splash-screen@3.0.1 --save

react-native link react-native-splash-screen
```
####三、在创建的react-native项目testSplash的默认入口文件App.js中添加如下代码（具体看源文件）：
```
import SplashScreen from 'react-native-splash-screen';
```
```
componentDidMount() {
    SplashScreen.hide(); // 隐藏启动屏
}
```
####四、修改MainActivity.java文件
找到"android/app/src/main/java/com/testSplash/MainActivity.java",添加如下代码：

```
import android.os.Bundle; // 添加这一行
import com.facebook.react.ReactActivity;
import org.devio.rn.splashscreen.SplashScreen; // 添加这一行

public class MainActivity extends ReactActivity {
//添加下面这段代码，从这里开始
   @Override
    protected void onCreate(Bundle savedInstanceState) {
        SplashScreen.show(this);  // here
        super.onCreate(savedInstanceState);
    }
    //到这里结束
    // ...other code
}
```
####五、在 android/app/src/mian/res目录下创建layout文件夹，并在创建的layout文件夹中创建launch_screen.xml
内容如下：

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/launch_screen">
</LinearLayout>
```
####六、在 android/app/src/mian/res目录下创建drawable-xhdpi文件夹，并添加名为launch_screen.png的图片
+ res下面可以创建多个drawable-XXX的文件夹，用来适配不同分辨率的手机，也可以使用一个；

>可以有以下几种类型：
>
+ drawable-ldpi
+ drawable-mdpi
+ drawable-hdpi
+ drawable-xhdpi
+ drawable-xxhdpi
+ drawable-xxxhdpi

具体可以看项目

####七、解决白屏问题
> android/app/src/main/res/values/styles.xml中添加 <item name="android:windowIsTranslucent">true</item> 设置透明背景

```
<resources>

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
      <!-- Customize your theme here. -->
      <!--设置透明背景-->
      <item name="android:windowIsTranslucent">true</item>
    </style>

</resources>
```

####八、推荐一个项目
[https://github.com/duheng/Mozi](https://github.com/duheng/Mozi)