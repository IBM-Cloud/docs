---

copyright:
  years: 2015, 2016
  
---

# 로거 활성화, 구성 및 사용
{: #enable-logger}

{{site.data.keyword.amashort}} 클라이언트 SDK는 `java.util.logging` 또는 `log4j`와
같이 익숙한 다른 로그 프레임워크와 유사한 로깅 프레임워크를 제공합니다. 로깅 프레임워크는
여러 개의 패키지별 로거 인스턴스, 여러 로그 레벨, 애플리케이션 충돌에 대한 스택 추적 캡처 등을
지원합니다. 

또한 로깅된 데이터를 로컬 저장소에 보존하도록 구성하고 요청 시 {{site.data.keyword.amashort}} 서비스로 전송할 수도 있습니다.

{{site.data.keyword.amashort}} 클라이언트 SDK 로깅 프레임워크는 다음과 같은
로그 레벨(로그 수준이 가장 낮은 레벨부터 가장 자세한 레벨까지)을 권장 사용 가이드라인과 함께 지원합니다. 

* `FATAL` - 복구할 수 없는 충돌 또는 정지에 사용합니다. FATAL 레벨은
복구할 수 없는 오류를 로깅하는 데 사용하고, 사용자에게는 애플리케이션 충돌로
표시됩니다. 
* `ERROR` - 예상치 못한 예외 또는 예상치 못한 네트워크 프로토콜 오류에 사용합니다.
* `WARN` - 더 이상 사용되지 않는 API 사용 또는 느린 네트워크 응답과 같이 중요한 오류로 간주되지 않는 사용 경고를 로그합니다.
* `INFO` - 유용할 수 있는 초기화 이벤트 및 기타 데이터를 보고하는 데 사용합니다.
* `DEBUG` - 개발자가 애플리케이션 결함을 해결하는 데 도움이 되도록 디버그 명령문을 보고하는 데 사용합니다.

로깅 프레임워크를 사용하기 전에 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화했는지 확인하십시오.
다음 샘플은 {{site.data.keyword.amashort}} 클라이언트 SDK 로깅 프레임워크의 기본 사용법을
보여줍니다. 

### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

### iOS - Objective-C
{: #enable-logger-objectc}

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**참고:** {{site.data.keyword.amashort}} 클라이언트 SDK는 Objective-C로 구현되므로,
이전 로거 API를 사용하려면 `IMFLoggerExtension.swift` 파일을 Swift 프로젝트에 추가해야 할 수도 있습니다.
이 파일은 [Mobile Client Access
클라이언트 SDK 아카이브](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)에 있습니다. 


### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");


logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");

```

로거 클래스에서 다음과 같은 추가 메소드를 찾을 수 있습니다. 

* `setCapture` - 나중에 {{site.data.keyword.amashort}} 서비스로 전송할 로그 정보 보존을 사용 또는 사용 안함으로 설정합니다.
* `setLevel` - 로그 메시지를 저장할 최소 로그 레벨을 설정합니다.
* `send` - 보존된 로그를 {{site.data.keyword.amashort}} 서비스로 전송합니다.

예를 들어, 캡처가 설정되어 있고 로거 레벨이 FATAL로 구성되어 있는 경우
로거는 미발견 예외를 캡처합니다. 미발견 예외는 종종 사용자에게 애플리케이션 충돌로 표시되지만,
충돌 이벤트까지 이어지는 로그는 캡처하지 않습니다. 그 대신 로거 레벨을 더 자세하게 지정하면
FATAL 로거 항목으로 이어지는 로그(예: WARN 및 ERROR)도 캡처됩니다. 

**참고: ** 플랫폼별 전체 로거 API 참조는 [SDK, 샘플,
API 참조](sdks-samples-apis.html)에 나와 있습니다. 로거 API는 {{site.data.keyword.amashort}} 클라이언트 SDK 코어의 일부입니다. 


## 샘플 사용법
{: #sample-logger-usage}

다음 코드 스니펫은 샘플 로거 사용법을 보여줍니다. 

### Android
{: #enable-logger-sample-android}

```Java
// Enable persisting logs
Logger.setCapture(true);

// Set the minimum log level to be printed and persisted
Logger.setLevel(Logger.LEVEL.INFO);

// Create two logger instances
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
Logger.send();
```

### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Enable persisting logs
[IMFLogger setCapture:YES];

// Start capturing uncaught exceptions
[IMFLogger captureUncaughtExceptions];

// Set the minimum log level to be printed and persisted
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Create two logger instances
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Log messages with different levels
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Send persisted logs to the {{site.data.keyword.amashort}} service
[IMFLogger send];
```

### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Enable persisting logs
IMFLogger.setCapture(true)

// Start capturing uncaught exceptions
IMFLogger.captureUncaughtExceptions()

// Set the minimum log level to be printed and persisted
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Create two logger instances
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Log messages with different levels
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Send persisted logs to the {{site.data.keyword.amashort}} service
IMFLogger.send()

```

### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
MFPLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
MFPLogger.setLevel(MFPLogger.INFO);

// Create two logger instances
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug ("debug message");
logger2.info ("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
MFPLogger.send(success, failure);
```

## {{site.data.keyword.amashort}} 클라이언트 SDK 내부 로그 사용
{: #enable-logger-sdklogs}
이 기능은 현재 {{site.data.keyword.amashort}} 클라이언트 SDK의 Android 버전에서만 사용할 수 있습니다. 

{{site.data.keyword.amashort}} 클라이언트 SDK는 뛰어난 개발 환경을 제공하기 위해
내부 디버그 메시지를 포함한 Logcat 출력을 불필요하게 많이 생성하지 않습니다. 따라서 기본적으로
{{site.data.keyword.amashort}} SDK가 DEBUG 레벨을 사용하여 생성하는 내부 로그 메시지는
인쇄되지 않습니다. 다음 API를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK의
내부 로그 메시지를 모두 인쇄하도록 설정할 수 있습니다. 


```
Logger.setSDKInternalLoggingEnabled(true);
```
