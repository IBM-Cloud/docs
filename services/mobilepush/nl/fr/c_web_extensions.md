---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des applications et extensions Chrome pour recevoir des notifications de type {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Dernière mise à jour : 18 janvier 2017
{: .last-updated}

Vous pouvez autoriser les applications et extensions Google Chrome à recevoir des
{{site.data.keyword.mobilepushshort}}. Vérifiez que vous avez exécuté la procédure [Configuration des données
d'identification pour un fournisseur de notification](t__main_push_config_provider.html) avant de poursuivre.

## Installation du logiciel SDK client pour {{site.data.keyword.mobilepushshort}}
{: #web_install}

Cette rubrique décrit comment installer et utiliser le logiciel SDK Push JavaScript du client afin de développer davantage vos applications et extensions Chrome.

### Initialisation dans les applications et extensions Google Chrome

Pour installer le logiciel SDK Javascript dans les applications et extensions Chrome, procédez comme suit :

Téléchargez les fichiers `BMSPushSDK.js` et `manifest_Chrome_Ext.json` (pour les extensions Chrome) ou
`manifest_Chrome_App.json` (pour les applications Chrome) depuis le
[SDK push Web
Bluemix![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master "Icône de lien externe"){: new_window}.



- Pour les applications Chrome, configurez le fichier manifeste :
 1. Dans le fichier `manifest_Chrome_App.json`, fournissez le nom, la description et les icônes.
 2. Ajoutez le fichier `BMSPushSDK.js` dans `app.background.scripts`.
 3. Changez `manifest_Chrome_App.json` en `manifest.json`.

- Pour les extensions Chrome, configurez le fichier manifeste :
 1. Dans le fichier `manifest_Chrome_Ext.json`, fournissez le nom, la description et les icônes.
 2. Ajoutez le fichier `BMSPushSDK.js` dans `background.scripts`.
 3. Changez `manifest_Chrome_Ext.json` en `manifest.json`.

Dans le fichier `background.js`, ajoutez les lignes de code ci-dessous pour recevoir des notifications push : 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## Initialisation du logiciel SDK Push 
{: #web_initialize}

Initialisez le logiciel SDK Push avec les services {{site.data.keyword.mobilepushshort}} Bluemix `appGUID` et `appRegion`.  

Pour obtenir votre service appGUID, sélectionnez l'option **Configuration** dans le panneau de navigation pour vos services push initialisés puis cliquez sur **Options pour application mobile**. Modifiez le fragment de code pour qu'il utilise le paramètre appGUID de votre service de notifications push Bluemix.

La valeur de `AppRegion` spécifie l'emplacement où est hébergé le service {{site.data.keyword.mobilepushshort}}. Vous pouvez utiliser l'une des trois valeurs suivantes :

 - Pour Dallas, Etats-Unis :	 `.ng.bluemix.net`
 - Pour le Royaume-Uni :			 `.eu-gb.bluemix.net`
 - Pour Sydney :		 `.au-syd.bluemix.net`

```
 var bmsPush = new BMSPush();
    function callback(response) {
 alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Enregistrement des applications et extensions Chrome
{: #web_register}

Utilisez l'API `register()` pour enregistrer l'appareil auprès du service {{site.data.keyword.mobilepushshort}}. Pour procéder à un enregistrement depuis Google Chrome, ajoutez la clé d'API FCM (Firebase Cloud Messaging) ou GCM (Google Cloud Messaging) et l'URL de site Web dans le tableau de bord de configuration Web du service {{site.data.keyword.mobilepushshort}} Bluemix. Pour plus d'informations, voir [Configuration de données d'identification pour Google Cloud Messaging (GCM)](t_push_provider_android.html), dans la rubrique relative à la configuration de Chrome.

Pour l'enregistrement depuis Mozilla Firefox, ajoutez l'URL de site Web dans le tableau de bord de configuration Web du service {{site.data.keyword.mobilepushshort}} Bluemix, dans la configuration Firefox.

Utilisez les fragments de code ci-après pour procéder à l'enregistrement auprès du service {{site.data.keyword.mobilepushshort}} Bluemix.
```
var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}




