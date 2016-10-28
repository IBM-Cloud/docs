---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Initiation à {{site.data.keyword.iotinsurance_short}}
(bêta)
{: #iotins_gettingstarted}
Dernière mise à jour : 16 septembre 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} est un service {{site.data.keyword.Bluemix_notm}} que vous pouvez utiliser pour collecter,
gérer et analyser des données provenant des assurés connectés. {{site.data.keyword.iotinsurance_short}} vous permet de proposer des évaluations
personnalisées des risques, une protection en temps réel et des réductions sur les coûts d'assurance.
{:shortdesc}

Pour que ce service soit opérationnel, vous devez déployer les services et les applications nécessaires, puis configurer les services.

**Configuration requise :** avant de commencer, assurez-vous de disposer des éléments requis suivants :
- Une instance du [service {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) doit exister dans votre espace {{site.data.keyword.Bluemix_notm}}.
- Au moins 2 Go de mémoire doivent être disponible dans votre organisation {{site.data.keyword.Bluemix_notm}} pour activer la fonction de déploiement.

## Déploiement des services et des applications nécessaires
{: #deploying_services}

1. Pour déployer tous les services et toutes les applications nécessaires, dans la [console {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), cliquez sur la vignette du service {{site.data.keyword.iotinsurance_short}}, puis sur **Déployer**.

  {{site.data.keyword.iotinsurance_short}} déploie tous les services et toutes les applications Node.js dont il a besoin. Il lie
automatiquement les applications aux services.

  Chaque instance de service utilise le plan de service par défaut. Vous pouvez mettre les plans de service à niveau ultérieurement dans la console
du service. Vous pouvez aussi utiliser une instance existante d'un service en supprimant la nouvelle instance et en liant manuellement l'instance existante
au service {{site.data.keyword.iotinsurance_short}}. Pour plus d'informations sur les applications, voir
[A propos d'{{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Vérifiez que tous les services et toutes les applications ont été créés et fonctionnent correctement. Dans votre console {{site.data.keyword.Bluemix_notm}}, vérifiez que toutes les applications possèdent le statut `En cours d'exécution`.

3. Vérifiez que le tableau de bord {{site.data.keyword.iotinsurance_short}} est opérationnel et que vous pouvez accéder aux API.
  1. Cliquez sur la vignette du service {{site.data.keyword.iotinsurance_short}}, puis sélectionnez l'onglet **Données d'identification pour le service**.
  2. Cliquez sur **Afficher les données d'identification** et prenez note de l'ID utilisateur et du mot de passe. Vous utiliserez ces données d'identification dans les étapes suivantes.
  3. Ouvrez le tableau de bord {{site.data.keyword.iotinsurance_short}} en sélectionnant l'onglet **Gérer** et en cliquant sur **Ouvrir**.
  4. Revenez à l'onglet **Gérer**. Affichez les API en cliquant sur **API**.

## Configuration des services
{: #iot4i_configservices}
Procédez comme suit pour configurer les services :

### Configuration de {{site.data.keyword.amashort}}
{: #config_ama}
1. Dans votre console {{site.data.keyword.Bluemix_notm}}, copiez l'URL de l'application d'API {{site.data.keyword.iotinsurance_short}}. Cliquez à l'aide du bouton droit de la souris sur la vignette de l'application d'API et sélectionnez l'option permettant de copier l'emplacement du lien.

2. Ouvrez le service {{site.data.keyword.amashort}}. Le service est disponible dans la section Services de votre console {{site.data.keyword.Bluemix_notm}}.

3. Dans la section **Personnalisé**, cliquez sur **Configurer**, puis entrez les données d'authentification suivantes :

  - **Nom de domaine** : `IoT4I`

  - **URL de fournisseur d'identité personnalisé** : collez l'URL de l'application d'API que vous avez copiée à la première étape. 

  - **Vos URI de redirection d'application Web** : ne renseignez pas cette zone.

### Configuration de {{site.data.keyword.mobilepushshort}}
{: #config_push}
Afin d'activer les notifications push pour une application mobile existante, vous devez configurer le service {{site.data.keyword.mobilepushshort}}
et ajouter un fichier Public
Key Cryptography Standards (PKCS) 12. Pour des informations sur l'application mobile, voir [Installation et
connexion du modèle d'application mobile](iotinsurance_mobile_app.html). Pour des informations sur {{site.data.keyword.mobilepushshort}}, voir
[Initiation à Push Notifications](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Ouvrez le service {{site.data.keyword.mobilepushshort}}.
  2. Cliquez sur l'option **Configurer Push**.
  3. Dans la section Certificat Apple Push Notification, téléchargez le fichier PKCS 12 pour votre application mobile et entrez le mot
de
passe.

Etape suivante ?
{: #whats_next}
Découvrez {{site.data.keyword.iotinsurance_short}}.

- Créez une [association entre un utilisateur et un bouclier](iotinsurance_create_users.html).
- Installez et connectez le [modèle d'application mobile](iotinsurance_mobile_app.html).
- Améliorez les performances avec des [services avancés](iotinsurance_advancedservices.html).
- Affichez les [API](https://iot4i-docs-api.mybluemix.net/dist/).

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}
* [Code du modèle d'application mobile dans Github](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Référence d'API
{: #api}
* [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs){:new_window}

## Liens connexes
{: #general}
* [Documentation {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Forum de
support des développeurs](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Forum de support stackoverflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
