    ---

copyright:
 years: 2015 2016

---


# Habilitación de aplicaciones Android para recibir {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Última actualización: 16 de agosto de 2016
{: .last-updated}

Habilite las aplicaciones Android para recibir {{site.data.keyword.mobilepushshort}} y enviar {{site.data.keyword.mobilepushshort}} a sus dispositivos. 

## Instalación del SDK Push del cliente con Gradle
{: #android_install}

En esta sección se describe cómo instalar y utilizar el SDK Push del cliente para seguir desarrollando sus aplicaciones Android.

El SDK push de servicios móviles de Bluemix® se puede añadir mediante Gradle. Gradle descarga automáticamente artefactos desde los repositorios y los deja a disposición de su aplicación Android. Asegúrese de que ha configurado correctamente Android Studio y el SDK de Android Studio. Para obtener más información sobre cómo configurar el sistema, consulte [Visión general de Android Studio](https://developer.android.com/tools/studio/index.html). Para obtener información sobre Gradle, consulte [Configuración de compilaciones de Gradle](http://developer.android.com/tools/building/configuring-gradle.html).

1. En Android Studio, tras crear y abrir la aplicación móvil, abra el archivo **build.gradle** de la aplicación. 
2. Añada las dependencias siguientes a la aplicación móvil. Estas sentencias de importación son necesarias para los fragmentos de código:

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


2. Añada las dependencias siguientes a la aplicación móvil. Las líneas siguientes añaden el SDK del cliente push de servicios de Bluemix™ Mobile y el SDK de los servicios de Google Play a las dependencias del ámbito de compilación.

	```
	dependencies {
	  compile group: 'com.ibm.mobilefirstplatform.clientsdk.android', 
		name: 'push', 
		version: '2.+',
		ext: 'aar', 
		transitive: true
	}  
	```
3. En el archivo **AndroidManifest.xml**, añada los permisos siguientes. Para ver un manifiesto de muestra, consulte [Aplicación de ejemplo helloPush de Android](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Para ver un archivo Gradle de muestra, consulte [Archivo Gradle de compilación de muestra](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

	```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="com.ibm.clientsdk.android.app.permission.C2D_MESSAGE" />
	<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
	<uses-permission android:name="android.permission.WAKE_LOCK" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>

	```
   Aquí puede leer más información sobre los [permisos de Android](http://developer.android.com/guide/topics/security/permissions.html).
4. Añade los valores de intención de notificación para la actividad. Este valor inicia la
          aplicación cuando el usuario pulsa la notificación recibida desde el área de notificación.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Nota**: sustituya *Your_Android_Package_Name* en la acción anterior por el nombre del paquete de aplicaciones utilizado en la aplicación.

5. Añade el servicio de intento de Google Cloud Messaging (GCM) y los filtros de intento para las notificaciones de sucesos RECEIVE.

	```
	service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />

	<receiver
	    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.internal.MFPPushBroadcastReceiver"
	    android:permission="com.google.android.c2dm.permission.SEND">
	    <intent-filter>
	        <action android:name="com.google.android.c2dm.intent.RECEIVE" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	    <intent-filter>
	        <action android:name="android.intent.action.BOOT_COMPLETED" />

	        <category android:name="com.ibm.mobilefirstplatform.clientsdk.android.app" />
	    </intent-filter>
	</receiver>
	```


## Inicialización del SDK push para aplicaciones Android
{: #android_initialize}

Un lugar común para colocar el código de inicialización se encuentra en el método onCreate de la actividad principal en su aplicación Android.

Para obtener la ruta y el GUID de la aplicación, seleccione la opción Configuración del panel de navegación de los servicios push inicializados y pulse **Opciones móviles**.
Utilice estos valores para su ruta y GUID de la app. Modifique el fragmento de código para que utilice los parámetros appRoute y appGUID de la aplicación Bluemix.


###Inicializar el SDK principal

```
// Inicialice el SDK for Java (Android) con IBM Bluemix AppGUID y la ruta
BMSClient.getInstance().initialize(getApplicationContext(), appRoute , appGuid, bluemixRegionSuffix);

```


####appRoute
{: approute}

Especifica la ruta que se asigna a la aplicación de servidor que ha creado en Bluemix.

####AppGUID
{: appguid}

Especifica la clave exclusiva asignada a la instancia del servicio {{site.data.keyword.mobilepushshort}} en Bluemix. Este valor distingue
                entre mayúsculas y minúsculas. Puede obtener este valor en Opciones móviles, en el panel de control Push.

####bluemixRegionSuffix
{: bluemixRegionSuffix}

Especifica la ubicación en la que se aloja la aplicación. Puede utilizar uno de estos tres valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

###Inicializar el SDK push del cliente

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "AppGUID");
```
####AppGUID
{: AppGUID}

Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.

## Registro de dispositivos Android
{: #android_register}

Utilice la API `MFPPush.register()` para registrar el dispositivo con el servicio {{site.data.keyword.mobilepushshort}}. Para efectuar el registro para dispositivos Android, añada la información de Google Cloud Messaging (GCM) en el panel de control de configuración del servicio {{site.data.keyword.mobilepushshort}} de Bluemix. Para obtener más información, consulte [Configuración de credenciales para Google Cloud Messaging](t_push_provider_android.html).

Copie y pegue los siguientes fragmentos de código en la aplicación para móviles de
                    Android.

```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
	    @Override
	    public void onSuccess(String deviceId) {
	           //maneje el éxito aquí
	    }
	    @Override
	    public void onFailure(MFPPushException ex) {
	    //maneje la anomalía aquí
	    }
	});
```

```
	//Maneja la notificación cuando llega
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
	    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Manejar la notificación push
	    }
	};
```


## Recepción de notificaciones push en dispositivos Android
{: #android_receive}

Para registrar el objeto notificationListener con push, invoque el método **MFPPush.listen()**. Este método normalmente se llama desde
                                el método **onResume()** de la actividad que maneja
                            las notificaciones push.

1. Para registrar el objeto notificationListener con push, invoque el método **listen()**. Este método normalmente se llama desde
                                el método **onResume()** de la actividad que maneja
                            las notificaciones push.

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
  ```
2. Cree el proyecto y ejecútelo en el dispositivo o en el emulador. Cuando se invoque el método onSuccess() para la escucha de respuestas en el método register(), confirmará que el dispositivo se ha registrado correctamente con el servicio {{site.data.keyword.mobilepushshort}}. En este momento puede enviar un mensaje tal como se describe en Envío de notificaciones push básicas.
3. Verifique que los dispositivos hayan recibido la notificación. Si la aplicación se encuentra en segundo
          plano, la notificación se manejará mediante el
            **MFPPushNotificationListener**. Si la aplicación se encuentra en segundo plano, se mostrará un
          mensaje en la barra de notificaciones.


## Envío de {{site.data.keyword.mobilepushshort}} básicas
{: #send}

Una vez que haya desarrollado sus aplicaciones, puede enviar notificaciones push básicas (sin
  utilizar etiquetas, identificadores, cargas útiles adicionales o archivos de sonido).

1. En **Elegir la audiencia**, seleccione una de las siguientes audiencias:
      **Todos los dispositivos**, o por plataforma: **Sólo dispositivos iOS** o
      **Sólo dispositivos Android**. 

	**Nota**: Cuando seleccione la opción **Todos los dispositivos**, todos los dispositivos suscritos a notificaciones push recibirán notificaciones.

![pantalla Notificaciones](images/tag_notification.jpg)

2. En **Crear la notificación**, especifique el mensaje y, a continuación, pulse **Enviar**.
3. Verifique que los dispositivos hayan recibido la notificación. La captura de pantalla siguiente muestra un recuadro de alerta que maneja una notificación push
en el primer plano en un dispositivo Android.

![Notificación push en primer plano en Android](images/Android_Screenshot.jpg)

La captura de pantalla siguiente muestra una notificación push en segundo plano para Android.

![Notificación push en el fondo en Android](images/background.jpg)



## Siguientes pasos
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar
        las notificaciones basadas en código y las opciones avanzadas.

Añada estas funciones del servicio de notificaciones push a la app.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones push avanzadas](t_advance_notifications.html).
