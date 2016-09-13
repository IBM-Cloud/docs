---

copyright:
 years: 2015, 2016

---

# 起始設定 Push SDK for iOS 應用程式
{: #enable-push-ios-notifications-initialize}

放置起始設定碼的一般位置位於 iOS 應用程式的應用程式委派中。按一下「Bluemix 應用程式儀表板」中的**行動式選項**鏈結，以取得應用程式的路徑及應用程式 GUID。

##起始設定 Core SDK

###Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

##起始設定 Client Push SDK

###Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

## 路徑、GUID 及 Bluemix 地區

**appRoute**

指定指派給您在 Bluemix 上所建立之伺服器應用程式的路徑。

**GUID**

指定指派給您在 Bluemix 上所建立之應用程式的唯一索引鍵。此值區分大小寫。

**bluemixRegionSuffix**

指定管理應用程式的位置。```bluemixRegion``` 參數指定您要使用的 Bluemix 部署。您可以使用 ```BMSClient.REGION`` 靜態內容設定此值，然後使用下列三個值的其中一個：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
