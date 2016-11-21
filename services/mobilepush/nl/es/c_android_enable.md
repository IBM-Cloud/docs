---

copyright:
 years: 2015 2016

---


# Habilitación de aplicaciones Android para recibir {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Última actualización: 19 de octubre de 2016
{: .last-updated}

Puede habilitar aplicaciones Android para recibir {{site.data.keyword.mobilepushshort}} en sus dispositivos. Android Studio es un requisito previo y es el método recomendado para crear proyectos de Android. Es esencial tener un conocimiento básico de Android Studio.

## Instalación del SDK Push del cliente con Gradle
{: #android_install}

En esta sección se describe cómo instalar y utilizar el SDK Push del cliente para seguir desarrollando sus aplicaciones Android.

El SDK push de servicios móviles de Bluemix® se puede añadir mediante Gradle. Gradle descarga automáticamente artefactos desde los repositorios y los deja a disposición de su aplicación Android. Asegúrese de que ha configurado correctamente Android Studio y el SDK de Android Studio. Para obtener más información sobre cómo configurar el sistema, consulte [Visión general de Android Studio](https://developer.android.com/tools/studio/index.html). Para obtener información sobre Gradle, consulte [Configuración de compilaciones de Gradle](http://developer.android.com/tools/building/configuring-gradle.html).

1. En Android Studio, tras crear y abrir la aplicación móvil, abra el archivo **build.gradle** de la aplicación.
2. Añada las dependencias siguientes a la aplicación móvil. Las líneas siguientes añaden el SDK del cliente push de servicios de Bluemix™ Mobile y el SDK de los servicios de Google Play a las dependencias del ámbito de compilación.
```
com.ibm.mobilefirstplatform.clientsdk.android:push:2.+
```
    {: codeblock}
2. Cree el proyecto para asegurarse de que se resuelvan las dependencias.
3. Añada las dependencias siguientes a la aplicación móvil. Estas sentencias de importación son necesarias para los fragmentos de código:
```
import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
```
    {: codeblock}

2. En el archivo **AndroidManifest.xml**, añada los permisos siguientes. Para ver un manifiesto de muestra, consulte [Aplicación de ejemplo helloPush de Android](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Para ver un archivo Gradle de muestra, consulte [Archivo Gradle de compilación de muestra](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).
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
	{: codeblock}
 Aquí puede leer más información sobre los [permisos de Android](http://developer.android.com/guide/topics/security/permissions.html).

4. Añade los valores de intención de notificación para la actividad. Este valor inicia la aplicación cuando el usuario pulsa la notificación recibida desde el área de notificación.
```
<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```
	{: codeblock}
**Nota**: sustituya *Your_Android_Package_Name* en la acción anterior por el nombre del paquete de aplicaciones utilizado en la aplicación.

5. Añada el servicio de intento de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM) y los filtros de intento para las notificaciones de sucesos RECEIVE.
```
<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService" />
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
    {: codeblock}

6. El servicio de {{site.data.keyword.mobilepushshort}} da soporte a la recuperación de notificaciones individuales desde la bandeja de notificaciones. Para las notificaciones a las que se accede desde la bandeja de notificaciones, se le proporcionará un controlador sólo para la notificación que se ha pulsado. Todas las notificaciones se mostrarán cuando la aplicación se abra normalmente. Actualice el archivo **AndroidManifest.xml** con el siguiente fragmento de código para utilizar esta funcionalidad:

```
<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```

## Inicialización del SDK push para aplicaciones Android
{: #android_initialize}

Un lugar común para colocar el código de inicialización se encuentra en el método onCreate de la actividad principal en su aplicación Android. Hay dos componentes del SDK que deben inicializarse. Uno es el SDK principal y el otro es el SDK push creado en la parte superior del SDK principal.

###Inicializar el SDK principal

```
// Inicializar el SDK para Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

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
	{: codeblock}

####AppGUID
{: appguid_initialize_client_push_sdk}

Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}. Este valor distingue entre mayúsculas y minúsculas. Abra el panel de control Notificación Push y seleccione el separador Configurar. Puede obtener este valor en Opciones móviles, en el separador Configurar del panel de control Servicio de notificaciones Push. 

## Registro de dispositivos Android
{: #android_register}

Utilice la API `MFPPush.register()` para registrar el dispositivo con el servicio {{site.data.keyword.mobilepushshort}}. Para efectuar el registro para dispositivos Android, añada la información de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM) en el panel de control de configuración del servicio {{site.data.keyword.mobilepushshort}} de Bluemix. Para obtener más información, consulte [Configuración de credenciales para Google Cloud Messaging](t_push_provider_android.html).

Copie los siguientes fragmentos de código en la aplicación para móviles de Android.

```
//Registre dispositivos Android
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
	{: codeblock}


```
//Maneja la notificación cuando llega
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Manejar la notificación push
	    }
};
```
	{: codeblock}

## Recepción de notificaciones push en dispositivos Android
{: #android_receive}

Para registrar el objeto notificationListener con push, invoque el método **MFPPush.listen()**. Este método normalmente se llama desde el método **onResume()** de la actividad que maneja las notificaciones push.

1. Para registrar el objeto notificationListener con push, invoque el método **listen()**. Este método normalmente se llama desde el método **onResume()** de la actividad que maneja las notificaciones push.
```
@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
       push.listen(notificationListener);
	   }
}
```
	{: codeblock}

2. Cree el proyecto y ejecútelo en el dispositivo o en el emulador. Cuando se invoque el método onSuccess() para la escucha de respuestas en el método register(), confirmará que el dispositivo se ha registrado correctamente con el servicio {{site.data.keyword.mobilepushshort}}. En este momento puede enviar un mensaje tal como se describe en Envío de notificaciones push básicas.
3. Verifique que los dispositivos hayan recibido la notificación. Si la aplicación se encuentra en segundo plano, la notificación se manejará mediante el **MFPPushNotificationListener**. Si la aplicación se encuentra en segundo plano, se mostrará un mensaje en la barra de notificaciones.


## Envío de {{site.data.keyword.mobilepushshort}} básicas
{: #send}

Una vez que haya desarrollado sus aplicaciones, puede enviar notificaciones push básicas.

Para ello, realice estos pasos:

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione la opción **Enviar a**. Las opciones admitidas son **Dispositivo por etiqueta**, **ID de dispositivo**, **ID de usuario**, **Dispositivos Android**, **Dispositivos iOS**, **Notificaciones web** y **Todos los dispositivos**.
**Nota**: Cuando seleccione la opción **Todos los dispositivos**, todos los dispositivos suscritos a {{site.data.keyword.mobilepushshort}} recibirán notificaciones.
![pantalla Notificaciones](images/tag_notification.jpg)

2. En el campo **Mensaje**, redacte el mensaje. Elija configurar los valores opcionales según sea necesario.
3. Pulse **Enviar**.
3. Verifique que los dispositivos hayan recibido la notificación.

La captura de pantalla siguiente muestra un recuadro de alerta que maneja una notificación push
en el primer plano en un dispositivo Android.

![Notificación push en primer plano en Android](images/Android_Screenshot.jpg)

La captura de pantalla siguiente muestra una notificación push en segundo plano para Android.

![Notificación push en el fondo en Android](images/background.jpg)

### Valores opcionales para el envío de notificaciones
{: #send_otpional_setting}

Puede personalizar aún más los valores de {{site.data.keyword.mobilepushshort}} para el envío de notificaciones a dispositivos Android. Se admiten las siguientes opciones de personalización.
![Valores personalizados de Android](images/android_custom_settings.jpg)

- **Contraer clave**: las claves contraídas se adjuntan a las notificaciones. Si llegan varias notificaciones de forma secuencias con la misma clave contraída cuando el dispositivo está desconectado, estas se contraerán. Cuando el dispositivo vuelva a conectarse, recibirá las notificaciones del servidor FCM/GCM y mostrará solo la última notificación transportada con la misma clave contraída. Si no se establece esta clave contraída, se almacenarán los mensajes nuevos y antiguos para entregarlos más adelante.
- **Sonido**: indica un fragmento de sonido que se reproducirá al recibir una notificación. Da soporte a la opción predeterminada o al nombre de un recurso de sonido incorporado en la aplicación.
- **Icono**: Especifique el nombre del icono que se mostrará para la notificación. Asegúrese de que haya empaquetado el icono en la carpeta res/drawable, con la aplicación cliente.
- **Prioridad**: especifica las opciones para asignar la prioridad de entrega a los mensajes. Una prioridad `high` o `max` dará como resultado una notificación de aviso, mientras que los mensajes con prioridad `low` o `default` no establecerán conexiones de red en un dispositivo en modo suspendido. Para los mensajes con la opción definida en `min`, se enviará una notificación silenciosa.
- **Visibilidad**: puede optar por definir la opción de visibilidad de notificación en `public` o `private`. La opción `private` limita la visualización pública y puede habilitarla si el dispositivo está protegido mediante pin o un patrón y si el valor de notificación está definido para ocultar contenido privado de las notificaciones. Cuando la visibilidad se establece como `private`, debe mencionarse algún campo de "redacción". Solo se mostrará el contenido especificado en el campo de redacción en la pantalla bloqueada del dispositivo. Si se elige `public` se entregarán notificaciones que se pueden leer libremente.
- **Tiempo de duración**: este valor se establece en segundos. Si no se especifica este parámetro, el servidor FCM/GCM almacenará el mensaje cuatro semanas e intentará entregarlo. La validez caduca transcurridas cuatro semanas. El intervalo de valores posible es de 0 a 2.419.200 segundos.
- **Retrasar cuando esté desocupado**: si se define como `true`, el servidor FCM/GCM no entregará la notificación cuando el dispositivo esté desocupado. Establezca este valor en `false` para garantizar que se entregan notificaciones aunque el dispositivo esté desocupado.
- **Sync**: al definir esta opción como `true`, se sincronizan las notificaciones de todos los dispositivos registrados. Si un usuario dispone de varios dispositivos con la misma aplicación instalada, al leer la notificación en un dispositivo se suprimirán las notificaciones del resto de los dispositivos. Debe asegurarse que está registrado al servicio {{site.data.keyword.mobilepushshort}} con userId para que esta opción funcione.
- **Carga útil adicional**: permite especificar valores personalizados de carga útil para las notificaciones.


## Pasos siguientes
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar las notificaciones basadas en código y las opciones avanzadas.

Añada estas características de Servicio de notificaciones push a la aplicación.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Habilitación de notificaciones push avanzadas](t_advance_badge_sound_payload.html).
