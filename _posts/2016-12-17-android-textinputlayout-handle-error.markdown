---
layout:     post
title:      "TextInputLayout 处理错误"
subtitle:   " \"使用 TextInputLayout 条件验证\""
date:       2016-12-17 21:27:00
author:     "TechJene"
header-img: "img/post-2016-csdn.jpg"
catalog: true
tags:
    - Android
    - TextInputLayout
    - 译文
---
> "乾坤展清眺，万景若相借。"

**说明**：原发布于 [CSDN 个人博客](http://blog.csdn.net/yaoyuandemeili/article/details/53713826)

- 学习平台：Android Studio 2.2.3 (基于win8.1 Pro)
- ADT：Nexus5
- API：24
- 文章参考自：[Creating a Login Screen Using TextInputLayout](https://code.tutsplus.com/tutorials/creating-a-login-screen-using-textinputlayout--cms-24168)

### 第一步：实现 onClick 方法

1.定义 mButton
```
private Button mButton;
```
2.使用匿名类方式注册监听器
```
mButton = (Button)findViewById(R.id.button);

mButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {

}
```
3.在 onClick 方法中调用 hideKeyboard。  
因为使用 button 登陆，用户不再需要键盘，但是系统不会自动隐藏虚拟键盘。

```java
/**
 * 隐藏虚拟键盘
 */
private void hideKeyboard() {
        View view = getCurrentFocus();
        if (view != null) {
            ((InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE)).
                    hideSoftInputFromWindow(view.getWindowToken(), InputMethodManager.HIDE_NOT_ALWAYS);
        }
 }
```

### 第二步：输入信息验证
按照原文，假设 Username 是邮箱，则只需提醒用户是否输入有效邮箱地址。

需要依赖 Pattern 和 Matcher 两个类来验证字符串。  
注意是：  
java.util.regex.Matcher;和  
java.util.regex.Pattern;

```
private static final String EMAIL_PATERN = "^[a-zA-Z0-9#_~!$&'()*+,;=:.\"(),:;<>@\\[\\]\\\\]+@[a-zA-Z0-9-]+(\\.[a-zA-Z0-9-]+)*$";

private Pattern pattern = Pattern.compile(EMAIL_PATERN);

private Matcher matcher;
```
接下来就是验证邮箱的方法：

```
/**
 * 邮箱验证
 */
public boolean validateEmail(String email) {
     matcher = pattern.matcher(email);
     return matcher.matches();
}
```
然后验证 Password：  
简单起见，仍按照原文，以长度限制密码。

```
/**
* 密码长度限制
*/
public boolean validatePassword(String password) {
    return password.length() > 5;
}
```

### 第三步：获取数据
与 LinearLayout 和 ScrollView 不同，TextInputLayout 只是一个容器，可以使用 getEditText 方法获得子元素，不需要使用 findViewById。

```
String username = usernameWrapper.getEditText().getText().toString();
String password = passwordWrapper.getEditText().getText().toString();
```

### 第四步：错误显示
需要的方法是 setErrorEnabled 和 setError。

setError 用于错误消息提示，显示在EditText的下方。  
传入的参数为 null，错误消息将清空。并且它会使得整个 EditText 控件变为红色。

setErrorEnabled 开启错误提醒功能。  
这直接影响到布局的大小，增加底部padding为错误标签让出空间。

在 setError 设置错误消息之前开启这个功能意味着在显示错误的时候布局不会变化。



```
@Override
public void onClick(View view) {
    hideKeyboard();

    String username = usernameWrapper.getEditText().getText().toString();
    String password = passwordWrapper.getEditText().getText().toString();

    if (!validateEmail(username)) {
        usernameWrapper.setError("Not a valid address!");
    } else if (!validatePassword(password)) {
        passwordWrapper.setError("Not a valid password!");
    } else {
        usernameWrapper.setErrorEnabled(false);
        passwordWrapper.setErrorEnabled(false);
        Toast.makeText(getApplicationContext(), "登陆成功", Toast.LENGTH_SHORT).show();
    }
}
```
以上基本就是参考文章的简单翻译，我自己做一下学习记录。


---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
