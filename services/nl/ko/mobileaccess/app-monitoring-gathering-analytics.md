---

copyright:
  years: 2015, 2016

---

# 사용량 분석 수집
{: #usage-analytics}

사용량 분석을 기록하고 기록된 데이터를 {{site.data.keyword.amashort}} 서비스로 전송하도록
{{site.data.keyword.amashort}} 클라이언트 SDK를 구성할 수 있습니다. 

**참고: ** 사용량 분석을 기록하기 전에 로깅 캡처를 사용으로 설정했는지 확인하십시오. 

사용량 분석 기록과 전송을 시작하려면 다음 API를 사용하십시오. 

### Android
{: #usage-analytics-android}

```Java
// Enable recording of usage analytics
MFPAnalytics.enable();

// Start recording application startup time
// Add this code in the onCreate method of your main Activity
MFPAnalytics.startLoggingApplicationStartup();

// Record the duration of application startup
// Add this code in the onStart method of your main Activity
MFPAnalytics.logApplicationStartup();

// Record application foreground and background events
// Add this code in the onPause and onResume methods of your main Activity
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

```Objective-C
// Enable usage analytics recording
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Start recording application lifecycle events
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Enable usage analytics recording
IMFAnalytics.sharedInstance().setEnabled(true)

// Start recording application lifecycle events
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
MFPAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
MFPAnalytics.send();
```
**참고:** Cordova 애플리케이션을 개발 중인 경우 애플리케이션 라이프사이클 이벤트 레코딩을
사용으로 설정하려면 기본 API를 사용하십시오. 
