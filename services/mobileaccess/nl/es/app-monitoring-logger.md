---

copyright:
  years: 2015, 2016
  
---

# Habilitación, configuración y uso del registrador
{: #enable-logger}
Última actualización: 6 de mayo de 2016
{: .last-updated}

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

**Nota:** el SDK del cliente de {{site.data.keyword.amashort}} se implementa con Objective-C; por ello, es posible que tenga que añadir el archivo `IMFLoggerExtension.swift` al proyecto de Swift para utilizar la anterior API de registrador. Este archivo se encuentra en el [archivo del SDK del cliente de {{site.data.keyword.amashort}}](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


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

Encontrar los métodos siguientes en las clases del registrador:

* `setCapture`: habilita o inhabilita el envío posterior de la información de registro persistente al servicio de {{site.data.keyword.amashort}}.
* `setLevel`: define el nivel mínimo de registro para guardar mensajes de registro.
* `send`: envía registros persistentes al servicio de {{site.data.keyword.amashort}}.

Por ejemplo, cuando la captura está en ON y el nivel de registro está configurado en FATAL, el registrador capturará excepciones no percibidas. A menudo, estas excepciones no percibidas aparecen como bloqueos de aplicación a los usuarios, pero no capturan ningún registro que conduzca al suceso de bloqueo. Como alternativa, un nivel más detallado garantiza que también se capturen los registros que llevan a una entrada FATAL del registrador, como WARN o ERROR.

**Nota:** en [SDK, ejemplos y referencias de API](sdks-samples-apis.html) encontrará referencias de la API del registrador. La API del registrador forma parte del Core del SDK del cliente de {{site.data.keyword.amashort}}.


## Ejemplo de uso
{: #sample-logger-usage}

Los siguientes fragmentos de código son un ejemplo del uso del registrador:

### Android
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

### iOS - Objective-C
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

### iOS - Swift
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

### Cordova
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

## Habilitación de los registros internos del SDK del cliente de {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Esta característica está disponible actualmente en la versión para Android del SDK del cliente de {{site.data.keyword.amashort}}.

El SDK del cliente de {{site.data.keyword.amashort}} mejora la experiencia de desarrollo porque no hace aumentar innecesariamente la salida de LogCat con los mensajes internos de depuración. Por tanto, de forma predeterminada los mensajes internos de registro que produce el SDK del {{site.data.keyword.amashort}} no se imprimen a nivel de depuración. Puede habilitar que se impriman estos mensajes del SDK del cliente de {{site.data.keyword.amashort}} con la API siguiente:


```
Logger.setSDKInternalLoggingEnabled(true);
```
