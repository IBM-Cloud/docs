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


# Instrumentation de MQA avec une application Android (obsolète)
{: #instrumentAnd}


Si vous souhaitez utiliser {{site.data.keyword.mqafull}} avec votre application Android, vous devez télécharger le logiciel SDK et l'instrumenter en effectuant quelques modifications à l'aide de l'environnement de développement Android Studio.
{: shortdesc}

Pour pouvoir instrumenter une application avec {{site.data.keyword.mqa}}, vous devez disposer d'un compte {{site.data.keyword.Bluemix}} et avoir installé la version de l'environnement de développement adaptée aux plateformes de l'application que vous instrumentez.

Pour instrumenter {{site.data.keyword.mqa}} en vue de son exécution avec votre application Android, procédez comme suit :

1. Ajoutez les droits requis et téléchargez le logiciel SDK dans votre projet Android.

	1. Ouvrez votre projet dans Android Studio.
	
	2. Sélectionnez **File** > **New** > **New Module**.
	
	3. Dans l'assistant *Create New Module*, sous *More Modules*, sélectionnez **Import .JAR or .AAR Package**, puis cliquez sur **Next**.
	
	4. Dans la zone File name, entrez le nom du fichier .aar du logiciel SDK {{site.data.keyword.mqa}} que vous avez téléchargé et cliquez sur **Finish**.
	
	5. Commencez à ajouter {{site.data.keyword.mqa}} à votre application mobile dans le projet Android Studio en sélectionnant **File** > **Project Structure**.
	
	6. Sélectionnez le module de votre application dans la fenêtre Project Structure, puis sélectionnez l'onglet *Dependencies*.
	
	7. Sélectionnez **+**, puis **Module Dependency**.
	
	8. Dans la fenêtre Choose Modules, sélectionnez le module Android {{site.data.keyword.mqa}} que vous avez importé, puis cliquez sur **OK**.
	
	9. Sélectionnez **OK** pour fermer la fenêtre Project Structure.
	
	10. Mettez à jour le fichier manifeste Android en vous assurant que les activités suivantes figurent dans une entrée `<application>` :
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. Vérifiez que les droits requis suivants sont indiqués dans le fichier manifeste :
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	Le code suivant est un exemple possible de fichier `AndroidManifest.xml` :

		```
		<?xml version="1.0" encoding="utf-8"?>
        <manifest xmlns:android=
		  "http://schemas.android.com/apk/res/android"
        package="com.applause.android"
        android:versionCode="6"
        android:versionName="2.3" >

        <uses-sdk android:minSdkVersion="8" />

        <!-- Required permission -->
        <uses-permission android:name="android.permission.INTERNET" /> 
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

2. Configurez une nouvelle session à lancer à chaque connexion.

	1. Ajoutez le fragment de code suivant dans la classe `MainActivity` de votre application, qui figure dans le fichier `MainActivity.java`. Il utilise votre clé d'application pour envoyer des données à {{site.data.keyword.mqa}}.
		 
		```
		public static final String APP_KEY = "Votre_Clé_Application";
		```
		{: codeblock}
		
		Remplacez *Votre_Clé_Application* par votre clé d'application issue de la page App Settings de {{site.data.keyword.mqa}}.
	
	2. Pour utiliser le générateur de configuration de {{site.data.keyword.mqa}}, importez d'abord les éléments suivants en les ajoutant dans le fichier `MainActivity.java` de votre application : 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. Créez un objet de configuration dans l'événement onCreate de votre classe MainActivity. Cet objet fournit plusieurs méthodes que vous pouvez utiliser pour indiquer des éléments de configuration. A la fin de la configuration de l'objet, vous appelez une méthode build() pour finaliser l'objet. Voici un exemple de configuration terminée :
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. Dans la classe Application de votre application, ajoutez le code de configuration et démarrez les sessions {{site.data.keyword.mqa}} en appelant la méthode `MQA.startNewSession()` dans l'événement `onCreate` de votre classe Application.
	
	    Par exemple : 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        Exemple étendu :

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
		  "Votre_Clé_Application";
 
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

3. Poursuivez en procédant comme indiqué dans [Initiation à {{site.data.keyword.mqa}}](index.html).


# Liens connexes
{: #rellinks notoc}

## Liens connexes
{: #general notoc}
* [Initiation à {{site.data.keyword.mqa}}](index.html){:new_window}
