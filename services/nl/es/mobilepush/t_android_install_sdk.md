---

copyright:
 años: 2015, 2016

---

# Instalación del SDK Push del cliente con Gradle
{: #android_install}

En esta sección se describe cómo instalar y utilizar el SDK Push del cliente para seguir desarrollando
    sus aplicaciones Android.

El SDK push de servicios móviles de Bluemix® se puede añadir mediante Gradle. Gradle
          descarga automáticamente artefactos desde los repositorios y los deja a disposición de su aplicación
          Android. Asegúrese de que ha configurado correctamente Android Studio y el SDK de Android
          Studio. Para obtener más información sobre cómo configurar el sistema, consulte [Visión general de Android Studio](https://developer.android.com/tools/studio/index.html). Para obtener información sobre Gradle, consulte [Configuración de compilaciones de Gradle](http://developer.android.com/tools/building/configuring-gradle.html).

1. En Android Studio, tras crear y abrir la aplicación móvil, abra el archivo **build.gradle** de la aplicación. A continuación, añada las siguientes dependencias a la aplicación móvil. Estas sentencias de importación son necesarias para los fragmentos de código que se enumeran a continuación:

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. Añada las dependencias siguientes a la aplicación móvil. Las líneas siguientes añaden el SDK de cliente push de Bluemix™ Mobile Services y el SDK de Google Play Services a las dependencias de ámbito de compilación.

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+'
	  compile 'com.google.android.gms:play-services:7.8.0'
	}  
	```
1. En el archivo **AndroidManifest.xml**, añada los permisos siguientes. Para ver un manifiesto de muestra, consulte [Aplicación de ejemplo helloPush de Android](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Para ver un archivo Gradle de muestra, consulte [Archivo Gradle de compilación de muestra](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

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

	Puede leer más información sobre los [permisos de Android](http://developer.android.com/guide/topics/security/permissions.html) aquí.

1. Añade los valores de intención de notificación para la actividad. Este valor inicia la
          aplicación cuando el usuario pulsa la notificación recibida desde el área de notificación.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Nota**: sustituya *Your_Android_Package_Name* en la acción anterior con el nombre del paquete de aplicaciones utilizado en la aplicación.

1. Añade el servicio de intento de Google Cloud Messaging (GCM) y los filtros de intento para las notificaciones de sucesos RECEIVE.

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
