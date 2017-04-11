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


# Strumentazione di MQA con un'applicazione Android (Obsoleto)
{: #instrumentAnd}


Per utilizzare {{site.data.keyword.mqafull}} con la tua applicazione Android, devi scaricare l'SDK e strumentarla effettuando alcune modifiche utilizzando l'ambiente di sviluppo Android Studio.
{: shortdesc}

Prima di poter strumentare un'applicazione con {{site.data.keyword.mqa}}, devi avere un account {{site.data.keyword.Bluemix}} e aver correttamente installato la versione dell'ambiente di sviluppo per le piattaforme dell'applicazione che stai strumentando.

Per strumentare {{site.data.keyword.mqa}} in modo che utilizzi la tua applicazione Android, completa la seguente procedura:

1. Aggiungi le autorizzazioni necessarie e la SDK scaricata al tuo progetto Android.

	1. Apri il tuo progetto in Android Studio.
	
	2. Seleziona **File** > **New** > **New Module**.
	
	3. Nella procedura guidata *Create New Module*, in *More Modules*, seleziona **Import .JAR or .AAR Package** e fai quindi clic su **Next**.
	
	4. Nel campo del nome del file, immetti il nome del file .aar dell'SDK {{site.data.keyword.mqa}} che hai scaricato e fai clic su **Finish**.
	
	5. Inizia aggiungendo {{site.data.keyword.mqa}} alla tua applicazione mobile nel tuo progetto Android Studio selezionando **File** > **Project Structure**.
	
	6. Seleziona il modulo per la tua applicazione nella finestra Project Structure e seleziona la scheda *Dependencies*.
	
	7. Seleziona **+** e quindi **Module Dependency**.
	
	8. Nella finestra Choose Modules, seleziona il modulo Android {{site.data.keyword.mqa}} che hai importato e quindi fai clic su **OK**.
	
	9. Seleziona **OK** per chiudere la finestra Project Structure.
	
	10. Aggiorna il file manifest Android assicurandoti di includere le seguenti attività in una voce `<application>`:
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. Assicurati che siano elencate le seguenti autorizzazioni nel file manifest:
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	Il seguente codice mostra un esempio possibile del tuo file `AndroidManifest.xml`:

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

2. Configura una nuova sessione da utilizzare con ogni accesso.

	1. Aggiungi il seguente frammento di codice alla classe `MainActivity` della tua applicazione, che si trova nel file `MainActivity.java`. Utilizza la tua chiave di applicazione per inviare dati a {{site.data.keyword.mqa}}.
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		Sostituisci *Your_Application_Key_Goes_Here* con la tua chiave di applicazione dalla pagina delle impostazioni dell'applicazione di {{site.data.keyword.mqa}}.
	
	2. Per utilizzare il builder di configurazione {{site.data.keyword.mqa}}, importa prima i seguenti elementi aggiungendoli al file `MainActivity.java` della tua applicazione: 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. Crea un oggetto di configurazione nell'evento onCreate della tua classe MainActivity. Questo oggetto fornisce molti metodi che puoi utilizzare per specificare gli elementi di configurazione. Dopo aver terminato la configurazione dell'oggetto, richiama un metodo build() per finalizzare l'oggetto. Il seguente è un esempio di una configurazione completata:
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Fornisce la APP_KEY dell'applicazione del controllo qualità
		.withMode(Mode.QA) //Seleziona la modalità dell'applicazione del controllo qualità
		.build();
		```
		{: codeblock}
	
	4. Nella classe Application della tua applicazione, aggiungi il codice per configurare ed avviare le sessioni {{site.data.keyword.mqa}} richiamando il metodo `MQA.startNewSession()` nell'evento `onCreate` della tua classe Application.
	
	    Ad esempio:  
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        Esempio esteso:

		<pre><code>
		// importa classe Android
        import android.app.Application;

        // Assicurati di aver importato l'applicazione del controllo
		  qualità
        import com.ibm.mqa.MQA;
        import com.ibm.mqa.MQA.Mode;
        import com.ibm.mqa.config.Configuration;

        // Facoltativamente importa le funzioni di accesso
		  dell'applicazione del controllo qualità
        import com.ibm.mqa.Log;

        public class MyApplication extends Application {
 
	    public static final String APP_KEY = 
		  "Your_Application_Key_Goes_Here";
 
	    @Override
	    public void onCreate() {
		super.onCreate();
		 
		Configuration configuration = new 
		  Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Fornisce la APP_KEY dell'applicazione
		  del controllo qualità
		.withMode(Mode.QA) //Seleziona la modalità di produzione
		  del controllo qualità.  Questo esempio è per la modalità di preproduzione,
		//Utilizza .withMode(Mode.MARKET) per la modalità di produzione.
		.build();
 
		MQA.startNewSession(this, configuration);
	       }
             }
		</code></pre>
		{: codeblock}

3. Continua con la procedura nella pagina [Introduzione a {{site.data.keyword.mqa}}](index.html).


# Link correlati
{: #rellinks notoc}

## Link correlati
{: #general notoc}
* [Introduzione a {{site.data.keyword.mqa}}](index.html){:new_window}
