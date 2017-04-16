---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} 시작하기

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}}는 개발자, IT 관리자, 비즈니스 이해 당사자에게 모바일 앱의 성능 및 사용 실태에 대한 통찰을 제공합니다. {{site.data.keyword.mobileanalytics_short}}를 사용하면 다음을 수행할 수 있습니다.

* 데스크 탑이나 태블릿에서 사용자의 모든 애플리케이션의 성능과 사용량을 모니터하십시오.  
* 상태동향과 이상 항목을 빠르게 식별하고 문제를 해결하기 위해 세부적으로 분석하며 핵심 메트릭이 중요 임계값을 초과할 때 경보를 트리거합니다.
{: shortdesc}

**중요:** {{site.data.keyword.mobileanalytics_short}} 콘솔은 아직 Internet Explorer 브라우저를 지원하지 않으며 일부 기능이 제대로 작동하지 않을 수 있습니다. Firefox, Chrome 또는 Safari를 사용하십시오.

{{site.data.keyword.mobileanalytics_short}} 서비스를 빨리 시작하고 실행하려면 다음 단계를 수행하십시오.

1. {{site.data.keyword.mobileanalytics_short}} 서비스의 <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)--> 인스턴스를 작성한 후에는 {{site.data.keyword.Bluemix}} 대시보드의 **서비스** 섹션에서 타일을 클릭하여 {{site.data.keyword.mobileanalytics_short}} 콘솔에 액세스할 수 있습니다. 

 다양한 보기와 차트 및 해당 값을 바로 확인하는 데 도움이 되도록 {{site.data.keyword.mobileanalytics_short}} 콘솔에 **데모 모드** 옵션을 제공하며, 이 옵션을 통해 보기와 차트에 *데모 데이터*가 표시됩니다. 데모 데이터는 서비스가 인스턴스화된 후 처음에 실행될 때 콘솔의 기본 모드입니다. 고유 애플리케이션 및 분석 데이터를 서비스에 채운 후 데모 모드를 토글 *해제*하여 애플리케이션의 데이터를 여러 차트에서 볼 수 있습니다. Mobile Analytics 콘솔은 데모 모드에 있는 경우 읽기 전용이므로 새 경보 정의를 작성할 수 없습니다.

2. {{site.data.keyword.mobileanalytics_short}} [클라이언트 SDK](/docs/services/mobileanalytics/install-client-sdk.html)를 설치하십시오. 선택적으로 {{site.data.keyword.mobileanalytics_short}} [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}을 사용할 수 있습니다.

3. 클라이언트 SDK를 가져와서 다음 코드 스니펫을 사용하여 초기화하여 사용 분석을 기록하십시오.

	#### Android
	{: #android-import}

	다음 `import` 문을 프로젝트 파일의 시작 부분에 추가하십시오.
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
    import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
    import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **참고:** Swift SDK는 iOS 및 watchOS에서 사용 가능합니다. 
	
 다음 `import` 문을 `AppDelegate.swift` 프로젝트 파일의 시작 부분에 추가하여 `BMSCore` 프레임워크와 `BMSAnalytics` 프레임워크를 가져오십시오. 

   ```Swift
   import BMSCore
   import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Cordova 애플리케이션 루트 디렉토리에서 다음 명령을 실행하여 Cordova 플러그인을 추가하십시오. 

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. 애플리케이션 코드 내에서 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 초기화하여 사용 분석과 애플리케이션 세션을 기록하십시오([API 키](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) 값 사용).	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 **bluemixRegion** 매개변수는 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`)를 지정합니다.  
    <!-- , or `BMSClient.Region.Sydney`.-->
    
 `hasUserContext`의 값을 **true** 또는 **false**로 설정하십시오. False(기본값)인 경우 각 디바이스는 활성 사용자로 계수됩니다. 

 #### iOS
 {: #ios-initialize}
  
  애플리케이션 코드 내에서 클라이언트 SDK를 초기화하여 사용 분석과 애플리케이션 세션을 기록하십시오([API 키](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) 값 사용). 
	
  ```Swift
  BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
  Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
  ```
  {: codeblock}
			
   **bluemixRegion** 매개변수는 사용 중인 Bluemix 배치(예: `BMSClient.Region.usSouth` 또는 `BMSClient.Region.unitedKingdom`)를 지정합니다. 
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
 
 `hasUserContext`의 값을 **true** 또는 **false**로 설정하십시오. False(기본값)인 경우 각 디바이스는 활성 사용자로 계수됩니다. 
	
 #### Cordova
 {: #cordova-initialize}
	
 애플리케이션 코드 내에서 클라이언트 SDK를 초기화하여 사용 분석과 애플리케이션 세션을 기록하십시오([API 키](/docs/services/mobileanalytics/sdk.html#analytics-clientkey) 값 사용). 
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  **bluemixRegion** 매개변수는 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`)를 지정합니다. 
  
 **참고:** 애플리케이션(`your_app_name_here`)에서 사용하도록 선택한 이름이 {{site.data.keyword.mobileanalytics_short}} 콘솔에 애플리케이션 이름으로 표시됩니다. 애플리케이션 이름은 대시보드에서 애플리케이션 로그를 검색하는 필터로 사용됩니다. 플랫폼(예: Android 및 iOS)에 걸쳐 동일한 애플리케이션 이름을 사용하는 경우, 로그가 전송된 플랫폼에 상관없이 동일한 이름 아래에서 애플리케이션의 모든 로그를 볼 수 있습니다.

5. 기록된 사용 분석을 Mobile Analytics 서비스로 전송하십시오. 분석을 테스트하는 간단한 방법은 애플리케이션이 시작될 때 다음 코드를 실행하는 것입니다.

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
	BMSAnalytics.send()
	```
	{: codeblock}
	
	추가 {{site.data.keyword.mobileanalytics_short}} 기능(예: [로깅](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [네트워크 요청](/docs/services/mobileanalytics/sdk.html#network-requests) 및 [충돌 분석](/docs/services/mobileanalytics/sdk.html#report-crash-analytics))에 대해 알아보려면 [애플리케이션 인스트루먼트](/docs/services/mobileanalytics/sdk.html) 주제를 읽으십시오. 
	
6. 에뮬레이터 또는 디바이스에서 애플리케이션을 컴파일하고 실행하십시오.

7. 애플리케이션의 사용 분석을 표시하려면 {{site.data.keyword.mobileanalytics_short}} 콘솔로 이동하십시오. <!--[creating custom charts](app-monitoring.html#custom-charts),-->[경보 설정](/docs/services/mobileanalytics/app-monitoring.html#alerts)과 [앱 충돌 모니터링](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash)을 수행하여 애플리케이션을 모니터링할 수도 있습니다. 


# 관련 링크

## SDK
* [Android SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova 플러그인 코어 SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/bms-core){: new_window}

## API 참조
{: #api}
* [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
