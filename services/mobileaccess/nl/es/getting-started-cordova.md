---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configuración del plug-in de Cordova
{: #getting-started-cordova}

Prepare la aplicación del cliente Cordova con el SDK del cliente de {{site.data.keyword.amafull}}. Inicialice el gestor de autorización en el código Android (Java) o iOS (Objetivo C mediante el SDK de Swift y el archivo de cabecera relevante). Inicialice el cliente y realice solicitudes a recursos protegidos y no protegidos desde WebView.

{:shortdesc}

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:

* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Una instancia de un servicio {{site.data.keyword.amafull}}.
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Reino Unido` o `Sidney` y debe corresponder con los valores de SDK necesarios en el código Javascript de WebView: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.
* Una aplicación de Cordova o un proyecto existente. Para obtener más información sobre la configuración de la aplicación de Cordova, consulte el [sitio web de Cordova ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cordova.apache.org/ "Icono de enlace externo"){: new_window}.

## Instalación del plug-in de Cordova de {{site.data.keyword.amashort}}
{: #getting-started-cordova-plugin}

El SDK del cliente de {{site.data.keyword.amashort}} para Cordova es un plug-in de Cordova que incluye los SDK del cliente de {{site.data.keyword.amashort}} nativos. Se distribuye con la CLI (interfaz de línea de mandatos) y `npmjs`, un repositorio de plug-ins para proyectos de Cordova. La CLI de Cordova descarga los plug-ins automáticamente desde los repositorios y los pone a disposición de la aplicación de Cordova.

1. Añada las plataformas Android y/o iOS a la aplicación de Cordova. Ejecute uno o ambos de los mandatos siguientes desde la línea de mandatos:

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. Si ha añadido la plataforma Android, debe añadir el nivel de API mínimo admitido al archivo `config.xml` de la aplicación de Cordova. Abra el archivo `config.xml` y añada la línea siguiente al elemento `<platform name="android">`:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	El valor *minSdkVersion* debe ser `15` o superior. Consulte la [Guía de la plataforma Android ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/ "Icono de enlace externo"){: new_window} para obtener información actualizada sobre la *targetSdkVersion* soportada para el SDK de Android.

3. Si ha añadido el sistema operativo iOS, actualice el elemento `<platform name="ios">` con una declaración de destino:

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. Instalación del plug-in de Cordova para {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Configure la plataforma para Android, iOS, o ambos.

	####Android
	{: #cordova-android}

	Antes de abrir el proyecto en Android Studio, cree la aplicación de Cordova mediante la interfaz de línea de mandatos (CLI) para evitar errores de compilación.

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	Configure el proyecto Xcode del siguiente modo.

	1. Utilice la versión más reciente de Xcode para abrir el archivo `xcode.proj` en el directorio `<nombre_app>/platforms/ios`.

		**Importante:** Si recibe un mensaje para convertir a la última sintaxis de Swift, pulse **Cancelar**.

	2. Cree y ejecute la aplicación con Xcode.

	**Nota**: es posible que reciba el siguiente error al ejecutar `cordova build ios`. Este problema se debe a un error en el plugin de dependencias y se está realizando un seguimiento en el [Problema 12 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12 "Icono de enlace externo"){: new_window}. Puede ejecutar el proyecto iOS en XCode a través de un simulador o un dispositivo.

	```
	xcodebuild: error: No se ha podido encontrar un destino que coincida con el especificador de destino especificado:
			{ platform:iOS Simulator }

		Falta la opción de especificador de dispositivo necesaria.
		El tipo de dispositivo “iOS Simulator” requiere que se especifique “name” o “id”.
		Especifique “name” o “id”.
	```

6. Verifique que el plug-in se ha instalado correctamente ejecutando el siguiente mandato:

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. Habilite Keychain Sharing para iOS **activando** `Keychain Sharing` en el separador **Capacidades**.

8. Habilite **Define módulo** para iOS especificando el valor **YES** para `Define módulo` en el separador **Crear configuración** > **Paquete**.


## Inicialización del cliente de {{site.data.keyword.amashort}} en Cordova WebView (Javascript)
{: #getting-started-cordova-initialize}

Para utilizar el SDK del cliente de {{site.data.keyword.amashort}}, debe inicializarlo pasando el parámetro `applicationBluemixRegion`.

Añada la llamada siguiente al archivo `index.js` para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**NB:** Sustituya `<applicationBluemixRegion>` por la región en la que se aloja el servicio {{site.data.keyword.Bluemix_notm}}, consulte [Antes de empezar](#before-you-begin)..

##Inicialización de {{site.data.keyword.amashort}} AuthorizationManager desde el código nativo
{: #initializing-auth-manager}

Para poder utilizar `BMSAuthorizationManager`, tendrá que añadir el siguiente fragmento de código. El siguiente código nativo inicializa `BMSAuthorizationManager` con el `tenantId` del servicio de {{site.data.keyword.amashort}} (consulte [Antes de empezar](#before-you-begin)).

### Android (Java)

En el método `OnCreate` del archivo `MainActivity.java`, añada el código antes de `loadUrl`.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
Añada la inicialización del gestor de autorización en `AppDelegate.m` según su versión de Xcode.

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**Nota:** el nombre del archivo de cabecera importado se compone del nombre del módulo concatenado con la serie `-Swift.h`, por ejemplo, si el nombre del módulo es `Cordova`, la línea de importación debería ser `#import "Cordova-Swift.h"` Para encontrar el nombre del módulo, vaya a `Crear configuración` > `Paquete` > `Nombre del módulo del producto`.Sustituya `<tenantId>` por su id de arrendatario (consulte [Antes de empezar](#before-you-begin)).


## Cómo realizar una solicitud al servicio de programa de fondo móvil
{: #getting-started-request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes al servicio de programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido de la aplicación de programa de fondo móvil. En el navegador, abra el siguiente URL: `{applicationRoute}/protected` (por ejemplo, `http://my-mobile-backend.mybluemix.net/protected`).

	El punto final `/protected` de una aplicación de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se accede a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

2. Utilice la aplicación de Cordova para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`:

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. Cuando la solicitud se realiza correctamente, verá la siguiente salida en la utilidad LogCat o la consola de Xcode (según la plataforma que esté utilizando):

	![mensaje de realizado satisfactoriamente](images/getting-started-android-success.png)

	## Pasos siguientes
	{: #next-steps}

	Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Personalizada](custom-auth-cordova.html)
