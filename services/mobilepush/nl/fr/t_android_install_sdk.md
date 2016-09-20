---

Copyright :
  Années : 2015, 2016

---

# Installation du logiciel SDK Push du client à l'aide de Gradle
{: #android_install}

Cette section explique comment installer et utiliser le logiciel SDK Push du client afin de développer davantage vos applications Android.

Le logiciel SDK Push de Bluemix Mobile Services peut être ajouté à l'aide de Gradle. Gradle télécharge automatiquement des artefacts depuis des référentiels et les met à la disposition de votre application Android. Assurez-vous de configurer correctement Android Studio et le logiciel SDK Android Studio. Pour plus d'informations sur la configuration de votre système,
voir [Android Studio Overview](https://developer.android.com/tools/studio/index.html). Pour plus d'informations sur Gradle, voir [Configuring Gradle Builds](http://developer.android.com/tools/building/configuring-gradle.html).

1. Dans Android Studio, après avoir créé et ouvert une application mobile, ouvrez le fichier **build.gradle** de votre application. Ensuite, ajoutez les dépendances suivantes à votre application mobile. Ces instructions d'importation sont requises pour les fragments de code répertoriés ci-après.

	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```


1. Ajoutez les dépendances ci-après à votre application mobile. Les lignes suivantes ajoutent le logiciel SDK Push du client Bluemix Mobile Services et le logiciel SDK des services Google Play à vos dépendances de compilation :

	```
	dependencies {
	  compile 'com.ibm.mobilefirstplatform.clientsdk.android:push:1.+'
	  compile 'com.google.android.gms:play-services:7.8.0'
	}  
	```
1. Dans le fichier **AndroidManifest.xml**, ajoutez les droits ci-dessous. Pour afficher un exemple de manifeste, voir le [modèle d'application Android helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml). Pour afficher un exemple de fichier Gradle, voir l'[exemple de fichier de génération Gradle](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle).

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

	Vous trouverez davantage d'informations sur les [droits Android](http://developer.android.com/guide/topics/security/permissions.html) ici.

1. Ajoutez les paramètres d'intention de notification pour l'activité. Ce paramètre démarre l'application lorsque l'utilisateur clique sur la
notification reçue dans la zone de notification.

	```
	<intent-filter>  
		<action android:name="<Your_Android_Package_Name.IBMPushNotification"/>   
		<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
	```
	**Remarque** : Remplacez *Your_Android_Package_Name* dans l'action ci-dessus par le nom du package d'applications utilisé dans votre application.

1. Ajoutez le service d'intention Google Cloud Messaging (GCM) et des filtres d'intention pour les notifications d'événements RECEIVE.

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
