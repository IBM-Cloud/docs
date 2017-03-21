---

copyright:
 years: 2015, 2016

---

# Android 앱을 위한 푸시 SDK 초기화
{: #android_initialize}

초기화 코드를 배치하는 공통 위치는 Android 애플리케이션에서 기본 활동의 onCreate 메소드입니다. 

Bluemix 애플리케이션 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 애플리케이션 GUID를 확보하십시오. 라우트 및 앱 GUID에 이러한 값을 사용하십시오. Bluemix 앱 appRoute 및 appGUID 매개변수를 사용하려면 코드 스니펫을 수정하십시오. 


##Core SDK 초기화

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Bluemix에서 생성한 서버 애플리케이션에 지정된 라우트를 지정합니다.

**AppGUID**

Bluemix에서 생성한 애플리케이션에 지정된 고유 키를 지정합니다. 이 값은 대소문자를 구분합니다. 

**bluemixRegionSuffix**

앱이 호스트된 위치를 지정합니다. 다음 값 중 하나를 사용할 수 있습니다. 

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##클라이언트 푸시 SDK 초기화

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
