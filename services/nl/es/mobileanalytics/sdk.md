---

copyright:
  years: 2015, 2016

---

# Preparación de la aplicación para utilizar los SDK de cliente de {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}
*Última actualización: 27 de abril de 2016*
{: .last-updated}

Los SDK de {{site.data.keyword.mobileanalytics_full}} le permiten preparar su aplicación móvil.
{: shortdesc}

{{site.data.keyword.mobileanalytics_short}} le permite recopilar tres categorías de datos, cada una de las cuales requiere un nivel de instrumentación distinto:

1.  Datos predefinidos: esta categoría incluye información genérica de uso y de los dispositivos que se aplica a todas las apps. En esta categoría se encuentran los metadatos de dispositivo (sistema operativo y modelo de dispositivo) y los datos de uso (usuarios activos y sesiones de app), que indican el volumen, la frecuencia o el tiempo de uso de una app. Los datos predefinidos se recopilan automáticamente una vez inicializado el SDK de {{site.data.keyword.mobileanalytics_short}} en la app.
2. Eventos personalizados: esta categoría incluye los datos definidos por el usuario y los específicos de la app. Estos datos representan eventos que se producen en la app (por ejemplo, visualizaciones de páginas, selección de botones o compras en la app). Además de inicializar el SDK de {{site.data.keyword.mobileanalytics_short}} en la app, debe añadir una línea de código para cada evento personalizado del que desee hacer un seguimiento.
3. Mensajes de registro de cliente: esta categoría permite que los desarrolladores añadan líneas de código a la app que registran mensajes personalizados para ayudar al desarrollo y a la depuración. El desarrollador asigna un nivel de gravedad/detalle a todos los mensajes de registro y puede filtrarlos según el nivel asignado o bien conservar el espacio de almacenamiento configurando la app para que ignore los mensajes inferiores a un determinado nivel de registro. Para recopilar los datos de registro del cliente, debe inicializar el SDK de {{site.data.keyword.mobileanalytics_short}} en la app y añadir una línea de código para cada mensaje de registro.

En este momento, los SDK están disponibles para Android, iOS y WatchOS.

## Identificación del valor de la clave de cliente
{: #analytics-clientkey}

Identifique su valor **Clave de cliente** antes de configurar el SDK de cliente. La clave de cliente es necesaria para inicializar el SDK de cliente.
1. Abra el panel de control del servicio de {{site.data.keyword.mobileanalytics_short}}.
2. Pulse el icono de la llave inglesa para abrir el separador Claves de API.
3. En el separador Claves de API, anote el valor Clave de cliente.


## Inicialización de la app de Android para recopilar análisis
{: #initalize-ma-sdk-android}

Inicialice la aplicación para habilitar el envío de registros al servicio de {{site.data.keyword.mobileanalytics_short}}.

1. Importe el SDK de cliente añadiendo la siguiente sentencia `import` al inicio del archivo del proyecto:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Inicialice el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} en su aplicación de Android; para ello, añada el código de inicialización al método `onCreate` de la actividad principal de la aplicación de Android, o bien en una ubicación que sea más adecuada para su proyecto.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  Para utilizar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}, debe inicializar el `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica el despliegue de {{site.data.keyword.Bluemix_notm}} utilizado (por ejemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`).
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Inicialice Analytics utilizando el objeto de la aplicación de Android y asignándole el nombre de su aplicación. También necesitará el valor [**Clave de cliente**](#analytics-clientkey).
	
	```Java
	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE);
	// En este código de ejemplo, Analytics está configurado para registrar sucesos de ciclo de vida.
	```
  {: codeblock}

	**Sugerencia:** El nombre de la aplicación se utiliza como filtro para buscar registros de cliente en el panel de control. Si utiliza el mismo nombre de aplicación en varias plataformas (por ejemplo, en Android e iOS), podrá ver todos los registros de esa aplicación con el mismo nombre, independientemente de la plataforma desde la que se han enviado los registros.

## Inicialización de la app de iOS para recopilar análisis
{: #init-ma-sdk-ios}

Inicialice la aplicación para habilitar el envío de registros al servicio de {{site.data.keyword.mobileanalytics_short}}. El SDK de Swift está disponible para iOS y watchOS.

1. Importe las infraestructuras `BMSCore` y `BMSAnalytics`; para ello, añada las siguientes sentencias `import` al inicio del archivo del proyecto `AppDelegate.swift`:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. Para utilizar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}, primero debe inicializar la clase `BMSClient` con el siguiente código:

  Coloque el código de inicialización en el método `application(_:didFinishLaunchingWithOptions:)` de la aplicación delegada o en una ubicación que sea más adecuada para su proyecto.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    Para utilizar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}, debe inicializar el `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica el despliegue de {{site.data.keyword.Bluemix_notm}} utilizado (por ejemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`).
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Inicialice Analytics asignándole el nombre de su aplicación móvil. También necesitará el valor [**Clave de cliente**](#analytics-clientkey).

  El nombre de la aplicación se utiliza como filtro para buscar registros de cliente en el panel de control de {{site.data.keyword.mobileanalytics_short}}. Si utiliza el mismo nombre de aplicación en varias plataformas (por ejemplo, en Android e iOS), podrá ver todos los registros de esa aplicación con el mismo nombre, independientemente de la plataforma desde la que se han enviado los registros.

  Un parámetro `deviceEvents` opcional recopila de forma automática las analíticas de los eventos de nivel de dispositivo.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  Puede registrar sucesos de dispositivo en WatchOS utilizando los métodos `Analytics.recordApplicationDidBecomeActive()` y `Analytics.recordApplicationWillResignActive()`.
  
  Añada la siguiente línea al método `applicationDidBecomeActive()` de la clase ExtensionDelegate.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  Añada la siguiente línea al método applicationWillResignActive() de la clase ExtensionDelegate:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## Recopilación de análisis de uso
{: #app-monitoring-gathering-analytics}

  Puede configurar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} para registrar analíticas de uso y enviar los datos registrados al servicio de {{site.data.keyword.mobileanalytics_short}}.

  Utilice las siguientes API para empezar a registrar y enviar analíticas de uso:

#### Android
{: #android-usage-api}
	
```
// Inhabilitar el registro de las analíticas de uso (por ejemplo, para ahorrar espacio de disco)
// El registro está habilitado de forma predeterminada
Analytics.disable();
	
// Habilitar el registro de las analíticas de uso
Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Enviar las analíticas de uso registradas al servicio de Mobile Analytics
Analytics.send();
```
	
Analíticas de uso de ejemplo para registrar un evento:
	
```
// Registrar un evento de analíticas personalizado para gráficos personalizados, representado con un objeto JSON:
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Inhabilitar el registro de las analíticas de uso (por ejemplo, para ahorrar espacio de disco)
// El registro está habilitado de forma predeterminada
Analytics.enabled = false

// Habilitar el registro de las analíticas de uso
Analytics.enabled = true

// Enviar las analíticas de uso registradas al servicio de {{site.data.keyword.mobileanalytics_short}}
Analytics.send()
```

Analíticas de uso de ejemplo para registrar un evento:

```
// Registrar un evento de analíticas personalizado para gráficos personalizados
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

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

    #### Caso de ejemplo de nivel de registro
    {: #log-level-scenario}

    Si el nivel de registro está configurado en `FATAL`, el registrador captura las excepciones no capturadas, pero no captura ningún registro que conduzca al evento de bloqueo. Puede establecer un nivel de registro más detallado para garantizar que también se capturen los registros que puedan conducir a una entrada de registro `FATAL`, como `WARN` y `ERROR`.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### Ejemplo de uso del registrador
{: #sample-logger-usage}

**Nota:** Asegúrese de haber preparado la app para utilizar el [SDK de cliente de {{site.data.keyword.mobileanalytics_short}}](sdk.html) antes de utilizar la infraestructura de registro.
 
  En los siguientes fragmentos de código se muestra un ejemplo de uso del registrador:

#### Android
{: #android-logger-sample}

```
// Configurar el registrador para guardar los registros en el dispositivo y poder enviarlos posteriormente
// al servicio de {{site.data.keyword.mobileanalytics_short}}
// Está inhabilitado de forma predeterminada; se debe establecer en "true" para habilitar
Logger.storeLogs(true);

// Cambiar el nivel de registro mínimo (opcional)
// El parámetro predeterminado es Logger.LEVEL.DEBUG
Logger.setLogLevel(Logger.LEVEL.INFO);

// Enviar registros al servicio de {{site.data.keyword.mobileanalytics_short}}
Logger.send();
```

Casos de ejemplo del registrador:

```
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
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configurar el registrador para guardar los registros en el dispositivo y poder enviarlos posteriormente al servicio de {{site.data.keyword.mobileanalytics_short}} // Está inhabilitado de forma predeterminada; se debe establecer en "true" para habilitar Logger.logStoreEnabled = true

// Cambiar el nivel de registro mínimo (opcional)
// El parámetro predeterminado es LogLevel.Debug
Logger.logLevelFilter = LogLevel.Info

// Enviar registros al servicio de {{site.data.keyword.mobileanalytics_short}}
Logger.send()
```

Casos de ejemplo del registrador:
    
```
// Crear dos instancias del registrador
// Puede crear varias instancias de registro para organizar los registros
let logger1 = Logger.logger(forName: "feature1Logger")
let logger2 = Logger.logger(forName: "feature2Logger")
	
// Mensajes de registro con distintos niveles
logger1.debug("mensaje de depuración para la característica 1") 
//el mensaje logger1.debug no se registra porque el logLevelFilter está establecido en Info
logger2.info("mensaje informativo para la característica 2")
```

**Sugerencia**: Por motivos de privacidad, puede inhabilitar la salida del registrador para las aplicaciones compiladas en modo de publicación. De forma predeterminada, la clase Logger imprime registros en la consola de Xcode. En la configuración de compilación del destino, añada un indicador `-D RELEASE_BUILD` a la sección **Otros indicadores Swift** de la configuración de compilación de la versión.
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## Seguimiento de usuarios activos
{: #trackingusers}
Si lo desea, puede hacer un seguimiento de los usuarios que utilizan de forma activa la aplicación; para ello, pase el nombre del usuario activo a {{site.data.keyword.mobileanalytics_short}}.

#### Android
{: #android-tracking-users}

Añada el siguiente código en el momento en el que el usuario inicie la sesión:

```
Analytics.setUserIdentity("username");
```

Añada el siguiente código en el momento en el que el usuario finalice la sesión:

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

Añada el siguiente código en el momento en el que el usuario inicie la sesión:

```
Analytics.userIdentity = "username"
```

Añada el siguiente código en el momento en el que el usuario finalice la sesión:

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

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
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

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
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

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
      {: #mfp80}

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
{: #ignored-events}
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

# rellinks

## Referencia de API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
