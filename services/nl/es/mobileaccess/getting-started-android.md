---

copyright:
  años: 2015, 2016
  
---

# Configuración del SDK de Android
{: #getting-started-android}

Instrumente su aplicación de Android con el SDK del cliente de {{site.data.keyword.amashort}}, inicialice el SDK y realice solicitudes a recursos protegidos o no protegidos.

## Antes de empezar
{: #before-you-begin}
* Debe tener una instancia de un programa de fondo móvil que esté protegida por el servicio de {{site.data.keyword.amashort}}. Para obtener más información sobre cómo crear un programa de fondo móvil, consulte [Cómo empezar](getting-started.html).
* Configure correctamente Android Studio y el SDK de Android Studio. Para obtener más información sobre la configuración del entorno de desarrollo de Android, consulte las [Herramientas del desarrollador de Google](http://developer.android.com/sdk/index.html).


## Instalación del SDK del cliente de {{site.data.keyword.amashort}}
{: #install-mca-sdk}

El SDK del cliente de {{site.data.keyword.amashort}} se distribuye con Gradle, un gestor de dependencias para proyectos de Android. Gradle descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de Android.

1. Cree un proyecto de Android Studio o abra uno ya existente.

1. Abra el archivo `build.gradle`.
**Sugerencia**: es posible que el proyecto de Android tenga dos archivos `build.gradle`: para el proyecto y para módulo de la aplicación. Utilice el archivo del módulo de la aplicación.

1. Busque la sección de **dependencias** en el archivo `build.gradle`.  Añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.amashort}}:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// otras dependencias  
}
```

1. Sincronice el proyecto con Gradle. Pulse **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Abra el archivo `AndroidManifest.xml` para el proyecto de Android. Añada el permiso de acceso a Internet al elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #initalize-mca-sdk}

Inicialice el SDK pasando los parámetros de contexto, applicationGUID y applicationRoute al método `initialize`.


1. Desde la página principal del panel de control de {{site.data.keyword.Bluemix_notm}}, haga clic en la aplicación. Pulse **Opciones móviles**. Necesita los valores **Ruta de aplicación** y **GUID de aplicación** para inicializar el SDK.

2. Inicialice el SDK del cliente de {{site.data.keyword.amashort}} en la aplicación de Android.  Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `onCreate` de la actividad principal de la aplicación de Android.
<br/>
Sustituya *applicationRoute* y *applicationGUID* por los valores de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");
```


## Cómo realizar una solicitud al programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes al programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido del nuevo programa de fondo móvil. En el navegador, abra el siguiente URL: `{applicationRoute}/protected`. Por ejemplo: `http://mi-programa-fondo-móvil.mybluemix.net/protected`
<br/>El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de Android para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`

	```Java
	Request request = new Request("/protected", Request.GET);
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

1. Cuando la solicitud se realiza correctamente, verá la siguiente salida en la utilidad LogCat:

	![imagen](images/getting-started-android-success.png)

## Próximos pasos
{: #next-steps}

Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Personalizada](custom-auth-android.html)
