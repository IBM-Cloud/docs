---

copyright:
 years: 2015 2016

---


# Activation des applications pour recevoir {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Dernière mise à jour : 17 octobre 2016
{: .last-updated}

Vous pouvez désormais activer les applications Web Google Chrome et Mozilla Firefox pour recevoir des notifications {{site.data.keyword.mobilepushshort}}.

## Installation du logiciel SDK client de navigateur Web pour {{site.data.keyword.mobilepushshort}}
{: #web_install}

Cette rubrique décrit comment installer et utiliser le logiciel SDK Push JavaScript du client afin de développer davantage vos applications Web.

### Initialisation dans l'application Web Google Chrome

Pour installer le logiciel SDK Javascript dans l'application Web Chrome, procédez comme suit :

Téléchargez les fichiers `BMSPushSDK.js`, `BMSPushServiceWorker.js` et `manifest_Website.json` depuis le [logiciel SDK Push Web Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master).

1. Editez le fichier `manifest_Website.json`.

Pour le navigateur Google Chrome, remplacez la valeur de `name` par le nom de votre site Web. Changez la  valeur de `gcm_sender_id` en la remplaçant par la valeur sender_ID de votre élément FCM (Firebase Cloud Messaging) ou GCM (Google Cloud Messaging). Pour plus d'informations, voir la [documentation Google](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/#make_a_project_on_the_google_developer_console). La valeur gcm_sender_id ne contient que des chiffres.

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
 }
```
    {: codeblock}
 
Pour le navigateur Mozilla Firefox, ajoutez les valeurs suivantes dans le fichier `manifest.json`.     Remplacez la valeur de `name` par le nom de votre site.

```
{
  "name": "YOUR_WEBSITE_NAME"
 }
```
    {: codeblock}

2. Changez le nom de fichier `manifest_Website.json` en `manifest.json`.
3. Ajoutez les fichiers `BMSPushSDK.js`, `BMSPushServiceWorker.js` et `manifest.json` dans votre répertoire racine.
3. Incluez le fichier `manifest.json` dans la balise `<head>` de votre fichier html.
```
 <link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. Incluez le logiciel SDK Push Web Bluemix dans l'application Web depuis GitHub.
```
 <script src="BMSPushSDK.js" async></script>
```
    {: codeblock}

## Initialisation du logiciel SDK Push Web 
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

## Enregistrement de l'application Web
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

## Envoi des notifications de type {{site.data.keyword.mobilepushshort}} de base
  {: #send}

Une fois que vous avez développé vos applications, vous pouvez envoyer une notification push. 

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant **Notifications Web** comme option **Envoyer à**. 
2. Entrez le message qui doit être distribué dans la zone **Message**.
3. Vous pouvez choisir de fournir des paramètres facultatifs :
  - **Titre de la notification** : il s'agit du texte qui s'affichera comme en-tête de l'alerte du message.
  - **URL de l'icône de notification** : si votre message doit être distribué avec une icône de notification d'application, fournissez dans cette zone le lien à l'icône.
  - **Contenu supplémentaire** : spécifie les valeurs de contenu personnalisées pour vos notifications.

L'image suivante montre l'option Notifications Web du tableau de bord.

  ![Ecran Notifications](images/DashboardWebpush.jpg)
  
## Etapes suivantes
  {: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez configurer des notifications basées sur des balises et des options avancées.

Ajoutez ces fonctions du service {{site.data.keyword.mobilepushshort}} à votre application. Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html). Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).



