---

copyright:
  years: 2015, 2016
  
---

# Supervisión de aplicaciones
{: #app-monitoring}
Última actualización: 22 de septiembre de 2016
{: .last-updated}

Además de las características de seguridad, {{site.data.keyword.amafull}} también ofrece capacidades de supervisión y análisis para aplicaciones móviles. Puede grabar registros de clientes y supervisar datos con el SDK del cliente de {{site.data.keyword.amashort}}. Los desarrolladores pueden controlar cuándo se envían estos datos al servicio de {{site.data.keyword.amashort}}. Todos los sucesos de seguridad, como un error de autenticación o una autenticación correcta, que se produce en el servicio de {{site.data.keyword.amashort}} se registran automáticamente.
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

Cuando se entregan los datos a {{site.data.keyword.amashort}}, puede utilizar el panel de control de supervisión de {{site.data.keyword.amashort}} para obtener información de analíticas sobre aplicaciones móviles, dispositivos y registros de clientes. La información sobre las solicitudes que efectúa la aplicación en los recursos protegidos por {{site.data.keyword.amashort}} queda registrada de forma predeterminada.

Los datos registrados automáticamente incluyen información como el número de autenticaciones, los dispositivos nuevos y los usuarios nuevos. Además puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que notifica la información siguiente:

### Estadísticas de uso de las aplicaciones móviles
{: #usage-stats}

Puede configurar las aplicaciones móviles para que registren sucesos del ciclo de vida de la aplicación y para que envíen estos datos al servicio de {{site.data.keyword.amashort}} con unas sencillas llamadas de API. Puede registrar el número de apps abiertas, notificaciones push recibidas, etc.

### Capturas de registros del lado de cliente
{: #client-side-logcapture}

Las aplicaciones en capo pueden, de manera ocasional, experimentar problemas que necesiten la atención de un desarrollador para ser solucionados. No obstante, muchas veces es difícil reproducir esos problemas. Los desarrolladores que trabajaron en el código pueden carecer del entorno del dispositivo exacto para realizar las pruebas. En estas situaciones, es útil poder recuperar los registros de depuración de los dispositivos cliente en el entorno en el que ocurren los problemas.

### Conservación de los datos capturados
{: #preserve-captureddata}

No es posible garantizar la conservación de todos los datos capturados en el lado del cliente. Es posible que los usuarios estén ejecutando la aplicación móvil fuera de línea y que, a la vez, estén acumulando datos de análisis y de registro capturados. Como el cliente está fuera de línea con un espacio de sistema de archivos limitado, se conservarán los sucesos de anotaciones más recientes en detrimento de los más antiguos. El desarrollador debe decidir cuándo se envían los datos capturados al servicio de {{site.data.keyword.amashort}} utilizando las API proporcionadas.

## Utilización del panel de control de supervisión de {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Abra el panel de control de {{site.data.keyword.Bluemix}} y pulse la aplicación {{site.data.keyword.Bluemix_notm}}.

2. Cuando se abra el panel de control de la aplicación de {{site.data.keyword.Bluemix_notm}}, pulse en un icono de {{site.data.keyword.amashort}}.

3. Pulse el botón **Supervisión** en la navegación del panel de control de {{site.data.keyword.amashort}}.


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

#### Caso de ejemplo de nivel de registro
{: #log-level-scenario}

Cuando el nivel del registrador está configurado en `FATAL`, el registrador captura excepciones no capturadas, pero no captura ningún registro que lleve al suceso de bloqueo. Puede establecer un nivel de registrador más detallado para asegurarse de que también se capturen los registros que pueden llevar a una entrada de registrador `FATAL`, como por ejemplo `WARN` y `ERROR`.

Asegúrese de haber inicializado el SDK del cliente de {{site.data.keyword.amashort}} antes de utilizar la infraestructura de registro. Los ejemplos siguientes demuestran el uso básico de una infraestructura de registro del SDK del cliente de {{site.data.keyword.amashort}}.

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Asegúrese de que apunta a su región

Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

El parámetro **bluemixRegion** especifica qué despliegue de Bluemix está utilizando, por ejemplo, `BMSClient.REGION_US_SOUTH` y `BMSClient.REGION_UK`. 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // Puede cambiar la región
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
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // Puede cambiar la región

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

Encontrar los métodos siguientes en las clases del registrador:

* `setCapture`: habilita o inhabilita el envío posterior de la información de registro persistente al servicio de {{site.data.keyword.amashort}}.
* `setLevel`: define el nivel mínimo de registro para guardar mensajes de registro.
* `send`: envía registros persistentes al servicio de {{site.data.keyword.amashort}}.

Por ejemplo, cuando la captura está en ON y el nivel de registro está configurado en FATAL, el registrador capturará excepciones no percibidas. A menudo, estas excepciones no percibidas aparecen como bloqueos de aplicación a los usuarios, pero no capturan ningún registro que conduzca al suceso de bloqueo. Como alternativa, un nivel más detallado garantiza que también se capturen los registros que llevan a una entrada FATAL del registrador, como WARN o ERROR.

**Nota:** en [SDK, ejemplos y referencias de API](sdks-samples-apis.html) encontrará referencias de la API del registrador. La API del registrador forma parte del Core del SDK del cliente de {{site.data.keyword.amashort}}.


### Uso del registrador de ejemplo
{: #sample-logger-usage}

Los siguientes fragmentos de código son un ejemplo del uso del registrador:

#### Android
{: #enable-logger-sample-android}

```Java
// Configure el registrador para guardar registros en el dispositivo, de forma que
// se puedan enviar más tarde al servicio {{site.data.keyword.amashort}}
// Inhabilitado de forma predeterminada; establecido en true para habilitar
Logger.storeLogs(true);

// Cambiar el nivel de registro mínimo (opcional)
// El valor predeterminado es Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Crear dos instancias del registrador
// Puede crear varias instancias de registro para organizar los registros
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Registre mensajes con diferentes niveles
// Mensaje de depuración para la característica 1
// Mensaje de información para la característica 2
logger1.debug("debug message");
// el mensaje logger1.debug no está registrado porque el logLevelFilter está establecido en Info
logger2.info("info message");

// Envíe registros al servicio {{site.data.keyword.amashort}}
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Configure el registrador para guardar registros en el dispositivo, de forma que se puedan enviar más tarde al servicio {{site.data.keyword.amashort}}
// Inhabilitado de forma predeterminada; establecido en true para habilitar
Logger.logStoreEnabled = true

// Cambiar el nivel de registro mínimo (opcional)
// El valor predeterminado es LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Crear dos instancias del registrador
// Puede crear varias instancias de registro para organizar los registros
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")

// Registre mensajes con diferentes niveles
logger1.debug("debug message for feature 1")
// el mensaje logger1.debug no está registrado porque el logLevelFilter está establecido en Info
logger2.info("info message for feature 2")

// Envíe registros al servicio {{site.data.keyword.amashort}}
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Habilite registros persistentes
BMSLogger.setCapture(true);

// Defina el nivel de registro mínimo que imprimir y persistir
BMSLogger.setLevel(BMSLogger.INFO);

// Cree dos instancias del registrador
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");

// Registre mensajes con diferentes niveles
logger1.debug("debug message");
logger2.info("info message");

// Envíe registros persistentes al servicio de {{site.data.keyword.amashort}}
BMSLogger.send(success, failure);
```
{: codeblock}

### Habilitación de los registros internos del SDK del cliente de {{site.data.keyword.amashort}}
{: #enable-logger-sdklogs}
Esta característica está disponible actualmente en la versión para Android del SDK del cliente de {{site.data.keyword.amashort}}.

El SDK del cliente de {{site.data.keyword.amashort}} mejora la experiencia de desarrollo porque no hace aumentar innecesariamente la salida de LogCat con los mensajes internos de depuración. Por tanto, de forma predeterminada los mensajes internos de registro que produce el SDK del {{site.data.keyword.amashort}} no se imprimen a nivel de depuración. Puede habilitar que se impriman estos mensajes del SDK del cliente de {{site.data.keyword.amashort}} con la API siguiente:


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## Recopilación de analíticas de uso
{: #usage-analytics}

Puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que registre analíticas y envíe los datos registrados al servicio de {{site.data.keyword.amashort}}.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**Nota:** asegúrese de haber habilitado la captura de registro antes de empezar a registrar las analíticas de uso.

Utilice las API siguientes para empezar el registro y envío de analíticas de uso:

#### Android
{: #usage-analytics-android}

```Java
// Inhabilite el registro de analíticas de uso (por ejemplo, para ahorrar espacio de disco)
// El registro está habilitado de forma predeterminada
Analytics.disable();
	
// Habilite el registro de analíticas de uso
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Envíe las analíticas de uso registradas al servicio de Mobile Analytics
Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Inhabilite el registro de analíticas de uso (por ejemplo, para ahorrar espacio de disco)
// El registro está habilitado de forma predeterminada
Analytics.enabled = false

// Habilite el registro de analíticas de uso
Analytics.enabled = true

// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.mobileanalytics_short}}
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Habilite el registro de analíticas de uso
BMSAnalytics.enable();

// Envíe las analíticas de uso registradas al servicio de {{site.data.keyword.amashort}}
BMSAnalytics.send();
```
{: codeblock}

**Nota:** cuando esté desarrollando aplicaciones de Cordova, utilice la API nativa para habilitar el registro de sucesos de ciclo de vida de la aplicación.
