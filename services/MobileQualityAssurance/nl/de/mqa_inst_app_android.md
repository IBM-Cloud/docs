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


# MQA mit einer Android-App instrumentieren (veraltet)
{: #instrumentAnd}


Zur Verwendung von {{site.data.keyword.mqafull}} mit Ihrer Android-App müssen Sie das SDK herunterladen und es instrumentieren, indem Sie mithilfe der Android Studio-Entwicklungsumgebung einige Änderungen vornehmen.
{: shortdesc}

Bevor Sie eine App mit {{site.data.keyword.mqa}} instrumentieren können, müssen Sie über ein {{site.data.keyword.Bluemix}}-Konto und die ordnungsgemäß installierte Version der Entwicklungsumgebung für die Plattformen der App verfügen, die Sie instrumentieren.

Führen Sie die folgenden Tasks aus, um {{site.data.keyword.mqa}} für die Arbeit mit Ihrer Android-App zu instrumentieren:

1. Fügen Sie die erforderlichen Berechtigungen und das heruntergeladene SDK zu Ihrem Android-Projekt hinzu.

	1. Öffnen Sie Ihr Projekt in Android Studio.
	
	2. Wählen Sie **Datei** > **Neu** > **Neues Modul** aus.
	
	3. Wählen Sie im Assistenten für die Erstellung eines neuen Moduls unter *Weitere Module* die Option **.JAR- oder .AAR-Paket importieren** aus und klicken Sie anschließend auf **Weiter**.
	
	4. Geben Sie im Feld für den Dateinamen den Namen der {{site.data.keyword.mqa}}-SDK-AAR-Datei (.aar) ein, die Sie heruntergeladen haben, und klicken Sie auf **Fertigstellen**.
	
	5. Beginnen Sie mit dem Hinzufügen von {{site.data.keyword.mqa}} zu Ihrer mobilen App in Ihrem Android Studio-Projekt, indem Sie **Datei** > **Projektstruktur** auswählen.
	
	6. Wählen Sie das Modul für Ihre App im Fenster für die Projektstruktur aus und wählen Sie die Registerkarte *Abhängigkeiten* aus.
	
	7. Wählen Sie **+** und anschließend die Option **Modulabhängigkeit** aus.
	
	8. Wählen Sie im Fenster für die Modulauswahl das {{site.data.keyword.mqa}}-Android-Modul aus, das Sie importiert haben, und klicken Sie anschließend auf **OK**.
	
	9. Wählen Sie **OK** aus, um das Fenster für die Projektstruktur zu schließen.
	
	10. Aktualisieren Sie die Android-Manifestdatei, indem Sie sicherstellen, dass die folgenden Aktivitäten in einem Eintrag des Typs `<application>` enthalten sind:
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. Stellen Sie sicher, dass die folgenden erforderlichen Berechtigungen in der Manifestdatei aufgeführt sind:
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	Der folgende Code ist ein mögliches Beispiel für Ihre Datei `AndroidManifest.xml`:

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

2. Konfigurieren Sie bei jeder Anmeldung einen neue zu startende Sitzung.

	1. Fügen Sie das folgende Code-Snippet zur Klasse `MainActivity` Ihrer App hinzu; diese ist in der Datei `MainActivity.java` enthalten. Dabei wird Ihr Anwendungsschlüssel zum Senden von Daten an {{site.data.keyword.mqa}} verwendet.
		 
		```
		public static final String APP_KEY = "Eigener Anwendungsschlüssel";
		```
		{: codeblock}
		
		Ersetzen Sie *Eigener Anwendungsschlüssel* durch Ihren Anwendungsschlüssel von der Seite für die App-Einstellungen von {{site.data.keyword.mqa}}.
	
	2. Zur Nutzung des {{site.data.keyword.mqa}}-Konfigurationsbuilders müssen Sie zunächst die folgenden Elemente importieren, indem Sie sie zur Datei `MainActivity.java` Ihrer App hinzufügen: 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. Erstellen Sie im Ereignise 'onCreate' Ihrer Klasse 'MainActivity' ein Konfigurationsobjekt. Dieses Objekt stellt verschiedene Methoden bereit, mit deren Hilfe Sie Konfigurationselemente angeben können. Am Ende der Objektkonfiguration rufen Sie eine Methode des Typs build() auf, um das Objekt fertigzustellen. Im Folgenden sehen Sie ein Beispiel einer abgeschlossenen Konfiguration:
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. Fügen Sie in der Anwendungsklasse Ihrer App Code für die Konfiguration und den Start von {{site.data.keyword.mqa}}-Sitzungen durch Aufrufen der Methode `MQA.startNewSession()` des Ereignisses `onCreate` Ihrer Anwendungsklasse hinzu.
	
	    Beispiel: 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        Erweitertes Beispiel:

		<pre><code>
		// import Android class
        import android.app.Application;

        // Make sure that you import the quality assurance 
		  application
        import com.ibm.mqa.MQA;
        import com.ibm.mqa.MQA.Mode;
        import com.ibm.mqa.config.Configuration;

        // Optionally import the quality assurance 
		  application's logging functions
        import com.ibm.mqa.Log;

        public class MyApplication extends Application {
 
	    public static final String APP_KEY = 
		  "Your_Application_Key_Goes_Here";
 
	    @Override
	    public void onCreate() {
		super.onCreate();
		 
		Configuration configuration = new 
		  Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance 
		  application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance 
		  production mode.  This example is for preproduction mode, 
		//Use .withMode(Mode.MARKET) for production mode. 
		.build();
 
		MQA.startNewSession(this, configuration);
	       }
             }
		</code></pre>
		{: codeblock}

3. Fahren Sie mit den Schritten auf der Seite [Einführung in {{site.data.keyword.mqa}}](index.html) fort.


# Zugehörige Links
{: #rellinks notoc}

## Zugehörige Links
{: #general notoc}
* [Einführung in {{site.data.keyword.mqa}}](index.html){:new_window}
