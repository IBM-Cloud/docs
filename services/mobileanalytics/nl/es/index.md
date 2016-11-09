---

copyright:
  years: 2016
lastupdated: "2016-10-19"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.mobileanalytics_short}}
{: #gettingstartedtemplate}


Última actualización: 19 de octubre de 2016
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} proporciona a los desarrolladores, administradores de TI y a las partes interesadas del negocio información sobre el rendimiento de sus apps para móviles y cómo se utilizan. Supervise el rendimiento y el uso de todas las aplicaciones desde el escritorio o la tableta. Identifique rápidamente tendencias y anomalías, obtenga detalles para resolver problemas y desencadene alertas cuando las métricas de claves atraviesan umbrales críticos. 
{: shortdesc}

Para empezar a utilizar de inmediato el servicio de {{site.data.keyword.mobileanalytics_short}}, siga estos pasos:

1. Después de crear una instancia <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->del servicio de {{site.data.keyword.mobileanalytics_short}}, puede acceder a la consola de {{site.data.keyword.mobileanalytics_short}} pulsando el mosaico en el panel de control de la sección **Servicios** de {{site.data.keyword.Bluemix}}.

 El servicio de {{site.data.keyword.mobileanalytics_short}} se inicia con la **modalidad de demostración** habilitada. La modalidad de demostración rellena gráficos en las páginas **APP DATA** y **ALERTS**, de forma que puede ver cómo se mostrarán los datos. Puede desactivar la modalidad de demostración cuando tenga sus propios datos. La consola de {{site.data.keyword.mobileanalytics_short}} es de sólo lectura cuando se encuentre en modalidad de demostración, por lo que no podrá crear nuevas definiciones de alerta.

2. Instale los [SDK de cliente](install-client-sdk.html) de {{site.data.keyword.mobileanalytics_short}}. De forma opcional puede utilizar la {{site.data.keyword.mobileanalytics_short}} [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}.

3. Importe los SDK de cliente e inicialícelos con el siguiente fragmento de código para registrar las analíticas de uso.

	#### Android
	{: #android-initialize}
	1. Importe el SDK de cliente:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
		{: codeblock}
		
	2. Inicialice el SDK de cliente dentro del código de la aplicación para registrar el análisis de uso y las sesiones de aplicación utilizando el valor de [clave de API](sdk.html#analytics-clientkey).

		```Java
			BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
			
			Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.LIFECYCLE);
		```
		{: codeblock}
		
    El nombre que seleccione para la aplicación (`your_app_name_here`) se mostrará en la consola de {{site.data.keyword.mobileanalytics_short}} como el nombre de la aplicación. El nombre de la aplicación se utiliza como filtro para buscar registros de aplicaciones en el panel de control. Si utiliza el mismo nombre de aplicación en varias plataformas (por ejemplo, en Android e iOS), podrá ver todos los registros de esa aplicación con el mismo nombre, independientemente de la plataforma desde la que se han enviado los registros.
    
    El parámetro **bluemixRegion** especifica qué despliegue de {{site.data.keyword.Bluemix_notm}} está utilizando, por ejemplo, `BMSClient.REGION_US_SOUTH` y `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.-->
    
    **Nota:** Establezca el valor para `hasUserContext` en **true** o **false**. Si es false (valor predeterminado), cada dispositivo se cuenta como un usuario activo. El método [`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) no funcionará cuando `hasUserContext` es false. Si es true, cada uso de [`Analytics.setUserIdentity("username");`](sdk.html#android-tracking-users) cuenta como un usuario activo. No hay ninguna identidad de usuario predeterminado cuando `hasUserContext` es true y, por lo tanto, debe establecerse en rellenar los gráficos de usuario activo.

  #### iOS
  {: #ios-initialize}
  
  1. Importe las infraestructuras `BMSCore` y `BMSAnalytics`:
	```
	import BMSCore
    import BMSAnalytics
	```
	{: codeblock}
    
  2. Inicialice el SDK de cliente dentro del código de la aplicación para registrar el análisis de uso y las sesiones de aplicación utilizando el valor de [clave de API](sdk.html#analytics-clientkey).
 
	Swift:
	
	```Swift
	BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: DeviceEvent.lifecycle)	
	```
	{: codeblock}
		
	El nombre que seleccione para la aplicación (`your_app_name_here`) se mostrará en la consola de {{site.data.keyword.mobileanalytics_short}} como el nombre de la aplicación. El nombre de la aplicación se utiliza como filtro para buscar registros de aplicaciones en el panel de control. Si utiliza el mismo nombre de aplicación en varias plataformas (por ejemplo, en Android e iOS), podrá ver todos los registros de esa aplicación con el mismo nombre, independientemente de la plataforma desde la que se han enviado los registros.
	
	El parámetro **bluemixRegion** especifica qué despliegue de Bluemix está utilizando, por ejemplo `BMSClient.REGION_US_SOUTH` y `BMSClient.REGION_UK`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
	**Nota:** Establezca el valor para `hasUserContext` en **true** o **false**. Si es false (valor predeterminado), cada dispositivo se cuenta como un usuario activo. El método [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) no funcionará cuando `hasUserContext` es false. Si es true, cada uso de [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) cuenta como un usuario activo. No hay ninguna identidad de usuario predeterminado cuando `hasUserContext` es true y, por lo tanto, debe establecerse en rellenar los gráficos de usuario activo.

4. Envíe las analíticas de uso registradas al servicio de Mobile Analytics. Una manera fácil de probar las analíticas consiste en ejecutar el siguiente código en el momento de iniciar la aplicación:

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

	Lea el tema [Preparación de la aplicación](sdk.html) para obtener más información sobre prestaciones adicionales de {{site.data.keyword.mobileanalytics_short}}.
5. Compile y ejecute la aplicación en el emulador o dispositivo.

6. Vaya a la **Consola** de {{site.data.keyword.mobileanalytics_short}} para ver las analíticas de uso para su aplicación. También puede supervisar la aplicación <!--[creating custom charts](app-monitoring.html#custom-charts),-->[definiendo alertas](app-monitoring.html#alerts) y [supervisando bloqueos de la app](app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK de iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Referencia de API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
