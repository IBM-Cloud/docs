---

copyright:
 years: 2015, 2016

---

#啟用 iOS 應用程式來接收及傳送 {{site.data.keyword.mobilepushshort}}
{: #enable-push-ios-notifications}
前次更新：2016 年 10 月 19 日
{: .last-updated}

您可讓 iOS 應用程式接收 {{site.data.keyword.mobilepushshort}}，並將其傳送至您的裝置。


##安裝 CocoaPods
{: #enable-push-ios-notifications-install}

針對現有的 Xcode 專案，您可以使用 CocoaPods 相依關係管理工具來設定 Bluemix Mobile Services Client SDK。替代方案是手動安裝 SDK。

若要檢視 Swift Push Readme 檔，請移至 [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)。



1. 在 Mac 終端機中，使用下列指令來安裝 CocoaPods。
```
$ sudo gem install cocoapods
```
	{: codeblock}
2. 在終端機中輸入 `pod init` 指令，以起始設定 CocoaPods。請確定您從 Xcode 專案所在的目錄執行指令。`pod init` 指令會建立 Podfile。  
3. 在產生的 Podfile 中，新增必要 SDK 相依關係。根據您的喜好設定，複製下列其中一個 Podfile。
 
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

3. 從終端機中，移至您的專案資料夾，並使用 `pod update` 指令來安裝相依關係。

此指令會安裝相依關係並建立新的 Xcode 工作區。  
**附註**：請確定您一律開啟新的 Xcode 工作區，而不是原始 Xcode 專案檔：
```
$ open App.xcworkspace
```
	{: codeblock}

工作區會包含原始專案以及包含相依關係的 Pods 專案。若要修改 Bluemix Mobile Services 來源資料夾，您可以在 Pods 專案的 `Pods/yourImportedSourceFolder` 下找到它，例如：`Pods/BMSPush`。

##Carthage
{: #carthage}

使用 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 新增專案架構。請注意，不支援 Xcode8 形式的 Carthage。

1. 在 Cartfile 中新增 `BMSPush` 架構：
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. 執行 `carthage update` 指令。建置完成時，請將 `BMSPush.framework`、`BMSCore.framework` 及 `BMSAnalyticsAPI.framework` 拖曳至 Xcode 專案。
3. 遵循 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 網站上的指示，以完成整合。


##使用匯入的架構和來源資料夾
{: using-imported-frameworks}

在您的程式碼中參照 SDK。根據您的喜好設定，使用下列一種方法。

**Objective-C**

撰寫相關標頭的 `#import` 指引，例如：

```
	//Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFPush/IMFPush.h>
```
	{: codeblock}

**附註**：使用 CocoaPods 指令 `pod install` 或 `pod update` 更新 Pods 專案時，可能會置換 Bluemix Mobile Services 來源資料夾。如果您要保留原始檔案的自訂版本，請確保先進行備份，然後再發出下列其中一個指令。

**Swift**

請確定已具備下列必備項目：

- iOS 8.0 或以上版本
- Xcode 7


撰寫相關標頭的 `#import` 指引，例如：
```
//swift
import BMSCore
import BMSPush
```
	{: codeblock}
若要檢視 Swift Push Readme 檔，請移至 [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)。

##建置設定
{: build-settings}

移至 **Xcode > 建置設定 > 建置選項，然後將啟用位元碼**設為**否**。

**注意**：自 iOS 9 開始，對「應用程式傳輸安全 (ATS)」特性進行的變更可能會影響您處理鑑別處理程序的方式。下列部落格文章說明這些變更的相關資訊：[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 及 [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)。

## 起始設定 Push SDK for iOS 應用程式
{: #enable-push-ios-notifications-initialize}

放置起始設定碼的一般位置位於 iOS 應用程式的應用程式委派中。按一下「Push 儀表板」中的**行動選項**鏈結，以取得應用程式路徑及 GUID。

###起始設定 Core SDK
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

### 路徑、GUID 及 Bluemix 地區
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

指定指派給您在 Bluemix 上所建立之伺服器應用程式的路徑。

####GUID
{: ios-guid}

指定指派給您在 Bluemix 上所建立之應用程式的唯一索引鍵。此值區分大小寫。

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

指定管理應用程式的位置。`bluemixRegion` 參數指定您所使用的 Bluemix 部署。您可以使用 `BMSClient.REGION` 靜態內容設定此值，然後使用下列三個值的其中一個：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

指定指派給您在 Bluemix 上所建立之 {{site.data.keyword.mobilepushshort}} Service 的唯一 AppGUID 索引鍵。

###起始設定 Client Push SDK
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


## 登錄 iOS 應用程式及裝置
{: #enable-push-ios-notifications-register}


在裝置上安裝應用程式之後，應用程式必須向 APNs 登錄才能接收遠端通知。在應用程式接收到 APNs 所產生的裝置記號之後，必須將裝置記號傳回給 {{site.data.keyword.mobilepushshort}} Service。

若要登錄 iOS 應用程式及裝置，您需要：

1. 建立後端應用程式。
2. 將記號傳遞至 {{site.data.keyword.mobilepushshort}}。


###建立後端應用程式
{: create-a-backend-app}

在 Bluemix® 型錄的「樣板」區段中建立後端應用程式，以自動將 {{site.data.keyword.mobilepushshort}} Service 連結至此應用程式。如果您已建立後端應用程式，請確定將應用程式連結至 {{site.data.keyword.mobilepushshort}} Service。

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
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```
	{: codeblock}

###將記號傳遞至 {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

從 APNs 接收到記號之後，將記號傳遞至 {{site.data.keyword.mobilepushshort}}，這是 `registerWithDeviceToken` 方法的一部分。

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
    }  else
		{
    NSLog(@"%@",response.responseJson.description);
		}
	}];
 }
```
	{: codeblock}

**Swift**

從 APNs 接收到記號之後，將記號傳遞至 Push Notifications，這是 `didRegisterForRemoteNotificationsWithDeviceToken` 方法的一部分。

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


## 在 iOS 裝置上接收推送通知
{: #enable-push-ios-notifications-receiving}

您可以使用下列一種方法，在 iOS 裝置上接收推送通知。

**Objective-C**

若要在 iOS 裝置上接收推送通知，請將下列 Objective-C 方法新增至應用程式的應用程式委派。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```
	{: codeblock}

**Swift**

若要在 iOS 裝置上接收推送通知，請將下列 Swift 方法新增至應用程式的應用程式委派。
```
// For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
//UserInfo dictionary will contain data sent from the server
    }
```
	{: codeblock}

## 傳送基本推送通知
{: #send}

開發應用程式之後，您可以傳送基本推送通知。

若要傳送基本推送通知，請完成下列步驟：

1. 選取**傳送通知**，然後選擇**傳送至**選項來編寫訊息。支援的選項是**依標籤的裝置**、**裝置 ID**、**使用者 ID**、**Android 裝置**、**iOS 裝置**、**Web 通知**及**所有裝置**。  
**附註**：當您選取**所有裝置**選項時，所有已訂閱 {{site.data.keyword.mobilepushshort}} 的裝置都會接收到通知。
![通知畫面](images/tag_notification.jpg)

2. 在**訊息**欄位中，編寫訊息。視需要選擇配置選用設定。
3. 按一下**傳送**。
3. 驗證您的裝置已接收到通知。

下列影像顯示處理 {{site.data.keyword.mobilepushshort}} iOS 裝置的警示框。

![iOS 上的前景推送通知](images/iOS_Screenshot.jpg) 

### 傳送通知的選用設定
{: #send_ios_otpional_setting}

您可以進一步自訂 {{site.data.keyword.mobilepushshort}} 設定，以將通知傳送給 iOS 裝置。支援下列選用自訂選項。


- **徽章**：指出應用程式徽章上所顯示的號碼。預設值是零 (0)，而且這不會顯示徽章。 
- **音效**：指出要在收到通知時播放的音效短片。支援預設值或應用程式中所組合的音效資源名稱。
- **其他有效負載**：指定通知的自訂有效負載值。


## 後續步驟
{: #next_steps_tags}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將這些 Push Notifications Service 特性新增至您的應用程式。若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。若要使用進階通知選項，請參閱[啟用進階推送通知](t_advance_badge_sound_payload.html)。
