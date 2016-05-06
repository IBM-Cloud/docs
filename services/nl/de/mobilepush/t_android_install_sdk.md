---

copyright:
 years: 2015, 2016

---

# Client-Push-SDK mit Gradle installieren
{: #android_install}

In diesem Abschnitt wird die Vorgehensweise zum Installieren und Verwenden des Client-Push-SDK für die weitere Entwicklung Ihrer Android-Anwendungen beschrieben.

Das Push-SDK für mobile Bluemix®-Services kann mithilfe von Gradle hinzugefügt werden. Gradle lädt automatisch Artefakte aus Repositorys herunter und stellt Sie in Ihrer Android-Anwendung zur Verfügung. Stellen Sie sicher, dass Sie Android Studio und das Android Studio-SDK ordnungsgemäß einrichten. Weitere Informationen zum Einrichten Ihres Systems finden Sie unter [Android Studio Overview](https://developer.android.com/tools/studio/index.html). Informationen zu Gradle finden Sie in [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. Öffnen Sie in Android Studio nach dem Erstellen und Öffnen der mobilen Anwendung die Anwendungsdatei **build.gradle**. Fügen Sie dann die folgenden Abhängigkeiten zu Ihrer mobilen Anwendung hinzu. Diese Importanweisungen sind für die nachfolgend aufgeführten Code-Snippets erforderlich.

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. Fügen Sie die folgenden Abhängigkeiten zu Ihrer mobilen Anwendung hinzu. Mit den folgenden
Zeilen wird das Push-Client-SDK von Bluemix™ Mobile Services und das Google Play Services-SDK zu Ihren Abhängigkeiten für den Kompilierungsbereich hinzugefügt.

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+'
	  compile 'com.google.android.gms:play-services:7.8.0'
	}  
	```
1. Fügen Sie die folgenden Berechtigungen in der Datei **AndroidManifest.xml** hinzu. Ein Beispielmanifest
finden Sie in [Android helloPush Sample Application](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Eine Gradle-Beispieldatei finden Sie unter [Sample Build Gradle file](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

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

	Weitere Informationen zu Android-Berechtigungen finden Sie [hier](http://developer.android.com/guide/topics/security/permissions.html).

1. Fügen Sie die Einstellungen für die Benachrichtigungsabsicht für die Aktivität hinzu. Mit dieser Einstellung wird die Anwendung gestartet, wenn der Benutzer im Benachrichtigungsbereich auf die empfangene Benachrichtigung klickt.

	```
	<intent-filter>  
		<action android:name="<ihr_android-paketname.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Hinweis**: Ersetzen Sie *ihr_android-paketname* in der obigen Aktion durch den Namen des Anwendungspakets, der in Ihrer Anwendung verwendet wird.

1. Fügen Sie den Absichtsservice und Absichtsfilter von Google Cloud Messaging (GCM) für die Ereignisbenachrichtigungen des Typs RECEIVE hinzu.

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
