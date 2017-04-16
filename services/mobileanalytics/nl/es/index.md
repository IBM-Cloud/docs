---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.mobileanalytics_short}}

{: #gettingstartedtemplate}

{{site.data.keyword.mobileanalytics_full}} proporciona a los desarrolladores, administradores de TI y a las partes interesadas del negocio información sobre el rendimiento de sus apps para móviles y cómo se utilizan. {{site.data.keyword.mobileanalytics_short}} le permite:

* Supervisar el rendimiento y el uso de todas las aplicaciones desde el escritorio o la tableta.  
* Identificar rápidamente tendencias y anomalías, obtener detalles para resolver problemas y desencadenar alertas cuando las métricas de claves atraviesan umbrales críticos.
{: shortdesc}

**Importante:** La consola de {{site.data.keyword.mobileanalytics_short}} todavía no está preparada para el navegador Internet Explorer y es posible que alguna funcionalidad no funcione correctamente. Para conseguir la mejor experiencia, utilice Firefox, Chrome o Safari.

Para que el servicio {{site.data.keyword.mobileanalytics_short}} esté activo y en ejecución rápidamente, siga estos pasos:

1. Después de crear una instancia <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->del servicio de {{site.data.keyword.mobileanalytics_short}}, puede acceder a la consola de {{site.data.keyword.mobileanalytics_short}} pulsando el mosaico en el panel de control de la sección **Servicios** de {{site.data.keyword.Bluemix}}.

 Para ayudarle a familiarizarse con los distintos gráficos y vistas y el valor que aportan, se proporciona la opción de **modalidad de demostración** en la consola de {{site.data.keyword.mobileanalytics_short}}, con la que las vistas y los gráficos muestran *datos de demostración*. Los datos de demostración es la modalidad predeterminada de la consola cuando al iniciarse por primera vez tras crear la instancia del servicio. Cuando el servicio se rellene con sus propios datos analíticos y de aplicaciones, puede *desactivar* la modalidad de demostración para ver los datos de sus aplicaciones en distintos gráficos. La consola de Mobile Analytics es de sólo lectura cuando se encuentre en modalidad de demostración, por lo que no podrá crear nuevas definiciones de alerta.

2. Instale los [SDK cliente](/docs/services/mobileanalytics/install-client-sdk.html) de {{site.data.keyword.mobileanalytics_short}}. Opcionalmente, puede utilizar la {{site.data.keyword.mobileanalytics_short}} [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "icono de enlace externo"){:new_window}.

3. Importe los SDK de cliente e inicialícelos con el siguiente fragmento de código para registrar las analíticas de uso:

	#### Android
	{: #android-import}

	Añada las siguientes sentencias `import` al principio del archivo del proyecto:
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **Nota:** el SDK de Swift está disponible para iOS y watchOS.
	
 Importe las infraestructuras `BMSCore` y `BMSAnalytics`; para ello, añada las siguientes sentencias `import` al inicio del archivo del proyecto `AppDelegate.swift`:

   ```Swift
  import BMSCore
  import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Añada el plug-in de Cordova ejecutando el siguiente mandato desde el directorio raíz de la aplicación de Cordova:

 ```Javascript
 cordova plugin add bms-core
 ```
 {: codeblock}  

4. Inicialice el SDK de cliente de {{site.data.keyword.mobileanalytics_short}} del código de la aplicación para registrar el análisis de uso y las sesiones de aplicación utilizando el valor de [clave de API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 El parámetro **bluemixRegion** especifica qué despliegue de {{site.data.keyword.Bluemix_notm}} está utilizando, por ejemplo, `BMSClient.REGION_US_SOUTH` y `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->
    
 Establezca el valor para `hasUserContext` en **true** o **false**. Si es false (valor predeterminado), cada dispositivo se cuenta como un usuario activo. 

 #### iOS
 {: #ios-initialize}
  
  Inicialice el SDK de cliente dentro del código de la aplicación para registrar el análisis de uso y las sesiones de aplicación utilizando el valor de [clave de API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
  ```
  {: codeblock}
			
   El parámetro **bluemixRegion** especifica el despliegue de Bluemix que está utilizando, por ejemplo `BMSClient.Region.usSouth` o `BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
 
 Establezca el valor para `hasUserContext` en **true** o **false**. Si es false (valor predeterminado), cada dispositivo se cuenta como un usuario activo. 
	
 #### Cordova
 {: #cordova-initialize}
	
 Inicialice el SDK de cliente dentro del código de la aplicación para registrar el análisis de uso y las sesiones de aplicación utilizando el valor de [clave de API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // Puede cambiar la región
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  El parámetro **bluemixRegion** especifica qué despliegue de {{site.data.keyword.Bluemix_notm}} está utilizando, por ejemplo, `BMSClient.REGION_US_SOUTH` y `BMSClient.REGION_UK`.
  
 **Nota:** El nombre que seleccione para la aplicación (`your_app_name_here`) se mostrará en la consola de {{site.data.keyword.mobileanalytics_short}} como el nombre de la aplicación. El nombre de la aplicación se utiliza como filtro para buscar registros de aplicaciones en el panel de control. Si utiliza el mismo nombre de aplicación en varias plataformas (por ejemplo, en Android e iOS), podrá ver todos los registros de esa aplicación con el mismo nombre, independientemente de la plataforma desde la que se han enviado los registros.

5. Envíe las analíticas de uso registradas al servicio de Mobile Analytics. Una manera fácil de probar las analíticas consiste en ejecutar el siguiente código en el momento de iniciar la aplicación:

	#### Android
	{: #android-send}

	Utilice el método `Analytics.send()` para enviar datos analíticos al servidor. Puede colocar el método `Analytics.send()` en cualquier lugar del método `onCreate` de la actividad principal de la aplicación de Android, o en una ubicación que sea más adecuada para su proyecto. 
	
	Puede insertar `Analytics.send()` en cualquier lugar.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Utilice el método `Analytics.send` para enviar datos analíticos al servidor. Puede colocar el método `Analytics.send` en cualquier lugar del método `application(_:didFinishLaunchingWithOptions:)` de la aplicación delegada o en una ubicación que sea más adecuada para su proyecto. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	Utilice el método `BMSAnalytics.send` para enviar datos analíticos al servidor. Coloque el método `BMSAnalytics.send` en la ubicación que mejor se ajuste a su proyecto.
	
	```
	BMSAnalytics.send()
	```
	{: codeblock}
	
	Lea el tema [Preparación de la aplicación](/docs/services/mobileanalytics/sdk.html) para obtener más información sobre las funciones adicionales de {{site.data.keyword.mobileanalytics_short}}, como [registro](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger), [solicitudes de red](/docs/services/mobileanalytics/sdk.html#network-requests) y [analítica de bloqueo](/docs/services/mobileanalytics/sdk.html#report-crash-analytics).
	
6. Compile y ejecute la aplicación en el emulador o dispositivo.

7. Vaya a la consola de {{site.data.keyword.mobileanalytics_short}} para ver las analíticas de uso para su aplicación. También puede supervisar la aplicación <!--[creating custom charts](app-monitoring.html#custom-charts),-->[definiendo alertas](/docs/services/mobileanalytics/app-monitoring.html#alerts) y [supervisando bloqueos de la app](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [SDK de Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics "icono de enlace externo"){: new_window}  
* [SDK de iOS ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics "icono de enlace externo"){: new_window}
* [Cordova Plugin Core SDK ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.npmjs.com/package/bms-core "icono de enlace externo"){: new_window}

## Referencia de API
{: #api}
* [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "icono de enlace externo"){:new_window}
