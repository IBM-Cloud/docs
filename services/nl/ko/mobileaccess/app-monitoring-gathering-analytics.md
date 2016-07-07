---

copyright:
  years: 2015, 2016

---

# 사용량 분석 수집
{: #usage-analytics}
*마지막 업데이트 날짜: 2016년 5월 6일*
{: .last-updated}

사용량 분석을 기록하고 기록된 데이터를 {{site.data.keyword.amashort}} 서비스로 전송하도록 {{site.data.keyword.amashort}} 클라이언트 SDK를 구성할 수 있습니다.

**중요**: {{site.data.keyword.amashort}} 서비스의 모니터링 기능은 새로운 [{{site.data.keyword.mobileanalytics_short}} 서비스](https://console.ng.bluemix.net/catalog/services/mobile-analytics)로 마이그레이션될 계획입니다. 새로운 Swift SDK에서는 새 {{site.data.keyword.mobileanalytics_short}} 서비스를 활용하여, 훨씬 풍부한 분석 경험을 제공합니다. {{site.data.keyword.mobileanalytics_short}} 서비스는 올해 말 일반적으로 사용할 수 있도록 계획하여 현재 실험 단계에 있습니다. {{site.data.keyword.mobileanalytics_short}}가 사용 가능하게 되면 {{site.data.keyword.amashort}} 서비스의 모니터링 기능이 중단될 계획이므로 새로운 {{site.data.keyword.mobileanalytics_short}} 서비스와 Swift SDK를 사용하도록 애플리케이션이 마이그레이션되었는지 조사하는 것이 좋습니다. 

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

**중요**: Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix}} 모바일 서비스의 기본 SDK로 간주되므로 새로운 Swift SDK를 위해 올해 말에 중단될 계획입니다.

Objective-C SDK에서는 {{site.data.keyword.amashort}} 서비스의 모니터링 콘솔에 모니터링 데이터를 보고합니다. {{site.data.keyword.amashort}} 서비스의 모니터링 기능을 사용하는 경우 계속 Objective-C SDK를 사용하십시오.

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
**참고:** Cordova 애플리케이션을 개발 중인 경우 애플리케이션 라이프사이클 이벤트 레코딩을 사용으로 설정하려면 기본 API를 사용하십시오. 
