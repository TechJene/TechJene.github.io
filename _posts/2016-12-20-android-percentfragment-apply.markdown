---
layout:     post
title:      "PercentFrameLayout Demo"
subtitle:   " \"Merry Christmas\""
date:       2016-12-20 18:24:00
author:     "TechJene"
header-img: "img/post-2016-csdn.jpg"
catalog: true
tags:
    - Android
    - PercentFrameLayout
---
> "独乐乐不如众乐乐。"

**说明**：原发布于 [CSDN 个人博客](http://blog.csdn.net/yaoyuandemeili/article/details/53766737)

- 学习平台：Android Studio 2.2.3 (基于win8.1 Pro)
- ADT：Nexus5
- API：24

### 前言

《第一行代码》2th Edition 的 3.3.4 节讲到了百分比布局，郭老师用的是 4 个 Button 控件，不够好玩。

我用 ImageView 控件做了个有意思的 Demo，还是先上效果图
![这里写图片描述](http://img.blog.csdn.net/20161220164809630?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

哈哈，是的，你没有看错，Merry Christmas！
提前祝各位圣诞快乐！

### 正文

主要用到了PercentFrameLayout。  
下面是步骤。

#### 第一步：新建项目 UILayoutDemo
New Project，主 Activity 和 Layout 默认即可。  
或者布局命名为 percent_frame_layout.

#### 第二步：添加支持的 Library
1. 打开 app/build.gradle 文件，在 dependencies 中添加 percent 支持。  
或者手动添加 Project Structure-->app-->dependencies。  
**compile 'com.android.support:percent:25.1.0'**

```
dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:25.1.0'
    compile 'com.android.support:percent:25.1.0'
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:design:25.1.0'
}
```
2.同步改变  
修改 gradle 文件后，Android Studio 会弹出 Sync Now 的提示，同步即可。

#### 第三步：修改布局代码

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.percent.PercentFrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:id="@+id/percent_img1"
        android:layout_gravity="left|top"
        android:src="@drawable/front_01"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%" />

    <ImageView
        android:id="@+id/percent_img2"
        android:layout_gravity="right|top"
        android:src="@drawable/front_02"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%" />

    <ImageView
        android:id="@+id/percent_img3"
        android:layout_gravity="right|bottom"
        android:src="@drawable/front_04"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%" />

    <ImageView
        android:id="@+id/percent_img4"
        android:layout_gravity="left|bottom"
        android:src="@drawable/front_03"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%" />

</android.support.percent.PercentFrameLayout>
```
代码很基础，大家应该能看明白。
具体的代码解释请参考郭霖老师的《第一行代码》第二版 3.3.4 节。

#### 第四步：修改主Activity
1. 定义 Image 按钮

```
private ImageView mImgButton1;
private ImageView mImgButton2;
private ImageView mImgButton3;
private ImageView mImgButton4;
```
2.通过 findViewById() 方法找到 ImageView 的实例

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.percent_frame_layout);

    mImgButton1 = (ImageView) findViewById(R.id.percent_img1);
    mImgButton1.setOnClickListener(this);

    mImgButton2 = (ImageView) findViewById(R.id.percent_img2);
    mImgButton2.setOnClickListener(this);

    mImgButton3 = (ImageView) findViewById(R.id.percent_img3);
    mImgButton3.setOnClickListener(this);

    mImgButton4 = (ImageView) findViewById(R.id.percent_img4);
    mImgButton4.setOnClickListener(this);

}
```
3.调用 setImageResource() 方法获取新的图片

```
@Override
public void onClick(View view) {
    switch (view.getId()){
        case R.id.percent_img1:
            mImgButton1.setImageResource(R.drawable.tree_01);
            break;
        case R.id.percent_img2:
            mImgButton2.setImageResource(R.drawable.tree_02);
            break;
        case R.id.percent_img3:
            mImgButton3.setImageResource(R.drawable.tree_04);
            break;
        case R.id.percent_img4:
            mImgButton4.setImageResource(R.drawable.tree_03);
            break;
        default:
            break;
    }
}
```
#### 第五步：运行 & enjoy
![这里写图片描述](http://img.blog.csdn.net/20161220172414171?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
说明：
 1. 夕阳图是我拍的学校的稷下湖；
 2. 圣诞快乐图来自free图片共享网站：[FREEIMAGES](http://cn.freeimages.com/)

### 结语
 好，就这些！
 送上这首圣诞快乐！  
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="286" height="52" src="//music.163.com/outchain/player?type=2&id=5388787&auto=0&height=32"></iframe>



---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
