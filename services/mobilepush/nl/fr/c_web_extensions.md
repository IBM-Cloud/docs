---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des applications et extensions Chrome pour recevoir des notifications de type Push Notifications
{: #web_notifications}
Dernière mise à jour : 12 avril 2017
{: .last-updated}

Vous pouvez autoriser les applications et extensions Google Chrome à recevoir des
{{site.data.keyword.mobilepushshort}}. Vérifiez que vous avez exécuté la procédure [Configuration des données
d'identification pour un fournisseur de notification](t__main_push_config_provider.html) avant de poursuivre.

## Installation du logiciel SDK client pour Push Notifications
{: #web_install}

Cette rubrique décrit comment installer et utiliser le logiciel SDK Push JavaScript du client afin de développer davantage vos applications et extensions Chrome.

### Initialisation dans les applications et extensions Google Chrome
{: #initialize_google_extn_app}

Pour installer le logiciel SDK Javascript dans les applications et extensions Chrome, procédez comme suit :

Téléchargez les fichiers `BMSPushSDK.js` et `manifest_Chrome_Ext.json` (pour extensions Chrome) ou `manifest_Chrome_App.json` (pour applications Chrome Apps) depuis le site [Bluemix Web push SDK ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.



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



### Initialisation du logiciel SDK Push 
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

### Enregistrement des applications et extensions Chrome
{: #web_register}

Utilisez l'API `register()` pour enregistrer l'appareil auprès du service {{site.data.keyword.mobilepushshort}}. Pour procéder à un enregistrement depuis Google Chrome, ajoutez la clé d'API FCM (Firebase Cloud Messaging) et l'URL de site Web dans le tableau de bord de configuration Web du service {{site.data.keyword.mobilepushshort}} Bluemix.Pour plus d'informations, voir [Configuration des données d'identification pour un fournisseur de notification](t__main_push_config_provider.html). 

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


## Envoi de notifications de base aux Applications et extensions Google Chrome 
{: #web_extensions_notifications}

Une fois que vous avez développé vos applications, vous pouvez envoyer une notification push. 

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant **Notifications Web** comme option **Envoyer à**. 
2. Entrez le message qui doit être distribué dans la zone **Message**.
3. Vous pouvez choisir de fournir des paramètres facultatifs :
  - **Titre de la notification** : il s'agit du texte qui s'affichera comme en-tête de l'alerte du message.
  - **URL de l'icône de notification** : si votre message doit être distribué avec une icône de notification d'application, fournissez dans cette zone le lien à l'icône.
  - **Touche de réduction** : des touches de réduction sont attachées aux notifications. Si plusieurs notifications arrivent séquentiellement avec la même touche de réduction quand l'appareil est hors ligne, elles sont réduites. Quand un appareil passe en ligne, il reçoit des notifications du serveur FCM/GCM et n'affiche que la dernière notification portant la même touche de réduction. Si aucune touche de réduction n'est définie, les nouveaux et les anciens messages sont stockés pour une distribution future.
  - **Durée de vie** : cette valeur est définie en secondes. Si ce paramètre n'est pas spécifié, le serveur FCM/GCM stocke le message pendant quatre semaines et tente de le distribuer. La validité expire après quatre semaines. La plage des valeurs possibles va de 0 à 2419200 secondes.
  - ****Retarder si inactif : en définissant cette valeur à `true`, vous demandez au serveur FCM/GCM de ne pas distribuer de notification si le serveur est inactif. Définissez cette valeur à `false` pour garantir la distribution de la notification même si l'appareil est en veille.
  - **Contenu supplémentaire** : spécifie les valeurs de contenu personnalisées pour vos notifications.

L'image suivante montre l'option Applications et extensions Google Chrome du tableau de bord.

  ![Ecran Notifications](images/push_chrome_extns.jpg)
  
### Etapes suivantes
{: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez choisir de configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions de service {{site.data.keyword.mobilepushshort}} à votre application. Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html). Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).



