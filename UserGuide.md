标识：	                                                   
密级：
版本：V1.7


#  BizConfSDK使用说明书
Android

上海会畅通讯股份有限有限公司
二○一六年八月

##### 文档修改记录
| 版本号|修改内容描述					|修改人	|日期		  |备注	|
|------	|:-------------:		| -----:|		 |	|
|V1.0|新编						|Freeman|2016-08-23|	|
|V1.1|更改依赖关系					|Freeman|2016-10-19|	|
|V1.2|加会、起会添加cuid				|Freeman|2016-12-02|	|
|V1.3|添加会议结束通知，添加会前选项功能	|Freeman|2016-12-28|	|
|V1.4|SDK更新					|Freeman|2016-02-13|	|
|V1.5|添加https,添加友盟channelID			|Feeman|2016-03-07|	|
|V1.6|去除友盟，更换文字	         			|Freeman|2016-04-24|	|
|V1.6|更改域名                       			|Freeman|2017-05-27|	|
|v1.7|添加电话外呼接口              			|Freeman|2017-06-20|SDK版本1.2.0	||


### 目录
#### 第1章 简介
1.1 BizConf SDK
1.2 BizConf Video SDK for Android
1.3 用户须知
1.3.1 搭建项目环境要求
1.3.2 依赖库
#### 2.1 SDK Key
2.2 搭建项目
2.3 示例程序
#### 第3章 BizConfVideo SDK for Android-API使用
3.1 使用方法
3.2 接口说明
3.2.1 SDK初始化
3.2.2 开启会议
3.2.3 加入会议
3.2.4 注册结果
3.2.5 注册会议结束监听器
3.2.6 不自动打开摄像头
3.2.7 自动连接语音
3.3 添加自定义会议邀请
3.4 外呼参会人电话

## 第1章  简介
### 1.1 BizConf SDK
为了让应用更快捷的接入，现提供BizConf Video SDK为第三方提供可接入的API调用参数以保证验证、起会、参会等功能的可用性，开发者不需了解协议，只需要前台交互，以及将相关的参数修改成自身对应的参数即可使用。
BizConf Video SDK包含以下SDK：
*	BizConf SDK for Windows
*	BizConf SDK for iOS
*	BizConf SDK for Android
###  1.2 BizConf Video SDK for Android
BizConf Video SDK for Android，应用于移动设备应用开发，供用户开启会议、加入会议操作。
###  1.3 用户须知
#### 1.3.1 搭建项目环境要求
开发环境:AdnroidStudio
兼容性:Android 15以上


## 第2章  入门指南
### 2.1 SDK Key
使用SDK需要先申请Channel ID和SDK Key；
*	ChannelId:客户标识码
*	SDK Key:SDK认证密码
### 2.2 搭建项目
在工程的lib文件夹中加入aar文件
* bizconfcommonlib.aar
* bizconfsdk.aar
* bizconfvideosdk.aar
添加依赖关系
```css
dependencies {
    provided fileTree(include: ['*.jar'], dir: 'libs')
    compile(name: 'bizconfcommonlib', ext: 'aar')
    compile(name: 'bizconfsdk', ext: 'aar')
    compile(name: 'bizconfvideo', ext: 'aar')
    compile 'com.android.support:appcompat-v7:23.3.0'
    compile 'org.apache.directory.studio:org.apache.commons.lang:2.6'
    compile 'com.android.support:support-v4:23.3.0'
    compile 'com.google.code.gson:gson:2.8.0'
}
```

### 2.3 示例程序
根据参数说明在输入框填入方法参数即可使用接口功能.

## 第3章  BizConfVideo SDK for Android-API使用
### 3.1 使用举例

*	BizVideoService以Context作为参数调用getInstance(Context context)方法初始化BizVideoService
```java
  BizVideoService bizVideoService =
  BizVideoService.getInstance(Context context);
```
*	使用BizVideoService实例初始化sdk
```java
  bizVideoService.authSdk(String channelId,
                  String autoKey);
```
*	注册会议结束监听器、与SDK初始化监听器
```java
addMeetingFinishedListenerbizVideoService
(BizMeetingFinishedListener finishedlistener)
addSDKInitializeListener
(SDKInitializeListener InitializeListener);
```
*	调用BizVideoService实例的joinMeeting方法加入会议
```java
//获取SDK服务实例
BizVideoService bizVideoService = BizVideoService.getInstance(this);
//添加会议结束状态监听器
bizVideoService.addMeetingFinishedListener(this);
//添加SDK初始化状态变更监听器
bizVideoService.addSDKInitializeListener(this);
//SDK认证
bizVideoService.authSdk(channelId, autoKey);
//入会
bizVideoService.joinMeeting(userName, userNo, passWord, uid);
```


### 3.2 接口说明
#### 3.2.1 SDK初始化
初始化sdk方法
```java
authSdk (String channelId, String key)
```
参数说明:
**ChannelId**:客户标识码
**SDK Key**:SDK认证密码

#### 3.2.2 开启会议
```java
void startMeeting(String userId,
                  String userName,
                  String token,
                  String meetingNo，
                  String cuid)
```
参数说明:
**userId**:用户ID
**username**:用户名称
**meetingNo**:会议号码
**cuid**: cuid(非必填项目)
#### 3.2.3 加入会议
加入会议无密码
```java
void joinMeeting(String userName,
                  String meetingNo,
                  String uId，
                  String cuid)
```
参数说明:
**Username**:用户名称
**meetingNo**:会议号码
**uId**:参会人的身份标识(非必填)
**cuid**: cuid(非必填项目)

加入会议有密码
```java
void joinMeeting(String userName,
                  String meetingNo,
                  String password，
                  String uId，
                  String cuid)
```
参数说明:
**username**:用户名称
**meetingNo**:会议号码
**uId**: 参会人的身份标识(非必填)
**cuid**: cuid(非必填项目)


#### 3.2.4 注册结果

返回SDK是否认证成功,返回ture表示注册成功
```java
boolean isInitialized()
```

#### 3.2.5 注册会议结束监听器
```java
public void addMeetingFinishedListener(BizMeetingFinishedListener   
      bizMeetingFinishedListener)
```
参数说明:
**BizMeetingFinishedListener**:会议结束监听器，当会议结束时，BizMeetingFinishedListener的实例方法将会被回调。

#### 3.2.6 不自动打开摄像头
```java
public void setMeetingSettingCloseCamera(boolean meetingSettingCloseCamera)
```
参数说明:
**meetingSettingCloseCamera**：当参数为ture是选项打开
#### 3.2.7 自动连接语音
```java
public void setMeetingSettingConnectAudio(boolean meetingSettingConnectAudio)
```
参数说明:
**meetingSettingConnectAudio**：当参数为ture是选项打开

### 3.3 添加自定义会议邀请
自定义一个Activity，其intent-filter如下：
``` xml
        <activity android:name=".MyInviteActivity">
            <intent-filter>
                <action android:name=
      "meeting.confcloud.cn.bizaudiosdkdemo.intent.action.MeetingInvite" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
```
*这个action name为你的application package name加上“.intent.action.MeetingInvite”。*
你的Activity将会出现在邀请类型列表的顶端。
获取会议邀请数据：
在自定义的Activity中获取会议邀请的数据.
```java
Intent intent = getIntent();
Uri uri = intent.getData();
String subject = intent.getStringExtra(AndroidAppUtil.EXTRA_SUBJECT);
String text = intent.getStringExtra(AndroidAppUtil.EXTRA_TEXT);
```

### 3.4 外呼参会人电话
```java
/**
 * 电话呼叫联系人
 *
 * @param number   电话号码
 * @param username 用户名称
 * @param isCallMe 是否呼叫自己
 * @return 呼叫成功或失败
 */
public boolean dialOutUser(String number,
                            String username,
                            boolean isCallMe)
```
