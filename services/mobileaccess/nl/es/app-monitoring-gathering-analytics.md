---

copyright:
  years: 2015, 2016

---

# Recopilación de analíticas de uso
{: #usage-analytics}
Última actualización: 6 de mayo de 2016
{: .last-updated}

Puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que registre analíticas y envíe los datos registrados al servicio de {{site.data.keyword.amashort}}.

**Importante**: está previsto migrar las funciones de supervisión del servicio {{site.data.keyword.amashort}} al nuevo servicio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). El nuevo SDK de Swift utiliza el nuevo servicio de {{site.data.keyword.mobileanalytics_short}}, que proporciona más prestaciones de análisis. El servicio {{site.data.keyword.mobileanalytics_short}} actualmente se encuentra en fase experimental y está previsto que esté disponible de forma general en unos meses. Se recomienda investigar la migración de sus aplicaciones para utilizar el nuevo servicio {{site.data.keyword.mobileanalytics_short}} y el SDK de Swift ya que está previsto que las funciones de supervisión del servicio {{site.data.keyword.amashort}} dejen de utilizarse cuando {{site.data.keyword.mobileanalytics_short}} pase a estar disponible de forma general.

**Nota:** asegúrese de haber habilitado la captura de registro antes de empezar a registrar las analíticas de uso.

Utilice las API siguientes para empezar el registro y envío de analíticas de uso:

### Android
{: #usage-analytics-android}

```Java
// Habilite el registro de analíticas de uso
MFPAnalytics.enable();

// Empiece registrando el tiempo de inicio de la aplicación
// Añada este código al método onCreate de la actividad principal
MFPAnalytics.startLoggingApplicationStartup();

// Registre la duración del tiempo de inicio de la aplicación
// Añada este código al método onStart de la actividad principal
MFPAnalytics.logApplicationStartup();

// Registre los sucesos de fondo y primer plano de la aplicación
// Añada este código a los métodos onPause y onResume de la actividad principal
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

**Importante**: si bien el SDK de Objective-C sigue recibiendo soporte y sigue considerándose el SDK principal para {{site.data.keyword.Bluemix}} Mobile Services, está previsto dejar de mantenerlo en unos meses en favor del nuevo SDK de Swift.

El SDK de Objective-C notifica datos de supervisión a la Consola de supervisión del servicio {{site.data.keyword.amashort}}. Si confía en las funciones de supervisión del servicio {{site.data.keyword.amashort}}, siga utilizando el SDK de Objective-C.

```Objective-C
// Habilite el registro de analíticas de uso
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Empiece a registrar suceso de ciclo de vida de la aplicación
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Habilite el registro de analíticas de uso
IMFAnalytics.sharedInstance().setEnabled(true)

// Empiece registrando sucesos de ciclo de vida de la aplicación
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Habilite el registro de analíticas de uso
MFPAnalytics.enable();

// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
MFPAnalytics.send();
```
**Nota:** cuando esté desarrollando aplicaciones de Cordova, utilice la API nativa para habilitar el registro de sucesos de ciclo de vida de la aplicación.
