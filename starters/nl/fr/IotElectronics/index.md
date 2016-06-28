---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Création d'applications avec le module de démarrage {{site.data.keyword.iotelectronics}}
*Dernière mise à jour : 14 juin 2016*

{{site.data.keyword.iotelectronics_full}} est une solution de
bout en bout intégrée qui permet à vos applications de communiquer avec, de
contrôler, d'analyser et de mettre à jour des appareils connectés. Le
module de démarrage comprend une application de démarrage, qui vous permet de
créer et de contrôler des appareils simulés, ainsi qu'une application mobile
exemple, qui vous permet de contrôler ces appareils à partir de votre
périphérique mobile.
{:shortdesc}

**Prérequis**:  
Vérifiez que vous avez déployé le module de démarrage
{{site.data.keyword.iotelectronics}} dans la section Conteneurs
boilerplates du catalogue Bluemix. Cela entraîne le déploiement automatique
des applications et des services du module de démarrage, notamment {{site.data.keyword.amafull}}.

Pour commencer à utiliser {{site.data.keyword.iotelectronics}},
effectuez les tâches décrites ci-après, comme indiqué dans les sections qui
suivent : 

1. Activez les communications avec l'application mobile exemple en
configurant {{site.data.keyword.amashort}}.
2. Créez des appareils simulés à l'aide de l'application Web du
module de démarrage {{site.data.keyword.iotelectronics}}. 
3. Installez et connectez l'application mobile exemple. 

## Configuration de {{site.data.keyword.amashort}}
{: #configureMCA}
Pour pouvoir utiliser l'application mobile, vous devez configurer
{{site.data.keyword.amashort}}, comme suit :
1. Dans votre tableau de bord
{{site.data.keyword.Bluemix_notm}}, ouvrez [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html).
2. Dans la section **Personnalisé**, sélectionnez
**Configurer**.
3. Indiquez les données d'authentification suivantes : 
  - **Nom de domaine** : myRealm
  - **URL** : https://<*monAppDémarrageIoT4e*>.mybluemix.net  

    **Conseil :** Veillez à employer le préfixe sécurisé
`https://` dans l'URL. Vous trouverez l'URL de votre
application de démarrage en cliquant sur **Options pour application
mobile**.)
4. Enregistrez.

  Pour obtenir des instructions détaillées, voir
[Configuration
de {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA).

##Création d'appareils simulés
Pour créer un appareil simulé, procédez comme suit : 
1. Dans votre tableau de bord
{{site.data.keyword.Bluemix_notm}}, démarrez l'application
{{site.data.keyword.iotelectronics}}. 
2. Patientez jusqu'à ce que le message de statut `Votre
application est en cours d'exécution` s'affiche, puis cliquez sur
**Afficher l'appli** pour afficher l'application de
démarrage.   
3. Sélectionnez **Contrôlez à distance vos appareils
connectés**.
4. Accédez à la section intitulée **Ensuite, choisissez ou
ajoutez un nouveau lave-linge simulé** et cliquez sur le bouton
Ajouter (+). Un lave-linge est créé.

## Installation et connexion de l'application mobile exemple
Pour installer et connecter l'application mobile exemple, procédez comme
suit : 

*Remarque* : Vous devez disposer d'un périphérique iOS
pour utiliser l'application mobile exemple. 

1. Sur votre téléphone, ouvrez l'App Store et recherchez `ibm iot`. 
Sélectionnez **IBM IoT for Electronics** et installez
l'application. 
2. Connectez votre téléphone à votre organisation en scannant le code
Quick Response de connexion de l'application de démarrage. 
3. Connectez votre appareil simulé en scannant le code Quick Response
de l'appareil trouvé dans l'application de démarrage. 

  Pour obtenir des instructions détaillées, voir [Connexion de l'application mobile à votre environnement {{site.data.keyword.iotelectronics}}](iotelectronics_config_mobile.html#iot4e_connecting_mobile).

##Etapes suivantes
Découvrez ce que vous pouvez faire avec {{site.data.keyword.iotelectronics}}.

- Explorez l'application de démarrage pour savoir comment un fabricant
d'entreprise peut contrôler les appareils connectés à {{site.data.keyword.iot_short_notm}}.
- Explorez l'application mobile exemple pour savoir comment les
propriétaires d'appareil peuvent enregistrer leurs appareils et interagir
avec ces derniers. 
- Créez manuellement une panne de l'appareil pour déclencher des
alertes, des notifications et des actions auprès du fabricant et du
propriétaire de l'appareil. 
- Associez les données opérationnelles aux données utilisateur pour
comprendre le fonctionnement de vos produits et périphériques et savoir qui les
contrôle. 


# Liens connexes
{: #rellinks}
## Documentation sur les API
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## Composants
{: #general}

* [Documentation {{site.data.keyword.iotelectronics_full}}](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Exemples
{: #samples}
* [Application mobile exemple](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
