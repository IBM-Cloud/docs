---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de aplicaciones Android para recibir {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Última actualización: 14 de febrero de 2017
{: .last-updated}

Puede habilitar las aplicaciones de Android para recibir notificaciones push en sus dispositivos. Android Studio es un requisito previo y es el método recomendado para crear proyectos de Android. Es esencial tener un conocimiento básico de Android Studio.

## Instalación del SDK Push del cliente con Gradle
{: #android_install}

En esta sección se describe cómo instalar y utilizar el SDK Push del cliente para seguir desarrollando sus aplicaciones Android.

El SDK push de servicios móviles de Bluemix® se puede añadir mediante Gradle. Gradle descarga automáticamente artefactos desde los repositorios y los deja a disposición de su aplicación Android. Asegúrese de que ha configurado correctamente Android Studio y el SDK de Android Studio. Para obtener más información sobre cómo configurar el sistema, consulte [Visión general de Android Studio ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.android.com/tools/studio/index.html){: new_window}. Para obtener información sobre Gradle, consulte [Configuración de compilaciones Gradle ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}.

Tras crear y abrir la aplicación para móvil, siga estos pasos utilizando Android Studio.

1. Añada dependencias al archivo **build.gradle** a nivel de módulo. 	

	- Añada la siguiente dependencia para incluir el SDK de cliente push de Bluemix™ Mobile Services y el SDK de Google Play Services a las dependencias de ámbito de compilación.
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- Añada las siguientes dependencias para importar las sentencias necesarias para el fragmento de código.
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- Añada la siguiente dependencia al archivo **build.gradle** a nivel de módulo.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. Añada las siguientes dependencias al archivo **build.gradle** a nivel de proyecto.
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. En el archivo **AndroidManifest.xml**, añada los permisos siguientes. Para ver un manifiesto de ejemplo, consulte la [Aplicación de ejemplo helloPush de Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}. Para ver un archivo de ejemplo de Gradle, consulte el [Archivo de compilación de ejemplo de Gradle ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}.
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
Aquí encontrará más información sobre [permisos de Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://developer.android.com/guide/topics/security/permissions.html){: new_window}.

4. Añade los valores de intención de notificación para la actividad. Este valor inicia la aplicación cuando el usuario pulsa la notificación recibida desde el área de notificación.
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
```
	{: codeblock}
**Nota**: sustituya *Your_Android_Package_Name* en la acción anterior por el nombre del paquete de aplicaciones utilizado en la aplicación.

5. Añada el servicio de intento de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM) y los filtros de intento para las notificaciones de sucesos RECEIVE y REGISTRATION.
```
	<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService"
    android:exported="true" >
    	<intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
	</service>
<service
    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
    </intent-filter>
	</service>
```
    {: codeblock}

6. El servicio de {{site.data.keyword.mobilepushshort}} da soporte a la recuperación de notificaciones individuales desde la bandeja de notificaciones. Para las notificaciones a las que se accede desde la bandeja de notificaciones, se le proporcionará un controlador sólo para la notificación que se ha pulsado. Todas las notificaciones se mostrarán cuando la aplicación se abra normalmente. Actualice el archivo **AndroidManifest.xml** con el siguiente fragmento de código para utilizar esta funcionalidad:

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

Para configura el proyecto FCM y obtener las credenciales, consulte [Cómo obtener el ID de remitente y la clave de la API](t_push_provider_android.html). Siga estos pasos en la consola de Firebase Cloud Messaging (FCM).

1. En la consola de Firebase, pulse el icono **Configuración del proyecto**.
    ![Configuración del proyecto Firebase](images/FCM_4.jpg)

3. Seleccione **AÑADIR APP** o el **icono Añadir Firebase a la app Android** en el separador General del panel Sus apps.
    ![Adición de Firebase a Android](images/FCM_5.jpg)

4. En la ventana Añadir Firebase a la app Android, añada **com.ibm.mobilefirstplatform.clientsdk.android.push** como Nombre de paquete. El campo Apodo de app es opcional. Pulse **AÑADIR APP**. 
    ![Ventana Adición de Firebase a Android](images/FCM_1.jpg)

5. Incluya el nombre de paquete de la aplicación, especificando el nombre de paquete en la ventana Añadir Firebase a la app Android. El campo Apodo de app es opcional. Pulse **AÑADIR APP**. 

	![Adición del nombre de paquete de la aplicación](images/FCM_2.jpg)

6. Se generará el archivo `google-services.json`. Copie el archivo `google-services.json` al directorio raíz del módulo de aplicación de Android. Tenga en cuenta que el archivo `google-service.json` incluye los nombres de paquete añadidos.

    ![Adición del archivo json al directorio raíz de la aplicación](images/FCM_7.jpg)

5. En la ventana Añadir Firebase a la app Android, pulse **Continuar** y, a continuación, **Finalizar**. 

  

Cree y ejecute la aplicación.

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
//Inicializar SDK de cliente Push para Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
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
    	public void onSuccess(String response) {
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

1. Para registrar el objeto notificationListener con push, invoque el método **listen()**. Se suele llamar a este método desde los métodos **onResume()** y **onPause** de la actividad que gestiona las notificaciones push.


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



```
	@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
	}
```
	{: codeblock}

2. Cree el proyecto y ejecútelo en el dispositivo o en el emulador. Cuando se invoque el método onSuccess() para la escucha de respuestas en el método register(), confirmará que el dispositivo se ha registrado correctamente con el servicio {{site.data.keyword.mobilepushshort}}. En este momento puede enviar un mensaje tal como se describe en Envío de notificaciones push básicas.
3. Verifique que los dispositivos hayan recibido la notificación. Si la aplicación se encuentra en segundo plano, la notificación se manejará mediante el **MFPPushNotificationListener**. Si la aplicación se encuentra en segundo plano, se mostrará un mensaje en la barra de notificaciones.

## Supervisión de las notificaciones push en dispositivos Android
{: #android_monitor}

Para supervisar el estado actual de la notificación en la aplicación, puede implementar la interfaz `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` y definir el método onStatusChange(String messageId, MFPPushNotificationStatus status). 

El **messageId** es el identificador del mensaje enviado desde el servidor.  **MFPPushNotificationStatus** define el estado de las notificaciones como valores:

- **RECEIVED**: La app ha recibido la notificación. 
- **QUEUED**: La app pone en cola la notificación para invocar la escucha de notificación. 
- **OPENED**: El usuario abre la notificación pulsando la notificación de la bandeja o iniciándola desde el icono de la app o cuando la app está en primer plano. 
- **DISMISSED**: El usuario borra/descarta la notificación de la bandeja.

Debe registrar la clase **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener** con MFPPush.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
}
	});
```
    {: codeblock}


### Escucha del estado DISMISSED

Puede elegir escuchar en el estado DISMISSED en cualquiera de las siguientes condiciones:

- Cuando la app está activa (se ejecuta en primer o segundo plano)

  Añada el fragmento de código al archivo `AndroidManifest.xml`:

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- Cuando la app está activa (se ejecuta en primer o segundo plano) y no se ejecuta (cerrada)

Debe extender el receptor de difusión **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler** y sustituir el método **onReceive()**, donde el **MFPPushNotificationStatusListener** debe estar registrado antes de invocar el método **onReceive()** de la clase base.

```
	public class MyDismissHandler extends MFPPushNotificationDismissHandler {
	@Override
public void onReceive(Context context, Intent intent) {
	MFPPush.getInstance().setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
	// Handle status change
}
	});
super.onReceive(context, intent);
}
	}
```
    {: codeblock}


Añada el fragmento de código siguiente al archivo `AndroidManifest.xml`:

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

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

### Valores opcionales de Android para el envío de notificaciones
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

Añada estas características de servicio de notificaciones push a la app. Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Habilitación de notificaciones push avanzadas](t_advance_badge_sound_payload.html).
