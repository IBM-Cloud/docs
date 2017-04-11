---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#让 iOS 应用程序具有发送 {{site.data.keyword.mobilepushshort}} 的能力
{: #enable-push-ios-notifications}
上次更新时间：2017 年 2 月 14 日
{: .last-updated}

您可以让 iOS 应用程序具有对您的设备发送 {{site.data.keyword.mobilepushshort}} 的能力。


##安装 CocoaPods 
{: #enable-push-ios-notifications-install}

对于现有 Xcode 项目，可以使用 CocoaPods 依赖关系管理工具来设置 Bluemix Mobile 服务客户机 SDK。替代方法是手动安装该 SDK。

要查看 Swift Push 自述文件，请转至[自述文件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}。



1. 在 Mac 终端中，使用以下命令安装 CocoaPods：

```$ sudo gem install cocoapods
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


##使用 Carthage 添加框架
{: #carthage}

使用 [Carthage ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}，向项目添加框架。请注意，Xcode8 中不支持 Carthage。

1. 将 `BMSPush` 框架添加到 Cartfile 中：
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. 运行 `carthage update` 命令。构建完成时，请将 `BMSPush.framework`、`BMSCore.framework` 和 `BMSAnalyticsAPI.framework` 拖动到 Xcode 项目中。
3. 遵循 [Carthage ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} 站点上的指示，完成集成。

##设置 iOS SDK
{: ios-sdk}

设置 iOS SDK，将以下代码添加到应用程序的 **AppDelegate.swift** 文件中。请注意，这也会向 APN 进行注册。  
```
func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##使用导入的框架和源文件夹
{: using-imported-frameworks}

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


##构建设置
{: build-settings}

转至 **Xcode > 构建设置 > 构建选项**，然后将**启用位代码**设置为**否**。

**注意**：自 iOS 9 起，对应用程序传输安全性 (ATS) 功能的更改可能会影响您处理认证过程的方式。以下博客帖子描述相关更改的更多信息：[iOS 9 中的 ATS 和 Bitcode ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} 和[立即将 iOS 9 应用程序连接到 Bluemix![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}。

## 为 iOS 应用程序初始化推送 SDK
{: #enable-push-ios-notifications-initialize}

在 iOS 应用程序中，通常会将初始化代码放置在应用程序代表中。单击“推送”仪表板的**移动选项**链接，以获取应用程序路径和 GUID。

###初始化核心 SDK
{: Initializing-the-core-sdk}


```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
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

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

指定分配给在 Bluemix 上创建的 {{site.data.keyword.mobilepushshort}} 服务的唯一 AppGUID 键。

###初始化客户机推送 SDK
{: initializing-the-client-Push-SDK}

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


###将令牌传递至 {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

从 APNs 收到令牌后，将令牌传递给 {{site.data.keyword.mobilepushshort}}（`registerWithDeviceToken` 方法的一部分）。

从 APNs 收到令牌后，将该令牌传递给 Push Notifications（作为 `didRegisterForRemoteNotificationsWithDeviceToken`
方法的一部分）。

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


## 在 iOS 设备上接收推送通知
{: #enable-push-ios-notifications-receiving}


要在 iOS 设备上接收推送通知，请将以下 Swift 方法添加到应用程序的应用程序代表中。

```
// For Swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
{ //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

## 在 iOS 设备上监视推送通知
{: ios-monitoring}

要监视通知的当前状态，请将以下 Swift 方法添加到应用程序的应用程序代表中。

```
	// Send notification status when app is opened by clicking the notifications
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 let push =  BMSPushClient.sharedInstance
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

```
	// Send notification status when the app is in background mode.
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 self.showAlert(title: "Recieved Push notifications", message: payLoad)
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

##启用交互式通知

现在，您可以通过启用交互式通知，利用更多详细信息来补充 iOS 通知，如添加图像、地图或响应按钮。这样做可为客户提供更多背景信息，同时可让客户立即采取操作而无需离开当前环境。  

要启用交互式通知，请使用以下代码：

```
	// This defines the button action.
let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
	// This defines category for the buttons
let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
	// This updates the registration to include the buttonsPass the defined category into iOS BMSPushClientOptions
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

## 后续步骤
{: #next_steps_tags}

成功设置基本通知后，可以配置基于标记的通知和高级选项。

将这些 Push Notifications 服务功能添加到应用程序中。
要使用基于标记的通知，请参阅[基于标记的通知](c_tag_basednotifications.html)。
要使用高级通知选项，请参阅[启用高级推送通知](t_advance_badge_sound_payload.html)。
