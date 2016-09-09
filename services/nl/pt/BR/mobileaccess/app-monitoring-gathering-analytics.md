---

copyright:
  years: 2015, 2016

---

# Reunindo análise de uso
{: #usage-analytics}
Última atualização: 6 de maio de 2016
{: .last-updated}

É possível configurar o {{site.data.keyword.amashort}} client SDK para registrar a análise de uso e enviar os dados registrados ao serviço {{site.data.keyword.amashort}}.

**Importante**: as funções de monitoramento do serviço {{site.data.keyword.amashort}} são planejadas para
serem migradas para o novo serviço do [ {{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). O novo Swift SDK alavanca o novo serviço {{site.data.keyword.mobileanalytics_short}}, que fornece uma experiência analítica muito mais rica. O serviço {{site.data.keyword.mobileanalytics_short}} está atualmente em fase experimental com planos de se tornar geralmente disponível posteriormente este ano. Recomendamos investigar a migração de seus aplicativos para usar o novo serviço {{site.data.keyword.mobileanalytics_short}} e o Swift SDK, uma vez que as funções de monitoramento do serviço {{site.data.keyword.amashort}} estão planejadas para serem descontinuadas quando o {{site.data.keyword.mobileanalytics_short}} estiver geralmente disponível.

**Nota:** Assegure-se de que tenha ativado a captura de criação de log antes de iniciar o registro da análise de uso.

Use as APIs a seguir para iniciar a gravação e o envio da análise de uso:

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

**Importante:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix}} Mobile Services, ele está planejado para ser descontinuado posteriormente este ano em favor do novo Swift SDK.

O Objective-C SDK relata dados de monitoramento para o Monitoring Console do serviço {{site.data.keyword.amashort}}. Se você depende das funções de monitoramento do serviço {{site.data.keyword.amashort}}, continue a usar o Objective-C SDK.

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
**Nota:** Quando estiver desenvolvendo aplicativos Cordova, use a API nativa para ativar a gravação do evento de ciclo de vida do aplicativo.
