---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Preparación de la aplicación para utilizar los SDK de cliente de {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Los SDK de {{site.data.keyword.mobileanalytics_full}} le permiten preparar su aplicación para móvil.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} le permite recopilar dos <!--three--> categorías de datos, cada una de las cuales requiere un nivel de instrumentación distinto:

1. Datos predefinidos: esta categoría incluye información genérica de uso y de los dispositivos que se aplica a todas las aplicaciones. En esta categoría se encuentran los metadatos de dispositivo (sistema operativo y modelo de dispositivo) y los datos de uso (usuarios activos y sesiones de aplicaciones), que indican el volumen, la frecuencia o el tiempo de uso de una aplicación. Los datos predefinidos se recopilan automáticamente una vez inicializado el SDK de {{site.data.keyword.mobileanalytics_short}} en la aplicación.

2. Mensajes de registro de aplicaciones: esta categoría permite que los desarrolladores añadan líneas de código a la aplicación que registran mensajes personalizados para ayudar al desarrollo y a la depuración. El desarrollador asigna un nivel de gravedad/detalle a todos los mensajes de registro y puede filtrarlos según el nivel asignado o bien conservar el espacio de almacenamiento configurando la aplicación para que ignore los mensajes que estén a un nivel inferior a un determinado nivel de registro. Para recopilar los datos de registro de la aplicación, debe inicializar el SDK de {{site.data.keyword.mobileanalytics_short}} en la aplicación y añadir una línea de código para cada mensaje de registro.

3. Sucesos personalizados: Esta categoría incluye datos que define usted mismo y que son específicos de la app. Estos datos representan sucesos que se producen en la app, como las vistas de páginas, las pulsaciones de botones o las compras dentro de la app. Además de inicializar el SDK de {{site.data.keyword.mobileanalytics_short}} en la app, debe añadir una línea de código para cada suceso personalizado que desee seguir. 

En este momento, los SDK están disponibles para Android, iOS, WatchOS y Cordova.

## Identificación del valor de la clave de API de Credenciales de servicio
{: #analytics-clientkey}

Identifique el valor **Clave de API** antes de configurar el SDK de cliente. La clave de API es necesaria para inicializar el SDK de cliente.

1. Abra el panel de control del servicio de {{site.data.keyword.mobileanalytics_short}}.
2. Expanda **Ver credenciales** para revelar el valor de la Clave de API. Necesitará el valor de la Clave de API al inicializar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}.


## Inicialización de la aplicación para recopilar análisis
{: #initalize-ma-sdk}

Inicialice la aplicación para habilitar el envío de registros al servicio de {{site.data.keyword.mobileanalytics_short}}.

1. Importe el SDK de cliente.

	### Android
	{: #android-import notoc}

	Añada las siguientes sentencias `import` al principio del archivo del proyecto:
	
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
	```
	{: codeblock}
  
	### iOS
	{: #ios-import notoc}
	
	**Nota:** el SDK de Swift está disponible para iOS y watchOS.
	
	Importe las infraestructuras `BMSCore` y `BMSAnalytics`; para ello, añada las siguientes sentencias `import` al inicio del archivo del proyecto `AppDelegate.swift`:

	```Swift
	import BMSCore
	import BMSAnalytics
	```
	{: codeblock}  
   
	### Cordova
	{: #cordova-import notoc}
		
	Añada el plug-in de Cordova ejecutando el siguiente mandato desde el directorio raíz de la aplicación de Cordova:

	```Javascript
	cordova plugin add bms-core
	```
	{: codeblock}  

2. Inicialice el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} en la aplicación.

	### Android
	{: #android-init notoc}
	
	Inicialice el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} en su aplicación de Android; para ello, añada el código de inicialización al método `onCreate` de la actividad principal de la aplicación de Android, o bien en una ubicación que sea más adecuada para su proyecto.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Asegúrese de apuntar a su región
	```
	{: codeblock}

	Debe inicializar el `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica qué despliegue de {{site.data.keyword.Bluemix_notm}} está utilizando, por ejemplo, `BMSClient.REGION_US_SOUTH` y `BMSClient.REGION_UK`.
     
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
	### iOS
	{: #ios-init notoc}
    
	Primero inicialice la clase `BMSClient` con el siguiente código. Coloque el código de inicialización en el método `application(_:didFinishLaunchingWithOptions:)` de la aplicación delegada o en una ubicación que sea más adecuada para su proyecto.
	
	```Swift 
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
	```
	{: codeblock}

	Debe inicializar el `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica qué despliegue de {{site.data.keyword.Bluemix_notm}} está utilizando, por ejemplo, `BMSClient.Region.usSouth` o `BMSClient.Region.unitedKingdom`.
    <!-- , or `BMSClient.Region.Sydney`. -->
    
	### Cordova
	{: #cordova-init notoc}
    
	Inicialice **BMSClient** y **BMSAnalytics**. También necesitará el valor [**Clave de API**](#analytics-clientkey).

	```Javascript
  var applicationName = "HelloWorld";
  var apiKey =  "your_api_key_here";
  var hasUserContext = true;
  var deviceEvents = [BMSAnalytics.ALL];

	BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Make sure you point to your region	
  BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
	```
	{: codeblock}

	Para utilizar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}, debe inicializar el `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica qué despliegue de {{site.data.keyword.Bluemix_notm}} está utilizando, por ejemplo, `BMSClient.REGION_US_SOUTH` o `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. Inicialice Analytics utilizando el objeto de la aplicación y asignándole el nombre de su aplicación. 

	El nombre que seleccione para la aplicación (`your_app_name_here`) se mostrará en la consola de {{site.data.keyword.mobileanalytics_short}} como el nombre de la aplicación. El nombre de la aplicación se utiliza como filtro para buscar registros de aplicaciones en el panel de control. Si utiliza el mismo nombre de aplicación en varias plataformas (por ejemplo, en Android e iOS), podrá ver todos los registros de esa aplicación con el mismo nombre, independientemente de la plataforma desde la que se han enviado los registros.

	También es necesario el valor [**Clave de API**](#analytics-clientkey).

	### Android
	{: #android-init-analytics notoc}
	
	```Java
	// En este código de ejemplo, Analytics está configurado para registrar sucesos de ciclo de vida.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**Nota:** Establezca el valor para `hasUserContext` en **true** o **false**. Si es false (valor predeterminado), cada dispositivo se cuenta como un usuario activo. El método [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users), que le permite realizar el seguimiento del número de usuarios por dispositivo que están utilizando de forma activa la aplicación, no funcionará cuando `hasUserContext` sea false. Si es true, cada uso de [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) cuenta como un usuario activo. No hay ninguna identidad de usuario predeterminado cuando `hasUserContext` es true y, por lo tanto, debe establecerse en rellenar los gráficos de usuario activo.
	
	### iOS
	{: #ios-initialize-analytics notoc}
	
	```Swift
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
	```
	{: codeblock}
 	
	### watchOS
	{: #watchos-initialize-analytics notoc}
	 	
	```Swift
 	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
	```
	{: codeblock}
 	
	Un parámetro `deviceEvents` opcional recopila de forma automática las analíticas de los eventos de nivel de dispositivo.
	
	**Nota:** Establezca el valor para `hasUserContext` en **true** o **false**. Si es false (valor predeterminado), cada dispositivo se cuenta como un usuario activo. El método [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users), que le permite realizar el seguimiento del número de usuarios por dispositivo que están utilizando de forma activa la aplicación, no funcionará cuando `hasUserContext` sea false. Si `hasUserContext` es true, cada uso de [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) cuenta como un usuario activo. No hay ninguna identidad de usuario predeterminado cuando `hasUserContext` es true y, por lo tanto, debe establecerse en rellenar los gráficos de usuario activo.

	#### watchOS
	{: #watchos-record-device notoc}

	Puede registrar sucesos de dispositivo en WatchOS utilizando los métodos `Analytics.recordApplicationDidBecomeActive()` y `Analytics.recordApplicationWillResignActive()`.
  
	Añada la siguiente línea al método `applicationDidBecomeActive()` de la clase ExtensionDelegate:
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
	{: codeblock}

	Añada la siguiente línea al método `applicationWillResignActive()` de la clase ExtensionDelegate:
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. Ya ha inicializado la aplicación para recopilar analíticas. A continuación puede [enviar datos de analíticas](sdk.html#app-monitoring-gathering-analytics) al servicio de {{site.data.keyword.mobileanalytics_short}}.


## Recopilación de análisis de uso
{: #app-monitoring-gathering-analytics}

Puede configurar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} para registrar analíticas de uso y enviar los datos registrados al servicio de {{site.data.keyword.mobileanalytics_short}}.

Utilice las siguientes API para empezar a registrar y enviar analíticas de uso:


### Android
{: #android-usage-api notoc}
	
```
// Inhabilitar el registro de las analíticas de uso (por ejemplo, para ahorrar espacio de disco)
// El registro está habilitado de forma predeterminada
Analytics.disable();
	
// Habilitar el registro de las analíticas de uso
Analytics.enable();
		
// Enviar las analíticas de uso registradas al servicio de Mobile Analytics
Analytics.send(new ResponseListener() {
            @Override
            public void onSuccess(Response response) {
                // Handle Analytics send success here.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Handle Analytics send failure here.
            }
        });
```
{: codeblock}
	
Análisis de uso de ejemplo para el registro de un suceso:
	
```
// Registre un suceso de análisis personalizado
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


### iOS - Swift
{: #ios-usage-api notoc}

```
// Inhabilitar el registro de las analíticas de uso (por ejemplo, para ahorrar espacio de disco)
// El registro está habilitado de forma predeterminada
Analytics.isEnabled = false

// Habilitar el registro de las analíticas de uso
Analytics.isEnabled = true

// Enviar las analíticas de uso registradas al servicio de Mobile Analytics
Analytics.send(completionHandler: { (response: Response?, error: Error?) in

    if let response = response {
        // Handle Analytics send success here.
    }
    if let error = error {
        // Handle Analytics send failure here.
    }
})
```
{: codeblock}

Análisis de uso de ejemplo para el registro de un suceso:

```Swift
// Registre un suceso de análisis personalizado
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

### Cordova
{: #usage-analytics-cordova notoc}

```JavaScript
  // Habilitar registro de analíticas de uso
  BMSAnalytics.enable();
  
// Inhabilitar registro de analíticas de uso
  BMSAnalytics.disable();

// Enviar analíticas de uso registradas al servicio {{site.data.keyword.mobileanalytics_short}}
  BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
		},
	function (err) {
		console.log('fail: ' + err);
		});
```
{: codeblock}

Análisis de uso de ejemplo para el registro de un suceso:

```JavaScript
// Registre un suceso de análisis personalizado
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

**Nota:** cuando esté desarrollando aplicaciones Cordova, utilice la API nativa para habilitar el registro de sucesos de ciclo de vida de la aplicación.
  
## Habilitación, configuración y uso de Logger
{: #app-monitoring-logger}

El SDK de cliente de {{site.data.keyword.mobileanalytics_full}} proporciona una infraestructura de registro parecida a otras infraestructuras de registro que pueda conocer, como `java.util.logging` o `log4j`. La infraestructura de registro admite varias instancias del registrador por paquete, distintos niveles de registro, la captura de seguimientos de pilas del bloqueo de una aplicación, etc.

También puede configurar los datos registrados para almacenarlos en el dispositivo en el que se ejecuta la aplicación y enviar posteriormente estos registros del dispositivo al servicio de {{site.data.keyword.mobileanalytics_short}}.

<!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

La infraestructura de registro del SDK de cliente de {{site.data.keyword.mobileanalytics_short}} admite los siguientes niveles de registro, que aparecen ordenados de menos a más detallados, con directrices de uso recomendado:

  * `FATAL`: uso para bloqueos irrecuperables. El nivel `FATAL` está reservado para errores de registro irrecuperables que ven los usuarios como un bloqueo de aplicación
  * `ERROR`: uso para excepciones inesperadas o errores de protocolo de red inesperados
  * `WARN`:se utiliza para registrar advertencias de uso que no se consideran errores críticos, como el uso de API en desuso o en caso de una respuesta de red lenta
  * `INFO`: se utiliza para registrar eventos de inicialización y otros datos que podrían ser importantes, pero no urgentes
  * `DEBUG`: se utiliza para registrar sentencias de depuración y permitir que los desarrolladores puedan resolver los defectos de las aplicaciones


### Caso de ejemplo de nivel de registro
{: #log-level-scenario notoc}

Si el nivel de registro está configurado en `FATAL`, el registrador captura las excepciones no capturadas, pero no captura ningún registro que conduzca al evento de bloqueo. Puede establecer un nivel de registro más detallado para garantizar que también se capturen los registros que puedan conducir a una entrada de registro `FATAL`, como `WARN` y `ERROR`.

Cuando el nivel de registro es `DEBUG`, también obtiene registros del SDK de cliente de Mobile Analytics, que se incluye cuando se envían los registros.

<!-- **Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core. -->


### Ejemplo de uso del registrador
{: #sample-logger-usage notoc}

**Nota:** Asegúrese de que ha preparado la aplicación para que utilice el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} antes de utilizar la infraestructura de registro.
 
En los siguientes fragmentos de código se muestra un ejemplo de uso del registrador:


#### Android
{: #android-logger-sample notoc}

```
// Configurar el registrador para guardar los registros en el dispositivo
// y poder enviarlos posteriormente al servicio de Mobile Analytics
// Está inhabilitado de forma predeterminada; se establece en true para habilitar
Logger.storeLogs(true);

// Cambiar el nivel de registro mínimo (opcional)
// El parámetro predeterminado es Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Crear dos instancias del registrador
// Puede crear varias instancias de registro para organizar los registros
Logger logger1 = Logger.getLogger("logger1");
Logger logger2 = Logger.getLogger("logger2");

// Mensajes de registro con distintos niveles
// Mensaje de depuración para la característica 1
// Mensaje informativo para la característica 2
logger1.debug("debug message");
//el mensaje logger1.debug no se registra porque el LogLevelFilter está establecido en Info
logger2.info("info message");

// Enviar registros al servicio de Mobile Analytics
        Logger.send(new ResponseListener() {
	@Override
            public void onSuccess(Response response) {
		// Handle Logger send success here.
                    }

	@Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
		// Handle Logger send failure here.
                    }
});        
```
{: codeblock}


#### iOS - Swift
{: #ios-logger-sample-swift2 notoc}

```
// Configurar el registrador para guardar los registros en el dispositivo
// y poder enviarlos posteriormente al servicio de Mobile Analytics
// Está inhabilitado de forma predeterminada; se debe establecer en true para habilitar
Logger.isLogStorageEnabled = true

// Cambiar el nivel de registro mínimo (opcional)
// El parámetro predeterminado es LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Crear dos instancias del registrador
// Puede crear varias instancias de registro para organizar los registros
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Mensajes de registro con distintos niveles
logger1.debug(message: "mensaje de depuración para característica 1") 
// El mensaje logger1.debug no se registra porque
// logLevelFilter está establecido en info
logger2.info(message: "info message for feature 2")

// Enviar registros al servicio de Mobile Analytics
Logger.send(completionHandler: { (response: Response?, error: Error?) in
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**Sugerencia:** Por motivos de privacidad, puede inhabilitar la salida del registrador para las aplicaciones compiladas en modo de publicación. De forma predeterminada, la clase Logger imprime registros en la consola de Xcode. En la configuración de compilación del destino, añada un indicador `-D RELEASE_BUILD` a la sección **Otros indicadores Swift** de la configuración de compilación de la versión.
    

#### Cordova
{: #enable-logger-sample-cordova notoc}

```
// Habilitar registros permanentes
  BMSLogger.storeLogs(true);

// Establecer el nivel mínimo de registro para que se imprima y sea permanente
  BMSLogger.setLogLevel(BMSLogger.INFO);

var logger1 = BMSLogger.getLogger("logger1");
  var logger2 = BMSLogger.getLogger("logger2");   

// Registrar mensajes con distintos niveles
  logger1.debug ("debug message");
  logger2.info ("info message");

// Enviar registros permanentes al servicio {{site.data.keyword.mobileanalytics_short}}
  BMSLogger.send();
  BMSAnalytics.send();
```
{: codeblock}


<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs notoc}

The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android notoc}

```
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift notoc}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## Realización de una solicitud de red
{: #network-requests}

Puede configurar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} para [realizar una solicitud de red](/docs/mobile/sdk_network_request.html). Asegúrese de haber inicializado `BMSClient` y `BMSAnalytics` y de haber importado los SDK de clientes.

<!--
#### Android
{: #android-network-requests notoc}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests notoc}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests notoc}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->


## Informe de la analítica de bloqueo
{: #report-crash-analytics}

Puede ver [application crash data](app-monitoring.html#monitor-app-crash) enviando información de analíticas y de registro a {{site.data.keyword.mobileanalytics_short}}.

El método `Analytics.send()` rellena las tablas **Visión general de bloqueos** y **Bloqueos** en la página **Bloqueos**. Los gráficos de esta sección se habilitan utilizando el proceso de inicialización y de envío para su análisis; no es necesaria ninguna configuración especial.

El método `Logger.send()` rellena las tablas **Resumen de bloqueos** y **Detalles de bloqueo** en la página **Resolución de problemas**. Debe habilitar la aplicación para almacenar y enviar registros para rellenar los gráficos de esta sección, añadiendo una sentencia adicional en el código de la aplicación:


### Android
{: #android-crash-statement notoc}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

Consulte [ejemplo del uso del registrador](sdk.html#android-logger-sample).


### iOS
{: #ios-crash-statement notoc}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Consulte [ejemplo del uso del registrador](sdk.html##ios-logger-sample-swift2).


### Cordova
{: #cordova-crash-statement notoc}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Consulte [ejemplo del uso del registrador](sdk.html##ios-logger-sample-swift2).


## Seguimiento de usuarios activos
{: #trackingusers}

Si la aplicación puede reconocer usuarios exclusivos en un dispositivo, puede hacer un seguimiento de forma opcional de los usuarios que utilizan activamente la aplicación; para ello, pase el nombre del usuario activo a {{site.data.keyword.mobileanalytics_short}}. 

Habilite el rastreo de usuarios inicializando {{site.data.keyword.mobileanalytics_short}} con `hasUserContext=true`. De lo contrario, {{site.data.keyword.mobileanalytics_short}} solamente captura un usuario por dispositivo. 


### Android
{: #android-tracking-users notoc}

Añada el siguiente código para rastrear cuando el usuario inicie la sesión:

```
Analytics.setUserIdentity("username");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

### iOS - Swift
{: #ios-tracking-users notoc}

Añada el siguiente código para rastrear cuando el usuario inicie la sesión:

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->


### Cordova
{: #cordova-tracking-users notoc}

Añada el siguiente código para rastrear cuando el usuario inicie la sesión:

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp notoc}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70 notoc}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values notoc}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71 notoc}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values notoc}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80 notoc}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events notoc}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->


## Qué hacer a continuación
{: #what-to-do-next notoc}

Ahora puede ir a la consola de {{site.data.keyword.mobileanalytics_short}} para ver las analíticas de uso (por ejemplo, los dispositivos nuevos y el total de dispositivos que utilizan la aplicación). También puede supervisar la aplicación <!--[creating custom charts](app-monitoring.html#custom-charts),-->[definiendo alertas](app-monitoring.html#alerts) y [supervisando bloqueos de la app](app-monitoring.html#monitor-app-crash).


# Enlaces relacionados
{: #rellinks notoc}

## Referencia de API
{: #api notoc}

* [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
