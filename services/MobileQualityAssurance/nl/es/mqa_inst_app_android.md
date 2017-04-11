---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Preparación de MQA con una app de Android (en desuso)
{: #instrumentAnd}


Para utilizar {{site.data.keyword.mqafull}} con la app de Android, debe descargar el SDK y prepararlo realizando algunos cambios mediante el entorno de desarrollo de Android Studio.
{: shortdesc}

Para poder preparar una app con {{site.data.keyword.mqa}}, debe tener una cuenta de {{site.data.keyword.Bluemix}} y la versión correctamente instalada del entorno de desarrollo para las plataformas de la app que está preparando.

Para preparar {{site.data.keyword.mqa}} para que funcione con la app de Android, lleve a cabo las siguientes tareas:

1. Añada los permisos necesarios y el SDK descargado al proyecto de Android.

	1. Abra el proyecto en Android Studio.
	
	2. Seleccione **Archivo** > **Nuevo** > **Módulo nuevo**.
	
	3. En el asistente *Crear módulo nuevo*, en *Más módulos*, seleccione **Importar paquete .JAR o .AAR** y, a continuación, pulse **Siguiente**.
	
	4. En el campo Nombre de archivo, escriba el nombre del archivo .aar del SDK de {{site.data.keyword.mqa}} que ha descargado y pulse **Finalizar**.
	
	5. Comience añadiendo {{site.data.keyword.mqa}} a su app para móvil en el proyecto de Android Studio seleccionando **Archivo** > **Estructura del proyecto**.
	
	6. Seleccione el módulo para la app en la ventana Estructura del proyecto y seleccione el separador *Dependencias*.
	
	7. Seleccione **+** y, a continuación, seleccione **Dependencia de módulo**.
	
	8. En la ventana Elegir módulos, seleccione el módulo de Android de {{site.data.keyword.mqa}} que haya importado y, a continuación, pulse **Aceptar**.
	
	9. Seleccione **Aceptar** para cerrar la ventana Estructura del proyecto.
	
	10. Actualice el archivo de manifiesto de Android asegurándose de que las actividades siguientes estén incluidas en una entrada `<application>`:
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. Asegúrese de que los permisos necesarios siguientes estén listados en el archivo de manifiesto:
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	El código siguiente muestra un ejemplo posible del archivo `AndroidManifest.xml`:

		```
		<?xml version="1.0" encoding="utf-8"?>
        <manifest xmlns:android=
		  "http://schemas.android.com/apk/res/android"
        package="com.applause.android"
        android:versionCode="6"
        android:versionName="2.3" >

        <uses-sdk android:minSdkVersion="8" />

        <!-- Required permission -->
        <uses-permission android:name=
		  "android.permission.INTERNET" /> 
        <uses-permission android:name=
		  "android.permission.READ_EXTERNAL_STORAGE" />
        <uses-permission android:name=
		  "android.permission.SYSTEM_ALERT_WINDOW" /> 

        <!-- Optional permissions -->
  
        <uses-permission android:name=
		  "android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name=
		  "android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name=
		  "android.permission.READ_PHONE_STATE" />
        <uses-permission android:name=
		  "android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name=
		  "android.permission.ACCESS_FINE_LOCATION" />
        <uses-permission android:name=
		  "android.permission.BLUETOOTH" />
        <!-- ... rest of your application's 
		  permissions, if any -->

        <application
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme"
        android:name=".MyApplication' >

        <!-- ... rest of your application's components -->

        <!-- Quality assurance application activities -->
        <activity android:name=
		  "com.ibm.mqa.ui.ProblemActivity" />
        <activity android:name=
		  "com.ibm.mqa.ui.FeedbackActivity" />
        <activity android:name=
		  "com.ibm.mqa.ui.ScreenshotEditorActivity" /> 
        </application>

        </manifest>
		```
	    {: codeblock}

2. Configure que empiece una sesión nueva con cada inicio de sesión.

	1. Añada el siguiente fragmento de código a la clase `MainActivity` de la app, que se encuentra en el archivo `MainActivity.java`. Utiliza su clave de aplicación para enviar datos a {{site.data.keyword.mqa}}.
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		Sustituya *Your_Application_Key_Goes_Here* por su clave de aplicación desde la página Configuración de la app de {{site.data.keyword.mqa}}.
	
	2. Para utilizar el compilador de configuración de {{site.data.keyword.mqa}}, importe en primer lugar los elementos siguientes añadiéndolos al archivo `MainActivity.java` de su app: 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. Cree un objeto de configuración en el suceso onCreate de la clase MainActivity. Este objeto proporciona varios métodos que puede utilizar para especificar elementos de configuración. Al terminar la configuración del objeto, puede invocar un método build() para finalizar el objeto. A continuación se muestra un ejemplo de una configuración completa:
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Proporciona la APP_KEY de la aplicación de control de calidad
		.withMode(Mode.QA) //Selecciona la modalidad de aplicación del control de calidad
		.build();
		```
		{: codeblock}
	
	4. En la clase Aplicación de la app, añada código para configurar e iniciar sesiones de {{site.data.keyword.mqa}} invocando el método `MQA.startNewSession()` en el suceso `onCreate` de la clase Aplicación.
	
	    Por ejemplo: 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        Ejemplo ampliado:

		<pre><code>
		// importar clase Android
        import android.app.Application;

        // Asegúrese de importar la aplicación de control de calidad
		
        import com.ibm.mqa.MQA;
        import com.ibm.mqa.MQA.Mode;
        import com.ibm.mqa.config.Configuration;

        // Opcionalmente, importe las funciones de registro de la aplicación de control de calidad
		
        import com.ibm.mqa.Log;

        public class MyApplication extends Application {
 
	    public static final String APP_KEY = 
		  "Your_Application_Key_Goes_Here";
 
	    @Override
	    public void onCreate() {
		super.onCreate();
		 
		Configuration configuration = new 
		  Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Proporciona la APP_KEY de la aplicación de control de calidad
		
		.withMode(Mode.QA) //Selecciona la modalidad de producción del control de calidad. Este ejemplo es para la modalidad de preproducción,
		//Utilice .withMode(Mode.MARKET) para la modalidad de producción.
		.build();
 
		MQA.startNewSession(this, configuration);
	       }
             }
		</code></pre>
		{: codeblock}

3. Continúe con los pasos de la página [Iniciación a {{site.data.keyword.mqa}}](index.html).


# Enlaces relacionados
{: #rellinks notoc}

## Enlaces relacionados
{: #general notoc}
* [Iniciación a {{site.data.keyword.mqa}}](index.html){:new_window}
