---

copyright:
  years: 2015, 2016
  
---

# Supervisión de aplicaciones
{: #app-monitoring}
*Última actualización: 28 de junio de 2016*
{: .last-updated}

Además de las características de seguridad, {{site.data.keyword.amafull}} también ofrece capacidades de supervisión y análisis para aplicaciones móviles. Puede grabar registros de clientes y supervisar datos con el SDK del cliente de {{site.data.keyword.amashort}}. Los desarrolladores pueden controlar cuándo se envían estos datos al servicio de {{site.data.keyword.amashort}}. Todos los sucesos de seguridad, como un error de autenticación o una autenticación correcta, que se produce en el servicio de {{site.data.keyword.amashort}} se registran automáticamente.

**Nota**: está previsto migrar las funciones de supervisión del servicio {{site.data.keyword.amashort}} al nuevo servicio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). El nuevo SDK de Swift utiliza el nuevo servicio de {{site.data.keyword.mobileanalytics_short}}, que proporciona más prestaciones de análisis. El servicio {{site.data.keyword.mobileanalytics_short}} actualmente se encuentra en fase experimental y está previsto que esté disponible de forma general en unos meses. Se recomienda investigar la migración de sus aplicaciones para utilizar el nuevo servicio {{site.data.keyword.mobileanalytics_short}} y el SDK de Swift ya que está previsto que las funciones de supervisión del servicio {{site.data.keyword.amashort}} dejen de utilizarse cuando {{site.data.keyword.mobileanalytics_short}} pase a estar disponible de forma general.

Cuando se entregan los datos a {{site.data.keyword.amashort}}, puede utilizar el panel de control de supervisión de {{site.data.keyword.amashort}} para obtener información de analíticas sobre aplicaciones móviles, dispositivos y registros de clientes. La información sobre las solicitudes que efectúa la aplicación en los recursos protegidos por {{site.data.keyword.amashort}} queda registrada de forma predeterminada.

Los datos registrados automáticamente incluyen información como el número de autenticaciones, los dispositivos nuevos y los usuarios nuevos. Además puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que notifica la información siguiente:

### Estadísticas de uso de las aplicaciones móviles
{: #usage-stats}

Puede configurar las aplicaciones móviles para que registren sucesos del ciclo de vida de la aplicación y para que envíen estos datos al servicio de {{site.data.keyword.amashort}} con unas sencillas llamadas de API. Puede registrar el número de apps abiertas, notificaciones push recibidas, etc.

### Capturas de registros del lado de cliente
{: #client-side-logcapture}

Las aplicaciones en capo pueden, de manera ocasional, experimentar problemas que necesiten la atención de un desarrollador para ser solucionados. No obstante, muchas veces es difícil reproducir esos problemas. <!--in R&D.--> Los desarrolladores que trabajaron en el código pueden carecer del entorno del dispositivo exacto para realizar las pruebas. En estas situaciones, es útil poder recuperar los registros de depuración de los dispositivos cliente en el entorno en el que ocurren los problemas.

### Conservación de los datos capturados
{: #preserve-captureddata}

No es posible garantizar la conservación de todos los datos capturados en el lado del cliente. Es posible que los usuarios estén ejecutando la aplicación móvil fuera de línea y que, a la vez, estén acumulando datos de análisis y de registro capturados. Como el cliente está fuera de línea con un espacio de sistema de archivos limitado, se conservarán los sucesos de anotaciones más recientes en detrimento de los más antiguos. El desarrollador debe decidir cuándo se envían los datos capturados al servicio de {{site.data.keyword.amashort}} utilizando las API proporcionadas.

## Utilización del panel de control de supervisión de {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Abra el panel de control de {{site.data.keyword.Bluemix}} y pulse la aplicación {{site.data.keyword.Bluemix_notm}}.

2. Cuando se abra el panel de control de la aplicación de {{site.data.keyword.Bluemix_notm}}, pulse en un mosaico de {{site.data.keyword.amashort}}.

3. En el panel de control de {{site.data.keyword.amashort}}, pulse en el enlace **Supervisión** del menú de la izquierda.

## Habilitación, configuración y uso del registrador
{: #enable-logger}

El SDK del cliente de {{site.data.keyword.amashort}} proporciona una infraestructura de registro que es similar a otras infraestructuras que es posible que conozca, como `java.util.logging` o `log4j`. La infraestructura de registro admite varias instancias de registrador por paquete, diferentes niveles de registro, captura de los seguimientos de pila en caso de bloqueo de la aplicación y más.

También puede configurar que los datos de registro persistan en un almacén local, que pueda enviarse al servicio de {{site.data.keyword.amashort}} a petición.

La infraestructura de registro del SDK del cliente de {{site.data.keyword.amashort}} admite los siguientes niveles de registro, que aparecen de menos a más detallados, con las directrices de uso recomendadas:

* `FATAL`: se usa para bloqueos no recuperables. El nivel FATAL se reserva para errores no recuperables de registro, que aparecen como "bloqueo de la aplicación" a los usuarios.
* `ERROR`: se usa para excepciones o errores de protocolo de red no esperados.
* `WARN`: para registrar avisos de uso que no se consideran errores críticos, como el uso de API obsoletas o la respuesta de red lenta.
* `INFO`: se usa para notificar sucesos de inicialización y otros datos que pueden ser útiles.
* `DEBUG`: se usa para notificar sentencias de depuración para que los desarrolladores puedan resolver defectos de la aplicación.

Asegúrese de haber inicializado el SDK del cliente de {{site.data.keyword.amashort}} antes de utilizar la infraestructura de registro. Los ejemplos siguientes demuestran el uso básico de una infraestructura de registro del SDK del cliente de {{site.data.keyword.amashort}}.

**Importante**: está previsto migrar las funciones de supervisión del servicio {{site.data.keyword.amashort}} al nuevo servicio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). El nuevo SDK de Swift utiliza el nuevo servicio de {{site.data.keyword.mobileanalytics_short}}, que proporciona más prestaciones de análisis. El servicio {{site.data.keyword.mobileanalytics_short}} actualmente se encuentra en fase experimental y está previsto que esté disponible de forma general en unos meses. Se recomienda investigar la migración de sus aplicaciones para utilizar el nuevo servicio {{site.data.keyword.mobileanalytics_short}} y el SDK de Swift ya que está previsto que las funciones de supervisión del servicio {{site.data.keyword.amashort}} dejen de utilizarse cuando {{site.data.keyword.mobileanalytics_short}} pase a estar disponible de forma general.

#### Android
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

#### iOS - Objective-C
{: #enable-logger-objectc}

**Importante**: si bien el SDK de Objective-C sigue recibiendo soporte y sigue considerándose el SDK principal para {{site.data.keyword.Bluemix}} Mobile Services, está previsto dejar de mantenerlo en unos meses en favor del nuevo SDK de Swift.

El SDK de Objective-C notifica datos de supervisión a la Consola de supervisión del servicio {{site.data.keyword.amashort}}. Si confía en las funciones de supervisión del servicio {{site.data.keyword.amashort}}, siga utilizando el SDK de Objective-C.

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

#### iOS - Swift
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

**Nota:** el SDK del cliente de {{site.data.keyword.amashort}} se implementa con Objective-C; por ello, es posible que tenga que añadir el archivo `IMFLoggerExtension.swift` al proyecto de Swift para utilizar la anterior API de registrador. Este archivo se encuentra en el [archivo del SDK del cliente de {{site.data.keyword.amashort}}](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


#### Cordova
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

Encontrar los métodos siguientes en las clases del registrador:

* `setCapture`: habilita o inhabilita el envío posterior de la información de registro persistente al servicio de {{site.data.keyword.amashort}}.
* `setLevel`: define el nivel mínimo de registro para guardar mensajes de registro.
* `send`: envía registros persistentes al servicio de {{site.data.keyword.amashort}}.

Por ejemplo, cuando la captura está en ON y el nivel de registro está configurado en FATAL, el registrador capturará excepciones no percibidas. A menudo, estas excepciones no percibidas aparecen como bloqueos de aplicación a los usuarios, pero no capturan ningún registro que conduzca al suceso de bloqueo. Como alternativa, un nivel más detallado garantiza que también se capturen los registros que llevan a una entrada FATAL del registrador, como WARN o ERROR.

**Nota:** en [SDK, ejemplos y referencias de API](sdks-samples-apis.html) encontrará referencias de la API del registrador. La API del registrador forma parte del Core del SDK del cliente de {{site.data.keyword.amashort}}.


### Ejemplo de uso
{: #sample-logger-usage}

Los siguientes fragmentos de código son un ejemplo del uso del registrador:

#### Android
{: #enable-logger-sample-android}

```Java
// Habilite registros persistentes
Logger.setCapture(true);

// Defina el nivel de registro mínimo que imprimir y persistir
Logger.setLevel(Logger.LEVEL.INFO);

// Cree dos instancias del registrador
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Registre mensajes con diferentes niveles
logger1.debug("debug message");
logger2.info("info message");

// Envíe registros persistentes al servicio de {{site.data.keyword.amashort}}
Logger.send();
```

#### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Habilite registros persistentes
[IMFLogger setCapture:YES];

// Empiece a capturar excepciones no capturadas
[IMFLogger captureUncaughtExceptions];

// Define el nivel de registro mínimo que imprimir y persistir
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Cree dos instancias de registrador
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Registre mensajes con diferentes niveles
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Envíe registros persistentes al servicio de {{site.data.keyword.amashort}}
[IMFLogger send];
```

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Habilite los registros persistentes
IMFLogger.setCapture(true)

// Inicie la captura de excepciones no capturadas
IMFLogger.captureUncaughtExceptions()

// Defina el nivel de registro mínimo que imprimir y persistir
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Cree dos instancias de registro
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Registre mensajes con niveles diferentes
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Envíe registros persistentes al servicio de {{site.data.keyword.amashort}}
IMFLogger.send()

```

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Habilite registros persistentes
MFPLogger.setCapture(true);

// Defina el nivel de registro mínimo que imprimir y persistir
MFPLogger.setLevel(MFPLogger.INFO);

// Cree dos instancias del registrador
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Registre mensajes con diferentes niveles
logger1.debug("debug message");
logger2.info("info message");

// Envíe registros persistentes al servicio de {{site.data.keyword.amashort}}
MFPLogger.send(success, failure);
```

### Habilitación de los registros internos del SDK del cliente de {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Esta característica está disponible actualmente en la versión para Android del SDK del cliente de {{site.data.keyword.amashort}}.

El SDK del cliente de {{site.data.keyword.amashort}} mejora la experiencia de desarrollo porque no hace aumentar innecesariamente la salida de LogCat con los mensajes internos de depuración. Por tanto, de forma predeterminada los mensajes internos de registro que produce el SDK del {{site.data.keyword.amashort}} no se imprimen a nivel de depuración. Puede habilitar que se impriman estos mensajes del SDK del cliente de {{site.data.keyword.amashort}} con la API siguiente:


```
Logger.setSDKInternalLoggingEnabled(true);
```

## Recopilación de analíticas de uso
{: #usage-analytics}

Puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que registre analíticas y envíe los datos registrados al servicio de {{site.data.keyword.amashort}}.

**Importante**: está previsto migrar las funciones de supervisión del servicio {{site.data.keyword.amashort}} al nuevo servicio [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). El nuevo SDK de Swift utiliza el nuevo servicio de {{site.data.keyword.mobileanalytics_short}}, que proporciona más prestaciones de análisis. El servicio {{site.data.keyword.mobileanalytics_short}} actualmente se encuentra en fase experimental y está previsto que esté disponible de forma general en unos meses. Se recomienda investigar la migración de sus aplicaciones para utilizar el nuevo servicio {{site.data.keyword.mobileanalytics_short}} y el SDK de Swift ya que está previsto que las funciones de supervisión del servicio {{site.data.keyword.amashort}} dejen de utilizarse cuando {{site.data.keyword.mobileanalytics_short}} pase a estar disponible de forma general.

**Nota:** asegúrese de haber habilitado la captura de registro antes de empezar a registrar las analíticas de uso.

Utilice las API siguientes para empezar el registro y envío de analíticas de uso:

#### Android
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

#### iOS - Objective-C
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

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Habilite el registro de analíticas de uso
IMFAnalytics.sharedInstance().setEnabled(true)

// Empiece registrando sucesos de ciclo de vida de la aplicación
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Habilite el registro de analíticas de uso
MFPAnalytics.enable();

// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
MFPAnalytics.send();
```
**Nota:** cuando esté desarrollando aplicaciones de Cordova, utilice la API nativa para habilitar el registro de sucesos de ciclo de vida de la aplicación.
