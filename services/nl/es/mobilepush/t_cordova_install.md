---

copyright:
 años: 2015, 2016

---

# Instalación del plug-in Push de Cordova
{: #cordova_install}

Instale y utilice el plug-in Push del cliente para seguir desarrollando sus aplicaciones Cordova. Esto también instala el plug-in Core de Cordova, que inicializa
          la conexión a Bluemix.

### Antes de empezar

1. Descargue las versiones más recientes de Android Studio SDK y Xcode.
1. Configure el emulador. Para Android Studio, utilice un emulador que dé soporte a la API de Google Play.
1. Instale la herramienta de línea de mandatos de Git. Para Windows, asegúrese de que selecciona la opción **Ejecutar Git desde la ventana del indicador de mandatos**. Para obtener información sobre cómo descargar e instalar esta herramienta, consulte [Git](https://git-scm.com/downloads).

1. Instale la herramienta Node.js y NPM (Node Package Manager). La herramienta de línea de mandatos NPM está empaquetada con Node.js. Para obtener información sobre cómo descargar e instalar Node.js, consulte [Node.js](https://nodejs.org/en/download/).
1. Desde la línea de mandatos, instale las herramientas de línea de mandatos de Cordova mediante el mandato **npm install -g cordova**. Esto es necesario para utilizar el plug-in Push de Cordova. Para obtener información sobre cómo instalar Cordova y configurar la aplicación de Cordova, consulte [Cordova Apache](https://cordova.apache.org/#getstarted).

	**Nota**: Para ver el archivo readme del plug-in Push de Cordova, vaya a [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)


## Instalación del plug-in Push de Cordova
1. Vaya a la carpeta en la que desea crear la aplicación de Cordova y ejecute el mandato siguiente para crear una aplicación de Cordova. Si ya tiene una aplicación de Cordova, vaya al paso 3.


	cordova create your_app_name
	cd your_app_name
	```
1. Opcional: (Opcional) Edite el archivo **config.xml** y cambie el nombre de la aplicación en el elemento <name> a uno de su elección, en lugar del nombre HelloCordova predeterminado.

	**Nota**: Asegúrese de que especifica el ID de paquete correcto. Si no lo hace, se visualizarán los siguientes mensajes de error en Xcode.
	* El ejecutable se ha firmado con titularidades no válidas.
	* Las titularidades especificadas en el archivo Titularidades de firmado de código de la aplicación no coinciden con las especificadas en el perfil de suministro.

	Para solucionar este problema, especifique el ID de paquete correcto en Xcode o en el archivo **config.xml** de la aplicación de Cordova.

1. Añada la API soportada mínima o la declaración de destino del despliegue al archivo config.xml para la aplicación de Cordova. El valor de minSdkVersion debe ser superior a 15. El valor targetSdkVersion siempre debe reflejar el SDK de Android más reciente disponible desde Google.
	* **Android**: Con el editor, abra el archivo config.xml y actualice el
elemento ```<platform name="android">``` con las versiones SDK de destino y mínimas:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS**: Actualice el elemento <platform name="ios"> con una declaración de destino de despliegue:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Desde la interfaz de línea de mandatos (CLI) de Cordova, añada las plataformas iOS, Android, o ambas utilizando los mandatos siguientes:

	```
	cordova platform add ios
	cordova platform add android
	```
1. Desde el directorio raíz de la aplicación de Cordova, especifique el mandato siguiente para instalar el plug-in Push de Cordova: **cordova plugin add ibm-mfp-push**.

	En función de las plataformas añadidas, verá algo similar a lo siguiente:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Desde *your-app-root-folder*, verifique que los plug-ins Core y Push de Cordova se hayan instalado correctamente, mediante el siguiente mandato: **cordova plugin list**.

	En función de las plataformas añadidas, verá algo similar a lo siguiente:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (Solo iOS): Configure su entorno de desarrollo de iOS.
	a. Abra el archivo your-app-name.xcodeproj en el directorio *your-app-name***/platforms/ios** con Xcode.

	b. Añada la cabecera de puente. Vaya a **Crear configuración > Compilador de Swift - Generación de códigos > Cabecera puente de Objective-C** y añada la vía de acceso siguiente: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Añada el parámetro Frameworks. Vaya a **Crear configuración > Enlaces > Runpath Search Paths** y añada el parámetro siguiente:
	```
	@executable_path/Frameworks
	```
	d. Elimine la marca de comentario de las siguientes sentencias de importación de Push en la cabecera de enlace por puente. Vaya a *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Cree y ejecute la aplicación con Xcode.
1. (Solo Android): Cree su proyecto de Android utilizando el mandato siguiente:
**cordova build android**.

	**Nota**: Antes de abrir el proyecto en Android Studio, primero debe crear la aplicación de Cordova mediante la CLI de Cordova. De lo contrario, se encontrará con errores de creación.

1. Siguiente paso. [Inicialización del plug-in de
            Cordova](t_cordova_initalize.html).
