---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为移动设备启用通知
{: #c_enable_push-notifications}
上次更新时间：2017 年 4 月 12 日
{: .last-updated}

请确保您已经完成[配置通知提供程序的凭证](t__main_push_config_provider.html)。

本部分描述了如何使您的客户机应用程序（移动、Web 浏览器应用程序以及 Chrome Apps and Extensions）能够接收推送通知，如何创建基本通知、获取和初始化SDK 或插件，以及如何注册您的设备或浏览器来接收推送通知。您还可以通过 [REST API](t_restapi.html) 使移动和 Web 浏览器应用程序能够接收推送通知。

**注**：对于设备、浏览器、Chrome Apps and Extensions 注册，{{site.data.keyword.mobilepushshort}} 服务会保持对通知提供者颁发的令牌的唯一引用。对于 Apple，通知提供者为 APNs；而对于 Google，则为 FCM。{{site.data.keyword.mobilepushshort}} 服务通知提供者可能会基于一些原因让令牌失效。 

例如，在设备上卸载应用程序期间。在这种情况下，如果有传递通知的尝试，通知提供者就会给出有关设备已失效的响应，{{site.data.keyword.mobilepushshort}} 服务会根据该响应来除去设备或 Web 浏览器注册。这样会抑制后续的尝试，阻止将通知发送给这些已失效的设备。


## 使 Android 应用程序能够接收推送通知
{: #tag_based_notifications}


您可以让 Android 应用程序具有向您的设备接收推送通知的能力。Android Studio 是必备软件，也是构建 Android 项目的建议方法。必须具有 Android Studio 的基本知识。

### 使用 Gradle 安装客户机推送 SDK
{: #android_install}

本部分描述如何安装和使用客户机推送 SDK 来进一步开发 Android 应用程序。

可以使用 [Gradle ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window} 来添加 {{site.data.keyword.Bluemix}} Mobile Services Push SDK，Gradle 会自动从存储库下载工件，并使其可供 Android 应用程序使用。确保正确设置了 [Android Studio ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.android.com/tools/studio/index.html) 和 Android Studio SDK。 

创建并打开移动应用程序后，使用 Android Studio 完成以下步骤。

1. 向模块级别 **build.gradle** 文件添加依赖关系。 	

	- 添加以下依赖关系会将 Bluemix™ Mobile 服务推送客户机 SDK 和 Google 播放服务 SDK 添加到编译作用域依赖关系中。
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- 添加以下依赖关系可以导入代码片段所需的语句。
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- 在结尾，向模块级别 **build.gradle** 文件添加以下依赖关系。
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. 向项目级别 **build.gradle** 文件添加以下依赖关系。
```
dependencies {
classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. 在 **AndroidManifest.xml** 文件中，添加以下许可权，要查看样本清单，请参阅 [Android helloPush 样本应用程序 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}。要查看样本 Gradle 清单，请参阅 [样本构建 Gradle 文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}。
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
在此处了解有关 [Android 许可权 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://developer.android.com/guide/topics/security/permissions.html){: new_window} 的信息。
4. 添加活动的通知意向设置。此设置会在用户单击通知区域中收到的通知时启动应用程序。
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```
	{: codeblock}
**注**：将上述操作中的 *Your_Android_Package_Name* 替换为应用程序中使用的应用程序包名称。

5. 针对 RECEIVE 和 REGISTRATION 事件通知，添加 Firebase 云消息传递 (FCM) 或 Google 云消息传递 (GCM) 意向服务和意向过滤器。
```
	<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
	</service>
<service
    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
    </intent-filter>
	</service>
```
    {: codeblock}

6. {{site.data.keyword.mobilepushshort}} 服务支持从通知区检索个别通知。对于从通知区访问的通知，系统仅会就单击的通知向您提供手柄。当正常打开应用程序时会显示所有通知。使用以下片段来更新 **AndroidManifest.xml** 文件，以使用此功能：

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

确保您已经完成[配置通知提供程序的凭证](t__main_push_config_provider.html)来设置 FCM 项目并获取凭证。使用 Firebase 云消息传递 (FCM) 控制台完成以下步骤。

1. 在 Firebase 控制台中，单击**项目设置**图标。![Firebase 项目设置](images/FCM_4.jpg)

3. 从您的应用程序窗格的“常规”选项卡中选择**添加应用程序**或**添加 Firebase 至您的 Android 应用程序图标**。![添加 Firebase 至 Android](images/FCM_5.jpg)

4. 在“添加 Firebase 至您的 Android 应用程序”窗口中，添加 **com.ibm.mobilefirstplatform.clientsdk.android.push** 作为程序包名。“应用程序昵称”字段为可选字段。单击**添加应用程序**。
![“添加 Firebase 至您的 Android”窗口](images/FCM_1.jpg)

5. 通过在“添加 Firebase 至您的 Android 应用程序”窗口中，输入应用程序的程序包名。“应用程序昵称”字段为可选字段。单击**添加应用程序**。
 

	![添加应用程序的程序包名](images/FCM_2.jpg)

6. 生成 `google-services.json` 文件。将 `google-services.json` 文件复制到 Android 应用程序模块根目录。请注意，`google-service.json` 文件包括添加的程序包名。

    ![添加 json 文件至应用程序根目录](images/FCM_7.jpg)

5. 在“添加 Firebase 至您的 Android 应用程序”窗口中，单击**继续**然后单击**完成**。 

  

构建并运行应用程序。

### 为 Android 应用程序初始化推送 SDK
{: #android_initialize}

在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中。SDK 有两个组件需要初始化。一个是核心 SDK，另一个是在核心 SDK 上构建的推送 SDK。

#### 初始化核心 SDK
{: #initz_core_sdk}

```
// Initialize the SDK for Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

指定托管应用程序的位置。可以使用以下三个值中的一个值：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### 初始化客户机推送 SDK
{: #initiz_client_pushSDK}

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

此为 {{site.data.keyword.mobilepushshort}} 服务的 AppGUID 键。此值区分大小写。打开 Push Notification 仪表板并选择“配置”选项卡。您可以从 Push Notification 服务仪表板上“配置”选项卡中的“移动选项”中获取此值。 

### 注册 Android 设备
{: #android_register}

使用 `MFPPush.register()` API 可向 {{site.data.keyword.mobilepushshort}} 服务注册设备。要注册 Android 设备，请在 Bluemix {{site.data.keyword.mobilepushshort}} 服务配置仪表板中添加 Firebase 云消息传递 (FCM) 信息。有关更多信息，请参阅[配置通知提供程序的凭证](t__main_push_config_provider.html)。

将以下代码片段复制到 Android 移动应用程序中。

```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
	    @Override
    	public void onSuccess(String response) {
    		//handle success here
	    }
	    @Override
    public void onFailure(MFPPushException ex) {
         //handle failure here
	    }
	});
```
	{: codeblock}


```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Handle Push Notification
	    }
	};
```
	{: codeblock}

### 在 Android 设备上接收推送通知
{: #android_receive}

1. 要向 Push Notifications 服务注册 notificationListener 对象，请使用 `MFPPush.listen()` 方法。此方法通常是通过处理推送通知的活动的 `onResume()` 和 `onPause` 方法进行调用的。
```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
	{: codeblock}
```
	@Override
protected void onPause() {super.onPause();
    if (push != null) {
        push.hold();
    }
}
```
	{: codeblock}

2. 构建项目，然后在设备或仿真器上运行该项目。在 register() 方法中针对响应侦听器调用 onSuccess() 方法时，这证实设备已成功注册 {{site.data.keyword.mobilepushshort}} 服务，现在可以发送推送通知。
3. 验证设备是否收到通知。如果应用程序在前台运行，那么通知将由 `MFPPushNotificationListener` 进行处理。如果应用程序在后台运行，那么通知栏中会显示一条消息。

### 在 Android 设备上监视推送通知
{: #android_monitor}

要监视应用程序中通知的当前状态，您可以实现 `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` 接口，并定义方法 onStatusChange(String messageId, MFPPushNotificationStatus status)。 

`messageId` 是从服务器发送的消息的标识。`MFPPushNotificationStatus` 将通知的状态定义为值：

- RECEIVED - 应用程序已接收通知。 
- QUEUED - 应用程序将通知排入队列，以用于调用通知侦听器。 
- OPENED - 用户通过单击托盘中的通知或从应用程序图标启动应用程序或当应用程序位于前台时，打开通知。 
- DISMISSED - 用户清除/关闭托盘中的通知。

您需要使用 MFPPush，来注册 `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` 类。

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
// Handle status change
}
});
```
    {: codeblock}


#### 侦听 DISMISSED 状态
{: #android_monitor_listen}

您可以选择在以下任何一个条件中，侦听 DISMISSED 状态：

- 当应用程序处于活动状态（在前台或后台运行）时

  添加以下片段到 `AndroidManifest.xml` 文件：

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
</intent-filter>
	</receiver>
```
	{: codeblock}

- 当应用程序处于活动状态（在前台或后台运行）和未在运行（已关闭）时

扩展 `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` 广播接收器并覆盖方法 `onReceive()`，其中 `MFPPushNotificationStatusListener` 应该在调用基类的方法 `onReceive()` 之前注册。

```
	public class MyDismissHandler extends MFPPushNotificationDismissHandler {
@Override
public void onReceive(Context context, Intent intent) {
MFPPush.getInstance().setNotificationStatusListener(new MFPPushNotificationStatusListener() {
@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
// Handle status change
}
});
super.onReceive(context, intent);
}
}
```
    {: codeblock}


添加以下片段到 `AndroidManifest.xml` 文件：

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
</intent-filter>
	</receiver>
```
    {: codeblock}

### 发送基本推送通知
{: #send-basic-notification}

开发应用程序后，可以发送基本推送通知。

要发送基本推送通知，请完成以下步骤：

1. 选择**发送通知**，并通过选择**发送至**选项编辑消息。支持的选项有**按标记列出设备**、**设备标识**、**用户标识**、**Android 设备**、**iOS 设备**、**Web 通知**和**所有设备**。
**注**：选择**所有设备**选项时，预订了 {{site.data.keyword.mobilepushshort}} 的所有设备都会收到通知。![“通知”屏幕](images/tag_notification.jpg)

2. 在**消息**字段中，编辑您的消息。根据需要，选择配置可选设置。
3. 单击**发送**。
3. 验证设备是否收到通知。

以下屏幕快照显示了在 Android 设备上前台处理推送通知的警报框。



![Android 上的前台推送通知](images/Android_Screenshot.jpg)

以下屏幕快照显示了 Android 后台的推送通知。


 ![Android 上的后台推送通知](images/background.jpg)

### 发送通知的可选 Android 设置
{: #send_otpional_setting}

对于向 Android 设备发送通知的 {{site.data.keyword.mobilepushshort}} 设置，您可以进一步定制。支持以下可选的定制选项：![Android 定制设置](images/android_custom_settings.jpg)

- 折叠键：折叠键附加在通知上。如果设备脱机时多个通知使用相同的折叠键按顺序抵达，那么将折叠通知。在设备联机时，将从 FCM/GCM 服务器接收通知，并只显示带有相同折叠键的最新通知。如果没有设置折叠键，将存储新和旧的消息，以在以后传递。
- 声音：指示在接收通知时播放声音片段。支持缺省值或应用程序中绑定的声音资源的名称。
- 图标：指定要针对通知显示的图标名称。请确保您已使用客户机应用程序，在 `res/drawable` 文件夹中包装了该图标。
- 优先级：指定将向消息分配传递优先级的选项。`high` 或 `max` 优先级将生成提醒通知，而 `low` 或 `default` 优先级的消息不会打开休眠设备上的网络连接。对于选项设置为 `min` 的消息，将发送静默通知。
- 可视性：您可以选择将通知可视性选项设置为 `public` 或 `private`。
`private` 选项限制公共查看，如果您的设备已通过锁定或模式保护，您可以选择启用该选项，通知设置将设置为**隐藏敏感的通知内容**。当可视性设置为 `private` 时，必须注意 `redact` 字段。仅 `redact` 字段中指定的内容会在设备的安全锁屏上显示。选择 `public` 时，通知可以自由阅读。
- 生存时间：此值以秒为单位进行设置。如果未指定此参数，FCM/GCM 服务器将把消息存储 4 周时间并将尝试传递。4 周后有效性到期。值可以为 0 至 2,419,200 秒之间的值。
- 空闲时延迟：将此值设置为 `true` 将指示 FCM/GCM 服务器在设备空闲时不要传递通知。将此值设置为 `false`，以确保在设备空闲时传递通知。
- 同步：通过将此选项设置为 `true`，将同步所有已注册设备的通知。如果某个用户名的用户在多个设备上安装了相同的应用程序，那么在一个设备上读取通知将确保删除其他设备上的通知。要使此选项生效，您需要确保已使用用户标识向 {{site.data.keyword.mobilepushshort}} 服务进行注册。
- 其他有效内容：为您的通知指定定制的有效内容值。


### 后续步骤
{: #next_steps_tag_based_notifications}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将这些推送通知服务功能添加到应用程序中。
要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。
要使用高级通知选项，请参阅[启用高级推送通知](t_advance_badge_sound_payload.html)。


## 使 Cordova 应用程序能够接收推送通知
{: #cordova_enable}


Cordova 是一种平台，用于通过 JavaScript、CSS 和 HTML 构建混合应用程序。{{site.data.keyword.mobilepushshort}} 服务支持开发基于 Cordova 的 iOS 和 Android 应用程序。

您可以让 Cordova 应用程序具有向您的设备接收推送通知的能力。

### 安装 Cordova 推送插件
{: #cordova_install}

安装并使用客户机推送插件来进一步开发 Cordova 应用程序。这还会安装 Cordova 核心插件，该插件会初始化与 Bluemix 的连接。

1. 下载最新版本的 Android Studio SDK 和 Xcode。
1. 设置仿真器。对于 Android Studio，请使用支持 Google Play API 的仿真器。
1. 安装 Git 命令行工具。对于 Windows，请确保选择**从 Windows 命令提示符运行 Git** 选项。有关如何下载和安装此工具的更多信息，请参阅 [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads){: new_window}。
1. 安装 Node.js 和 Node 软件包管理器 (NPM) 工具。NPM 命令行工具与 Node.js 捆绑在一起。有关如何下载和安装 Node.js 的更多信息，请参阅 [Node.js ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://nodejs.org/en/download/){: new_window}。
1. 在命令行中，使用 **npm install -g cordova** 命令来安装 Cordova 命令行工具。必须有该工具才能使用 Cordova 推送插件。有关如何安装 Cordova 并设置 Cordova 应用程序的更多信息，请参阅 [Cordova Apache ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cordova.apache.org/#getstarted){: new_window}。有关的更多信息，请参阅 Cordova 推送插件[自述文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}。
1. 切换到要在其中创建 Cordova 应用程序的文件夹，然后运行以下命令来创建 Cordova 应用程序。如果已有 Cordova 应用程序，请转至步骤 3。
```cordova create your_app_name
	cd your_app_name
	```
	{: codeblock}
- 可选：您可以编辑 **config.xml** 文件，然后将 <name> 元素中的应用程序名称更改为所选名称，而不使用缺省 HelloCordova 名称。

确保指定正确的捆绑软件标识。如果指定不正确的捆绑软件标识，那么以下错误消息可能会导致 Xcode。

* 对可执行文件进行签名的权利无效。
* 应用程序的“代码签名权利”文件中指定的权利与供应概要文件中指定的权利不同。要解决此问题，请在 Xcode 或 Cordova 应用程序 **config.xml** 文件中指定正确的捆绑软件标识。

1. 将支持的最低版本 API 或部署目标声明添加到 Cordova 应用程序的 config.xml 文件中。minSdkVersion 值必须高于 15。targetSdkVersion 值必须始终反映出 Google 上可用的最新版本 Android SDK。
	
	* Android - 使用编辑器，打开 **config.xml** 文件并使用最低 SDK 版本和目标 SDK 版本更新 `<platform name="android">` 元素：

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - 使用部署目标声明更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. 在 Cordova 命令行界面 (CLI) 中，使用以下命令添加 iOS 和/或 Android 平台：
```
cordova platform add ios
	cordova platform add android
	```
	{: codeblock}

1. 在 Cordova 应用程序根目录中，输入以下命令来安装 Cordova 推送插件：**cordova plugin add bms-push**。根据您所添加的平台，您可能会看到：
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. 在 your-app-root-folder 中，使用以下命令来验证 Cordova 核心和推送插件是否成功安装：**cordova plugin list**。根据您所添加的平台，您可能会看到：
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. 配置 iOS 开发环境。
2. 使用 Xcode 构建并运行应用程序。
1. 下载 Android 的 Firebase `google-services.json`，并将它们放在 Cordova 项目的根文件夹的 `[your-app-name]/platforms/android 中。
	1. 转至 `[your-app-name]/platforms/android`。
	2. 打开文件 `build.gradle`（路径：平台 > android > build.gradle）。
	3. 在 `build.gradle` 文件中查找 `buildscript` 文本。
	4. 在 classpath 行之后，添加一行 classpath 'com.google.gms:google-services:3.0.0'
	5. 然后查找“dependencies”。选择具有文本 `compile` 且依赖关系结束处的依赖关系，在那之后，添加此行：apply plugin: 'com.google.gms.google-services'。
	6. 准备并构建 Cordova Android 项目。
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**注**：在 Android Studio 中打开项目之前，先通过 Cordova CLI 构建 Cordova 应用程序。这将帮助您避免构建错误。
### 初始化 Cordova 插件
{: #cordova_initialize}

开始使用 {{site.data.keyword.mobilepushshort}} 服务 Cordova 插件之前，需要通过传递应用程序路径和应用程序 GUID 对其进行初始化。初始化该插件后，可以连接到在 Bluemix“仪表板”中创建的服务器应用程序。 Cordova 插件是 Android 和 iOS 客户机 SDK 的包装程序，可以使 Cordova 应用程序能够与 Bluemix 服务进行通信。

1. 通过将以下代码片段复制并粘贴到主 JavaScript 文件（通常位于 **www/js** 目录下）中来初始化 BMSClient。

```
onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

为应用程序传入区域。提供以下常量：

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

例如：

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**注**：如果是使用 Cordova CLI（例如，Cordova create app-name 命令）创建的 Cordova 应用程序，请将此 JavaScript 代码放入 index.js 文件内 onDeviceReady: function() 函数中的 app.receivedEvent 函数之后，以初始化 `BMSClient`。 


### 注册设备
{: #cordova_register}


要向 {{site.data.keyword.mobilepushshort}} 服务注册设备，请调用 register 方法。将以下代码片段复制到 Cordova 应用程序中，以注册设备。

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

以下 JavaScript 代码片段显示如何初始化 Bluemix Mobile Services 客户机 SDK，向 {{site.data.keyword.mobilepushshort}} 服务注册设备以及侦听推送通知。将此代码放入 JavaScript 文件中。

在 **onDeviceReady: function()** 中。

```
onDeviceReady: function() {
     app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

将以下 Swift 代码片段添加到应用程序代表类中。

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

### 后续步骤
{: #cordova_register_next}

使用以下命令构建项目，然后运行项目：

#### Android
{: #android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: #ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

### 在设备上接收推送通知
{: #cordova_receive}

复制以下代码片段，以在设备上接收推送通知。

#### JavaScript
{: #jvscrpt}

将以下 JavaScript 代码片段添加到 Cordova 应用程序的 Web 部分中。
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Android 通知属性
{: #And_notif}

以下部分列出了 Android 通知属性：

* **message** - 推送通知消息
* **payload** - 包含通知有效内容的 JSON 对象


#### iOS 通知属性
{: #ios_notif}

以下部分列出了 iOS 通知属性：

* **message** - 推送通知消息
* **payload** - 包含通知有效内容的 JSON 对象 action-loc-key - 此字符串用作键以从当前本地化版本中获取本地化字符串，用于适当按钮标题，而不是 `View`。
* **badge** - 要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。
* **sound** - 应用程序捆绑包中或应用程序数据容器的 Library/Sounds 文件夹中声音文件的名称。


将以下 Swift 代码片段添加到应用程序代表类中。
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

### 发送基本推送通知
{: #push-send-notifications}

开发应用程序后，可以发送基本推送通知。

要发送基本推送通知，请完成以下步骤：

1. 选择**发送通知**，并通过选择**发送至**选项编辑消息。支持的选项有**按标记列出设备**、**设备标识**、**用户标识**、**Android 设备**、**iOS 设备**、**Web 通知**和**所有设备**。
**注**：选择**所有设备**选项时，预订了 {{site.data.keyword.mobilepushshort}} 的所有设备都会收到通知。![“通知”屏幕](images/tag_notification.jpg)

2. 在**消息**字段中，编辑您的消息。根据需要，选择配置可选设置。
3. 单击**发送**。
3. 验证设备是否收到通知。

以下屏幕快照显示了在 Android 和 iOS 设备上前台处理 {{site.data.keyword.mobilepushshort}} 的警报框。


![Android 上的前台推送通知](images/Android_Screenshot.jpg)

![iOS 上的前台推送通知](images/iOS_Screenshot.jpg)

   下图显示 Android 上的后台 {{site.data.keyword.mobilepushshort}}。
 ![Android 上的后台推送通知](images/background.jpg)

#### 后续步骤
{: #next_steps_basic_notifications}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将 {{site.data.keyword.mobilepushshort}} 服务功能添加到应用程序中。
要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。
要使用高级通知选项，请参阅[启用高级推送通知](t_advance_badge_sound_payload.html)。


## 使 iOS 应用程序能够发送推送通知
{: #enable-push-ios-notifications}

您可以让 iOS 应用程序具有对您的设备发送 {{site.data.keyword.mobilepushshort}} 的能力。


### 安装 CocoaPods 
{: #enable-push-ios-notifications-install}

对于现有 Xcode 项目，可以使用 CocoaPods 依赖关系管理工具来设置 Bluemix Mobile 服务客户机 SDK。替代方法是手动安装该 SDK。

要查看 Swift Push 自述文件，请转至[自述文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}。



1. 在 Mac 终端中，使用以下命令安装 CocoaPods：

	```
		$ sudo gem install cocoapods
```
	{: codeblock}
2. 在终端中输入 `pod init` 命令来初始化 CocoaPods。请确保从 Xcode 项目所在的目录运行命令。`pod init` 命令创建 Podfile。  
3. 在生成的 Podfile 中，添加所需的 SDK 依赖关系。复制以下 Podfile。
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!
	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. 在终端中，转至项目文件夹，然后使用 `pod update` 命令安装依赖关系。

该命令会安装依赖关系并创建新的 Xcode 工作空间。  
**注**：确保始终打开新的 Xcode 工作空间，而不是原始 Xcode 项目文件：
```
$ open App.xcworkspace
	```
	{: codeblock}

该工作空间包含原始项目，以及包含依赖关系的 Pods 项目。要修改 Bluemix 移动服务源文件夹，您可以在 Pods 项目的 `Pods/yourImportedSourceFolder` 下找到该文件夹，例如：`Pods/BMSPush`。


### 使用 Carthage 添加框架
{: #carthage}

使用 [Carthage ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}，向项目添加框架。请注意，Xcode8 中不支持 Carthage。

1. 将 `BMSPush` 框架添加到 Cartfile 中：
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. 运行 `carthage update` 命令。构建完成时，请将 `BMSPush.framework`、`BMSCore.framework` 和 `BMSAnalyticsAPI.framework` 拖动到 Xcode 项目中。
3. 遵循 [Carthage ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} 站点上的指示，完成集成。

### 设置 iOS SDK
{: #ios-sdk}

设置 iOS SDK，将以下代码添加到应用程序的 **AppDelegate.swift** 文件中。请注意，这也会向 APNs 进行注册。  
```
func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### 使用导入的框架和源文件夹
{: #using-imported-frameworks}

在代码中引用 SDK。确保满足以下先决条件。

- iOS 8.0 或更高版本	
- Xcode 7

针对相关头编写 `#import` 伪指令，例如：
```
	 //swift
import BMSCore
import BMSPush
```
		{: codeblock}

要阅读 Swift Push 自述文件，请参阅[自述文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}。

**注**：使用 CocoaPods 命令 `pod install` 或 `pod update` 更新 Pods 项目可能覆盖 Bluemix Mobile 服务源文件夹。如果要保留原始文件的定制版本，请确保在发出其中某个命令之前已备份这些文件。


### 构建设置
{: #build-settings}

转至 **Xcode > 构建设置 > 构建选项**，然后将**启用位代码**设置为**否**。

**注意**：自 iOS 9 起，对应用程序传输安全性 (ATS) 功能的更改可能会影响您处理认证过程的方式。以下博客帖子描述相关更改的更多信息：[iOS 9 中的 ATS 和 Bitcode ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} 和[立即将 iOS 9 应用程序连接到 Bluemix![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}。

### 为 iOS 应用程序初始化推送 SDK
{: #enable-push-ios-notifications-initialize}

在 iOS 应用程序中，通常会将初始化代码放置在应用程序代表中。单击“推送”仪表板的**移动选项**链接，以获取应用程序路径和 GUID。

#### 初始化核心 SDK
{: #Initializing-the-core-sdk}

要使用 IBM Bluemix GUID 初始化 Swift 的核心 SDK，请使用以下代码片段。
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### 路径、GUID 和 Bluemix 区域
{: #route-guid-bluemix-region}


- **appRoute**：指定分配给在 Bluemix 上创建的服务器应用程序的路径。


- **GUID**：指定分配给在 Bluemix 上创建的应用程序的唯一键。此值区分大小写。


- **bluemixRegionSuffix**：指定托管应用程序的位置。`bluemixRegion` 参数指定要使用的 Bluemix 部署。可以使用 `BMSClient.REGION` 静态属性设置此值，并使用以下三个值中的一个值：

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID**：指定分配给在 Bluemix 上创建的 {{site.data.keyword.mobilepushshort}} 服务的唯一 AppGUID 键。

#### 初始化客户机推送 SDK
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### 注册 iOS 应用程序和设备
{: #enable-push-ios-notifications-register}

应用程序必须向 APNs 进行注册，才能在安装到设备上之后接收远程通知。当应用程序收到 APNs 生成的设备令牌后，必须将该令牌传递回 {{site.data.keyword.mobilepushshort}} 服务。

要注册 iOS 应用程序和设备，您需要：

1. 创建后端应用程序。
2. 将令牌传递给 {{site.data.keyword.mobilepushshort}}。


#### 创建后端应用程序
{: #create-a-backend-app}

在 Bluemix®“目录”的“样板”部分中创建后端应用程序，这会自动将该 {{site.data.keyword.mobilepushshort}} 服务绑定到此应用程序。如果已创建后端应用程序，请务必将该应用程序绑定到 {{site.data.keyword.mobilepushshort}} 服务。


#### 将令牌传递给 Push Notifications
{: #pass-token-push-notifications}

从 APNs 收到令牌后，将令牌传递给 {{site.data.keyword.mobilepushshort}}（`registerWithDeviceToken` 方法的一部分）。

```
func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }
  }
```
	{: codeblock}


### 在 iOS 设备上接收推送通知
{: #enable-push-ios-notifications-receiving}

要在 iOS 设备上接收推送通知，请将以下 Swift 方法添加到应用程序的应用程序代表中。

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### 在 iOS 设备上监视推送通知
{: #ios-monitoring}


可以监视已发送的推送通知的计数和当前状态。要启用监视，请基于事件将以下任一 Swift 方法添加到应用程序的应用程序代表。



- 通过单击通知打开应用程序时发送通知状态。
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) { 					let push =  BMSPushClient.sharedInstance
				let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		    	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
    		  print("Send message status to the Push server")
    	 }
		}
	```
			{: codeblock}



- 应用程序处于后台方式时发送通知状态
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
	 	 	let push =  BMSPushClient.sharedInstance
			let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
	}
	}
	```
			{: codeblock}


### 发送基本推送通知
{: #send}

开发应用程序后，可以发送基本推送通知。

要发送基本推送通知，请完成以下步骤：

1. 选择**发送通知**，并通过选择**发送至**选项编辑消息。支持的选项有**按标记列出设备**、**设备标识**、**用户标识**、**Android 设备**、**iOS 设备**、**Web 通知**和**所有设备**。
  
**注**：选择**所有设备**选项时，预订了 {{site.data.keyword.mobilepushshort}} 的所有设备都会收到通知。![“通知”屏幕](images/tag_notification.jpg)

2. 在**消息**字段中，编辑您的消息。根据需要，选择配置可选设置。
3. 单击**发送**。
3. 验证设备是否收到通知。

下图显示在 iOS 设备上处理 {{site.data.keyword.mobilepushshort}} 的警报框。

![iOS 上的前台推送通知](images/iOS_Screenshot.jpg) 

#### 发送通知的可选设置
{: #send_ios_otpional_setting}

您可以定制将通知发送至 IOS 设备的 {{site.data.keyword.mobilepushshort}} 设置。支持以下可选的定制选项。

- **角标**：指示在应用程序角标上显示的数字。缺省值为零 (0)，这样不会显示角标。 
- **声音**：指示在接收通知时播放声音片段。支持缺省值或应用程序中绑定的声音资源的名称。
- **其他有效内容**：为您的通知指定定制的有效内容值。

### 启用交互式通知
{: #enb_snd_ios_otpional}

现在，您可以通过启用交互式通知，利用更多详细信息来补充 iOS 通知，如添加图像、地图或响应按钮。这样做可为客户提供更多背景信息，同时可让客户立即采取操作而无需离开当前环境。  

要启用交互式通知，请使用以下代码：



- 定义按钮操作
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
		{: codeblock}


- 定义按钮的类别
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- 更新注册以包含按钮
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

要发送交互式通知，请完成以下步骤：

1. 在“编写”部分中，对于“发送至”下拉列表，选择 **iOS 设备**。
2. 输入您要发送的通知消息。
3. 在“可选设置”部分中，选择**移动**并单击 **iOS**。
4. 在“类型”下拉列表中，选择**混合**。
5. 在“类别”字段中，指定您在应用程序中定义的通知类型。 

![针对 iOS 的交互式通知](images/push_ios_notification_interactive.jpg) 

#### 后续步骤
{: #next_steps_02}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将这些 Push Notifications 服务功能添加到应用程序中。
要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。
要使用高级通知选项，请参阅[启用高级推送通知](t_advance_badge_sound_payload.html)。
