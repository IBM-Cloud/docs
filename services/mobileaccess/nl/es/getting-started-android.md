---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.

# Configuración del SDK de Android
{: #getting-started-android}

Instrumente su aplicación de Android con el SDK del cliente de {{site.data.keyword.amafull}}, inicialice el SDK y realice solicitudes a recursos protegidos o no protegidos.
{: shortdesc}

## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:

* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}}.
* Una instancia de un servicio {{site.data.keyword.amafull}}.
* Su **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amafull}}. Pulse el botón **Opciones móviles**. Los valores `tenantId` (también conocidos como `appGUID`) se muestran en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su **Ruta de aplicación**. Es el URL de la aplicación de programa de fondo. Necesita este valor para enviar solicitudes a sus puntos finales protegidos.
* Su {{site.data.keyword.Bluemix_notm}} **Región**.  Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`,  `Sidney` o `Reino Unido` y corresponde  lo valores de SDK requeridos en el código: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.
* Un proyecto de Android Studio, configurado para funcionar con Gradle. Para obtener más información sobre la configuración del entorno de desarrollo de Android, consulte las [Herramientas del desarrollador de Google ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://developer.android.com/sdk/index.html){: new_window}.

## Instalación del SDK del cliente de {{site.data.keyword.amashort}}
{: #install-mca-sdk}

El SDK del cliente de {{site.data.keyword.amashort}} se distribuye con Gradle, un gestor de dependencias para proyectos de Android. Gradle descarga automáticamente los artefactos desde los repositorios, y los pone a disposición para su aplicación de Android.

1. Cree un proyecto de Android Studio o abra uno ya existente.

1. Abra el archivo `build.gradle` para la aplicación (**no** el archivo `build.gradle` del proyecto).

1. Busque la sección de **dependencias** del archivo `build.gradle`.  Añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.amashort}}:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
}
	```
	{: codeblock}

1. Sincronice el proyecto con Gradle. Pulse **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Abra el archivo `AndroidManifest.xml` para el proyecto de Android. Añada el permiso de acceso a Internet al elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #initalize-mca-sdk}

Inicialice el SDK de cliente pasando los parámetros **context** y **region** al método `initialize`. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `onCreate` de la actividad principal de la aplicación de Android.

```Java
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));
```
{: codeblock}

* Sustituya `<applicationBluemixRegion>` por la región en la que se aloja el servicio {{site.data.keyword.Bluemix_notm}}.
* Sustituya `<MCAServiceTenantId>` por el **tenantId**

Para obtener más información sobre estos valores, consulte [Antes de comenzar](#before-you-begin).

## Cómo realizar una solicitud a la aplicación de programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido de la aplicación de programa de fondo móvil. En el navegador, abra el siguiente URL: `{applicationRoute}/protected` (por ejemplo, `http://my-mobile-backend.mybluemix.net/protected`).   

	El punto final `/protected` de una aplicación de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de Android para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`:

	```Java
	Request request = new Request("http://my-mobile-backend.mybluemix.net/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```
	{: codeblock}

1. Cuando la solicitud se realiza correctamente, verá la siguiente salida en la utilidad LogCat:

	![imagen](images/getting-started-android-success.png)

## Pasos siguientes
{: #next-steps}

Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.

* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Personalizada](custom-auth-android.html)
