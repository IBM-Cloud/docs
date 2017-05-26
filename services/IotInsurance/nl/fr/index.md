---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Initiation à {{site.data.keyword.iotinsurance_short}}
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} est un service {{site.data.keyword.Bluemix_notm}} que vous pouvez utiliser pour collecter,
gérer et analyser des données provenant des assurés connectés. {{site.data.keyword.iotinsurance_short}} vous permet de proposer des évaluations
personnalisées des risques, une protection en temps réel et des réductions sur les coûts d'assurance.
{:shortdesc}

Pour que ce service soit opérationnel, vous devez déployer les services et les applications nécessaires, puis configurer les services. Vous trouverez une présentation des services et de l'application, ainsi qu'un diagramme d'architecture dans la section [A propos d'{{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)

**Configuration requise :** avant de commencer, assurez-vous de disposer des éléments requis suivants :
- Une instance du [service {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) doit exister dans votre espace {{site.data.keyword.Bluemix_notm}}.
- Au moins 2 Go de mémoire doivent être disponible dans votre organisation {{site.data.keyword.Bluemix_notm}} pour activer la fonction de déploiement. Si vous effectuez une mise
à niveau depuis une version précédente, vous devez avoir au moins 2,5 Go disponibles.

## Déploiement des services et des applications nécessaires
{: #deploying_services}

1. Pour déployer tous les services et toutes les applications nécessaires, dans la [console {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), cliquez sur le service{{site.data.keyword.iotinsurance_short}}, puis sur **Déployer**.

  {{site.data.keyword.iotinsurance_short}} déploie tous les services et toutes les applications Node.js dont il a besoin. Il lie
automatiquement les applications aux services.

  Chaque instance de service utilise le plan de service par défaut. Vous pouvez mettre les plans de service à niveau ultérieurement dans la console
du service. Vous pouvez aussi utiliser une instance existante d'un service en supprimant la nouvelle instance et en liant manuellement l'instance existante
au service {{site.data.keyword.iotinsurance_short}}. Pour plus d'informations sur les applications, voir
[A propos d'{{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

  **Important :**  Lorsque vous déployez la version d'essai de {{site.data.keyword.iotinsurance_short}}, notez que les versions gratuites des autres services et
applications qui sont également déployées sont limitées dans leur fonctionnalité. {{site.data.keyword.iot_short_notm}} est limité à un maximum de 500 périphériques et
{{site.data.keyword.cloudant_short_notm}} est limité à un Go de données et possède des fonctions limitées de gestion des unités d'exécution en lecture et en écriture.

  **Remarque** : {{site.data.keyword.iotinsurance_short}} ne déploie plus {{site.data.keyword.amafull}}, ni {{site.data.keyword.mobilepushfull}}. Les versions antérieures d'{{site.data.keyword.iotinsurance_short}} utilisaient le service {{site.data.keyword.amashort}} pour traiter les réponses provenant de l'application mobile. Ce processus continue de fonctionner pour toutes les instances existantes d'{{site.data.keyword.iotinsurance_short}}. Vous devez cependant créer un processus d'authentification personnalisé pour utiliser l'application mobile avec les nouvelles instances d'{{site.data.keyword.iotinsurance_short}}. Vous pouvez également, si vous le souhaitez, [créer une instance de {{site.data.keyword.mobilepushshort}}](https://console.ng.bluemix.net/docs/services/mobilepush/index.html), la configurer et la lier à l'API {{site.data.keyword.iotinsurance_short}}.

2. Vérifiez que le tableau de bord {{site.data.keyword.iotinsurance_short}} est opérationnel et que vous pouvez accéder aux API.
  1. Ouvrez le tableau de bord {{site.data.keyword.iotinsurance_short}} en cliquant sur **Ouvrir**. Acceptez les données d'identification préremplies en cliquant sur **Connexion**.
  2. Revenez à la console de service {{site.data.keyword.iotinsurance_short}} et consultez les API en cliquant sur **API**.

  **Remarque :** Après le déploiement, vous pouvez accéder directement au tableau de bord ou aux API en entrant leurs URL respectives dans votre navigateur. Lorsque vous utilisez cette méthode, vous devez entrer vos données d'identification pour le service {{site.data.keyword.iotinsurance_short}}. Pour trouver vos données d'identification, revenez à la console de service {{site.data.keyword.iotinsurance_short}}. Cliquez sur l'onglet **Données d'identification pour le service**, puis cliquez sur **Afficher les données d'identification**. Prenez note de l'ID utilisateur et du mot de passe.


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## Création et configuration de {{site.data.keyword.mobilepushshort}}
{: #config_push}

(facultatif) Pour activer les notifications push pour une application mobile existante, vous pouvez, si vous le souhaitez, créer une instance du service
{{site.data.keyword.mobilepushshort}}, la lier à l'API {{site.data.keyword.iotinsurance_short}} et ajouter un fichier PKCS (Public Key Cryptography Standards) 12. Pour des informations sur l'application mobile, voir [Installation et
connexion du modèle d'application mobile](iotinsurance_mobile_app.html). Pour plus d'informations sur {{site.data.keyword.mobilepushshort}}, voir [Initiation à Push Notifications](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

Pour configurer le service après sa création, procédez comme suit :

  1. Ouvrez le service {{site.data.keyword.mobilepushshort}}.
  2. Cliquez sur **Configurer**.
  3. Dans la section Certificat Apple Push Notification, téléchargez le fichier PKCS 12 pour votre application mobile et entrez le mot
de
passe.

## Utilisation des données de Weather Company
{: #weather_company}

(facultatif) {{site.data.keyword.iotinsurance_short}} fournit un ensemble de données statiques de Weather Company que vous pouvez afficher à des fins de démonstration. Vous pouvez
également accéder aux données de Weather Company en direct en créant une instance du service [{{site.data.keyword.weatherfull}} ](../Weather/index.html) et en
l'associant à l'application météo de {{site.data.keyword.iotinsurance_short}}.

**Important :** La version gratuite du service {{site.data.keyword.weather_short}} est limitée à 10.000 demandes. Vous pouvez effectuer une mise à niveau à
une version payante si vous avez besoin de plus de demandes.

Etape suivante ?
{: #whats_next}
Découvrez {{site.data.keyword.iotinsurance_short}}.

- Utilisez les instructions et les API contenues dans le kit d'outils de bouclier pour créer une [association entre un utilisateur et un bouclier](iotinsurance_shield_toolkit.html).
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- Téléchargez ou affichez tous les [exemples d'API sur le site de GitHub
![icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}.
