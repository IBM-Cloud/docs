<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Cómo empezar con el ejemplo HelloWorld
{: #gettingstarted-cordova}

Si desea empezar a trabajar con una nueva aplicación para Cordova, puede utilizar la app HelloWorld. Esta app muestra cómo conectarse al programa de fondo de Bluemix desde una app para móvil sin autenticación. La app ya tiene instalado el SDK. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en Bluemix.
<ol>
	<li>En la sección Contenedores modelo del catálogo de Bluemix, pulse MobileFirst Services Starter.</li>
    	<li>Especifique un nombre y un host para la app y pulse **Crear**.</li>
    	<li>Pulse **Finalizar**. </li>
</ol>
2. Obtenga el proyecto de GitHub. De forma opcional, utilice el mandato git clone para obtener el proyecto. En el sistema, abra el terminal y, a continuación, escriba el siguiente mandato:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. Ejecute los siguientes mandatos desde el directorio del proyecto para añadir los entornos de las plataformas Android e iOS:

Android:
```
cordova platform add android
```

iOS:
```
cordova platform add ios
```

4. Añada el plug-in de Cordova con el siguiente mandato:
```
cordova plugin add ibm-mfp-core
```

5. Configure la app de Cordova para Android, iOS o para ambos sistemas.

 * Android

	 Antes de abrir el proyecto en Android Studio, compile y ejecute la aplicación de Cordova mediante la interfaz de línea de mandatos (CLI) a fin de evitar errores de compilación.

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Configure el proyecto de Xcode del siguiente modo, a fin de evitar errores de compilación:

	    1. Utilice la versión más reciente de Xcode para abrir el archivo xcode.proj en el directorio &lt;nombre_app&gt;/platforms/ios.

			**Importante:** Si recibe un mensaje para "Convertir a la sintaxis de Swift más reciente", pulse Cancelar.

		2. Vaya a **Crear configuración > Compilador de Swift - Generación de códigos >Cabecera puente de Objective-C** y añada la siguiente vía de acceso:

		```
		<nombre_proyecto>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. Vaya a **Crear configuración > Enlaces > Vías de acceso de búsqueda Runpath ** y añada el siguiente parámetro Frameworks:

		```
		@executable_path/Frameworks
		```
		4. Compile y ejecute la aplicación con Xcode.

6. Configure el ejemplo HelloWorld
<ol>
	<li>Vaya al directorio en el que ha clonado el proyecto</li>
	<li>Abra el archivo &lt;dir_app&gt;/www/js/index.js y sustituya la &lt;RUTA_APLICACIÓN&gt; y el &lt;ID_APLICACIÓN&gt; por los valores de ruta e ID de aplicación de Bluemix.</li>
</ol>

Nota: Asegúrese de que la &lt;RUTA_APLICACIÓN&gt; utiliza de forma segura el protocolo https.

```
// Bluemix credentials
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. Ejecute el ejemplo en su dispositivo o emulador de dispositivo móvil.

   Compile la app de Cordova con los siguientes mandatos:
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   Ejecute la app de ejemplo con los siguientes mandatos:
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


Se muestra una aplicación con una sola vista y con el botón **PING BLUEMIX**. Al pulsar el botón, la aplicación prueba la conexión desde el cliente a la aplicación de fondo de Bluemix. La conexión se prueba con la ruta de aplicación especificada en el archivo index.js.


![Aplicación Hello World conectada correctamente a Bluemix](images/yayconnected.jpg "Figura 1. Aplicación Hello World conectada correctamente a Bluemix")

Cuando se haya conectado correctamente a Bluemix desde la app para móvil, se mostrará el mensaje ¡Se ha conectado!
8. Resuelva cualquier problema.


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Si la conexión falla, se mostrará el mensaje "Algo salió mal". Se incluye más información sobre el error.
Compruebe lo siguiente:
 * Compruebe que ha pegado correctamente los valores de la ruta y del GUID.
 * Consulte el registro de depuración de Xcode o de Android.
 * Consulte el estado de la app en Bluemix.

## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móvil, consulte Configuración del SDK del cliente de Cordova.

# rellinks

## ejemplos
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
