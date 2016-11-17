---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Initiation à {{site.data.keyword.iotinsurance_short}}

{{site.data.keyword.iotinsurance_full}} est un service {{site.data.keyword.Bluemix_notm}} que vous pouvez utiliser pour collecter,
gérer et analyser des données provenant des assurés connectés. {{site.data.keyword.iotinsurance_short}} vous permet de proposer des évaluations
personnalisées des risques, une protection en temps réel et des réductions sur les coûts d'assurance.
{:shortdesc}

Pour que ce service soit opérationnel, vous devez déployer les services et les applications nécessaires, puis configurer les services. Vous trouverez une présentation des services et de l'application, ainsi qu'un diagramme d'architecture dans la section [A propos d'{{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)

**Configuration requise :** avant de commencer, assurez-vous de disposer des éléments requis suivants :
- Une instance du [service {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) doit exister dans votre espace {{site.data.keyword.Bluemix_notm}}.
- Au moins 2 Go de mémoire doivent être disponible dans votre organisation {{site.data.keyword.Bluemix_notm}} pour activer la fonction de déploiement.

## Déploiement des services et des applications nécessaires
{: #deploying_services}

1. Pour déployer tous les services et toutes les applications nécessaires, dans la [console {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), cliquez sur le service{{site.data.keyword.iotinsurance_short}}, puis sur **Déployer**.

  {{site.data.keyword.iotinsurance_short}} déploie tous les services et toutes les applications Node.js dont il a besoin. Il lie
automatiquement les applications aux services.

  Chaque instance de service utilise le plan de service par défaut. Vous pouvez mettre les plans de service à niveau ultérieurement dans la console
du service. Vous pouvez aussi utiliser une instance existante d'un service en supprimant la nouvelle instance et en liant manuellement l'instance existante
au service {{site.data.keyword.iotinsurance_short}}. Pour plus d'informations sur les applications, voir
[A propos d'{{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Vérifiez que le tableau de bord {{site.data.keyword.iotinsurance_short}} est opérationnel et que vous pouvez accéder aux API.
  1. Ouvrez le tableau de bord {{site.data.keyword.iotinsurance_short}} en cliquant sur **Ouvrir**. Acceptez les données d'identification préremplies en cliquant sur **Connexion**.
  2. Revenez à la console de service {{site.data.keyword.iotinsurance_short}} et consultez les API en cliquant sur **API**.

  **Remarque :** Après le déploiement, vous pouvez accéder directement au tableau de bord ou aux API en entrant leurs URL respectives dans votre navigateur. Lorsque vous utilisez cette méthode, vous devez entrer vos données d'identification pour le service {{site.data.keyword.iotinsurance_short}}. Pour trouver vos données d'identification, revenez à la console de service {{site.data.keyword.iotinsurance_short}}. Cliquez sur l'onglet **Données d'identification pour le service**, puis cliquez sur **Afficher les données d'identification**. Prenez note de l'ID utilisateur et du mot de passe. 

## Configuration des services
{: #iot4i_configservices}
Procédez comme suit pour configurer les services :

### Configuration de {{site.data.keyword.amashort}}
{: #config_ama}
1. Revenez à la console Bluemix. Toutes les applications et tous les services qui ont été déployés par {{site.data.keyword.iotinsurance_short}} s'affichent. 

1. Copiez l'URL de l'application d'API {{site.data.keyword.iotinsurance_short}}. Cliquez à l'aide du bouton droit de la souris sur l'application d'API et sélectionnez l'option permettant de copier l'emplacement du lien.

2. Ouvrez le service {{site.data.keyword.amashort}}. Le service est disponible dans la section Services de votre console {{site.data.keyword.Bluemix_notm}}.

3. Activez l'authentification en cliquant sur **Activer**.

4. Dans la section **Personnalisé**, cliquez sur **Configurer**, puis entrez les données d'authentification suivantes :

  - **Nom de domaine** : `IoT4I`

  - **URL de fournisseur d'identité personnalisé** : collez l'URL de l'application d'API que vous avez copiée à la première étape.

  - **Vos URI de redirection d'application Web** : ne renseignez pas cette zone.

5. Sauvegardez vos paramètres. Vous pouvez maintenant revenir à la console de service {{site.data.keyword.iotinsurance_short}} ou à votre console {{site.data.keyword.Bluemix_notm}}. 

### Configuration de {{site.data.keyword.mobilepushshort}}
{: #config_push}
Afin d'activer les notifications push pour une application mobile existante, vous devez configurer le service {{site.data.keyword.mobilepushshort}}
et ajouter un fichier Public
Key Cryptography Standards (PKCS) 12. Pour des informations sur l'application mobile, voir [Installation et
connexion du modèle d'application mobile](iotinsurance_mobile_app.html). Pour des informations sur {{site.data.keyword.mobilepushshort}}, voir
[Initiation à Push Notifications](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Ouvrez le service {{site.data.keyword.mobilepushshort}}.
  2. Cliquez sur **Configurer**.
  3. Dans la section Certificat Apple Push Notification, téléchargez le fichier PKCS 12 pour votre application mobile et entrez le mot
de
passe.


Etape suivante ?
{: #whats_next}
Découvrez {{site.data.keyword.iotinsurance_short}}.

- Utilisez les instructions et les API contenues dans le kit d'outils de bouclier pour créer une [association entre un utilisateur et un bouclier](iotinsurance_shield_toolkit.html).
- Installez et connectez le [modèle d'application mobile](iotinsurance_mobile_app.html).
- Téléchargez ou affichez toutes les [API du site GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples).

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}
* [Code du modèle d'application mobile dans GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Référence d'API
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## Liens connexes
{: #general}
* [Documentation {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Forum de
support des développeurs](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Forum de support stackoverflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
