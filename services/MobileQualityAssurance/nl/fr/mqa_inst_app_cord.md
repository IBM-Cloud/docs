---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Instrumentation de MQA avec une application Cordova (obsolète)
{: #instrumentcord}

Si vous souhaitez utiliser {{site.data.keyword.mqafull}} avec votre application Cordova, vous devez télécharger le logiciel SDK et l'instrumenter en effectuant quelques modifications à l'aide de l'interface de ligne de commande.
{: shortdesc}

Pour pouvoir instrumenter une application avec {{site.data.keyword.mqa}}, vous devez disposer d'un compte {{site.data.keyword.Bluemix}} et avoir installé la version de l'environnement de développement adaptée aux plateformes de l'application que vous instrumentez.

Pour instrumenter {{site.data.keyword.mqa}} en vue de son exécution avec votre application Cordova, procédez comme suit :

1. Ajoutez les droits requis et téléchargez le logiciel SDK dans votre projet Cordova.

	1. Ouvrez une invite de commande et accédez au répertoire contenant vos fichiers de projet.

	2. Ajoutez le plug-in {{site.data.keyword.mqa}} dans votre projet Cordova en procédant comme indiqué ci-après, en fonction de votre environnement :

		**Important** : si vous utilisez Xcode 7.x sur iOS 9, vous devez définir le paramètre Enable Bitcode sur la valeur No dans Xcode Build Settings. Pour modifier ce paramètre, ouvrez Xcode avec le fichier de projet Cordova .xcodeproj, qui se trouve dans le dossier platform\iPhone.

		* IBM MobileFirst™ Platform Foundation version 7.1 :

			1. Entrez la commande suivante pour installer le plug-in {{site.data.keyword.mqa}} :

				```
				mfp cordova plugin add emplacement_plug-in
				```
				{: codeblock}

			Où *emplacement_plug-in* correspond au chemin du répertoire du plug-in {{site.data.keyword.mqa}} extrait que vous avez téléchargé.

			2. Si votre application s'exécute sur Android, renommez le fichier `nom_pojet/nom_application/platforms/android/custom_rules.xml` en `custom_rules.xml.bak`.

		* Apache Cordova de version antérieure à la version 4.0 :
			1. Entrez la commande suivante pour installer le plug-in {{site.data.keyword.mqa}} :

				```
				cordova plugin add emplacement_plug-in
				```
				{: codeblock}

			Où *emplacement_plug-in* correspond au chemin du répertoire du plug-in {{site.data.keyword.mqa}} extrait que vous avez téléchargé.

			2. Entrez la commande suivante pour ajouter un plug-in requis supplémentaire :

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. Si votre application s'exécute sur Android, renommez le fichier `nom_pojet/nom_application/platforms/android/custom_rules.xml` en `custom_rules_bak.xml`.

		* Apache Cordova version 4.0 ou ultérieure :

			1. Entrez la commande suivante :

				```
				cordova plugin add emplacement_plug-in
				```
				{: codeblock}

			Où *emplacement_plug-in* correspond au chemin du répertoire du plug-in Cordova {{site.data.keyword.mqa}} extrait que vous avez téléchargé.

			2. Entrez la commande suivante pour ajouter un plug-in requis supplémentaire :

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. Démarrez une nouvelle session de {{site.data.keyword.mqa}} à chaque connexion.

	1. Ouvrez le fichier `index.js` qui se trouve dans le répertoire `nom_votre_projet\www\js`.

	2. Ajoutez la fonction et les paramètres suivants dans la fonction `onDeviceReady()` figurant dans le fichier `index.js`. Placez la fonction avant l'accolade de fin de la fonction.

	Restriction : si vous souhaitez qu'une application, déjà instrumentée pour Mobile Quality Assurance avec une version plus ancienne du plug-in pour Cordova, utilise les fonctions incluses dans le plug-in Mobile Quality Assurance pour Cordova versions 3.0.18 et ultérieures, vous devez régénérer et remplacer votre clé d'application. Pour plus d'informations sur la régénération de votre clé d'application, reportez-vous à la rubrique relative à la gestion des paramètres des applications. Les clés d'application générées avant février 2016 fonctionnent toujours avec l'ancien plug-in, mais ne fonctionnent plus si vous mettez à niveau votre plug-in vers la version 3.0.18, ou ultérieure.

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "votre_Clé_Application_Android_MQA" ,
				notificationsEnabled: true},
			ios: {
				appKey: "votre_Clé_Application_iOS_MQA" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. Poursuivez en procédant comme indiqué dans [Initiation à {{site.data.keyword.mqa}}](index.html).



# Liens connexes
{: #rellinks notoc}

## Liens connexes
{: #general notoc}
* [Initiation à {{site.data.keyword.mqa}}](index.html){:new_window}
