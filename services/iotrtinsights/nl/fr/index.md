---

Copyright :
  Années : 2015, 2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*Dernière mise à jour : 11 février 2016*

{{site.data.keyword.iotrtinsights_full}} sur Bluemix ({{site.data.keyword.iotrtinsights_short}}) vous permet d'effectuer des analyses de données en temps réel à partir de vos périphériques Internet of Things (Internet des objets) et d'obtenir des informations sur leur santé et sur l'état global de vos opérations.
{:shortdesc}

Pour pouvoir utiliser {{site.data.keyword.iotrtinsights_short}}, vous devez configurer le service {{site.data.keyword.iot_full}} ({{site.data.keyword.iot_short}}) pour la connexion de votre moteur d'analyse à vos périphériques. Vous pouvez utiliser un service {{site.data.keyword.iot_short}} existant ou en créer un nouveau. Pour être rapidement opérationnel, vous pouvez déployer dans votre organisation l'application téléphonique Internet of Things (Internet des objets) et le service {{site.data.keyword.iot_short}} qui lui est associé. 

Pour être rapidement opérationnel avec ce service, procédez comme suit :
1. Déployez le service {{site.data.keyword.iotrtinsights_short}} dans votre organisation Bluemix.
  1. A partir de votre tableau de bord de compte Bluemix, cliquez sur **Utiliser des services ou des API**.
  2. Localisez la section Internet of Things (Internet des objets) du catalogue de service et sélectionnez **{{site.data.keyword.iotrtinsights_short}}**.
  3. Sur la page {{site.data.keyword.iotrtinsights_short}}, vérifiez les sélections pour Ajout de service :  
    - Espace - Prenez soin de déployer le service dans le même espace que celui dans lequel vous avez déployé le service {{site.data.keyword.iot_short}}. 
    - Appli - Laissez non lié. 
    - Nom de service - Modifiez éventuellement le nom du service et remplacez-le par un nom facile à mémoriser. Le nom s'affiche dans la vignette IoT {{site.data.keyword.iotrtinsights_short}} dans le tableau de bord Bluemix. 
    - Plan sélectionné - Sélectionnez Gratuit ou choisissez un plan d'achat adapté à vos besoins.  
    > **Important :** Le plan {{site.data.keyword.iotrtinsights_short}} gratuit vous permet de déployer une seule instance du service par organisation.
  4. Cliquez sur **Utiliser** pour déployer {{site.data.keyword.iotrtinsights_short}} dans vos services Bluemix. 
2. Facultatif : Utilisez votre téléphone comme périphérique IoT avec IoT {{site.data.keyword.iotrtinsights_short}}.
Utilisez l'application téléphonique Internet of Things (Internet des objets) pour configurer rapidement votre smartphone afin qu'il agisse comme un périphérique IoT que vous pourrez utiliser pour vérifier votre environnement {{site.data.keyword.iotrtinsights_short}} et commencez à définir des analyses en temps réel sur les données. Pour plus d'informations sur l'application téléphonique Internet of Things (Internet des objets), voir le projet [Internet of Things phone application](https://github.com/ibm-messaging/IoT-html5-phone). 

  Pour créer l'application et connecter votre téléphone à {{site.data.keyword.iot_full}} :
  1. Cliquez sur le bouton suivant pour commencer le processus de déploiement :
  [![Icône Déployer dans Bluemix](images/deploy_to_bluemix.png "Deploy to Bluemix icon")(https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "Déployer le téléphone IoT dans Bluemix")(images/deploy_to_bluemix.png "Icône Déployer dans Bluemix")]  
  > **Remarque :** Le déploiement de l'application téléphonique Internet of Things (Internet des objets) a pour effet de déployer également un service {{site.data.keyword.iot_short}} (*iot-phone-iotf-service*) qui se lie automatiquement à l'application téléphonique. Ajoutez cette instance  {{site.data.keyword.iot_short}} en tant que source de données pour tester l'application téléphonique Internet of Things (Internet des objets). Le déploiement a également pour effet de créer un service Cloudant NoSQL DB (*iot-phone-cloudant-cloudantNoSQLDB*) qui est utilisé par l'application.

  2. Cliquez sur **Approuver** si vous êtes invité à approuver automatiquement l'accès pour le service IBM Single Sign On (OAuth Consent).  
  >**Astuce :** Si vous ne disposez pas de compte Bluemix, vous pouvez vous connecter pour activer votre compte d'essai Bluemix gratuit. 
  2. Remplacez le contenu de la zone Nom de l'application par un nom facilement mémorisable ; en l'occurrence, nous utiliserons le nom *application téléphonique* tout au long de ces instructions. Ce nom apparaît dans une vignette d'application dans votre tableau de bord Bluemix et fait partie de l'URL qui s'affichera lorsque vous connecterez votre téléphone à {{site.data.keyword.iot_short}}.
  2. Cliquez sur **Déployer**.
  2. Une fois le processus de déploiement terminé et le message 'Réussite' affiché, revenez à votre tableau de bord Bluemix. La vignette *application téléphonique* et la vignette *iot-phone-iotf-service* sont ajoutées à votre compte. 
  1. A partir du tableau de bord Bluemix, cliquez sur la vignette *application téléphonique*. 
  2. Depuis votre téléphone, ouvrez un navigateur et accédez à l'URL Routes qui est affichée au-dessous du nom d'application. Lorsque vous y êtes invité, entrez un ID de périphérique de votre choix pour identifier votre téléphone en tant que périphérique dans les tableaux de bord {{site.data.keyword.iot_short}} et IoT {{site.data.keyword.iotrtinsights_short}}. 
  3. Cliquez sur **Connecter** pour connecter votre téléphone à {{site.data.keyword.iot_short}} *iot-phone-iotf-service*.
  La vue est régénérée et affiche les données qui sont envoyées de votre téléphone à votre {{site.data.keyword.iot_short}}.
2. Créez et configurez un service Internet of Things (Internet des objets).   
> **Astuce :** Si vous avez déployé l'application téléphonique Internet of Things (Internet des objets), *iot-phone-iotf-service* est déjà créé et vous pouvez ignorer cette étape.   

  1. Connectez-vous à l'organisation Bluemix et sélectionnez l'espace dans lequel vous souhaitez déployer IoT {{site.data.keyword.iotrtinsights_short}}.
  2. A partir du tableau de bord Bluemix, cliquez sur **Utiliser des services ou des API**.
  3. Localisez la section Internet of Things (Internet des objets) du catalogue de service et sélectionnez **Internet of Things (Internet des objets)**.
  4. Sur la page {{site.data.keyword.iot_full}}, vérifiez les sélections pour Ajout de service et cliquez sur **Utiliser** pour ajouter {{site.data.keyword.iot_short}} à vos services Bluemix.
Une fois le service {{site.data.keyword.iot_short}} déployé, vous êtes conduit sur la page de gestion des services. 
3. Localisez les clés d'API de connexion.
Si vous avez créé un nouveau service {{site.data.keyword.iot_short}}, vous devez à présent créer des clés d'API pour connecter les deux services. Si vous utilisez un service existant, vous pouvez utiliser les clés existantes.  
  1. A partir du tableau de bord Bluemix, cliquez sur la vignette Internet of Things (Internet des objets).   
  >**Remarque :** Si vous utilisez l'application téléphonique Internet of Things (Internet des objets), cliquez sur la vignette *iot-phone-iotf-service*.   

  1. Cliquez sur **Lancer le tableau de bord** pour ouvrir le tableau de bord {{site.data.keyword.iot_full}}. 
  2. Naviguez jusqu'à **Accès > Clés d'API**.
  3. Cliquez sur **Générer une clé d'API**.
  3. Notez la clé d'API, le jeton d'authentification et l'ID organisation affichés en haut du tableau de bord {{site.data.keyword.iot_short}}.
  Vous utiliserez ces informations dans IoT {{site.data.keyword.iotrtinsights_short}} pour connecter les services.
4. Connectez votre service {{site.data.keyword.iot_short}} et votre service IoT {{site.data.keyword.iotrtinsights_short}}. 
  1. A partir du tableau de bord Bluemix, cliquez sur la vignette IoT {{site.data.keyword.iotrtinsights_short}}.   
  2. Sur la page de service, cliquez sur **Ajouter une source de données**.
  2. Sur la page Gérer les sources de données dans la console {{site.data.keyword.iotrtinsights_short}}, cliquez sur **Ajouter une source de données**.
  3. Attribuez un nom descriptif à la source de données et entrez les informations suivantes que vous avez collectées précédemment :
    - ID organisation
    - Clé d'API
    - Jeton d'authentification
  4. Cliquez sur l'![icône Créer](images/create.png "icône Créer") pour créer la source de données et établissez une connexion à celle-ci. 
4. Commencez à utiliser {{site.data.keyword.iotrtinsights_short}}.
Vous pouvez à présent commencer à utiliser {{site.data.keyword.iotrtinsights_short}} en ajoutant des utilisateurs, en connectant vos périphériques, en configurant vos tableaux de bord pour visualiser les données de périphérique pertinentes et en définissant des alertes. 
>**Sélection de votre instance {{site.data.keyword.iotrtinsights_short}} :** Si vous êtes autorisé à accéder à d'autres instances {{site.data.keyword.iotrtinsights_short}} en tant qu'opérateur ou administrateur, vous pouvez passer rapidement d'une instance à l'autre. Dans la console {{site.data.keyword.iotrtinsights_short}}, cliquez sur votre nom d'utilisateur et sélectionnez l'instance à laquelle vous souhaitez accéder.    

# rellinks
## samples
* [Application téléphonique Internet of Things (Internet des objets)](https://github.com/ibm-messaging/IoT-html5-phone)
* [Recettes Internet of Things (Internet des objets) developerWorks](https://developer.ibm.com/recipes/)
* [Création d'applis à l'aide de l'application de démarrage Internet of Things (Internet des objets)](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## api
* [Documentation API](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## general
* [A propos de](iotrtinsights_overview.html)   
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [Initiation à {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [dW Answers on IBM developerWorks](https://developer.ibm.com/answers/topics/iot-real-time/)
