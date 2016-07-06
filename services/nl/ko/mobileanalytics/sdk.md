---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하도록 애플리케이션 인스트루먼트
{: #mobileanalytics_sdk}
*마지막 업데이트 날짜: 2016년 4월 27일*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} SDK를 사용하면 모바일 애플리케이션을 인스트루먼트할 수 있습니다.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}}를 사용하면 각각 다른 정도의 인스트루먼테이션이 필요한 세 가지 카테고리의 데이터를 수집할 수 있습니다.

1.  사전 정의된 데이터 - 이 카테고리에는 모든 앱에 적용되는 일반 사용 및 디바이스 정보가 포함됩니다. 이 카테고리 내에는 볼륨, 빈도 또는 앱 사용 기간을 표시하는 디바이스 메타데이터(운영 체제 및 디바이스 모델) 및 사용 데이터(활성 사용자 및 앱 세션)이 있습니다. 사전 정의된 데이터는 사용자의 앱에서 {{site.data.keyword.mobileanalytics_short}} SDK를 초기화한 후에 자동으로 수집됩니다.
2. 사용자 정의 이벤트 - 이 카테고리에는 사용자를 정의하는 데이터 및 특정 앱에 대한 데이터가 포함됩니다. 이 데이터는 페이지 보기, 단추 탭 또는 앱 내 구매와 같은 앱에서 발생하는 이벤트를 표시합니다. 앱 내에서의 {{site.data.keyword.mobileanalytics_short}} SDK 초기화 외에도 추적할 각 사용자 정의 이벤트에 대해 한 행을 추가해야 합니다.
3. 클라이언트 로그 메시지 - 이 카테고리를 사용하면 개발자가 개발 및 디버깅을 지원하기 위해 사용자 정의 메시지를 로그하는 앱을 통해 코드의 행을 추가할 수 있습니다. 
개발자는 각 로그 메시지에 심각도/상세도 레벨을 지정하며 레벨을 지정함으로써 후속적으로 메시지를 필터링하거나 지정된 로그 레벨 아래의 메시지를 무시하도록 앱을 구성하여 스토리지 공간을 유지할 수 있습니다. 클라이언트 로그 데이터를 수집하려면 각 로그 메시지에 대해 코드의 한 행을 추가하고 앱 내에서 {{site.data.keyword.mobileanalytics_short}} SDK를 초기화해야 합니다.

현재 SDK는 Android, iOS 및 WatchOS에 대해 사용 가능합니다.

## 클라이언트 키 값 식별
{: #analytics-clientkey}

클라이언트 SDK를 설정하기 전에 **클라이언트 키** 값을 식별하십시오. 클라이언트 키는 클라이언트 SDK를 초기화하는 데 필수입니다.
1. {{site.data.keyword.mobileanalytics_short}} 서비스 대시보드를 여십시오.
2. 렌치 아이콘을 클릭하여 API 키 탭을 여십시오.
3. API 키 탭에서 클라이언트 키 값을 기록해 두십시오.


## 분석을 수집하기 위해 Android 앱 초기화
{: #initalize-ma-sdk-android}

{{site.data.keyword.mobileanalytics_short}} 서비스로 로그를 전송할 수 있도록 애플리케이션을 초기화하십시오.

1. 다음 `import` 문을 프로젝트 파일의 맨 위에 추가하여 클라이언트 SDK를 가져오십시오.

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Android 애플리케이션의 기본 활동의 `onCreate` 메소드 내 또는 프로젝트에 가장 적합한 위치에 초기화 코드를 추가하여 Android 애플리케이션에서 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 초기화할 수 있습니다.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하려면 **bluemixRegion** 매개변수를 사용하여 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용자가 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다. 예를 들어, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` 또는 `BMSClient.REGION_SYDNEY`입니다.
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Android 애플리케이션 오브젝트를 사용하고 사용자의 애플리케이션 이름을 제공하여 Analytics를 초기화하십시오. 또한 [**클라이언트 키**](#analytics-clientkey) 값이 필요합니다.
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// In this code example, Analytics is configured to record lifecycle events.
	```
  {: codeblock}

	**팁:** 애플리케이션 이름은 대시보드에서 클라이언트 로그를 검색하기 위한 필터로 사용됩니다. 플랫폼(예: Android 및 iOS)에 걸쳐 동일한 애플리케이션 이름을 사용하는 경우, 로그가 전송된 플랫폼에 상관없이 동일한 이름 아래에서 애플리케이션의 모든 로그를 볼 수 있습니다.

## 분석을 수집하기 위해 iOS 앱 초기화
{: #init-ma-sdk-ios}

{{site.data.keyword.mobileanalytics_short}} 서비스로 로그를 전송할 수 있도록 애플리케이션을 초기화하십시오. Swift SDK는 iOS 및 watchOS에 대해 사용 가능합니다.

1. 다음 `import` 문을 `AppDelegate.swift` 프로젝트 파일의 맨 위에 추가하여 `BMSCore` 및 `BMSAnalytics` 프레임워크를 가져오십시오.

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하려면 다음 코드를 사용하여 먼저 `BMSClient`를 초기화해야 합니다.

  애플리케이션 위임의 `application(_:didFinishLaunchingWithOptions:)` 메소드 또는 프로젝트에 가장 적합한 위치에 초기화 코드를 배치하십시오.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하려면 **bluemixRegion** 매개변수를 사용하여 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용자가 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다. 예를 들어, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` 또는 `BMSClient.REGION_SYDNEY`입니다.
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. 사용자의 모바일 애플리케이션 이름을 제공하여 Analytics를 초기화하십시오. 또한 [**클라이언트 키**](#analytics-clientkey) 값이 필요합니다.

  애플리케이션 이름은 {{site.data.keyword.mobileanalytics_short}} 대시보드에서 클라이언트 로그를 검색하기 위한 필터로 사용됩니다. 플랫폼(예: Android 및 iOS)에 걸쳐 동일한 애플리케이션 이름을 사용함으로써 로그가 전송된 플랫폼에 상관없이 동일한 이름 아래에서 애플리케이션의 모든 로그를 볼 수 있습니다.

  선택적 `deviceEvents` 매개변수는 자동으로 디바이스 레벨의 이벤트에 대한 분석을 수집합니다.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  `Analytics.recordApplicationDidBecomeActive()` 및 `Analytics.recordApplicationWillResignActive()` 메소드를 사용하여 WatchOS에 대한 디바이스 이벤트를 기록할 수 있습니다.
  
  ExtensionDelegate 클래스의 `applicationDidBecomeActive()` 메소드에 다음 행을 추가하십시오.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  ExtensionDelegate 클래스의 applicationWillResignActive() 메소드에 다음 행을 추가하십시오.
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## 사용 분석 수집
{: #app-monitoring-gathering-analytics}

  사용 분석을 기록하고 기록된 데이터를 {{site.data.keyword.mobileanalytics_short}} 서비스로 전송하도록 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 구성할 수 있습니다.

  다음 API를 사용하여 사용 분석 기록 및 전송을 시작하십시오.

#### Android
{: #android-usage-api}
	
```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();// Enable recording of usage analytics
Analytics.enable();Analytics.log(eventJSONObject);// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
	
이벤트 로깅에 대한 샘플 사용 분석:
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object:
JSONObject eventJSONObject = new JSONObject();eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false// Enable recording of usage analytics
Analytics.enabled = true// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```

이벤트 로깅에 대한 샘플 사용 분석:

```
// Log a custom analytics event for custom charts
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## 로거 사용 설정, 구성 및 사용
{: #app-monitoring-logger}

  {{site.data.keyword.mobileanalytics_full}} 클라이언트 SDK는 사용자가 익숙한 기타 로깅 프레임워크(`java.util.logging` 또는 `log4j` 등)와 유사한 로깅 프레임워크를 제공합니다. 로깅 프레임워크는 다중 패키지별 로거 인스턴스, 다른 로그 레벨, 애플리케이션 충돌에 대한 스택 추적 캡처 등을 지원합니다.

  또한 애플리케이션이 실행 중인 디바이스에 로깅된 데이터를 저장하고 나중에 해당 디바이스 로그를 {{site.data.keyword.mobileanalytics_short}} 서비스로 전송하도록 구성할 수 있습니다.

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK 로깅 프레임워크는 다음 로그 레벨을 지원합니다. 해당 로그 레벨은 가장 자세한 레벨부터 나열되며 권장되는 사용 가이드라인이 함께 제공됩니다.

  * `심각` - 복구 불가능한 충돌 또는 정지에 대해 사용됩니다. `심각` 레벨은 애플리케이션이 충돌할 때 사용자에게 표시되는 복구 불가능한 오류를 로깅하기 위해 예약됩니다.
  * `오류` - 예상치 못한 예외 또는 예상치 못한 네트워크 프로토콜 오류에 대해 사용됩니다.
  * `경고` - 더 이상 사용되지 않는 API 또는 느린 네트워크 응답 등과 같이 중요한 오류로 간주되지 않는 사용 경고를 로깅하는 데 사용됩니다.
  * `정보` - 중요하나 긴급하지는 않은 초기화 이벤트 및 기타 데이터를 보고하는 데 사용됩니다.
  * `디버그` - 개발자가 애플리케이션 결함을 해결하는 데 도움을 주기 위해 디버그 명령문을 보고하는 데 사용됩니다.

    #### 로그 레벨 시나리오
    {: #log-level-scenario}

    로거 레벨이 `심각`으로 구성된 경우, 로거가 미발견 예외를 캡처하나 충돌 이벤트를 발생시키는 임의의 로그를 캡처하지 않습니다. `심각` 로거 항목이 발생할 수 있는 로그(`경고` 및 `오류`)도 캡처되도록 더 자세한 로거 레벨을 설정할 수 있습니다.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### 샘플 로거 사용법
{: #sample-logger-usage}

**참고:** 로깅 프레임워크를 사용하기 전에 [{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK](sdk.html)를 사용하도록 앱을 인스트루먼트했는지 확인하십시오.
 
  다음은 샘플 로거 사용법을 표시하는 코드 스니펫입니다.

#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they
// can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send();
```

로거 시나리오:

```
// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message");
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.mobileanalytics_short}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service
Logger.send()
```

로거 시나리오:
    
```
// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")// Log messages with different levels
logger1.debug("debug message for feature 1")
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")
```

**팁**: 개인정보 보호정책과 관련하여 릴리스 모드로 빌드된 애플리케이션에 대해 로거 출력을 사용하지 않도록 설정할 수 있습니다. 기본적으로 로거 클래스는 로그를 Xcode 콘솔에 인쇄합니다. 대상에 대한 빌드 설정에서 `-D RELEASE_BUILD` 플래그를 릴리스 빌드 구성의 **기타 Swift 플래그** 섹션에 추가하십시오.
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## 활성 사용자 추적
{: #trackingusers}
필요한 경우, 활성 사용자의 사용자 이름을 {{site.data.keyword.mobileanalytics_short}}에 전달하여 얼마나 많은 사용자가 애플리케이션을 적극적으로 사용하고 있는지 추적할 수 있습니다.

#### Android
{: #android-tracking-users}

사용자가 로그인하는 경우에 대해 다음 코드를 추가하십시오.

```
Analytics.setUserIdentity("username");
```

사용자가 로그아웃하는 경우에 대해 다음 코드를 추가하십시오.

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

사용자가 로그인하는 경우에 대해 다음 코드를 추가하십시오.

```
Analytics.userIdentity = "username"
```

사용자가 로그아웃하는 경우에 대해 다음 코드를 추가하십시오.

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->

# 관련 링크

## API 참조
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
