---

copyright:
 years: 2015, 2016

---

#让 iOS 应用程序具有接收和发送 {{site.data.keyword.mobilepushshort}} 的能力 
{: #enable-push-ios-notifications}
上次更新时间：2016 年 10 月 19 日
{: .last-updated}

您可以让 iOS 应用程序具有对您的设备接收和发送 {{site.data.keyword.mobilepushshort}} 的能力。


##安装 CocoaPods 
{: #enable-push-ios-notifications-install}

对于现有 Xcode 项目，可以使用 CocoaPods 依赖关系管理工具来设置 Bluemix Mobile 服务客户机 SDK。替代方法是手动安装该 SDK。

要查看 Swift Push 自述文件，请转至[自述文件](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)。




1. 在 Mac 终端中，使用以下命令安装 CocoaPods：

```
$ sudo gem install cocoapods
```
	{: codeblock}
2. 在终端中输入 `pod init` 命令来初始化 CocoaPods。请确保从 Xcode 项目所在的目录运行命令。`pod init` 命令创建 Podfile。  
3. 在生成的 Podfile 中，添加所需的 SDK 依赖关系。基于您的首选项，复制以下任何一个 Podfile。
 
**Objective-C**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	pod 'IMFCore'
	pod 'IMFPush'
```
	{: codeblock}

**Swift**
   
```
source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!target 'MyApp' do
	    platform :ios, '9.0'
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


##Carthage
{: #carthage}

使用 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 将框架添加到项目中。请注意，Xcode8 中不支持 Carthage。

1. 将 `BMSPush` 框架添加到 Cartfile 中：
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. 运行 `carthage update` 命令。构建完成时，请将 `BMSPush.framework`、`BMSCore.framework` 和 `BMSAnalyticsAPI.framework` 拖动到 Xcode 项目中。
3. 遵循 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 站点上的指示信息以完成集成。


##使用导入的框架和源文件夹
{: using-imported-frameworks}

在代码中引用 SDK。基于您的首选项，使用以下任何一种方法。

**Objective-C**

针对相关头编写 `#import` 伪指令，例如：

```
	//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```
	{: codeblock}

**注**：使用 CocoaPods 命令 `pod install` 或 `pod update` 更新 Pods 项目可能覆盖 Bluemix Mobile 服务源文件夹。如果要保留原始文件的定制版本，请确保在发出其中某个命令之前已备份这些文件。

**Swift**

确保存在以下先决条件：

- iOS 8.0 或更高版本
- Xcode 7


针对相关头编写 `#import` 伪指令，例如：
```
//swift
import BMSCore
import BMSPush
```
	{: codeblock}
要查看 Swift Push 自述文件，请转至[自述文件](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)。
##构建设置
{: build-settings}

转至 **Xcode > 构建设置 > 构建选项**，然后将**启用位代码**设置为**否**。

**注意**：自 iOS 9 起，对应用程序传输安全性 (ATS) 功能的更改可能会影响您处理认证过程的方式。以下博客帖子描述了有关这些更改的更多信息：[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 和 [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)。

## 为 iOS 应用程序初始化推送 SDK
{: #enable-push-ios-notifications-initialize}

在 iOS 应用程序中，通常会将初始化代码放置在应用程序代表中。单击“推送”仪表板的**移动选项**链接，以获取应用程序路径和 GUID。

###初始化核心 SDK
{: Initializing-the-core-sdk}

**Objective-C**

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```
	{: codeblock}

**Swift**

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
myBMSClient.defaultRequestTimeout = 10.0 // Timeout in seconds
```
	{: codeblock}

### 路径、GUID 和 Bluemix 区域
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

指定分配给在 Bluemix 上创建的服务器应用程序的路径。

####GUID
{: ios-guid}

指定分配给在 Bluemix 上创建的应用程序的唯一键。此值区分大小写。

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

指定托管应用程序的位置。`bluemixRegion` 参数指定要使用的 Bluemix 部署。可以使用 `BMSClient.REGION` 静态属性设置此值，并使用以下三个值中的一个值：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

指定分配给在 Bluemix 上创建的 {{site.data.keyword.mobilepushshort}} 服务的唯一 AppGUID 键。

###初始化客户机推送 SDK
{: initializing-the-client-Push-SDK}

**Objective-C**

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
```
	{: codeblock}

**Swift**

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## 注册 iOS 应用程序和设备
{: #enable-push-ios-notifications-register}


应用程序必须向 APNs 进行注册，才能在安装到设备上之后接收远程通知。当应用程序收到 APNs 生成的设备令牌后，必须将该令牌传递回 {{site.data.keyword.mobilepushshort}} 服务。

要注册 iOS 应用程序和设备，您需要：

1. 创建后端应用程序。
2. 将令牌传递给 {{site.data.keyword.mobilepushshort}}。


###创建后端应用程序
{: create-a-backend-app}

在 Bluemix®“目录”的“样板”部分中创建后端应用程序，这会自动将该 {{site.data.keyword.mobilepushshort}} 服务绑定到此应用程序。如果已创建后端应用程序，请务必将该应用程序绑定到 {{site.data.keyword.mobilepushshort}} 服务。

**Objective-C**

```
//For Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```
	{: codeblock}

**Swift**

```
//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```
	{: codeblock}

###将令牌传递至 {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

从 APNs 收到令牌后，将令牌传递给 {{site.data.keyword.mobilepushshort}}（`registerWithDeviceToken` 方法的一部分）。

**Objective-C**

```
//For Objective-C
		-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{
     IMFClient *client = [IMFClient sharedInstance];
	[client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];
	// get Push instance
	IMFPushClient* push = [IMFPushClient sharedInstance];
	[push initializeWithAppGUID:@"appGUID"];
	[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
    if (error){
     NSLog(@"%@",error.description);
  }  else {
    NSLog(@"%@",response.responseJson.description);
}
}];
 }
```
	{: codeblock}

**Swift**

从 APNs 收到令牌后，将该令牌传递给 Push Notifications（作为 `didRegisterForRemoteNotificationsWithDeviceToken`
方法的一部分）。

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.initializeWithAppGUID("appGUID")
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


## 在 iOS 设备上接收推送通知
{: #enable-push-ios-notifications-receiving}

您可以使用以下任何一种方法，在 iOS 设备上接收推送通知。

**Objective-C**

要在 iOS 设备上接收推送通知，请将以下 Objective-C 方法添加到应用程序的应用程序代表中。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```
	{: codeblock}

**Swift**

要在 iOS 设备上接收推送通知，请将以下 Swift 方法添加到应用程序的应用程序代表中。
```
// For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
//UserInfo dictionary will contain data sent from the server
   }

```
	{: codeblock}

## 发送基本推送通知
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

### 发送通知的可选设置
{: #send_ios_otpional_setting}

您可以定制将通知发送至 IOS 设备的 {{site.data.keyword.mobilepushshort}} 设置。支持以下可选的定制选项。

- **角标**：指示在应用程序角标上显示的数字。缺省值为零 (0)，这样不会显示角标。 
- **声音**：指示在接收通知时播放声音片段。支持缺省值或应用程序中绑定的声音资源的名称。
- **其他有效内容**：为您的通知指定定制的有效内容值。


## 后续步骤
{: #next_steps_tags}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将这些 Push Notifications 服务功能添加到应用程序中。要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。要使用高级通知选项，请参阅[启用高级推送通知](t_advance_badge_sound_payload.html)。
