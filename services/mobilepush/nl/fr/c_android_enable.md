---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des applications Android pour recevoir des notifications de type {{site.data.keyword.mobilepushshort}}
{: #tag_based_notifications}
Dernière mise à jour : 14 février 2017
{: .last-updated}

Vous pouvez activer des applications Android pour recevoir des notifications push sur vos appareils. Android Studio, qui est un prérequis, est la méthode recommandée pour générer des projets Android. Une connaissance de base d'Android Studio est essentielle.

## Installation du logiciel SDK Push du client à l'aide de Gradle
{: #android_install}

Cette section explique comment installer et utiliser le logiciel SDK Push du client afin de développer davantage vos applications Android.

Le logiciel SDK Push de Bluemix® Mobile Services peut être ajouté en utilisant Gradle. Gradle télécharge automatiquement des artefacts depuis des référentiels et les met à la disposition de votre application Android. Assurez-vous de configurer correctement Android Studio et le logiciel SDK Android Studio. Pour plus d'informations sur la configuration de votre système, accédez au site [Android Studio Overview ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.android.com/tools/studio/index.html){: new_window}. Pour plus d'informations sur Gradle, accédez au site [Configuring Gradle Builds ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}.

Après avoir créé et ouvert votre application mobile, effectuez les étapes suivantes à l'aide d'Android Studio.

1. Ajoutez des dépendances à votre fichier **build.gradle** de niveau Module. 	

	- Ajoutez la dépendance suivante pour inclure le logiciel SDK Push du client Bluemix™ Mobile Services et le logiciel SDK des services Google Play à vos dépendances de compilation.
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- Ajoutez les dépendances suivantes pour importer des instructions qui sont requises pour les fragments de code.
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- Ajoutez la dépendance suivante à la fin de votre fichier de niveau Module **build.gradle**.
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. Ajoutez les dépendances suivantes à votre fichier **build.gradle** de niveau Projet.
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. Dans le fichier **AndroidManifest.xml**, ajoutez les droits ci-dessous. Pour consulter un exemple de manifeste, accédez au site [Android helloPush Sample Application ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}. Pour consulter un exemple de fichier Gradle, accédez au site [Sample Build Gradle file ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}.
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
Pour plus d'informations sur les autorisations Android, visitez le site [Android permissions ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/guide/topics/security/permissions.html){: new_window}.
4. Ajoutez les paramètres d'intention de notification pour l'activité. Ce paramètre démarre l'application lorsque l'utilisateur clique sur la notification reçue dans la zone de notification.
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
```
	{: codeblock}
**Remarque** : remplacez *Your_Android_Package_Name* dans l'action précédente par le nom du package d'applications utilisé dans votre application.

5. Ajoutez le service d'intention FCM (Firebase Cloud Messaging) ou GCM (Google Cloud Messaging) et des filtres d'intention pour les notifications d'événements RECEIVE et REGISTRATION.
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

6. Le service {{site.data.keyword.mobilepushshort}} prend en charge l'extraction des notifications individuelles depuis la zone de notification. Pour les notifications atteintes à partir de la zone de notification, un descripteur ne vous est fourni que pour la notification sur laquelle vous cliquez. Toutes les notifications s'affichent quand l'application est ouverte normalement. Mettez à jour votre fichier **AndroidManifest.xml** avec le fragment de code ci-après pour utiliser cette fonctionnalité :

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

Pour configurer le projet FCM et obtenir vos données d'identification, consultez [Obtention de votre ID d'émetteur et de la clé d'API](t_push_provider_android.html). Effectuez les étapes suivantes à l'aide de la console FCM (Firebase Cloud Messaging).

1. Dans la console Firebase, cliquez sur l'icône **Project Settings**.
    ![Paramètres du projet Firebase](images/FCM_4.jpg)

3. Sélectionnez l'icône **ADD APP** ou **Add Firebase to your Android app** dans l'onglet General du volet Your apps.
    ![Ajout de Firebase à Android](images/FCM_5.jpg)

4. Dans la fenêtre Add Firebase to your Android app, ajoutez **com.ibm.mobilefirstplatform.clientsdk.android.push** en tant que nom du package. La zone App nickname est facultative. Cliquez sur **Ajouter une application**.
    ![Ajout de Firebase à votre fenêtre Android](images/FCM_1.jpg)

5. Incluez le nom de package de votre application en l'entrant dans la fenêtre Add Firebase to your Android app. La zone App nickname est facultative. Cliquez sur **Ajouter une application**. 

	![Ajout du nom de package de votre application](images/FCM_2.jpg)

6. Le fichier `google-services.json` est généré. Copiez le fichier `google-services.json` dans le répertoire racine de votre module d'application Android. Vous pouvez constater que le fichier `google-service.json` inclut les noms de packages que vous avez ajouté.

    ![Ajout du fichier json au répertoire racine de votre application](images/FCM_7.jpg)

5. Dans la fenêtre Add Firebase to your Android app, cliquez sur **Continuer**, puis sur **Terminer**. 

  

Générez et exécutez votre application.

## Initialisation du logiciel SDK Push pour les applis Android
{: #android_initialize}

Le code d'initialisation se trouve généralement dans la méthode onCreate de l'activité principale de votre application Android. Deux composants du logiciel SDK doivent être initialisés. Le premier est le logiciel SDK de base et l'autre, le logiciel SDK push qui repose sur le premier.

### Initialisation du logiciel SDK de base

```
// Initialisation du SDK pour Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: bluemixRegionSuffix}

Indique l'emplacement où l'appli est hébergée. Vous pouvez utiliser l'une des trois valeurs suivantes :

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

### Initialisation du logiciel SDK Push du client

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: appguid_initialize_client_push_sdk}

Il s'agit de la clé AppGUID du service {{site.data.keyword.mobilepushshort}}. Cette valeur est sensible à la casse. Ouvrez le tableau de bord de notification push et sélectionnez l'onglet de configuration. Vous pouvez obtenir cette valeur depuis Options pour application mobile, à partir de l'onglet de configuration du tableau de bord du service Push Notifications. 

## Enregistrement d'appareils Android
{: #android_register}

Utilisez l'API `MFPPush.register()` pour enregistrer l'appareil auprès du service {{site.data.keyword.mobilepushshort}}. Pour enregistrer des appareils Android, ajoutez les informations FCM (Firebase Cloud Messaging) et GCM (Google Cloud Messaging (GCM) dans le tableau de bord de configuration du service {{site.data.keyword.mobilepushshort}} Bluemix. Pour plus d'informations, voir [Configuration de données d'identification pour Google Cloud Messaging](t_push_provider_android.html).

Copiez les fragments de code suivants dans votre application mobile Android.

```
	//Enregistrement d'appareils Android
	push.registerDevice(new MFPPushResponseListener<String>() {
    	@Override
    	public void onSuccess(String response) {
    		//Traitement en cas de réussite
	    }
		@Override
    public void onFailure(MFPPushException ex) {
    		//Traitement en cas d'échec
	    }
		});
```
	{: codeblock}


```
	//Traitement de la notification à son arrivée
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
	    public void onReceive (final MFPSimplePushNotification message){
	      // Traitement de la notification Push
	    }
		};
```
	{: codeblock}

## Réception de notifications push sur des appareils Android
{: #android_receive}

Pour enregistrer l'objet notificationListener auprès de push, appelez la méthode **MFPPush.listen()**. En général, elle est appelée depuis la méthode **onResume()** de l'activité qui traite les notifications push.

1. Pour enregistrer l'objet notificationListener auprès de push, appelez la méthode **listen()**. En général, elle est appelée depuis les méthodes  **onResume()** et **onPause** de l'activité qui traite les notifications push.


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

2. Générez le projet et exécutez-le sur l'appareil ou l'émulateur. Quand la méthode onSuccess() pour le programme d'écoute des réponses dans la méthode register() est appelée, cela signifie que l'appareil a été enregistré auprès du service {{site.data.keyword.mobilepushshort}}. A ce stade, vous pouvez envoyer un message comme décrit dans la rubrique Envoi de notifications push de base.
3. Vérifiez que vos appareils ont reçu votre notification. Si l'application se trouve au premier-plan, la notification est traitée par **MFPPushNotificationListener**. Si elle se trouve en arrière-plan, un message est affiché dans la barre de notification.

## Suivi des notifications push sur les appareils Android 
{: #android_monitor}

Pour surveillance du statut actuel de la notification dans l'application, vous pouvez implémenter l'interface `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` et définir la méthode onStatusChange(String messageId, MFPPushNotificationStatus status). 

Le **messageId** est l'identificateur du message envoyé depuis le serveur.  **MFPPushNotificationStatus** définit le statut des notifications sous forme de valeurs :

- **RECEIVED** - L'application a reçu la notification. 
- **QUEUED** - L'application place en file d'attente la notification pour appel du programme d'écoute des notifications. 
- **OPENED** - L'utilisateur ouvre la notification en cliquant sur celle-ci dans le bac ou en la lançant depuis l'icône d'application ou lorsque l'application est à l'avant-plan. 
- **DISMISSED** - L'utilisateur supprime/rejette la notification dans le bac.

Vous devez enregistrer la classe **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener** auprès de MFPPush.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
}
	});
```
    {: codeblock}


### Ecoute du statut DISMISSED (rejeté)

Vous pouvez opter d'être à l'écoute du statut DISMISSED sous l'une des conditions suivantes :

- Lorsque l'application est active (opérant en avant ou en arrière-plan)

  Ajoutez ce fragment de code à votre fichier `AndroidManifest.xml` :

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
	{: codeblock}

- Lorsque l'application est à la fois active (opérant en avant ou en arrière-plan) et non en opération (fermée)

Vous devez étendre le récepteur de diffusion **com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler** et redéfinir la méthode **onReceive()**, où **MFPPushNotificationStatusListener** doit être enregistré avant d'appeler la méthode **onReceive()** de la classe de base.

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


Ajoutez le fragment de code suivant à votre fichier `AndroidManifest.xml` :

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
	</intent-filter>
	</receiver>
```
    {: codeblock}

## Envoi des notifications de type {{site.data.keyword.mobilepushshort}} de base
{: #send}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base.

Pour envoyer des notifications push de base, procédez comme suit :

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant une option **Envoyer à**. Les options prises en charge sont **Appareil par étiquette**, **ID de l'appareil**, **ID utilisateur**, **Appareils Android**, **Appareils IOS**, **Notifications Web** et **Tous les appareils**.
**Remarque **: si vous sélectionnez l'option **Tous les appareils**, tous les appareils qui sont abonnés à des notifications de type {{site.data.keyword.mobilepushshort}} recevront les notifications.
![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Message**, composez votre message. Configurez les paramètres facultatifs, selon les besoins.
3. Cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

La capture d'écran suivante présente une boîte d'alerte relative à une notification push s'exécutant au premier plan sur un appareil Android.

![Notification push qui s'exécute au premier plan sur un appareil Android](images/Android_Screenshot.jpg)

La capture d'écran suivante présente une notification push qui s'exécute en arrière-plan sur un appareil Android.

![Notification push qui s'exécute en arrière-plan sur un appareil Android](images/background.jpg)

### Paramètres Android facultatifs pour envoi de notifications
{: #send_otpional_setting}

Vous pouvez personnaliser les paramètres de type {{site.data.keyword.mobilepushshort}} pour l'envoi de notifications vers des appareils Android. Les options de personnalisation facultative suivantes sont prises en charge.
![Paramètres Android personnalisés](images/android_custom_settings.jpg)

- **Touche de réduction** : des touches de réduction sont attachées aux notifications. Si plusieurs notifications arrivent séquentiellement avec la même touche de réduction quand l'appareil est hors ligne, elles sont réduites. Quand un appareil passe en ligne, il reçoit des notifications du serveur FCM/GCM et n'affiche que la dernière notification portant la même touche de réduction. Si aucune touche de réduction n'est définie, les nouveaux et les anciens messages sont stockés pour une distribution future.
- **Son** : indique le clip audio à exécuter à réception d'une notification. Prend en charge le fichier par défaut ou utilise le nom de la ressource audio intégré dans l'application.
- **Icône** : spécifie le nom de l'icône à afficher pour la notification. Assurez-vous de bien avoir placé l'icône dans le dossier res/drawable, avec l'application client.
- **Priorité** : spécifie les options d'affectation de la priorité de distribution aux messages. Une priorité `élevée` ou `max` générera des notifications d'alerte, tandis que des messages dont la priorité est à `faible` ou `par défaut` n'ouvriront pas les connexions réseau sur un appareil en veille. Pour les messages dont l'option a été définie à `min`, une notification silencieuse sera émise.
- **Visibilité** : vous pouvez choisir de définir l'option de visibilité de notification sur `public` ou `privé`. L'option `privé` limite l'affichage public ; vous pouvez choisir de l'activer si votre appareil est sécurisé avec un code ou un numéro confidentiel et que le paramètre de notification est défini sur "Masquer le contenu sensible de la notification". Quand la visibilité est configurée sur `privé`, une zone "occulter" doit être mentionnée. Seul le contenu spécifié dans la zone "occulter" s'affichera sur l'écran verrouillé et sécurisé de l'appareil. L'option `public` permet une lecture libre des notifications.
- **Durée de vie** : cette valeur est définie en secondes. Si ce paramètre n'est pas spécifié, le serveur FCM/GCM stocke le message pendant quatre semaines et tente de le distribuer. La validité expire après quatre semaines. La plage des valeurs possibles va de 0 à 2419200 secondes.
- ****Retarder si inactif : en définissant cette valeur à `true`, vous demandez au serveur FCM/GCM de ne pas distribuer de notification si le serveur est inactif. Définissez cette valeur à `false` pour garantir la distribution de la notification même si l'appareil est en veille.
- **Sync**: quand cette option est définie à `true`, les notifications figurant sur tous vos appareils enregistrés sont synchronisés. Si l'utilisateur identifié par un nom d'utilisateur qui lui est propre dispose de plusieurs appareils avec la même application installée, la lecture de la notification sur un appareil garantit une suppression des notifications sur les autres appareils. Vous devez vérifier que vous êtes enregistré auprès du service {{site.data.keyword.mobilepushshort}} avec le bon ID utilisateur pour que cette option fonctionne.
- **Contenu supplémentaire** : spécifie les valeurs de contenu personnalisées pour vos notifications.


## Etapes suivantes
{: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options avancées.

Ajoutez ces fonctions de service de notifications push à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).
