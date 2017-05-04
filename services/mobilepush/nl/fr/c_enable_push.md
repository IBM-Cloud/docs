---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des notifications pour les appareils mobiles
{: #c_enable_push-notifications}
Dernière mise à jour : 12 avril 2017
{: .last-updated}

Vérifiez que vous avez exécuté la procédure [Configuration des données d'identification pour un fournisseur de
notification](t__main_push_config_provider.html).

Cette section décrit comment configurer vos applications - mobiles, Web et applications et extensions Chrome - pour qu'elles reçoivent des notifications push, comment créer des notifications de base, obtenir et initialiser le logiciel SDK ou le plug-in et comment enregistrer votre appareil ou votre navigateur pour qu'il reçoive des notifications push. Vous pouvez également activer vos applications mobiles et de navigateur Web pour la réception de notifications push en utilisant l'[API REST](t_restapi.html).

**Remarque **: Dans le cas d'enregistrement d'un appareil, d'un navigateur, d'applications et d'extensions Chrome, le service
{{site.data.keyword.mobilepushshort}} conserve une référence unique pour les jetons issus des fournisseurs de notification -
des APN pour Apple ou FCM pour Google. Les jetons peuvent être invalidés par le fournisseur de service {{site.data.keyword.mobilepushshort}} pour un certain nombre de raisons. 

Ceci peut survenir, par exemple, lors de la désinstallation d'une application sur l'appareil. Dans un tel scénario, quand une tentative de distribution d'une notification est effectuée et reçoit une réponse des fournisseurs indiquant que l'appareil est invalidé, le service {{site.data.keyword.mobilepushshort}} retire les enregistrements de l'appareil ou du navigateur Web, ce qui aura pour effet d'empêcher d'autres tentatives d'envoi de notifications à l'appareil invalidé.


## Activation des applications Android pour recevoir des notifications push
{: #tag_based_notifications}


Vous pouvez activer des applications Android pour recevoir des notifications push sur vos appareils. Android Studio, qui est un prérequis, est la méthode recommandée pour générer des projets Android. Une connaissance de base d'Android Studio est essentielle.

### Installation du logiciel SDK Push du client à l'aide de Gradle
{: #android_install}

Cette section explique comment installer et utiliser le logiciel SDK Push du client afin de développer davantage vos applications Android.

Vous pouvez ajouter le logiciel SDK Push de {{site.data.keyword.Bluemix}} Mobile Services en utilisant [Gradle ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window}, qui télécharge automatiquement des artefacts depuis des référentiels et les met à la disposition de votre application Android. Assurez-vous de configurer correctement [Android Studio ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.android.com/tools/studio/index.html) et le logiciel SDK Android Studio.  

Après avoir créé et ouvert votre application mobile, procédez comme suit en utilisant Android Studio.

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
 Vous trouverez plus d'informations sur les [autorisations Android ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://developer.android.com/guide/topics/security/permissions.html){: new_window} ici.

4. Ajoutez les paramètres d'intention de notification pour l'activité. Ce paramètre démarre l'application lorsque l'utilisateur clique sur la
notification reçue dans la zone de notification.
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

Vérifiez que vous avez exécuté la procédure [Configuration des données d'identification pour un fournisseur de notification](t__main_push_config_provider.html) pour configurer le projet FCM et obtenir vos données d'identification. Effectuez les étapes suivantes à l'aide de la console FCM (Firebase Cloud Messaging).

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

### Initialisation du logiciel SDK Push pour les applis Android
{: #android_initialize}

Le code d'initialisation se trouve généralement dans la méthode onCreate de l'activité principale de votre application Android. Deux composants du logiciel SDK doivent être initialisés. Le premier est le logiciel SDK de base et l'autre, le logiciel SDK push qui repose sur le premier.

#### Initialisation du logiciel SDK de base
{: #initz_core_sdk}

```
// Initialisation du SDK pour Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

Indique l'emplacement où l'appli est hébergée. Vous pouvez utiliser l'une des trois valeurs suivantes :

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### Initialisation du logiciel SDK Push du client
{: #initiz_client_pushSDK}

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

Il s'agit de la clé AppGUID du service {{site.data.keyword.mobilepushshort}}. Cette valeur est sensible à la casse. Ouvrez le tableau de bord de notification push et sélectionnez l'onglet de configuration. Vous pouvez obtenir cette valeur depuis Options pour application mobile, à partir de l'onglet de configuration du tableau de bord du service Push Notifications. 

### Enregistrement d'appareils Android
{: #android_register}

Utilisez l'API `MFPPush.register()` pour enregistrer l'appareil auprès du service {{site.data.keyword.mobilepushshort}}. Pour enregistrer des appareils Android, ajoutez les informations FCM (Firebase Cloud Messaging) dans le tableau de bord de configuration du service {{site.data.keyword.mobilepushshort}} Bluemix. Pour plus d'informations, voir [Configuration des données d'identification pour un fournisseur de notification](t__main_push_config_provider.html).

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

### Réception de notifications push sur des appareils Android
{: #android_receive}

1. Pour enregistrer l'objet notificationListener auprès du service Push Notifications, utilisez la méthode `MFPPush.listen()`. En général, elle est appelée depuis les méthodes  `onResume()` et `onPause` de l'activité qui traite les notifications push.
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

2. Générez le projet et exécutez-le sur l'appareil ou l'émulateur. Quand la méthode onSuccess() pour le programme d'écoute des réponses dans la méthode register() est appelée, cela confirme que l'appareil a été enregistré auprès du service {{site.data.keyword.mobilepushshort}} et vous pouvez maintenant envoyer une notification push.
3. Vérifiez que vos appareils ont reçu votre notification. Si l'application se trouve au premier-plan, la notification est traitée par `MFPPushNotificationListener`. Si elle se trouve en arrière-plan, un message est affiché dans la barre de notification.

### Suivi des notifications push sur les appareils Android
{: #android_monitor}

Pour surveillance du statut actuel de la notification dans l'application, vous pouvez implémenter l'interface `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` et définir la méthode onStatusChange(String messageId, MFPPushNotificationStatus status). 

Le `messageId` est l'identificateur du message envoyé depuis le serveur.  `MFPPushNotificationStatus` définit le statut des notifications sous forme de valeurs :

- RECEIVED - l'application a reçu la notification. 
- QUEUED - l'application place en file d'attente la notification pour appel du programme d'écoute des notifications. 
- OPENED - l'utilisateur ouvre la notification en cliquant sur celle-ci dans le bac ou en la lançant depuis l'icône d'application ou quand l'application est à l'avant-plan. 
- DISMISSED - l'utilisateur supprime/rejette la notification dans le bac.

Vous devez enregistrer la classe `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` auprès de MFPPush.

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
	@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
		// Handle status change
}
	});
```
    {: codeblock}


#### Ecoute du statut DISMISSED (rejeté)
{: #android_monitor_listen}

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

Etendez le récepteur de diffusion `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` et redéfinissez la méthode `onReceive()`, où `MFPPushNotificationStatusListener` doit être enregistré avant d'appeler la méthode `onReceive()` de la classe de base.

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

### Envoi de notifications push de base
{: #send-basic-notification}

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

Vous pouvez personnaliser les paramètres de type {{site.data.keyword.mobilepushshort}} pour l'envoi de notifications vers des appareils Android. Les options de personnalisation facultative suivantes sont prises en charge : ![Paramètres Android personnalisés](images/android_custom_settings.jpg)

- Clé de réduction : des clés de réduction sont attachées aux notifications. Si plusieurs notifications arrivent séquentiellement avec la même clé de réduction quand l'appareil est hors ligne, elles sont réduites. Quand un appareil passe en ligne, il reçoit des notifications du serveur FCM/GCM et n'affiche que la dernière notification portant la même clé de réduction. Si aucune clé de réduction n'est définie, les nouveaux et les anciens messages sont stockés pour une distribution future.
- Son : indique le clip audio à exécuter à réception d'une notification. Prend en charge le fichier par défaut ou utilise le nom de la ressource audio intégré dans l'application.
- Icône : spécifie le nom de l'icône à afficher pour la notification. Assurez-vous de bien avoir placé l'icône dans le dossier `res/drawable`, avec l'application client.
- Priorité : spécifie les options d'affectation de la priorité de distribution aux messages. Une priorité `élevée` ou `max` générera des notifications d'alerte, tandis que des messages dont la priorité est à `faible` ou `par défaut` n'ouvriront pas les connexions réseau sur un appareil en veille. Pour les messages dont l'option a été définie à `min`, une notification silencieuse sera émise.
- Visibilité : vous pouvez choisir de définir l'option de visibilité de notification sur `public` ou `privé`. L'option `privé` limite l'affichage public ; vous pouvez choisir de l'activer si votre appareil est sécurisé avec un code ou un numéro confidentiel et que le paramètre de notification sélectionné permet de masquer le contenu sensible de la notification. Quand la visibilité est configurée sur `privé`, une zone d'occultation doit être mentionnée. Seul le contenu spécifié dans cette zone apparaîtra sur un écran verrouillé sécurisé sur l'appareil. L'option `public` permet une lecture libre des notifications.
- Durée de vie : cette valeur est définie en secondes. Si ce paramètre n'est pas spécifié, le serveur FCM/GCM stocke le message pendant quatre semaines et tente de le distribuer. La validité expire après quatre semaines. La plage des valeurs possibles va de 0 à 2419200 secondes.
- Retarder si inactif : en définissant cette valeur à `true`, vous demandez au serveur FCM/GCM de ne pas distribuer de notification si le serveur est inactif. Définissez cette valeur à `false` pour garantir la distribution de la notification même si l'appareil est en veille.
- Sync : quand cette option est définie à `true`, les notifications figurant sur tous vos appareils enregistrés sont synchronisées. Si l'utilisateur identifié par un nom d'utilisateur qui lui est propre dispose de plusieurs appareils avec la même application installée, la lecture de la notification sur un appareil garantit une suppression des notifications sur les autres appareils. Vous devez vérifier que vous êtes enregistré auprès du service {{site.data.keyword.mobilepushshort}} avec le bon ID utilisateur pour que cette option fonctionne.
- Contenu supplémentaire : spécifie les valeurs de contenu personnalisées pour vos notifications.


### Etapes suivantes
{: #next_steps_tag_based_notifications}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions de service de notifications push à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).


## Configuration des applications Cordova pour la réception de notifications push
{: #cordova_enable}


Cordova est une plateforme permettant de construire des applications hybrides avec JavaScript, CSS et HTML. Le service {{site.data.keyword.mobilepushshort}} prend en charge le développement d'applications iOS et Android reposant sur Cordova.

Vous pouvez activer les applications Cordova pour recevoir des notifications push sur vos appareils.

### Installation du plug-in Cordova Push
{: #cordova_install}

Installez et utilisez le plug-in push client pour développer davantage vos applications Cordova, ce qui a pour effet d'installer aussi le plug-in Cordova core, qui initialise votre connexion à Bluemix.

1. Téléchargez les dernières versions d'Android Studio SDK et Xcode.
1. Configurez votre émulateur. Pour Android Studio, utilisez un émulateur qui prend en charge l'API Google Play.
1. Installez l'outil de ligne de commande Git. Pour Windows, prenez soin de sélectionner l'option **Run Git from the Window Command Prompt**. Pour plus d'informations sur le téléchargement et l'installation de cet outil, voir [Git ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}.
1. Installez Node.js et l'outil Node Package Manager (NPM). L'outil de ligne de commande NPM est intégré à Node.js. Pour plus d'informations sur le téléchargement et l'installation de Node.js, voir [Node.js ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://nodejs.org/en/download/){: new_window}.
1. A partir de la ligne de commande, installez les outils de ligne de commande Cordova à l'aide de la commande **npm install -g cordova**. Cette action est requise pour pouvoir utiliser le plug-in push Cordova. Pour plus d'informations sur l'installation de Cordova et la configuration de votre application Cordova, voir [Cordova Apache ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/#getstarted){: new_window}. Pour plus d'informations, reportez-vous au [fichier Readme ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} du plug-in Push de Cordova.
1. Placez-vous dans le dossier dans lequel créer votre application Cordova et exécutez la commande ci-dessous pour créer une application Cordova. Si vous possédez déjà une application Cordova, passez à l'étape 3.
```cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Facultatif : vous pouvez éditer le fichier **config.xml** et remplacer le nom de l'application dans l'élément <name> par le nom de votre choix, plutôt que d'utiliser le nom par défaut HelloCordova.

Prenez soin de spécifier l'ID de bundle approprié. Les messages d'erreur suivants risquent d'être générés dans Xcode, si un ID de bundle incorrect est spécifié.

* The executable was signed with invalid entitlements.
* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile. Pour corriger ce problème, spécifiez l'ID de bundle approprié dans Xcode ou dans le fichier **config.xml** de votre appli Cordova.

1. Ajoutez l'API minimale prise en charge ou la déclaration de cible de déploiement dans le fichier config.xml de votre application Cordova. La valeur de minSdkVersion doit être supérieure à 15. La valeur de targetSdkVersion doit toujours refléter le logiciel SDK Android le plus récent disponible auprès de Google.
	
	* Android - Ouvrez dans votre éditeur le fichier **config.xml** et mettez à jour l'élément
`<platform name="android">` en spécifiant les versions minimum et cible du SDK :

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - Mettez à jour l'élément <platform name="ios"> avec une déclaration cible de déploiement :

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. A partir de l'interface de ligne de commande Cordova, ajoutez vos plateformes iOS et/ou Android en utilisant la commande suivante :
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Depuis le répertoire racine de votre application Cordova, entrez la commande suivante afin d'installer le plug-in push Cordova : **cordova plugin add bms-push**. Selon les plateformes que vous avez ajoutées, vous pouvez voir :
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. Depuis votre dossier répertoire_racine_application, vérifiez que les plug-in Cordova core et push ont été installés correctement en entrant la commande suivante : **cordova  plugin list**. Selon les plateformes que vous avez ajoutées, vous pouvez voir :
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Configurez votre environnement de développement iOS.
2. Construisez et exécutez votre application avec Xcode.
1. Téléchargez vos fichiers Firebase `google-services.json` pour Android et placez-les sous le dossier racine de votre projet
Cordova ( `[nom_de_votre_application]/platforms/android.
	1. Accédez au dossier `[nom_de_votre_application]/platforms/android`.
	2. Ouvrez le fichier `build.gradle` (chemin : plateforme > android > build.gradle).
	3. Recherchez le texte `buildscript` dans le fichier `build.gradle`.
	4. Ajoutez la ligne 'com.google.gms:google-services:3.0.0' après celle du chemin de  classes (classpath)
	5. Accédez à la section "dependencies". Sélectionnez les dépendances comportant le texte `compile` et l'endroit marquant la
fin de la
dépendance et ajoutez juste après cette ligne :apply plugin: 'com.google.gms.google-services'.
	6. Préparez et construisez votre projet Cordova Android.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Remarque** : avant d'ouvrir votre projet dans Android Studio, générez votre application Cordova via l'interface CLI Cordova, afin d'éviter des erreurs de génération.

### Initialisation du plug-in Cordova
{: #cordova_initialize}

Pour pouvoir utiliser le plug-in Cordova du service {{site.data.keyword.mobilepushshort}}, vous devez l'initialiser en transmettant la route de l'application et
l'identificateur global unique de l'application. Une fois le plug-in initialisé, vous pouvez vous connecter à l'application serveur que vous avez créée dans le tableau de bord Bluemix. Le plug-in Cordova est l'encapsuleur pour les logiciels SDK de client Android et iOS qui permettent à une application Cordova de communiquer avec les services Bluemix.

1. Initialisez le client BMS en copiant et en collant le fragment de code suivant dans votre fichier JavaScript principal (généralement situé sous le répertoire **www/js**).

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

Indiquez la région pour votre application. Les constantes suivantes sont fournies :

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

Par exemple :

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Remarque **: si vous avez créé une application Cordova à l'aide de l'interface CLI de Cordova (par exemple, avec la commande Cordova
create app-name, placez ce code Javascript dans le fichier index.js après la fonction app.receivedEvent dans la fonction onDeviceReady: function()
afin d'initialiser le client `BMSClient`. 


### Enregistrement des appareils
{: #cordova_register}


Pour enregistrer un appareil auprès du service {{site.data.keyword.mobilepushshort}}, appelez la méthode d'enregistrement. Copiez le fragment de code suivant dans votre application Cordova pour enregistrer un appareil.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

Le fragment de code JavaScript ci-après montre comment initialiser le logiciel SDK de votre client Bluemix Mobile Services, enregistrer un appareil avec le service {{site.data.keyword.mobilepushshort}} et passer en mode écoute sur les notifications push. Incluez ce code dans votre fichier Javascript.

Dans **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

Ajoutez le fragment de code Swift suivant à la classe de votre délégué d'application :

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

### Etapes suivantes
{: #cordova_register_next}

Générez votre projet, puis exécutez-le à l'aide des commandes suivantes :

#### Android
{: #android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: #ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

### Réception de notifications push sur les appareils
{: #cordova_receive}

Copiez le fragment de code ci-après pour recevoir des notifications push sur les appareils.

#### JavaScript
{: #jvscrpt}

Ajoutez le fragment de code JavaScript suivant à la partie Web de votre application Cordova :
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Propriétés de notification Android
{: #And_notif}

La section suivante répertorie les propriétés de notification Android :

* **message** - Message de notification Push
* **payload** - objet JSON comportant un contenu de notification


#### Propriétés de notification iOS
{: #ios_notif}

La section suivante répertorie les propriétés de notification iOS :

* **message** - Message de notification Push
* **payload** - Objet JSON comportant un contenu de notification
action-loc-key -  La chaîne est utilisée comme clé pour obtenir une chaîne localisée à l'emplacement actuel, à utiliser comme titre de bouton approprié au lieu de `View`.
* **badge** - numéro à utiliser comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
* **sound** - Nom d'un fichier son dans le bundle de l'application ou dans le dossier Library/Sounds du conteneur des données d'application.


Ajoutez les fragments de code Swift suivants à la classe de votre délégué d'application :
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

### Envoi de notifications push de base
{: #push-send-notifications}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base.

Pour envoyer des notifications push de base, procédez comme suit :

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant une option **Envoyer à**. Les options prises en charge sont **Appareil par étiquette**, **ID de l'appareil**, **ID utilisateur**, **Appareils Android**, **Appareils IOS**, **Notifications Web** et **Tous les appareils**.
**Remarque **: si vous sélectionnez l'option **Tous les appareils**, tous les appareils qui sont abonnés à des notifications de type {{site.data.keyword.mobilepushshort}} recevront les notifications.
![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Message**, composez votre message. Configurez les paramètres facultatifs, selon les besoins.
3. Cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

Les captures d'écran suivantes présentent une boîte de dialogue d'alerte qui traite une notification de type {{site.data.keyword.mobilepushshort}} s'exécutant au premier plan sur un appareil Android et sur un appareil iOS.

![Notification push qui s'exécute au premier plan sur un appareil Android](images/Android_Screenshot.jpg)

![Notification push qui s'exécute au premier plan sur un appareil iOS](images/iOS_Screenshot.jpg)

   L'image suivante montre {{site.data.keyword.mobilepushshort}} en arrière-plan pour Android.
![Notification push qui s'exécute en arrière-plan sur un appareil Android](images/background.jpg)

#### Etapes suivantes
{: #next_steps_basic_notifications}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options
avancées.

Ajoutez les fonctions du service {{site.data.keyword.mobilepushshort}} à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).


## Activation des applications iOS pour envoyer des notifications push
{: #enable-push-ios-notifications}

Vous pouvez permettre aux applications iOS d'envoyer des {{site.data.keyword.mobilepushshort}} à vos appareils.


### Installation de CocoaPods
{: #enable-push-ios-notifications-install}

Pour un projet Xcode existant, vous pouvez configurer le logiciel SDK client des services Bluemix Mobile en utilisant l'outil de gestion des dépendances CocoaPods. Vous pouvez aussi installer le logiciel SDK manuellement.

Pour consulter le fichier Readme de Swift Push, accédez au site [Readme![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Installez CocoaPods en exécutant la commande suivante sur votre terminal Mac :
	```
		$ sudo gem install cocoapods
	```
	{: codeblock}
2. Entrez la commande `pod init` dans le terminal pour initialiser CocoaPods. Assurez-vous de bien exécuter la commande depuis le répertoire où se trouve votre projet Xcode. La commande `pod init` crée un fichier Pod.  
3. Dans le fichier Pod généré, ajoutez les dépendances de logiciel SDK requises. Copiez le fichier Pod suivant :
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copiez la liste suivante telle quelle et supprimez les dépendances superflues.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
		pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. Depuis le terminal, accédez au dossier de votre projet et installez des dépendances avec la commande `pod update`.

Cette commande installe vos dépendances et crée un nouvel espace de travail Xcode.  
**Remarque** : Prenez soin de toujours ouvrir le nouvel espace de travail Xcode au
lieu du fichier de projet Xcode d'origine :
```
  $ open App.xcworkspace
```
	{: codeblock}

Cet espace de travail contient votre projet d'origine et le projet Pods contenant vos dépendances. Pour modifier le dossier source des services mobiles Bluemix, vous le trouverez dans votre projet Pods, sous `Pods/yourImportedSourceFolder`. Exemple : `Pods/BMSPush`.

### Ajout d'infrastructures à l'aide de Carthage
{: #carthage}

Ajoutez des infrastructures à votre projet à l'aide de [Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Notez que Carthage dans Xcode8 n'est pas pris en charge.

1. Ajoutez des infrastructures `BMSPush` à votre fichier Cartfile :
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
	```
	{: codeblock}
2. Exécutez la commande `carthage update`. Lorsque la construction est terminée, faites glisser `BMSPush.framework`, `BMSCore.framework` et `BMSAnalyticsAPI.framework` dans votre projet Xcode.
3. Suivez les instructions du site [Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} pour compléter l'intégration.

### Configuration du logiciel SDK pour iOS
{: #ios-sdk}

Installez le kit de développement de logiciels (SDK) iOS et ajoutez le code suivant au fichier **AppDelegate.swift** dans votre application. Notez que ceci effectue également un enregistrement auprès des APN.  
```
  func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool 
 {  
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### Utilisation d'infrastructures et de dossiers source importés
{: #using-imported-frameworks}

Référencez le logiciel SDK dans votre code. Vérifiez que les prérequis suivants sont en place.

- iOS 8.0 ou version ultérieure	
- Xcode 7

Ecrivez des directives `#import` pour les en-têtes pertinents, par exemple :
```
	 //swift
import BMSCore
import BMSPush
```
		{: codeblock}

Pour consulter le fichier Readme de Swift Push, accédez au site [Readme ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Remarque** : La mise à jour de votre projet Pods via les commandes CocoaPods `pod install` ou `pod update` peut remplacer les dossiers source des services Bluemix Mobile. Si
vous voulez conserver vos versions personnalisées des fichiers d'origine, prenez soin de les sauvegarder avant d'entrer l'une de ces commandes.


### Paramètres de génération
{: #build-settings}

Accédez à **Xcode > Build Settings > Build Options** et affectez à l'option Set Enable Bitcode la valeur **No**.

**Attention** : Depuis iOS 9, des modifications apportées à la fonction App Transport Security (ATS) peuvent avoir un impact sur la façon dont vous gérez le processus d'authentification. Les articles de blogue suivants fournissent des informations supplémentaires sur les modifications : [ATS and Bitcode in iOS 9 ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} et [Connect your iOS 9 app to Bluemix today ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

### Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-initialize}

Le code d'initialisation se trouve généralement dans le délégué d'application de l'application iOS. Cliquez sur le lien **Options pour application mobile** dans votre tableau de bord Push pour obtenir la route de l'application et l'identificateur global unique.

#### Initialisation du logiciel SDK de base
{: #Initializing-the-core-sdk}

Pour initialiser le logiciel SDK de base pour Swift avec l'identificateur global unique GUID, la route et la région Bluemix, utilisez le fragment de code suivant.
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### Route, identificateur global unique et région Bluemix
{: #route-guid-bluemix-region}


- **appRoute** : spécifie la route qui a été affectée à l'application serveur que vous avez créée dans Bluemix.


- **GUID** : spécifie la clé unique qui a été affectée à l'application que vous avez créée dans Bluemix. Cette
valeur est sensible à la casse.


- **bluemixRegionSuffix** : spécifie l'emplacement dans lequel l'application est hébergée. Le paramètre `bluemixRegion` spécifie le déploiement Bluemix que vous utilisez. ous pouvez définir cette valeur avec une propriété statique `BMSClient.REGION` et utiliser l'une des trois valeurs suivantes :

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID** : spécifie la clé AppGUID unique qui a été affectée au service {{site.data.keyword.mobilepushshort}} que vous avez créé dans Bluemix.

#### Initialisation du logiciel SDK Push du client
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### Enregistrement d'applications et d'appareils iOS
{: #enable-push-ios-notifications-register}

Une application doit être enregistrée auprès d'APNS pour pouvoir recevoir des notifications distantes, après installation sur un appareil. Une fois que le jeton d'appareil généré par APNS est reçu par l'application, il doit être transmis au service {{site.data.keyword.mobilepushshort}}.

Pour enregistrer les applications et les appareils iOS, vous devez :

1. Créez une application d'arrière plan.
2. Passer le jeton à {{site.data.keyword.mobilepushshort}}.


#### Créez une application d'arrière plan
{: #create-a-backend-app}

Créez une application d'arrière plan dans la section Boilerplates du catalogue Bluemix® , ce qui lie automatiquement le service {{site.data.keyword.mobilepushshort}} à cette application. Si
vous avez déjà créé une application dorsale, prenez soin de la lier au service {{site.data.keyword.mobilepushshort}}.


#### Passage de jetons au service de notifications push
{: #pass-token-push-notifications}

Une fois que le jeton envoyé par APNS a été reçu, transmettez-le à {{site.data.keyword.mobilepushshort}} dans le cadre de la méthode `registerWithDeviceToken`.

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
       else{
            print( "Error during device registration \(error) ")
           print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
   }
  }
```
	{: codeblock}


### Réception de notifications push sur des appareils iOS
{: #enable-push-ios-notifications-receiving}

Pour recevoir des notifications push sur des appareils iOS, ajoutez la méthode Swift suivante au délégué d'application de votre application :

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### Suivi des applications push sur les unités iOS
{: #ios-monitoring}


Vous pouvez surveiller le nombre et le statut actuel des notifications push qui ont été envoyées. Pour permettre cette surveillance, ajoutez l'une des méthodes Swift suivante au délégué d'application de votre application reposant sur l'événement.



- Envoi du statut de notification quand l'application est ouverte en cliquant sur la notification.
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) { 					let push =  BMSPushClient.sharedInstance
				let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
				let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		    	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
    		  print("Send message status to the Push server")
    	 }
		}
	```
			{: codeblock}



- Envoi du statut de notification quand l'application est en mode arrière-plan.
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
	 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
	 	 	let push =  BMSPushClient.sharedInstance
			let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
	 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
	}
	}
	```
			{: codeblock}


### Envoi de notifications push de base
{: #send}

Une fois que vous avez développé vos applications, vous pouvez envoyer des notifications push de base.

Pour envoyer des notifications push de base, procédez comme suit :

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant une option **Envoyer à**. Les options prises en charge sont **Appareil par étiquette**, **ID de l'appareil**, **ID utilisateur**, **Appareils Android**, **Appareils IOS**, **Notifications Web** et **Tous les appareils**.  
**Remarque **: si vous sélectionnez l'option **Tous les appareils**, tous les appareils qui sont abonnés à des notifications de type {{site.data.keyword.mobilepushshort}} recevront les notifications.
![Ecran Notifications](images/tag_notification.jpg)

2. Dans la zone **Message**, composez votre message. Configurez les paramètres facultatifs, selon les besoins.
3. Cliquez sur **Envoyer**.
3. Vérifiez que vos appareils ont reçu votre notification.

L'image suivante présente une boîte de dialogue d'alerte qui traite une notification de type {{site.data.keyword.mobilepushshort}} sur un appareil iOS.

![Notification push qui s'exécute au premier plan sur un appareil iOS](images/iOS_Screenshot.jpg) 

#### Paramètres facultatifs pour l'envoi de notifications
{: #send_ios_otpional_setting}

Vous pouvez personnaliser les paramètres de type {{site.data.keyword.mobilepushshort}} pour l'envoi de notifications vers des appareils iOS. Les options de personnalisation facultative suivantes sont prises en charge.

- **Badge** : indique le nombre qui s'affiche sur le badge d'application. La valeur par défaut, zéro (0), n'affiche pas de badge. 
- **Son** : indique le clip audio à exécuter à réception d'une notification. Prend en charge le fichier par défaut ou utilise le nom de la ressource audio intégré dans l'application.
- **Contenu supplémentaire** : spécifie les valeurs de contenu personnalisées pour vos notifications.

### Activation des notifications interactives
{: #enb_snd_ios_otpional}

Vous pouvez à présent enrichir vos notifications iOS en leur ajoutant plus de détails, comme une image, une mappe ou un bouton de réponse en activant les notifications interactives. Ceci
fournit des informations de contexte supplémentaires aux utilisateurs, ainsi que la possibilité de lancer une action immédiate sans quitter le contexte en cours.  

Pour activer les notifications interactives, utilisez le code ci-après :



- Pour définir l'action de bouton
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
	```
		{: codeblock}


- Pour définir la catégorie pour les boutons
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- Pour mettre à jour l'enregistrement afin d'inclure des boutons
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

Pour envoyer une notification interactive, procédez comme suit :

1. Dans la section Compose, pour la liste déroulante Envoyer à, sélectionnez **Appareils IOS**.
2. Entrez le message de notification que vous voudrez peut-être envoyer.
3. Dans la section Paramètres facultatifs, sélectionnez **Mobile** et cliquez sur **iOS**.
4. Dans la liste déroulante Type, sélectionnez **Mixte**.
5. Dans la zone Catégorie, spécifiez le type de notification que vous avez défini dans votre application. 

![Notification interactive pour iOS](images/push_ios_notification_interactive.jpg) 

#### Etapes suivantes
{: #next_steps_02}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions du service de notifications push à votre application.
Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html).
Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).
