---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}}(베타) 시작하기  

{: #gettingstartedtemplate}
*마지막 업데이트 날짜: 2016년 5월 17일*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} 서비스를 사용하여 모바일 앱 및 모바일 디바이스의 상태, 동작, 컨텍스트를 측정하십시오.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} 서비스를 빠르게 시작하고 실행하려면 다음 단계를 따르십시오.

1. [{{site.data.keyword.mobileanalytics_short}} 서비스의 인스턴스를 작성](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)한 후에는 {{site.data.keyword.Bluemix}} 대시보드의 서비스 섹션에서 타일을 클릭하여 {{site.data.keyword.mobileanalytics_short}} 콘솔에 액세스할 수 있습니다.

  **중요:** 새로 작성된 Mobile Analytics 서비스를 처음 열 때 서비스가 사용자 ID의 유효성을 검증할 수 있도록 {{site.data.keyword.Bluemix_notm}}에서 사용자에 대한 서비스에 필수 정보를 제공하도록 허용하는지 여부를 확인하기 위한 창이 표시됩니다. **확인**을 클릭하여 {{site.data.keyword.mobileanalytics_short}} 콘솔로 진행하십시오. 취소하면 {{site.data.keyword.mobileanalytics_short}} 콘솔이 열리지 않습니다.

2. {{site.data.keyword.mobileanalytics_short}} [클라이언트 SDK](install-client-sdk.html)를 설치하십시오.

3. 클라이언트 SDK를 가져와서 다음 코드 스니펫을 사용하여 초기화하여 사용 분석을 기록하십시오.

	#### Android
	{: #android-initialize}
	1. 클라이언트 SDK 가져오기:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
	2. 애플리케이션 코드 내에서 클라이언트 SDK를 초기화하고 [클라이언트 키](sdk.html#analytics-clientkey) 값을 사용하여 사용 분석 및 애플리케이션 세션을 기록하십시오.

		```Java
			try {
			     BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
	            //The Bluemix region provided is invalid
	        }
				Analytics.init(getApplication(), your_app_name, your_client_key, Analytics.DeviceEvent.LIFECYCLE);
		```
    **bluemixRegion** 매개변수는 사용자가 사용 중인 Bluemix 배치를 지정합니다. 예를 들어, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` 또는 `BMSClient.REGION_SYDNEY`입니다.

  #### iOS
  {: #ios-initialize}
  1. `BMSCore` 및 `BMSAnalytics` 프레임워크 가져오기:
  ```
    import BMSCore
    import BMSAnalytics
    ```
  2. 애플리케이션 코드 내에서 클라이언트 SDK를 초기화하고 [클라이언트 키](sdk.html#analytics-clientkey) 값을 사용하여 사용 분석 및 애플리케이션 세션을 기록하십시오.
 
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName(your_app_name, apiKey: your_client_key, deviceEvents: DeviceEvent.LIFECYCLE)
	```
  **bluemixRegion** 매개변수는 사용자가 사용 중인 Bluemix 배치를 지정합니다. 예를 들어, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` 또는 `BMSClient.REGION_SYDNEY`입니다.

4. 기록된 사용 분석을 Mobile Analytics 서비스로 전송하십시오. 분석을 테스트하는 간단한 방법은 애플리케이션이 시작될 때 다음 코드를 실행하는 것입니다.

	#### Android
	{: #android-send}

	Android 애플리케이션의 기본 활동의 `onCreate` 메소드 내 또는 프로젝트에 가장 적합한 위치에 `Analytics.send()` 메소드를 추가할 수 있습니다.

	```
	Analytics.send();
	```

	#### iOS
	{: #ios-send}

	`Analytics.send` 메소드를 사용하여 분석 데이터를 서버에 전송하십시오. 애플리케이션 위임의 `application(_:didFinishLaunchingWithOptions:)` 메소드 또는 프로젝트에 가장 적합한 위치에 `Analytics.send` 메소드를 배치하십시오.

	```
	Analytics.send()
	```

	[애플리케이션 인스트루먼트](sdk.html) 주제를 읽으십시오.
5. 에뮬레이터 또는 디바이스에서 애플리케이션을 컴파일하고 실행하십시오.

6. {{site.data.keyword.mobileanalytics_short}} **대시보드**로 이동하여 애플리케이션을 사용하는 새 디바이스 및 디바이스 총계 등의 사용 분석을 보십시오. 또한 [사용자 정의 차트 작성](app-monitoring.html#custom-charts), [경보 설정](app-monitoring.html#alerts) 및 [앱 충돌 모니터링](app-monitoring.html#monitor-app-crash)을 사용하여 앱을 모니터링할 수 있습니다.


# 관련 링크

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
