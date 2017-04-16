---

copyright:
  years: 2015, 2016
  
---

# 애플리케이션 모니터링
{: #app-monitoring}
마지막 업데이트 날짜: 2016년 9월 22일
{: .last-updated}

{{site.data.keyword.amafull}}는 보안 기능 이외에도 모바일 애플리케이션에 대한 모니터링 및 분석을 제공합니다. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 클라이언트 로그 및 모니터 데이터를 기록할 수 있습니다. 개발자는 이 데이터를 {{site.data.keyword.amashort}} 서비스로 전송할 시기를 제어할 수 있습니다. {{site.data.keyword.amashort}} 서비스에서 발생하는 모든 보안 이벤트(예: 인증 성공 또는 실패)는 자동으로 로깅됩니다. 
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

데이터가 {{site.data.keyword.amashort}}에 전달되면 {{site.data.keyword.amashort}} 모니터링 대시보드를 사용하여 모바일 애플리케이션, 디바이스 및 클라이언트 로그에 대한 분석 정보를 얻을 수 있습니다. 기본적으로 애플리케이션이 {{site.data.keyword.amashort}}에서 보호되는 리소스에 대해 작성하는 요청에 대한 정보가 기록됩니다.

자동으로 기록되는 데이터에는 인증, 새 디바이스 및 새 사용자 수와 같은 정보가 포함됩니다. 또한 다음 정보를 보고하도록 {{site.data.keyword.amashort}} 클라이언트 SDK를 구성할 수 있습니다.

### 모바일 애플리케이션의 사용 통계
{: #usage-stats}

몇 번의 단순 API 호출로 애플리케이션 라이프사이클 이벤트를 기록하고 기록된 데이터를 {{site.data.keyword.amashort}} 서비스로 전송하도록 모바일 애플리케이션을 구성할 수 있습니다. 앱 열림, 수신된 푸시 알림의 수 등을 기록할 수 있습니다. 

### 클라이언트측 로그 캡처
{: #client-side-logcapture}

실제 사용되는 애플리케이션에는 때때로 수정하는 데 개발자의 노력이 필요한 문제점이 발생하기도 합니다. 이러한 문제점을 다시 만들어 내기는 어렵습니다. 코드를 작업한 개발자는 문제를 테스트할 수 있는 환경이나 정확한 디바이스가 부족할 수 있습니다. 이러한 경우, 로그가 작성되는 환경에서 문제가 발생한 경우라 클라이언트 디바이스에서 디버그 로그를 검색하는 것이 도움이 됩니다. 

### 캡처한 데이터 보존
{: #preserve-captureddata}

캡처한 모든 데이터를 클라이언트측에 보존할 수 있는 방법은 없습니다. 사용자가 오프라인에서 모바일 애플리케이션을 실행하고 동시에 캡처한 분석 및 로그 데이터를 누적할 수 있습니다. 클라이언트가 오프라인인 경우 파일 시스템 공간에 제한이 있기 때문에, 이전에 로그된 이벤트는 더 최근에 로그된 이벤트를 유지하기 위해 영구 제거해야 합니다. 개발자가 제공된 API를 사용하여 캡처한 데이터를 {{site.data.keyword.amashort}} 서비스로 전송할 시기를 결정해야 합니다. 

## {{site.data.keyword.amashort}} 모니터링 대시보드 사용
{: #monitoring-dashboard}

1. {{site.data.keyword.Bluemix}} 대시보드를 열고 {{site.data.keyword.Bluemix_notm}} 애플리케이션을 클릭하십시오. 

2. {{site.data.keyword.Bluemix_notm}} 애플리케이션 대시보드가 열리면 {{site.data.keyword.amashort}} 타일을 클릭하십시오. 

3. {{site.data.keyword.amashort}} 대시보드 탐색에서 **모니터링** 단추를 클릭하십시오.


## 로거 활성화, 구성 및 사용
{: #enable-logger}

{{site.data.keyword.amashort}} 클라이언트 SDK는 `java.util.logging` 또는 `log4j`와 같이 익숙한 다른 로그 프레임워크와 유사한 로깅 프레임워크를 제공합니다. 로깅 프레임워크는 여러 개의 패키지별 로거 인스턴스, 여러 로그 레벨, 애플리케이션 충돌에 대한 스택 추적 캡처 등을 지원합니다. 

또한 로깅된 데이터를 로컬 저장소에 보존하도록 구성하고 요청 시 {{site.data.keyword.amashort}} 서비스로 전송할 수도 있습니다.

{{site.data.keyword.amashort}} 클라이언트 SDK 로깅 프레임워크는 다음과 같은 로그 레벨(최소부터 최대 상세 레벨 순서로 나열됨)을 권장 사용 가이드라인과 함께 지원합니다.

* `FATAL` - 복구할 수 없는 충돌 또는 정지에 사용합니다. FATAL 레벨은 복구할 수 없는 오류를 로깅하는 데 사용하고, 사용자에게는 애플리케이션 충돌로 표시됩니다. 
* `ERROR` - 예상치 못한 예외 또는 예상치 못한 네트워크 프로토콜 오류에 사용합니다.
* `WARN` - 더 이상 사용되지 않는 API 사용 또는 느린 네트워크 응답과 같이 중요한 오류로 간주되지 않는 사용 경고를 로그합니다.
* `INFO` - 유용할 수 있는 초기화 이벤트 및 기타 데이터를 보고하는 데 사용합니다.
* `DEBUG` - 개발자가 애플리케이션 결함을 해결하는 데 도움이 되도록 디버그 명령문을 보고하는 데 사용합니다.

#### 로그 레벨 시나리오
{: #log-level-scenario}

로거 레벨이 `FATAL`로 구성되면 로거가 미발견 예외를 캡처하지만 충돌 이벤트까지 이어지는 로그는 캡처하지 않습니다. 보다 상세한 로거 레벨을 설정하여 `FATAL` 로거 항목으로 이어지는 로그(예: `WARN`, `ERROR`)도 캡처할 수 있습니다. 

로깅 프레임워크를 사용하기 전에 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화했는지 확인하십시오. 다음 샘플은 {{site.data.keyword.amashort}} 클라이언트 SDK 로깅 프레임워크의 기본 사용법을 보여줍니다.

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

**bluemixRegion** 매개변수는 사용 중인 Bluemix 배치(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK`)를 지정합니다.  

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // You can change the region
Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)

let logger = Logger.logger(forName: "myLogger")

logger.debug(“debug info")
logger.info(“info message")
logger.warn(“warning message")
logger.error(“error message")
logger.fatal(“fatal message")
```
{: codeblock}
<!--
**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).
-->

#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

로거 클래스에서 다음과 같은 추가 메소드를 찾을 수 있습니다. 

* `setCapture` - 나중에 {{site.data.keyword.amashort}} 서비스로 전송할 로그 정보 보존을 사용 또는 사용 안함으로 설정합니다.
* `setLevel` - 로그 메시지를 저장할 최소 로그 레벨을 설정합니다.
* `send` - 보존된 로그를 {{site.data.keyword.amashort}} 서비스로 전송합니다.

예를 들어, 캡처가 설정되어 있고 로거 레벨이 FATAL로 구성되어 있는 경우 로거는 미발견 예외를 캡처합니다. 미발견 예외는 종종 사용자에게 애플리케이션 충돌로 표시되지만, 충돌 이벤트까지 이어지는 로그는 캡처하지 않습니다. 그 대신 로거 레벨을 더 자세하게 지정하면 FATAL 로거 항목으로 이어지는 로그(예: WARN 및 ERROR)도 캡처됩니다. 

**참고: ** 플랫폼별 전체 로거 API 참조는 [SDK, 샘플 및 API 참조](sdks-samples-apis.html)에 나와 있습니다. 로거 API는 {{site.data.keyword.amashort}} 클라이언트 SDK 코어의 일부입니다.


### 샘플 로거 사용법
{: #sample-logger-usage}

다음 코드 스니펫은 샘플 로거 사용법을 보여줍니다. 

#### Android
{: #enable-logger-sample-android}

```Java
// Configure Logger to save logs to the device so that they 
// can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional)
// The default setting is Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Create two logger instances
// You can create multiple log instances to organize your logs
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Log messages with different levels
// Debug message for feature 1
// Info message for feature 2
logger1.debug("debug message"); 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message");

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// Log messages with different levels
logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info
logger2.info("info message for feature 2")

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
BMSLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
BMSLogger.setLevel(BMSLogger.INFO);

// Create two logger instances
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
BMSLogger.send(success, failure);
```
{: codeblock}

### {{site.data.keyword.amashort}} 클라이언트 SDK 내부 로그 사용
{: #enable-logger-sdklogs}
이 기능은 현재 {{site.data.keyword.amashort}} 클라이언트 SDK의 Android 버전에서만 사용할 수 있습니다.

{{site.data.keyword.amashort}} 클라이언트 SDK는 내부 디버그 메시지를 포함한 Logcat 출력을 불필요하게 늘리지 않음으로써 더 나은 개발 경험을 제공합니다. 따라서 기본적으로 {{site.data.keyword.amashort}} SDK가 DEBUG 레벨을 사용하여 생성하는 내부 로그 메시지는 인쇄되지 않습니다. 다음 API를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK의 내부 로그 메시지를 모두 인쇄하도록 설정할 수 있습니다.


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## 사용량 분석 수집
{: #usage-analytics}

사용량 분석을 기록하고 기록된 데이터를 {{site.data.keyword.amashort}} 서비스로 전송하도록 {{site.data.keyword.amashort}} 클라이언트 SDK를 구성할 수 있습니다.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**참고: ** 사용량 분석을 기록하기 전에 로깅 캡처를 사용으로 설정했는지 확인하십시오. 

사용량 분석 기록과 전송을 시작하려면 다음 API를 사용하십시오. 

#### Android
{: #usage-analytics-android}

```Java
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false

// Enable recording of usage analytics
Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
BMSAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
BMSAnalytics.send();
```
{: codeblock}

**참고:** Cordova 애플리케이션을 개발 중인 경우 애플리케이션 라이프사이클 이벤트 레코딩을 사용으로 설정하려면 기본 API를 사용하십시오.
