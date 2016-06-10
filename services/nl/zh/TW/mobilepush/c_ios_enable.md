---

copyright:
 years: 2015, 2016

---

# 讓 iOS 應用程式可接收推送通知
{: #enable-push-ios-notifications}

讓 iOS 應用程式可接收推送通知，以及將推送通知傳送給您的裝置。


##安裝 CocoaPods
{: #enable-push-ios-notifications-install}

若為現有的 Xcode 專案，您可以使用 CocoaPods 相依關係管理工具來設定 Bluemix Mobile Services Client SDK。替代方案是手動安裝 SDK。

**附註**：若要檢視 Swift Push Readme 檔，請移至 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master



1. 在 Mac 終端機中，使用下列指令來安裝 CocoaPods。
```
$ sudo gem install cocoapods
```
2. 在終端機中輸入下列指令，以起始設定 CocoaPods。發出此指令時，請確定是在 Xcode 專案所在的目錄中執行它。`pod init` 指令會建立檔案標題。
```
$ pod init
```
3. 在產生的 Podfile 中，新增您需要的 SDK 相依關係。請複製下列 Podfile。

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. 從「終端機」中，移至您的專案資料夾，並使用下列指令來安裝相依關係：
```
$ pod update
```
該指令會安裝相依關係並建立新的 Xcode 工作區。**附註**：請確定您一律開啟新的 Xcode 工作區，而不是原始 Xcode 專案檔：

	```
	$ open App.xcworkspace
	```
工作區會包含原始專案以及包含相依關係的 Pods 專案。如果您想要修改 Bluemix Mobile Services 來源資料夾，則可以在 Pods 專案的 `Pods/yourImportedSourceFolder` 下找到它，例如：`Pods/IMFGoogleAuthentication`。

##使用匯入的架構和來源資料夾

在您的程式碼中參照 SDK。


### Objective-C

撰寫相關標頭的 #import 指引，例如：

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**附註**：使用 CocoaPods 指令 `pod install` 或 `pod update` 更新 Pods 專案時，可能會置換 Bluemix Mobile Services 來源資料夾。如果您要保留原始檔案的自訂版本，請確保先進行備份，然後再發出下列其中一個指令。

###Swift

**先決條件**

- iOS 8.0 或以上版本
- Xcode 7


撰寫相關標頭的 #import 指引，例如：

```
//swift
import BMSCore
import BMSPush
```


##建置設定

移至 **Xcode > 建置設定 > 建置選項，然後將啟用位元碼**設為**否**。

**注意**：自 iOS 9 開始，對「應用程式傳輸安全 (ATS)」特性進行的變更可能會影響您處理鑑別處理程序的方式。下列部落格文章說明了這些變更的相關資訊：[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 及 [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## 起始設定 Push SDK for iOS 應用程式
{: #enable-push-ios-notifications-initialize}

放置起始設定碼的一般位置位於 iOS 應用程式的應用程式委派中。按一下「Bluemix 應用程式儀表板」中的**行動式選項**鏈結，以取得應用程式的路徑及應用程式 GUID。

###起始設定 Core SDK

####Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


###起始設定 Client Push SDK

####Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

####Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

### 路徑、GUID 及 Bluemix 地區

**appRoute**

指定指派給您在 Bluemix 上所建立之伺服器應用程式的路徑。

**GUID**

指定指派給您在 Bluemix 上所建立之應用程式的唯一索引鍵。此值區分大小寫。

**bluemixRegionSuffix**

指定管理應用程式的位置。```bluemixRegion``` 參數指定您要使用的 Bluemix 部署。您可以使用 ```BMSClient.REGION``` 靜態內容設定此值，然後使用下列三個值的其中一個：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




## 登錄 iOS 應用程式及裝置
{: #enable-push-ios-notifications-register}


應用程式必須向 APNs 登錄才能接收遠端通知，這通常發生在應用程式安裝到裝置上之後。在應用程式接收到 APNs 所產生的裝置記號之後，必須將裝置記號傳回給 Push Notifications Service。

若要登錄 iOS 應用程式及裝置，請執行下列動作：

1. 建立後端應用程式
2. 將記號傳遞至 Push Notifications


###建立後端應用程式

在 Bluemix® 型錄的「樣板」區段中建立後端應用程式，以自動將 Push 服務連結至此應用程式。如果您已建立後端應用程式，請確定將應用程式連結至 Push Notification Service。

####Objective-C

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

####Swift

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

###將記號傳遞至 Push Notifications

從 APNs 接收到記號之後，將記號傳遞至 Push Notifications，這是 ```registerDevice:withDeviceToken``` 方法的一部分。

####Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute: @"your-backend-route-here" backendGUID: @"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

####Swift

從 APNs 接收到記號之後，將記號傳遞至 Push Notifications，這是 ```didRegisterForRemoteNotificationsWithDeviceToken``` 方法的一部分。

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
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



## 在 iOS 裝置上接收推送通知
{: #enable-push-ios-notifications-receiving}

在 iOS 裝置上接收推送通知。

###Objective-C
若要在 iOS 裝置上接收推送通知，請將下列 Objective-C 方法新增至應用程式的應用程式委派。

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

###Swift
若要在 iOS 裝置上接收推送通知，請將下列 Swift 方法新增至應用程式的應用程式委派。

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }

```



## 傳送基本推送通知
{: #send}

開發應用程式之後，您可以傳送基本推送通知（不需要使用標籤、徽章、其他有效負載或音效檔）。


傳送基本推送通知。

1. 在**選擇對象**中，選取下列其中一個對象：**所有裝置**，或依平台：**僅限 IOS 裝置**或**僅限 Anroid 裝置**。

	**附註**：當您選取**所有裝置**選項時，所有已訂閱推送通知的裝置都會接收到您的通知。

	![通知畫面](images/tag_notification.jpg)

2. 在**建立您的通知**中，輸入您的訊息，然後按一下**傳送**。
3. 驗證您的裝置已接收到通知。

	下列擷取畫面顯示在 Android 及 iOS 裝置的前景中處理推送通知的警示框。

	![Android 上的前景推送通知](images/Android_Screenshot.jpg)

	![iOS 上的前景推送通知](images/iOS_Screenshot.jpg)

	下列擷取畫面顯示 Android 背景中的推送通知。
	![Android 上的背景推送通知](images/background.jpg)




## 後續步驟
{: #next_steps_tags}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將這些 Push Notifications Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。
若要使用進階通知選項，請參閱[進階推送通知](t_advance_notifications.html)。
