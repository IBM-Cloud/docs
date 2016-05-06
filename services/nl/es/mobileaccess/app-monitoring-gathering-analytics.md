---

copyright:
  años: 2015, 2016

---

# Recopilación de analíticas de uso
{: #usage-analytics}

Puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que registre analíticas y envíe los datos registrados al servicio de {{site.data.keyword.amashort}}.

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
