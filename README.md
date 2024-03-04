## 和缓视频医生Android SDK对接文档 3.6.8（快速接入版本）

[和缓视频医生SDK音箱版本接入文档](HHDoctor_SDK_SOUND.md)

[和缓视频医生SDK电视版本接入文档](HHDoctor_SDK_TV.md)

### 一、引入SDK

```
在project的build.gradle文件中加入如下配置，由于SDK是做成了私有库所以必须加入此配置

repositories {
    
    maven { url 'https://jitpack.io' }
}

在app moudule的build.gradle文件中引用和缓视频医生SDK，如下：

implementation 'com.github.HHMedic:hh_medic_sdk_android:3.6.8'
```

### 二、 初始化SDK

```
HHSDKOptions options = new HHSDKOptions(sdkProductId); //productId由和缓分配的产品Id
options.dev = true; //修改这个参数来切换测试环境和正式环境，当设置为true的时候是测试环境，设置为false为生产环境
HHDoctor.init(getApplicationContext(), options);
```

### 三、登录登出

```

//登录
String userToken = "这个参数是服务器和和缓服务器对接后得到的用户userToken";
HHDoctor.login(this, userToken, new HHLoginListener() {
            @Override
            public void onSuccess() {
               //这里处理登录后的逻辑
            }

            @Override
            public void onError(String s) {
               //处理登录失败后的逻辑，一般不会发生
            }
        });
        
//登出
HHDoctor.logOut(this); //this指的是上下文Context
```

### 四、跳转首页（必须登录后）

```
HHDoctor.message(this); //this指的是上下文Context
```

**如果需要支持O2O购药，跳转首页的同时上传经纬度，方法如下：**
```
 Location.sendLocation(context, longitude, latitude);
```
以上方法参数说明：context是上下文， longitude和latitude分别是经纬度，使用 gcj02 国测局坐标系

### 五、详细文档

[详细接入文档](Document.md)

[TRTC版本接入图像旋转问题及解决方案整理](Rotation.md)

[分享家人、邀请家人问诊、邀请家人专家问诊配置文档](share.md)

**注意如果需要对APP瘦身一定保留引用和缓视频SDK后出现的pic_error_78219.png这张图片，这张图片有特殊用途，删除会造成SDK不可用。**
