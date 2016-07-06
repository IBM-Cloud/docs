---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.mobileanalytics_short}} (Beta)  

{: #gettingstartedtemplate}
*Última actualización: 17 de mayo de 2016*
{: .last-updated}

Utilice el servicio de {{site.data.keyword.mobileanalytics_full}} para medir el estado, el comportamiento y el contexto de sus apps para móvil, los usuarios móviles y los dispositivos móviles.
{: shortdesc}

Para empezar a utilizar de inmediato el servicio de {{site.data.keyword.mobileanalytics_short}}, siga estos pasos:

1. Después de [crear una instancia](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) del servicio de {{site.data.keyword.mobileanalytics_short}}, puede acceder a la consola de {{site.data.keyword.mobileanalytics_short}} pulsando el mosaico de la sección Servicios del panel de control de {{site.data.keyword.Bluemix}}.

  **Importante:** La primera vez que abre el servicio de Mobile Analytics que acaba de crear, aparece una ventana para confirmar que permite que {{site.data.keyword.Bluemix_notm}} proporcione su información personal necesaria al servicio para que este pueda validar su identidad. Pulse **Confirmar** para continuar en la consola de {{site.data.keyword.mobileanalytics_short}}. Si pulsa Cancelar, la consola de {{site.data.keyword.mobileanalytics_short}} no se abrirá.

2. Instale los [SDK de cliente](install-client-sdk.html) de {{site.data.keyword.mobileanalytics_short}}.

3. Importe los SDK de cliente e inicialícelos con el siguiente fragmento de código para registrar las analíticas de uso.

	#### Android
	{: #android-initialize}
	1. Importe el SDK de cliente:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
	2. Inicialice el SDK de cliente dentro del código de la aplicación para registrar las analíticas de uso y las sesiones de la aplicación mediante el valor [Clave de cliente](sdk.html#analytics-clientkey).

		```Java
			try {
			     BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
	            //The Bluemix region provided is invalid
	        }
				Analytics.init(getApplication(), your_app_name, your_client_key, Analytics.DeviceEvent.LIFECYCLE);
		```
    El parámetro **bluemixRegion** especifica el despliegue de Bluemix utilizado (por ejemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`).

  #### iOS
  {: #ios-initialize}
  1. Importe las infraestructuras `BMSCore` y `BMSAnalytics`:
  ```
    import BMSCore
    import BMSAnalytics
    ```
  2. Inicialice el SDK de cliente dentro del código de la aplicación para registrar las analíticas de uso y las sesiones de la aplicación mediante el valor [Clave de cliente](sdk.html#analytics-clientkey).
 
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName(your_app_name, apiKey: your_client_key, deviceEvents: DeviceEvent.LIFECYCLE)
	```
  El parámetro **bluemixRegion** especifica el despliegue de Bluemix utilizado (por ejemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`).

4. Envíe las analíticas de uso registradas al servicio de Mobile Analytics. Una manera fácil de probar las analíticas consiste en ejecutar el siguiente código en el momento de iniciar la aplicación:

	#### Android
	{: #android-send}

	Puede añadir el método `Analytics.send()` al método `onCreate` de la actividad principal de la aplicación de Android, o bien en una ubicación que sea más adecuada para su proyecto.

	```
	Analytics.send();
	```

	#### iOS
	{: #ios-send}

	Utilice el método `Analytics.send` para enviar datos analíticos al servidor. Coloque el método `Analytics.send` en el método `application(_:didFinishLaunchingWithOptions:)` de la aplicación delegada o en una ubicación que sea más adecuada para su proyecto.

	```
	Analytics.send()
	```

	Lea el tema [Preparación de la aplicación](sdk.html).
5. Compile y ejecute la aplicación en el emulador o dispositivo.

6. Vaya al **panel de control** de {{site.data.keyword.mobileanalytics_short}} para ver las analíticas de uso (por ejemplo, los dispositivos nuevos y el total de dispositivos que utilizan la aplicación). También puede supervisar la app [creando gráficos personalizados](app-monitoring.html#custom-charts), [configurando alertas](app-monitoring.html#alerts) y [supervisando bloqueos de apps](app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK de iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
