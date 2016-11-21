---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"  
---
{:shortdesc: .shortdesc} 

# Configuración del plug-in de Cordova
{: #getting-started-cordova}


Instrumente su aplicación de Cordova con el SDK del cliente de {{site.data.keyword.amafull}}, inicialice el SDK y realice solicitudes a recursos protegidos y no protegidos.

{:shortdesc}

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).

* Una aplicación de Cordova o un proyecto existente. Para obtener más información sobre la configuración de aplicaciones de Cordova, consulte el [sitio web de Cordova](https://cordova.apache.org/).

## Instalación del plug-in de Cordova de {{site.data.keyword.amashort}}
{: #getting-started-cordova-plugin}

El SDK del cliente de {{site.data.keyword.amashort}} para Cordova es un plug-in de Cordova que incluye los SDK del cliente de {{site.data.keyword.amashort}} nativos. Se distribuye con la CLI (interfaz de línea de mandatos) y `npmjs`, un repositorio de plug-ins para proyectos de Cordova. La CLI de Cordova descarga los plug-ins automáticamente desde los repositorios y los pone a disposición de la aplicación de Cordova.

1. Añada las plataformas Android e iOS a la aplicación de Cordova. Ejecute uno o ambos de los mandatos siguientes desde la línea de mandatos:
   	
	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	
	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```

2. Si ha añadido la plataforma Android, debe añadir el nivel de API mínimo admitido al archivo `config.xml` de la aplicación de Cordova. Abra el archivo `config.xml` y añada la línea siguiente al elemento `<platform name="android">`:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	
	El valor *minSdkVersion* debe ser `15` o superior. El valor *targetSdkVersion* debe ser al menos el último SDK de Android disponible desde Google.

3. Si ha añadido el sistema operativo iOS, actualice el elemento `<platform name="ios">` con una declaración de destino:

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```

4. Instalación del plug-in de Cordova para {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configure la plataforma para Android, iOS, o ambos.

	####Android
	{: #cordova-android}

	Antes de abrir el proyecto en Android Studio, cree la aplicación de Cordova mediante la interfaz de línea de mandatos (CLI) para evitar errores de compilación.
	
	```Bash
	cordova build android
	```
	
	####iOS
	{: #cordova-ios}

	Configure el proyecto Xcode del siguiente modo para evitar errores de compilación.

	1. Utilice la versión más reciente de Xcode para abrir el archivo `xcode.proj` en el directorio `<nombre_app>/platforms/ios`.

		**Importante:** Si recibe un mensaje para convertir a la última sintaxis de Swift, pulse **Cancelar**.

	2. Vaya a **Valores de compilación > Compilador de Swift - Generación de código > Cabecera puente de Objective-C**, y añada la siguiente vía de acceso:

		`<nombre_proyecto>/Plugins/ibm-mfp-core/Bridging-Header.h`

	3. Vaya a **Valores de compilación > Enlazar > Vías de acceso de búsqueda de Runpath**, y añada el siguiente parámetro de Frameworks:

		`@executable_path/Frameworks
			`

	4. Cree y ejecute la aplicación con Xcode.

6. Verifique que el plug-in se ha instalado correctamente ejecutando el siguiente mandato:

	```Bash
	cordova plugin list
	```

## Inicialización del plug-in del cliente {{site.data.keyword.amashort}}
{: #getting-started-cordova-initialize}

Para utilizar el SDK del cliente de {{site.data.keyword.amashort}}, debe inicializarlo pasando los parámetros *applicationGUID* y *applicationRoute*.

1. Busque los valores de GUID y ruta de la aplicación en la página principal del panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse el nombre de la app y después **Opciones móviles** para visualizar los valores de **Ruta de aplicación** y **GUID de aplicación** para inicializar el SDK.

3. Añada la llamada siguiente al archivo `index.js` para inicializar el SDK del cliente de {{site.data.keyword.amashort}}. 

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

  * Sustituya `applicationRoute` y `applicationGUID` por los valores de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}.

##Inicialización de {{site.data.keyword.amashort}} AuthorizationManager
{: #initializing-auth-manager}

Utilice el siguiente código JavaScript en la aplicación de Cordova para inicializar el AuthorizationManager de {{site.data.keyword.amashort}}.

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```

Sustituya el valor de `tenantId` por el `tenantId` del servicio de {{site.data.keyword.amashort}}. Puede encontrar este valor pulsando el botón **Mostrar credenciales** en el icono del servicio {{site.data.keyword.amashort}}.

## Cómo realizar una solicitud a la aplicación de programa de fondo móvil
{: #getting-started-request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido de la nueva aplicación de programa de fondo móvil. En el navegador, abra el siguiente URL: `{applicationRoute}/protected` (por ejemplo, `http://my-mobile-backend.mybluemix.net/protected`).

	El punto final `/protected` de una aplicación de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se accede a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

2. Utilice la aplicación de Cordova para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
	console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

3. Cuando la solicitud se realiza correctamente, verá la siguiente salida en la utilidad LogCat o la consola de Xcode (según la plataforma que esté utilizando):

	![imagen](images/getting-started-android-success.png)

	## Pasos siguientes
	{: #next-steps}

	Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Personalizada](custom-auth-cordova.html)
