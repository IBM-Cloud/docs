---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Important : Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.**

# Configuration du plug-in Cordova
{: #getting-started-cordova}

Instrumentez votre application client Cordova avec le SDK client d'{{site.data.keyword.amafull}}. Initialisez le gestionnaire d'autorisations dans
votre code Android (Java) ou iOS (Objective C) en utilisant le SDK Swift et le fichier d'en-tête pertinents. Initialisez le client et envoyez des demandes à des ressources protégées et non protégées à partir de WebView.

{:shortdesc}

## Avant de commencer
{: #before-you-begin}
Vous devez disposer des éléments suivants :

* Une instance d'une application {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Une instance d'un service {{site.data.keyword.amafull}}.
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney`, et correspondre aux valeurs requises dans le code Javascript de WebView : `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` ou `BMSClient.REGION_UK`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.
* Une application Cordova ou un projet existant. Pour plus d'informations sur la configuration de votre application Cordova, voir le [site Web Cordova ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cordova.apache.org/){: new_window}.

## Installation du plug-in {{site.data.keyword.amashort}} Cordova
{: #getting-started-cordova-plugin}

Le SDK client de {{site.data.keyword.amashort}} pour Cordova est un plug-in Cordova qui encapsule les SDK client natifs de
{{site.data.keyword.amashort}}. Il est distribué à l'aide de l'interface de ligne de commande Cordova et de `npmjs`, un référentiel de plug-ins pour les projets Cordova. L'interface
CLI de Cordova télécharge automatiquement des plug-ins depuis les référentiels et les rend disponibles depuis votre application Cordova.

1. Ajoutez les plateformes Android et/ou iOS à votre application Cordova. Exécutez l'une des commandes suivantes ou les deux à partir de la ligne de commande :

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. Si vous avez ajouté la plateforme Android, vous devez ajouter le niveau d'API minimal pris en charge au fichier `config.xml` de votre application Cordova. Ouvrez
le fichier `config.xml` et ajoutez la ligne suivante à l'élément `<platform
name="android">` :

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	La valeur de *minSdkVersion* doit être supérieure ou égale à `15`. Reportez-vous au manuel [Android Platform Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} pour être tenu informé de la version *targetSdkVersion* prise en charge pour le SDK Android.

3. Si vous avez ajouté le système d'exploitation iOS, déclarez une cible dans l'élément `<platform name="ios">` :

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. Installez le plug-in Cordova de {{site.data.keyword.amashort}} :

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Configurez votre plateforme pour Android, iOS, ou les deux.

	####Android
	{: #cordova-android}

	Avant d'ouvrir votre projet dans Android Studio, générez votre application Cordova via votre interface de ligne de commande (CLI) pour éviter des erreurs
de génération.

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	Configurez comme suit votre projet Xcode.

	1. Utilisez la version Xcode la plus récente pour ouvrir votre fichier `xcode.proj` depuis le répertoire
`<app_name>/platforms/ios`.

		**Important :** si vous recevez un message vous invitant à procéder à une conversion vers la dernière syntaxe Swift, cliquez sur **Annuler**.

	2. Générez et exécutez votre application avec Xcode.

	**Remarque **: vous risquez de recevoir l'erreur suivante lors de l'exécution de `cordova build ios`. Ce problème est dû à un bogue dans un plug-in de dépendance (suivi dans [Issue 12 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12){: new_window}. Vous pouvez toujours exécuter le projet iOS dans XCode via un simulateur ou un appareil.

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```

6. Vérifiez que l'installation du plug-in a abouti en exécutant la commande suivante :

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. Activez le partage de chaîne de certificats pour iOS en basculant **Keychain Sharing** sur `On` dans l'onglet **Capabilities**.

8. Activez **Defines Module** pour iOS en basculant **Defines Module** sur `YES` dans l'onglet **Build Settings** > **Packaging**.


## Initialisation du client {{site.data.keyword.amashort}} dans le WebView Cordova (Javascript)
{: #getting-started-cordova-initialize}

Pour utiliser le SDK client de {{site.data.keyword.amashort}}, initialisez-le en lui transmettant le paramètre `applicationBluemixRegion`.

Ajoutez l'appel suivant à votre fichier `index.js` pour initialiser le SDK client de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**NB :** Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre service {{site.data.keyword.Bluemix_notm}} est hébergé, voir [Avant de commencer](#before-you-begin).

##Initialisation du gestionnaire AuthorizationManager {{site.data.keyword.amashort}} à partir de votre code natif
{: #initializing-auth-manager}

Pour utiliser `BMSAuthorizationManager`, vous devez ajouter l'extrait de code suivant. Le code natif suivant initialise le gestionnaire `BMSAuthorizationManager` avec le service {{site.data.keyword.amashort}}, `tenantId` (voir [Avant de commencer](#before-you-begin)).

### Android (Java)

Dans la méthode `OnCreate` du fichier `MainActivity.java`, ajoutez le code avant `loadUrl`.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
Ajoutez l'initialisation du Gestionnaire d'autorisations dans `AppDelegate.m` selon votre version de Xcode.

```Objective-C
  #import "<nom_votre_module>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**Remarque :** le nom du fichier d'en-têtes importé est composé du nom de votre module concaténé à la chaîne `-Swift.h`, par exemple, si le nom de votre module est `Cordova` alors la ligne d'importation est `#import "Cordova-Swift.h"`. Pour trouver le nom du module, allez à
`Build Settings` > `Packaging` > `Product Module Name`.
Remplacez `<tenantId>` par l'DI de votre locataire (voir [Avant de commencer](#before-you-begin)).


## Envoi d'une demande au service back end mobile
{: #getting-started-request}

Une fois que le SDK client {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des requêtes à votre service back end
mobile.

1. Essayez d'envoyer une requête à un noeud final protégé de votre application back end
mobile. Dans votre navigateur, ouvrez l'URL suivante : `{applicationRoute}/protected` (`http://my-mobile-backend.mybluemix.net/protected`, par exemple).

	Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

2. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. Lorsque votre demande aboutit, la sortie suivante figure dans la console LogCat ou Xcode (selon la plateforme utilisée) :

	![message de succès](images/getting-started-android-success.png)

	## Etapes suivantes
	{: #next-steps}

	Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Authentification personnalisée](custom-auth-cordova.html)
