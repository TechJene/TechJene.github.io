---
layout:     post
title:      "实现 hint 浮动显示(二)"
subtitle:   " \"TextInputLayout 的使用步骤\""
date:       2016-12-17 20:39:00
author:     "TechJene"
header-img: "img/post-2016-csdn.jpg"
catalog: true
tags:
    - Android
    - hint  
    - TextInputLayout
---
> "今年春尽，杨花似雪，犹不见还家。"

**说明**：原发布于 [CSDN 个人博客](http://blog.csdn.net/yaoyuandemeili/article/details/53712450)

- 学习平台：Android Studio 2.2.3 (基于win8.1 Pro)
- ADT：Nexus5
- API：24
- 文章参考自：[Creating a Login Screen Using TextInputLayout](https://code.tutsplus.com/tutorials/creating-a-login-screen-using-textinputlayout--cms-24168)

### 正文

先上最终效果图：  
![这里写图片描述](http://img.blog.csdn.net/20161217201446004?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


接下来是步骤：

#### 1. 新建 TextInputLayoutDemo 项目
  New Project，主 activity：LoginActivity，  
  Layout 为 login_layout。

#### 2. 添加支持的 Library
  File-->Project Structure-->app--> 添加依赖库。
  com.android.support:design:25.0.1
  ![这里写图片描述](http://img.blog.csdn.net/20161217194119350?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


#### 3. 设计 Login 界面
  ![这里写图片描述](http://img.blog.csdn.net/20161217201611381?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)  
  显示一张图片和一个 Welcome，分别靠 ImageView 和 TextView 实现 。  
  两个 EditText，分别用于 Username 和 Password。  
  还有一个用于触发登陆的 Button。  
  下面是 login_layout.xml

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#e3e3e3"
    android:orientation="vertical"
    android:padding="@dimen/activity_horizontal_margin"
    tools:context=".LoginActivity">

    <ImageView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:src="@drawable/mylogo"/>

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="0.5"
        android:orientation="vertical">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:gravity="center"
            android:text="Welcome"
            android:textColor="#333333"
            android:textSize="30sp" />
    </RelativeLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_weight="0.5"
        android:orientation="vertical">

        <android.support.design.widget.TextInputLayout
            android:id="@+id/username_wrapper"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <EditText
                android:id="@+id/username"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="Username"
                android:inputType="textEmailAddress" />

        </android.support.design.widget.TextInputLayout>

        <android.support.design.widget.TextInputLayout
            android:id="@+id/password_wrapper"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/username_wrapper"
            android:layout_marginTop="4dp">

            <EditText
                android:id="@+id/password"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="Password"
                android:inputType="textPassword" />

        </android.support.design.widget.TextInputLayout>


        <Button
            android:id="@+id/button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="4dp"
            android:text="Login" />
    </LinearLayout>

</LinearLayout>

```
实际上，我做到这一步已经实现了 hint 的浮动显示，不过原文中还有一步，可能由于我使用的系统恰好可以，但是并非所有的系统到这一步就可以的。所以继续下一步。

#### 4.设置 Hints

首先，在 setContentView 方法下面初始化 TextInputLayout 视图引用。  
然后，使用 setHint 方法设置一个 hint。  
下面是代码：

```
   @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.login_layout);

        final TextInputLayout usernameWrapper = (TextInputLayout) findViewById(R.id.username_wrapper);
        final TextInputLayout passwordWrapper = (TextInputLayout) findViewById(R.id.password_wrapper);

        usernameWrapper.setHint("Username");
        passwordWrapper.setHint("Password");
    }
```
### 结语

至此，TextInputLayout实现hint 浮动显示就可以了。  
原文中还有关于条件验证的，我下一篇再继续。
谢谢！



---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
