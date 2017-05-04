---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하도록 애플리케이션 인스트루먼트
{: #mobileanalytics_sdk}

{{site.data.keyword.mobileanalytics_full}} SDK를 사용하면 모바일 애플리케이션을 인스트루먼트할 수 있습니다.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}}를 사용하면 각각 다른 정도의 인스트루먼테이션이 필요한 두<!--three--> 가지 카테고리의 데이터를 수집할 수 있습니다.

1. 사전 정의된 데이터 - 이 카테고리에는 모든 애플리케이션에 적용되는 일반 사용 정보와 디바이스 정보가 포함됩니다. 이 카테고리 내에는 볼륨, 빈도 또는 애플리케이션 사용 기간을 표시하는 디바이스 메타데이터(운영 체제 및 디바이스 모델)와 사용 데이터(활성 사용자 및 애플리케이션 세션)가 있습니다. 사전 정의된 데이터는 애플리케이션에서 {{site.data.keyword.mobileanalytics_short}} SDK를 초기화한 후 자동으로 수집됩니다. 

2. 애플리케이션 로그 메시지 - 개발자는 이 카테고리에서 개발과 디버깅을 지원하기 위해 사용자 정의 메시지를 로그하는 애플리케이션을 통해 코드의 행을 추가할 수 있습니다. 개발자는 각 로그 메시지에 심각도/상세도 레벨을 지정하고, 레벨을 지정하여 차후에 메시지를 필터링하거나 주어진 로그 레벨보다 낮은 레벨의 메시지를 무시하도록 애플리케이션을 구성하여 스토리지 영역을 유지할 수 있습니다. 애플리케이션 로그 데이터를 수집하려면 로그 메시지마다 한 행의 코드를 추가할 뿐 아니라 애플리케이션에서 {{site.data.keyword.mobileanalytics_short}} SDK를 초기화해야 합니다. 

3. 사용자 정의 이벤트 - 이 카테고리에는 자체적으로 정의하고 사용자 앱에 특정적인 데이터가 포함됩니다. 이 데이터는 페이지 보기, 단추 탭 또는 앱 내 구매 등과 같이 앱 내에서 발생하는 이벤트를 표시합니다. 사용자 앱에서 {{site.data.keyword.mobileanalytics_short}} SDK를 초기화하는 외에 추적하려는 각 사용자 정의 이벤트에 대한 코드의 행을 추가해야 합니다.  

현재 SDK는 Android, iOS, WatchOS 및 Cordova에서 사용 가능합니다. 

## 서비스 신임 정보 API 키 값 식별
{: #analytics-clientkey}

클라이언트 SDK를 설정하기 전에 **API 키** 값을 식별하십시오. API 키는 클라이언트 SDK를 초기화하는 데 필요합니다. 

1. {{site.data.keyword.mobileanalytics_short}} 서비스 대시보드를 여십시오.
2. **신임 정보 보기**를 펼쳐 API 키 값을 표시하십시오. {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 초기화하는 경우 API 키 값이 필요합니다. 


## 분석을 수집하기 위해 애플리케이션 초기화
{: #initalize-ma-sdk}

{{site.data.keyword.mobileanalytics_short}} 서비스로 로그를 전송할 수 있도록 애플리케이션을 초기화하십시오.

1. 클라이언트 SDK를 가져오십시오.

	### Android
	{: #android-import notoc}

	다음 `import` 문을 프로젝트 파일의 시작 부분에 추가하십시오.
	
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
	import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  	```
	{: codeblock}
  
	### iOS
	{: #ios-import notoc}
	
	**참고:** Swift SDK는 iOS 및 watchOS에서 사용 가능합니다. 
	
	다음 `import` 문을 `AppDelegate.swift` 프로젝트 파일의 시작 부분에 추가하여 `BMSCore` 프레임워크와 `BMSAnalytics` 프레임워크를 가져오십시오. 

	```Swift
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}  
   
	### Cordova
	{: #cordova-import notoc}
		
	Cordova 애플리케이션 루트 디렉토리에서 다음 명령을 실행하여 Cordova 플러그인을 추가하십시오. 

	```Javascript
	cordova plugin add bms-core
	```
	{: codeblock}  

2. 사용하는 애플리케이션에서 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 초기화하십시오.

	### Android
	{: #android-init notoc}
	
	Android 애플리케이션의 기본 활동의 `onCreate` 메소드 내 또는 프로젝트에 가장 적합한 위치에 초기화 코드를 추가하여 Android 애플리케이션에서 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 초기화할 수 있습니다.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
	{: codeblock}

	**bluemixRegion** 매개변수로 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`)를 지정합니다.
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
	### iOS
	{: #ios-init notoc}
    
	먼저 다음 코드를 사용하여 `BMSClient` 클래스를 초기화하십시오. 애플리케이션 위임에 관한 `application(_:didFinishLaunchingWithOptions:)` 메소드나 프로젝트에 가장 적합한 위치에 초기화 코드를 넣으십시오.
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
	```
	{: codeblock}

	**bluemixRegion** 매개변수로 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다(예: `BMSClient.Region.usSouth` 또는 `BMSClient.Region.unitedKingdom`). 
    <!-- , or `BMSClient.Region.Sydney`. -->
    
	### Cordova
	{: #cordova-init notoc}
    
	**BMSClient** 및 **BMSAnalytics**를 초기화하십시오. [**API 키**](#analytics-clientkey) 값이 필요합니다. 

	```Javascript
	var applicationName = "HelloWorld";
	var apiKey =  "your_api_key_here";
	var hasUserContext = true;
	var deviceEvents = [BMSAnalytics.ALL];

	BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Make sure you point to your region	
	BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
	```
	{: codeblock}

	{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하려면 **bluemixRegion** 매개변수로 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용자가 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다(예: `BMSClient.REGION_US_SOUTH` 또는 `BMSClient.REGION_UK`). 
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. 애플리케이션 오브젝트를 사용하고 사용자 애플리케이션의 이름을 제공하여 Analytics를 초기화하십시오.  

	애플리케이션(`your_app_name_here`)에서 사용하도록 선택한 이름이 {{site.data.keyword.mobileanalytics_short}} 콘솔에 애플리케이션 이름으로 표시됩니다. 애플리케이션 이름은 대시보드에서 애플리케이션 로그를 검색하는 필터로 사용됩니다. 플랫폼(예: Android 및 iOS)에 걸쳐 동일한 애플리케이션 이름을 사용하는 경우, 로그가 전송된 플랫폼에 상관없이 동일한 이름 아래에서 애플리케이션의 모든 로그를 볼 수 있습니다.

	[**API 키**](#analytics-clientkey) 값도 필요합니다. 

	### Android
	{: #android-init-analytics notoc}
	
	```Java
	// In this code example, Analytics is configured to record lifecycle events.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**참고:** `hasUserContext`에 대한 값을 **true** 또는 **false**로 설정하십시오. False(기본값)인 경우 각 디바이스는 활성 사용자로 계수됩니다. 디바이스마다 적극적으로 애플리케이션을 사용 중인 사용자 수를 추적할 수 있는 [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) 메소드는 `hasUserContext`가 false인 경우 작동하지 않습니다. true인 경우 [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users)의 개별 사용은 활성 사용자로 계수됩니다. `hasUserContext`가 true이고 기본 사용자 ID가 없으므로, 활성 사용자 차트를 채우도록 설정되어야 합니다.
	
	### iOS
	{: #ios-initialize-analytics notoc}
	
	```Swift 
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
 	```
	{: codeblock}
 	
	### watchOS
	{: #watchos-initialize-analytics notoc}
	 	
	```Swift
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
	```
	{: codeblock}
 	
	선택적 `deviceEvents` 매개변수는 자동으로 디바이스 레벨의 이벤트에 대한 분석을 수집합니다.
	
	**참고:** `hasUserContext`에 대한 값을 **true** 또는 **false**로 설정하십시오. False(기본값)인 경우 각 디바이스는 활성 사용자로 계수됩니다. 디바이스마다 적극적으로 애플리케이션을 사용 중인 사용자 수를 추적할 수 있는 [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) 메소드는 `hasUserContext`가 false인 경우 작동하지 않습니다. `hasUserContext`가 true인 경우 [`Analytics.userIdentity="username"`](sdk.html#ios-tracking-users)의 개별 사용은 활성 사용자로 계수됩니다. `hasUserContext`가 true이고 기본 사용자 ID가 없으므로, 활성 사용자 차트를 채우도록 설정되어야 합니다.

	#### watchOS
	{: #watchos-record-device notoc}

	`Analytics.recordApplicationDidBecomeActive()` 및 `Analytics.recordApplicationWillResignActive()` 메소드를 사용하여 WatchOS에 대한 디바이스 이벤트를 기록할 수 있습니다.
  
	ExtensionDelegate 클래스의 `applicationDidBecomeActive()` 메소드에 다음 행을 추가하십시오.
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
	{: codeblock}

	ExtensionDelegate 클래스의 `applicationWillResignActive()` 메소드에 다음 행을 추가하십시오.
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. 이제 분석을 수집할 수 있도록 애플리케이션을 초기화했습니다. 다음으로 {{site.data.keyword.mobileanalytics_short}} 서비스에 [분석 데이터를 전송](sdk.html#app-monitoring-gathering-analytics)할 수 있습니다. 


## 사용 분석 수집
{: #app-monitoring-gathering-analytics}

사용 분석을 기록하고 기록된 데이터를 {{site.data.keyword.mobileanalytics_short}} 서비스로 전송하도록 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 구성할 수 있습니다.

다음 API를 사용하여 사용 분석 기록 및 전송을 시작하십시오.


### Android
{: #android-usage-api notoc}
	
```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();// Enable recording of usage analytics
Analytics.enable();// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(new ResponseListener() {
            @Override
            public void onSuccess(Response response) {
                // Handle Analytics send success here.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Handle Analytics send failure here.
            }
        });
```
{: codeblock}
	
이벤트 로깅을 위한 샘플 사용법 분석:
	
```
// Log a custom analytics event
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


### iOS - Swift
{: #ios-usage-api notoc}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.isEnabled = false

// Enable recording of usage analytics
Analytics.isEnabled = true

// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        // Handle Analytics send success here.
    }
    if let error = error {
        // Handle Analytics send failure here.
    }
})
```
{: codeblock}

이벤트 로깅을 위한 샘플 사용법 분석:

```Swift
// Log a custom analytics event
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

### Cordova
{: #usage-analytics-cordova notoc}

```JavaScript
// Enable usage analytics recording
BMSAnalytics.enable();

// Disable usage analytics recording
BMSAnalytics.disable();

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
	},
	function (err) {
		console.log('fail: ' + err);
	});
```
{: codeblock}

이벤트 로깅을 위한 샘플 사용법 분석:

```JavaScript
// Log a custom analytics event
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

**참고:** Cordova 애플리케이션을 개발 중인 경우 애플리케이션 라이프사이클 이벤트 레코딩을 사용으로 설정하려면 기본 API를 사용하십시오.
  
## 로거 사용 설정, 구성 및 사용
{: #app-monitoring-logger}

{{site.data.keyword.mobileanalytics_full}} 클라이언트 SDK는 사용자가 익숙한 기타 로깅 프레임워크(`java.util.logging` 또는 `log4j` 등)와 유사한 로깅 프레임워크를 제공합니다. 로깅 프레임워크는 다중 패키지별 로거 인스턴스, 다른 로그 레벨, 애플리케이션 충돌에 대한 스택 추적 캡처 등을 지원합니다.

또한 애플리케이션이 실행 중인 디바이스에 로깅된 데이터를 저장하고 나중에 해당 디바이스 로그를 {{site.data.keyword.mobileanalytics_short}} 서비스로 전송하도록 구성할 수 있습니다.

<!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK 로깅 프레임워크는 다음 로그 레벨을 지원합니다. 해당 로그 레벨은 가장 자세한 레벨부터 나열되며 권장되는 사용 가이드라인이 함께 제공됩니다.

  * `FATAL` - 복구 불가능한 충돌 또는 정지에 대해 사용됩니다. `FATAL` 레벨은 애플리케이션이 충돌할 때 사용자에게 표시되는 복구 불가능한 오류를 로깅하기 위해 예약됩니다.
  * `ERROR` - 예상치 못한 예외 또는 예상치 못한 네트워크 프로토콜 오류에 대해 사용됩니다.
  * `WARN` - 더 이상 사용되지 않는 API 또는 느린 네트워크 응답 등과 같이 중요한 오류로 간주되지 않는 사용 경고를 로깅하는 데 사용됩니다.
  * `INFO` - 중요하나 긴급하지는 않은 초기화 이벤트 및 기타 데이터를 보고하는 데 사용됩니다.
  * `DEBUG` - 개발자가 애플리케이션 결함을 해결하는 데 도움을 주기 위해 디버그 명령문을 보고하는 데 사용됩니다.


### 로그 레벨 시나리오
{: #log-level-scenario notoc}

로거 레벨이 `FATAL`로 구성된 경우, 로거가 미발견 예외를 캡처하나 충돌 이벤트를 발생시키는 임의의 로그를 캡처하지 않습니다. `FATAL` 로거 항목이 발생할 수 있는 로그(`WARN` 및 `ERROR`)도 캡처되도록 더 자세한 로거 레벨을 설정할 수 있습니다.

로거 레벨이 `DEBUG`로 설정된 경우에는 Mobile Analytics 클라이언트 SDK 로그도 가져옵니다. 이 로그는 로그를 전송할 때 포함됩니다. 

<!-- **Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core. -->


### 샘플 로거 사용법
{: #sample-logger-usage notoc}

**참고:** 로깅 프레임워크를 사용하기 전에 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하도록 애플리케이션을 인스트루먼트했는지 확인하십시오. 
 
다음은 샘플 로거 사용법을 표시하는 코드 스니펫입니다.


#### Android
{: #android-logger-sample notoc}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message");
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");
// Send logs to the Mobile Analytics Service
Logger.send(new ResponseListener() {
	@Override
	public void onSuccess(Response response) {
		// Handle Logger send success here.
	}

	@Override
	public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
		// Handle Logger send failure here.
	}
});        
```
{: codeblock}


#### iOS - Swift
{: #ios-logger-sample-swift2 notoc}

```
// Configure Logger to save logs to the device so that they
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.isLogStorageEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Log messages with different levels
logger1.debug(message: "debug message for feature 1")
// The logger1.debug message is not logged because the
// logLevelFilter is set to info
logger2.info(message: "info message for feature 2")

// Send logs to the Mobile Analytics Service
Logger.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**팁**: 개인정보 보호정책과 관련하여 릴리스 모드로 빌드된 애플리케이션에 대해 로거 출력을 사용하지 않도록 설정할 수 있습니다. 기본적으로 로거 클래스는 로그를 Xcode 콘솔에 인쇄합니다. 대상에 대한 빌드 설정에서 `-D RELEASE_BUILD` 플래그를 릴리스 빌드 구성의 **기타 Swift 플래그** 섹션에 추가하십시오.
    

#### Cordova
{: #enable-logger-sample-cordova notoc}

```
// Enable persisting logs
BMSLogger.storeLogs(true);

// Set the minimum log level to be printed and persisted
BMSLogger.setLogLevel(BMSLogger.INFO);

var logger1 = BMSLogger.getLogger("logger1");
var logger2 = BMSLogger.getLogger("logger2");

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service
BMSLogger.send();
BMSAnalytics.send();
```
{: codeblock}


<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs notoc}

The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android notoc}

```
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift notoc}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## 네트워크 요청 작성
{: #network-requests}

[네트워크 요청을 작성](/docs/mobile/sdk_network_request.html)하도록 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 구성할 수 있습니다. `BMSClient` 및 `BMSAnalytics`를 이미 초기화했는지 확인하십시오. 

<!--
#### Android
{: #android-network-requests notoc}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests notoc}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests notoc}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->


## 충돌 분석 보고
{: #report-crash-analytics}

분석 정보와 로그 정보를 {{site.data.keyword.mobileanalytics_short}}에 보내 [애플리케이션 충돌 데이터](app-monitoring.html#monitor-app-crash)를 볼 수 있습니다. 

`Analytics.send()` 메소드는 **충돌** 페이지의 **충돌 개요** 표와 **충돌** 표를 채웁니다. 초기화를 사용하고 분석을 수행할 프로세스를 전송하여 이 섹션의 차트를 사용할 수 있습니다. 특수 구성은 필요하지 않습니다. 

`Logger.send()` 메소드는 **문제점 해결** 페이지의 **충돌 요약** 표와 **충돌 세부사항** 표를 채웁니다. 애플리케이션 코드에 추가 명령문을 추가하여 애플리케이션이 이 섹션의 차트를 채울 로그를 저장하고 전송하도록 해야 합니다. 


### Android
{: #android-crash-statement notoc}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

[샘플 로거 사용법](sdk.html#android-logger-sample)을 참조하십시오. 


### iOS
{: #ios-crash-statement notoc}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

[샘플 로거 사용법](sdk.html##ios-logger-sample-swift2)을 참조하십시오. 


### Cordova
{: #cordova-crash-statement notoc}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

[샘플 로거 사용법](sdk.html##ios-logger-sample-swift2)을 참조하십시오. 


## 활성 사용자 추적
{: #trackingusers}

애플리케이션이 디바이스에서 고유 사용자를 인식할 수 있는 경우 선택적으로 활성 사용자의 사용자 이름을 {{site.data.keyword.mobileanalytics_short}}에 전달하여 애플리케이션을 적극적으로 사용 중인 사용자 수를 추적할 수 있습니다.  

`hasUserContext=true`를 설정해서 {{site.data.keyword.mobileanalytics_short}}를 초기화하여 사용자 추적을 사용으로 설정하십시오. 그렇지 않으면 {{site.data.keyword.mobileanalytics_short}}에서 디바이스당 한 명의 사용자만 캡처합니다.  


### Android
{: #android-tracking-users notoc}

다음 코드를 추가하여 사용자가 로그인하는 경우를 추적하십시오. 

```
Analytics.setUserIdentity("username");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

### iOS - Swift
{: #ios-tracking-users notoc}

다음 코드를 추가하여 사용자가 로그인하는 경우를 추적하십시오. 

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->


### Cordova
{: #cordova-tracking-users notoc}

다음 코드를 추가하여 사용자가 로그인하는 경우를 추적하십시오. 

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp notoc}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

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
    {: #mfp70 notoc}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values notoc}

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
    {: #mfp71 notoc}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values notoc}

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
      {: #mfp80 notoc}

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
{: #ignored-events notoc}
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


## 다음에 수행할 작업
{: #what-to-do-next notoc}

이제 {{site.data.keyword.mobileanalytics_short}} 콘솔로 이동하여 애플리케이션을 사용하는 새 디바이스 및 디바이스 총계 등의 사용 분석을 확인할 수 있습니다. <!--[creating custom charts](app-monitoring.html#custom-charts),-->[경보 설정](app-monitoring.html#alerts)과 [앱 충돌 모니터링](app-monitoring.html#monitor-app-crash)을 수행하여 애플리케이션을 모니터링할 수도 있습니다. 


# 관련 링크
{: #rellinks notoc}

## API 참조
{: #api notoc}

* [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
