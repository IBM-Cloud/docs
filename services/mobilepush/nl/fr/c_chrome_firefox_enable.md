---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des applications pour recevoir {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Dernière mise à jour : 16 février 2017
{: .last-updated}

Vous pouvez permettre aux applications Web Google Chrome, Mozilla Firefox et Safari de recevoir des {{site.data.keyword.mobilepushshort}}. Vérifiez que
vous avez exécuté la procédure [Configuration des données d'identification pour un fournisseur de notification](t__main_push_config_provider.html)
avant de poursuivre.

## Installation du logiciel SDK client de navigateur Web pour {{site.data.keyword.mobilepushshort}}
{: #web_install}

Cette rubrique décrit comment installer et utiliser le logiciel SDK Push JavaScript du client afin de développer davantage vos applications Web.

### Initialisation dans l'application Web

Pour installer le logiciel SDK Javascript dans l'application Google Chrome Web, procédez comme suit :

Téléchargez les fichiers `BMSPushSDK.js`, `BMSPushServiceWorker.js` et `manifest_Website.json` depuis le
[logiciel SDK Push Web Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.

1. Editez le fichier `manifest_Website.json`.
	- Pour le navigateur Google Chrome, remplacez la valeur de `name` par le nom de votre site Web. Par exemple, `www.dailynewsupdates.com`. Changez la  valeur de `gcm_sender_id` en la remplaçant par la valeur sender_ID de votre élément FCM (Firebase Cloud Messaging) ou GCM (Google Cloud Messaging). Pour plus d'informations, voir [Obtention de votre ID d'émetteur et de la clé d'API](t_push_provider_android.html). La valeur gcm_sender_id ne contient que des chiffres.

		```
			{
	"name": "Nom_de_votre_site_Web",
  			"gcm_sender_id": "ID_émetteur_GCM"
			 }
		```
    		{: codeblock}
 
	- Dans le cas du navigateur Mozilla Firefox, ajoutez les valeurs suivantes dans le fichier `manifest_Website.json`. Indiquez un nom, `name`, approprié. Ce serait le nom de votre site Web.

		```
			{ 
	"name": "Nom_de_votre_site_Web"
			 }
		```
    		{: codeblock}

2. Changez le nom de fichier `manifest_Website.json` en `manifest.json`.
3. Ajoutez les fichiers `BMSPushSDK.js`, `BMSPushServiceWorker.js` et `manifest.json` au répertoire racine de votre site Web.
3. Incluez le fichier `manifest.json` dans la balise `<head>` de votre fichier html.
	```
		<link rel="manifest" href="manifest.json">
	```
    	{: codeblock}
4. Incluez le logiciel SDK Push Web Bluemix dans l'application Web.
	```
		<script src="BMSPushSDK.js" async></script>
	```
    	{: codeblock}

**Remarque** : Vérifiez que le code est déployé et prenez soin d'accéder au lien de l'exemple via `https` et non pas `http`. 

## Initialisation du logiciel SDK Push Web 
{: #web_initialize}

Initialisez le SDK en spécifiant le `GUID d'application` et la `Région de l'application
` du service Bluemix {{site.data.keyword.mobilepushshort}}.  

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
  	"appGUID":"GUID application push",
  "appRegion":"Région où le service est hébergé",
  "clientSecret":"clientSecret de votre service push"
  "websitePushIDSafari": "Paramètre facultatif pour notifications Push Safari uniquement. Cette valeur doit correspondre à l'ID Push de site Web fourni lors de la configuration côté serveur." }
  	bmsPush.initialize(initParams, callback)
```
	{: codeblock}

**Remarque **: si vos données d'identification pour le SDK Web push ont été modifiées, la remise du message risque d'échouer pour le
navigateur Chrome. Prenez soin d'appeler `bmsPush.unRegisterDevice` pour éviter un échec.

Si vous soumettez des paramètres erronés, vous pouvez rencontrer des erreurs liées à la configuration. Pour plus d'informations, voir [Résolution des erreurs de configuration push Web](troubleshooting_config_errors.html).

## Enregistrement de l'application Web
{: #web_register}

Utilisez l'API **register()** pour enregistrer l'appareil auprès du service {{site.data.keyword.mobilepushshort}}. Utilisez l'une des options suivantes, selon votre navigateur.

- Pour procéder à un enregistrement depuis Google Chrome, ajoutez la clé d'API FCM (Firebase Cloud Messaging) ou GCM (Google Cloud Messaging) et l'URL de site Web dans le tableau de bord de configuration Web du service {{site.data.keyword.mobilepushshort}} Bluemix. Pour plus d'informations, voir [Configuration de données d'identification pour Google Cloud Messaging (GCM)](t_push_provider_android.html), dans la rubrique relative à la configuration de Chrome.

- Pour l'enregistrement depuis Mozilla Firefox, ajoutez l'URL de site Web dans le tableau de bord de configuration Web du service {{site.data.keyword.mobilepushshort}} Bluemix, dans la configuration Firefox.

Utilisez les fragments de code ci-après pour procéder à l'enregistrement auprès du service {{site.data.keyword.mobilepushshort}} Bluemix.

```
	var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"GUID application push",
  "appRegion":"Région où le service est hébergé",
  "clientSecret":"clientSecret de votre service push"
  "websitePushIDSafari": "Paramètre facultatif pour notifications Push Safari uniquement. Cette valeur doit correspondre à l'ID Push de site Web fourni lors de la configuration côté serveur." }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}






