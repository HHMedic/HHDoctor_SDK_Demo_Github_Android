## 配置分享，用于【视频中邀请家人】、【邀请家人一起专家问诊】以及【分享家人】，sdk-3.6.4版本以及之后版本支持。

##### 【视频中邀请家人】：视频问诊中可点击邀请家人按钮分享卡片给微信好友，邀请微信好友共同问诊。

##### 【邀请家人一起专家问诊】：信息流中专家卡片可点击邀请家人分享卡片给微信好友，邀请微信好友共同与专家视频问诊

##### 【分享家人】：信息流更多页面中页面中分享家人功能，分享卡片给微信好友，好友可通过卡片进行视频问诊。

### 配置流程：

1.  配置sdk邀请文件，com.hh.share.HHWXMiniShareCard 继承 HHWXShareMiniCardApi，实现方法onShareToWXMiniProgram。（注意：com.hh.share.HHWXMiniShareCard为全路径类名）
   
3. 集成微信打开小程序[微信开发文档](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Launching_a_Mini_Program/Android_Development_example.html)

4. 在onShareToWXMiniProgram中调起小程序分享页。

   ​	

   ```
   @Override
   fun onShareToWXMiniProgram(context:Context, path:String,name:String) {
       
       val wxApi = WXAPIFactory.createWXAPI(context, KEY, false)
       val req = WXLaunchMiniProgram.Req()
       req.userName = name
       req.miniprogramType = WXLaunchMiniProgram.Req.MINIPTOGRAM_TYPE_RELEASE
       req.path = path
       wxApi?.sendReq(req)
   }
   ```

   

5. 混淆文件proguard-rules.pro中添加

   ```
   -keep class com.hh.share.HHWXMiniShareCard{*;}
   ```

   

   



