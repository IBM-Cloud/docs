---

copyright:
 years: 2015, 2016

---

# 为 iOS 应用程序初始化推送 SDK
{: #enable-push-ios-notifications-initialize}

在 iOS 应用程序中，通常会将初始化代码放置在应用程序代表中。单击 Bluemix 应用程序仪表板中的**移动选项**链接，以获取应用程序路径和 GUID。

##初始化核心 SDK

###Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstancemyBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

##初始化客户机推送 SDK

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

## 路径、GUID 和 Bluemix 区域

**appRoute**

指定分配给在 Bluemix 上创建的服务器应用程序的路径。

**GUID**

指定分配给在 Bluemix 上创建的应用程序的唯一键。此值区分大小写。

**bluemixRegionSuffix**

指定托管应用程序的位置。`bluemixRegion` 参数指定要使用的 Bluemix 部署。可以使用 `BMSClient.REGION` 静态属性设置此值，并使用以下三个值中的一个值：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
