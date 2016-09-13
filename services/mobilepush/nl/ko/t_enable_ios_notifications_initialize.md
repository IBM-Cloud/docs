---

copyright:
 years: 2015, 2016

---

# iOS 앱을 위한 푸시 SDK 초기화
{: #enable-push-ios-notifications-initialize}

초기화 코드를 배치하는 공통 위치는 iOS 애플리케이션에 대한 애플리케이션 위임자입니다.
Bluemix 애플리케이션 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 GUID를 확보하십시오. 

##Core SDK 초기화

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

##클라이언트 푸시 SDK 초기화

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

## 라우트, GUID 및 Bluemix 리젼

**appRoute**

Bluemix에서 생성한 서버 애플리케이션에 지정된 라우트를 지정합니다.

**GUID**

Bluemix에서 생성한 애플리케이션에 지정된 고유 키를 지정합니다. 이 값은 대소문자를 구분합니다. 

**bluemixRegionSuffix**

앱이 호스트된 위치를 지정합니다. ```bluemixRegion``` 매개변수는 사용 중인 Bluemix 배치를 지정합니다. 이 값을 ```BMSClient.REGION`` 정적 특성으로 설정하고 다음 값 중 하나를 사용할 수 있습니다.

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
