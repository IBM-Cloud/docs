---

copyright:
  years: 2016
lastupdated: "2016-10-31"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}}(베타) 시작하기

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}}는 개발자, IT 관리자, 비즈니스 이해 당사자에게 모바일 앱의 성능 및 사용 실태에 대한 통찰을 제공합니다. 데스크 탑이나 태블릿에서 사용자의 모든 애플리케이션의 성능과 사용량을 모니터하십시오. 상태동향과 이상 항목을 빠르게 식별하고 문제를 해결하기 위해 세부적으로 분석하며 핵심 메트릭이 중요 임계값을 초과할 때 경보를 트리거합니다.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} 서비스를 빠르게 시작하고 실행하려면 다음 단계를 따르십시오.

1. {{site.data.keyword.mobileanalytics_short}} 서비스의 <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)--> 인스턴스를 작성한 후에는 {{site.data.keyword.Bluemix}} 대시보드의 **서비스** 섹션에서 타일을 클릭하여 {{site.data.keyword.mobileanalytics_short}} 콘솔에 액세스할 수 있습니다. 

 **데모 모드**를 사용하는 {{site.data.keyword.mobileanalytics_short}} 서비스를 시작합니다. 데모 모드는 **앱 데이터** 페이지와 **경보** 페이지에서 차트를 채우므로 데이터가 표시되는 방식을 볼 수 있습니다. 사용자 자체 데이터가 있는 경우 데모 모드를 토글하여 끌 수 있습니다. {{site.data.keyword.mobileanalytics_short}} 콘솔은 데모 모드에 있는 경우 읽기 전용이므로 새 경보 정의를 작성할 수 없습니다. 

2. {{site.data.keyword.mobileanalytics_short}} [클라이언트 SDK](/docs/services/mobileanalytics/install-client-sdk.html)를 설치하십시오. 선택적으로 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}를 사용할 수 있습니다. 

3. 클라이언트 SDK를 가져와서 다음 코드 스니펫을 사용하여 초기화하여 사용 분석을 기록하십시오.

	#### Android
	{: #android-initialize}
	
	1. 클라이언트 SDK 가져오기:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
	
	2. 애플리케이션 코드 내에서 클라이언트 SDK를 초기화하여 사용 분석과 애플리케이션 세션을 기록하십시오([API 키](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) 값 사용). 

		```Java
		BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
			
		Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
		```
		{: codeblock}
		
    	애플리케이션(`your_app_name_here`)에서 사용하도록 선택한 이름이 {{site.data.keyword.mobileanalytics_short}} 콘솔에 애플리케이션 이름으로 표시됩니다. 애플리케이션 이름은 대시보드에서 애플리케이션 로그를 검색하는 필터로 사용됩니다. 플랫폼(예: Android 및 iOS)에 걸쳐 동일한 애플리케이션 이름을 사용하는 경우, 로그가 전송된 플랫폼에 상관없이 동일한 이름 아래에서 애플리케이션의 모든 로그를 볼 수 있습니다.
    
    	**bluemixRegion** 매개변수는 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`)를 지정합니다.  
    <!-- , or `BMSClient.Region.Sydney`.-->
    
    	**참고:** `hasUserContext`에 대한 값을 **true** 또는 **false**로 설정하십시오. False(기본값)인 경우 각 디바이스는 활성 사용자로 계수됩니다.  [`Analytics.setUserIdentity("username");`](/docs/services/mobileanalytics/sdk.html#android-tracking-users) 메소드는 `hasUserContext`가 false일 경우 작동하지 않습니다. true인 경우 [`Analytics.setUserIdentity("username");`](/docs/services/mobileanalytics/sdk.html#android-tracking-users)의 개별 사용은 활성 사용자로 계수됩니다. `hasUserContext`가 true이고 기본 사용자 ID가 없으므로, 활성 사용자 차트를 채우도록 설정되어야 합니다.

	#### iOS
	{: #ios-initialize}
  
	1. `BMSCore` 및 `BMSAnalytics` 프레임워크 가져오기: 
	
		```
		import BMSCore
	import BMSAnalytics
	```
		{: codeblock}
    
	2. 애플리케이션 코드 내에서 클라이언트 SDK를 초기화하여 사용 분석과 애플리케이션 세션을 기록하십시오([API 키](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) 값 사용). 
	
		```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
		```
		{: codeblock}
		
		애플리케이션(`your_app_name_here`)에서 사용하도록 선택한 이름이 {{site.data.keyword.mobileanalytics_short}} 콘솔에 애플리케이션 이름으로 표시됩니다. 애플리케이션 이름은 대시보드에서 애플리케이션 로그를 검색하는 필터로 사용됩니다. 플랫폼(예: Android 및 iOS)에 걸쳐 동일한 애플리케이션 이름을 사용하는 경우, 로그가 전송된 플랫폼에 상관없이 동일한 이름 아래에서 애플리케이션의 모든 로그를 볼 수 있습니다.
	
		**bluemixRegion** 매개변수는 사용 중인 Bluemix 배치(예: `BMSClient.Region.usSouth` 또는 `BMSClient.Region.unitedKingdom`)를 지정합니다. 
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
		**참고:** `hasUserContext`에 대한 값을 **true** 또는 **false**로 설정하십시오. False(기본값)인 경우 각 디바이스는 활성 사용자로 계수됩니다. [`Analytics.userIdentity="username"`](/docs/services/mobileanalytics/sdk.html#ios-tracking-users) 메소드는 `hasUserContext`가 false일 경우 작동하지 않습니다. true인 경우 [`Analytics.userIdentity="username"`](/docs/services/mobileanalytics/sdk.html#ios-tracking-users)의 개별 사용은 활성 사용자로 계수됩니다. `hasUserContext`가 true이고 기본 사용자 ID가 없으므로, 활성 사용자 차트를 채우도록 설정되어야 합니다.
	
	#### Cordova
	{: #cordova-initialize}
	
	애플리케이션 코드 내에서 클라이언트 SDK를 초기화하여 사용 분석과 애플리케이션 세션을 기록하십시오([API 키](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) 값 사용). 
	
		```Javascript
		var appName = "your_app_name_here";
		var apiKey = "your_api_key_here";
		
		BMSClient.initialize(BMSClient.REGION_US_SOUTH);
		BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
		```

4. 기록된 사용 분석을 Mobile Analytics 서비스로 전송하십시오. 분석을 테스트하는 간단한 방법은 애플리케이션이 시작될 때 다음 코드를 실행하는 것입니다.

	#### Android
	{: #android-send}

	`Analytics.send()` 메소드를 사용하여 분석 데이터를 서버에 전송하십시오. `Analytics.send()` 메소드를 Android 애플리케이션에서 기본 활동의 `onCreate` 메소드 또는 프로젝트에 가장 적합한 위치에 배치할 수 있습니다.  
	
	`Analytics.send()`를 위치에 상관 없이 삽입할 수 있습니다. 

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	`Analytics.send` 메소드를 사용하여 분석 데이터를 서버에 전송하십시오. `Analytics.send` 메소드를 애플리케이션 위임의 `application(_:didFinishLaunchingWithOptions:)` 메소드 또는 프로젝트에 가장 적합한 위치에 배치할 수 있습니다.  

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	`BMSAnalytics.send` 메소드를 사용하여 분석 데이터를 서버에 전송하십시오. `BMSAnalytics.send` 메소드를 프로젝트에 가장 적합한 위치에 배치하십시오. 
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	추가 {{site.data.keyword.mobileanalytics_short}} 기능(예: [로깅](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [네트워크 요청](/docs/services/mobileanalytics/sdk.html#network-requests) 및 [충돌 분석](/docs/services/mobileanalytics/sdk.html#report-crash-analytics))에 대해 알아보려면 [애플리케이션 인스트루먼트](/docs/services/mobileanalytics/sdk.html) 주제를 읽으십시오. 
	
5. 에뮬레이터 또는 디바이스에서 애플리케이션을 컴파일하고 실행하십시오.

6. 애플리케이션의 사용 분석을 표시하려면 {{site.data.keyword.mobileanalytics_short}} 콘솔로 이동하십시오. <!--[creating custom charts](app-monitoring.html#custom-charts),-->[경보 설정](/docs/services/mobileanalytics/app-monitoring.html#alerts)과 [앱 충돌 모니터링](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash)을 수행하여 애플리케이션을 모니터링할 수도 있습니다. 


# 관련 링크

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova 플러그인 코어 SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API 참조
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
