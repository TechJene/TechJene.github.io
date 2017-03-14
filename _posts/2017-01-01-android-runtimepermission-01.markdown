---
layout:     post
title:      "Android 运行时权限进阶"
subtitle:   " \"一次申请多个权限\""
date:       2017-01-01 22:34:00
author:     "TechJene"
header-img: "img/post-2016-csdn.jpg"
catalog: true
tags:
    - Android
    - 运行时权限
---
> "东城渐觉风光好。"

**说明**：原发布于 [CSDN 个人博客](http://blog.csdn.net/yaoyuandemeili/article/details/53968900)

- 学习平台：Android Studio 2.2.3 (基于win8.1 Pro)
- ADT：Nexus5
- API：24

### 前言

基于郭霖老师的《第一行代码》2th Edition的 7.2 节进行更改。  
**笔记名称：一次申请多个权限**

### 正文

#### 一、修改 MainActivity
1.新建一个 PermissionList

```
List<String> permissionList = new ArrayList<String>();
```

2.对需要申请的权限进行 if 判断  
按照郭老师讲解，以 CALL_PHONE 和 WRITE_EXTERNAL_STORAGE 为例

```
//2.对需要申请的权限进行if判断
if (ContextCompat.checkSelfPermission(MainActivity.this,
        Manifest.permission.CALL_PHONE) != PackageManager.PERMISSION_GRANTED){

    //如果未同意，则add进PermissionList
    permissionList.add(Manifest.permission.CALL_PHONE);
}
if (ContextCompat.checkSelfPermission(MainActivity.this,
        Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED){
    permissionList.add(Manifest.permission.WRITE_EXTERNAL_STORAGE);
}
                }
```
3.对 permissionList 进行判断

```
//3.对PermissionList进行判断
if (!permissionList.isEmpty()){
    /*进行权限申请，申请permissionList中的权限，permissionList为String，需要转换为String数组的参数格式。
    数组长度就是permissionList长度permissionList.size().
     */
    ActivityCompat.requestPermissions(MainActivity.this, permissionList.toArray(new String[permissionList.size()]), 1);
} else {
    //your own logical
    defineLogical();
}
```
如果 permissionList 为空，则说明权限都通过了，执行自定义逻辑即可。

```
private void defineLogical() {
    Toast.makeText(MainActivity.this, "所有权限申请通过", Toast.LENGTH_SHORT).show();
}
```
4.在 onRequestPermissionResult() 方法中处理用户回调

```
@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    switch (requestCode){
        case 1:
            //1>判断
            if (grantResults.length > 0){
                for (int grantResult : grantResults) {
                    if (grantResult != PackageManager.PERMISSION_GRANTED){
                        //此时至少有一个权限未被授权
                        Toast.makeText(MainActivity.this, "某个权限被拒绝了", Toast.LENGTH_SHORT).show();
                        return;
                    }
                }
                /*
                如果for循环成功执行完，即没有在中间被return掉，就说明所有权限都被同意了。
                此时就可以执行自己的逻辑了。
                 */
                defineLogical();
            }
            break;
        default:
            break;
    }
}
```

#### 二、在 AndroidManifest 中注册申请的权限

```
<uses-permission android:name="android.permission.CALL_PHONE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>

```

#### 三、运行截图
![这里写图片描述](http://img.blog.csdn.net/20170101221556174?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWWFveXVhbmRlbWVpbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 四、关于 WRITE_EXTERNAL_STORAGE

给大家推荐一本书《黑客大曝光：移动应用安全揭秘及防护措施》  
美国作者：伯格曼等人。机械工业出版社的。  
下面的观点来自此书。  
该书的4.11.2节，是关于Android系统通过外部存储的泄露。

> 任何文件若存储在可移动存储器之类的外部存储上，如SD卡或虚拟SD卡，则该文件相对于同一移动设备上的所有应用来说是全局可读和可写3的。
>
> 因此一个Android应用应该只在外部存储上存储该应用想共享的数据，以防止恶意应用获取敏感数据。

当然，郭老师所言也是一个原因。  

#### 五、无须申请权限的目录

郭老师还提到了第二种应用场景。  
我直接把Android Developers 官网内容拿过来
来源：[保存应用私有文件](https://developer.android.com/guide/topics/data/data-storage.html#AccessingExtFiles)

> 如果您正在处理的文件不适合其他应用使用（例如仅供您的应用使用的图形纹理或音效），则应该通过调用 getExternalFilesDir() 来使用外部存储上的私有存储目录。此方法还会采用 type 参数指定子目录的类型（例如 DIRECTORY_MOVIES）。 如果您不需要特定的媒体目录，请传递 null 以接收应用私有目录的根目录。
>
> 从 Android 4.4 开始，读取或写入应用私有目录中的文件不再需要 READ_EXTERNAL_STORAGE 或 WRITE_EXTERNAL_STORAGE 权限。

 以上是我个人对郭老师所讲内容的笔记。  

---------
> 愿你我都是有态度的人，相识于有温度的文字中。

最后，感谢阅读。
