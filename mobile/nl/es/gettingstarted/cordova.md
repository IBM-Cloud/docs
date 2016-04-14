<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Cómo empezar con el ejemplo HelloWorld
{: #gettingstarted-cordova}
*Última actualización: 2 de marzo de 2016*

Si desea empezar a trabajar con una aplicación para Cordova nueva, puede utilizar la app HelloWorld. Esta app muestra cómo conectar con el backend móvil en {{site.data.keyword.Bluemix}} desde una app móvil sin autenticación. La app la tiene instalado el SDK. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en {{site.data.keyword.Bluemix_notm}}.

	1. En la sección Contenedores modelo del catálogo de {{site.data.keyword.Bluemix_notm}}, pulse MobileFirst Services Starter.
	1. Especifique un nombre y un host para la app y pulse **Crear**.
	1. Pulse **Finalizar**.

2. Obtenga el proyecto de GitHub. Puede utilizar el mandato git clone para obtener el proyecto. En el sistema, abra el terminal y, a continuación, escriba el siguiente mandato:

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. Ejecute los siguientes mandatos desde su directorio de proyecto para añadir los entornos de plataforma Android e iOS:

	Android:

	```Bash
	cordova platform add android
	```

	iOS:

	```Bash
	cordova platform add ios
	```

4. Añada el plugin de Cordova con el siguiente mandato:

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configure su app de Cordova para Android, iOS o ambos.

	* **Android**

		Antes de abrir su proyecto en Android Studio, compile y ejecute su aplicación de Cordova mediante su aplicación de línea de mandatos (CLI) para evitar errores de compilación. 

		```Bash
		cordova build android
		```

		```Bash
		cordova run android
		```

	* **iOS**

		Configure su proyecto de Xcode como se indica a continuación, para evitar errores de compilación. 

		- Utilice la versión más reciente de Xcode para abrir el archivo `xcode.proj` en el directorio *&lt;nombre_app&gt;*/platforms/ios. 

			**Importante:** Si recibe un mensaje solicitando si desea convertir a la última sintaxis Swift, pulse **Cancelar**.

		- Vaya a **Valores de compilación > Compilador de Swift - Generación de códigos > Cabecera puente de Objective-C** y añada la siguiente vía de acceso:

			```
			<nombre_proyecto>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		- Vaya a **Valores de compilación > Enlaces > Vías de acceso de búsqueda de vías de acceso de ejecución** y añada el siguiente parámetro de Frameworks:

			```
			@executable_path/Frameworks
			```

		- Compile y ejecute su aplicación con Xcode.		
6. Configure el ejemplo HelloWorld.

	- Vaya al directorio donde ha clonado el proyecto. 
	- Abra el archivo *&lt;su_directorio_app&gt;*/www/js/index.js file y substituya LA *&lt;RUTA_APLICACIÓN&gt;* y EL *&lt;ID_APLICACIÓN&gt;* por sus valores de ruta y de ID de aplicación de Bluemix. 

		**Nota:** Compruebe que su ruta es segura utilizando el protocolo https. 

		```Javascript
		// Bluemix credentials
		route: "<RUTA_APLICACIÓN>",
		GUID: "<GUID_APLICACIÓN>",
		```

7. Ejecute el ejemplo en su dispositivo o emulador de dispositivo móvil. 

	Compile la app de Cordova utilizando los mandatos siguientes:

	```Bash
	cordova build android
	```

	```Bash
	cordova build ios
	```

	Ejecute la app de ejemplo utilizando los mandatos siguientes:

	```Bash
	cordova run android
	```

	```Bash
	cordova run ios
	```

Se mostrará una aplicación de vista única con un botón **PING BLUEMIX**. Cuando pulse el botón, la aplicación probará la conexión del cliente a la aplicación {{site.data.keyword.Bluemix_notm}} de fondo. La conexión se prueba utilizando la ruta de la aplicación que haya especificado en el archivo `index.js`.


![Aplicación Hello World conectada correctamente a Bluemix](images/yayconnected.jpg "Figura 1. Aplicación Hello World conectada correctamente a Bluemix")


Cuando se conecte correctamente a {{site.data.keyword.Bluemix_notm}} desde la app móvil, se mostrará un mensaje parecido a "¡Se ha conectado!".


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Si la conexión falla, se muestra un mensaje de error. En el mensaje se incluye más información sobre el error. Puede comprobar los siguientes elementos para resolver el error:

- Compruebe que ha pegado correctamente los valores de ruta y de GUID:
- Visualice el registro de depuración de Xcode o Android.
- Compruebe el estado de su app en {{site.data.keyword.Bluemix_notm}}.

## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móvil, consulte:
* [Mobile Client Access: Configuración del plug-in de Cordova](../services/mobileaccess/getting-started-cordova.html)
* [Notificaciones Push: Configuración del plug-in de Cordova](../mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
