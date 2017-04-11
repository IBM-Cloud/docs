---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualisation des données de terminal
{: #visualizingdata_data}

Cet exemple vous aide à visualiser les données historiques et en temps réel issues de terminaux enregistrés dans votre organisation {{site.data.keyword.iot_full}}.
{:shortdesc}

## Avant de commencer
{: #byb}

Avant de pouvoir visualiser vos données, vous devez exécuter les actions suivantes :

- Enregistrez vos terminaux sur votre organisation {{site.data.keyword.iot_short_notm}}.
- Assurez-vous que vos terminaux envoient des événements à {{site.data.keyword.iot_short_notm}}.
- [Téléchargez l'exemple de visualisation](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip) depuis le référentiel github et procédez à l'extraction du fichier .zip.
- [Installez l'outil de ligne de commande cf](../../starters/install_cli.html) à partir de {{site.data.keyword.Bluemix_notm}}.

## Exécution de l'exemple dans {{site.data.keyword.Bluemix_notm}}
{: #running_sample}

1. Créez une application dans {{site.data.keyword.Bluemix_notm}} à l'aide du logiciel SDK Node.js. Notez le nom de l'application et le nom d'hôte de l'application ; ces informations sont requises pour télécharger l'application sur {{site.data.keyword.Bluemix_notm}}.
2. Liez votre application node.JS à votre instance {{site.data.keyword.iot_short_notm}} dans votre tableau de bord {{site.data.keyword.Bluemix_notm}} en procédant comme suit :

  a. Dans votre tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'application Node.JS que vous avez créée.

  b. Cliquez sur **Lier un service ou une API**, puis sélectionnez votre service {{site.data.keyword.iot_short_notm}}, puis cliquez sur**Ajouter**.
3. A l'aide de l'outil de ligne de commande cf, passez dans le répertoire contenant l'exemple de package de visualisation extrait et exécutez la commande suivante pour vous connecter à {{site.data.keyword.Bluemix_notm}}.
```
cf api https://api.ng.bluemix.net
```
4. Ensuite, connectez-vous à {{site.data.keyword.Bluemix_notm}} à l'aide des informations suivantes :
```
cf login -u <your_bluemix_login_id>
```
Si vous n'utilisez pas l'organisation et l'espace par défaut, vous pouvez utiliser les informations suivantes :
```
cf target-o <your_bluemix_org> -s dev
```

5. Editez le fichier `manifest.yml` et mettez à jour les noms d'hôte et d'application à l'aide du format suivant :
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. Déployez votre exemple de visualisation à l'aide de la commande suivante :
```
cf push <your_application_name>
```
7. Dans votre navigateur, entrez l'URL suivante :
```
http://<your_application_name>.mybluemix.net
```

Tous les terminaux de votre organisation sont répertoriés dans le menu déroulant des terminaux. Lorsqu'un terminal est sélectionné, vous devriez accéder à la visualisation en temps réel des données que ce terminal envoie à votre service {{site.data.keyword.iot_short_notm}}. Pour voir les données historiques, cliquez sur le bouton **Données d'historique**.

## Personnalisation de l'exemple
{: #customize_sample}

Cet exemple d'application est une application Web autonome écrite sur l'infrastructure node.js. L'exemple visualise les événements qui sont envoyés par des terminaux enregistrés dans votre {{site.data.keyword.iot_short_notm}}. L'exemple utilise les outils suivants :

- Express : Infrastructure d'application Web Node.js
- JQuery : Appels d'interface utilisateur et Ajax
- Rickshaw : Outil de visualisation de graphiques
- Paho : Client MQTT

L'exemple d'application est structuré avec les répertoires suivants :

- Public
- CSS : Feuilles de style en cascade
- Images
- JS : Principaux fichiers de logique JavaScript
- Historian : code pour la visualisation des données historiques
- Realtime : code pour la visualisation des données en temps réel
- Uicontroller.js : code pour le contrôle de l'interface utilisateur
- Routes : Routage de la logique et de l'application Web
- Utils : Fonctions de programme utilitaire utilisée pour passer des appels HTTP
- Views : Fichiers d'interface utilisateur écrits en langage Jade
- -La bibliothèque de création de graphiques Rickshaw est utilisée afin de tracer le graphique des données historiques et en temps réel.

## Personnalisation de l'affichage des données en temps réel
{: #customize_real_time_display}

Le répertoire contenant le code de visualisation graphique pour les données en temps réel est `public/ja/realtime`. La logique de création de graphiques peut être personnalisée en éditant `public/js/historian/realtimeGraph.js`.

Le fichier qui fait référence à la bibliothèque MQTT Paho pour l'abonnement à des sujets et la réception d'événements de terminal depuis {{site.data.keyword.iot_short_notm}} figure dans `public/js/historian/realtime.js`.

Les événements de terminal sont transmis au fichier `realtimeGraph.js` pour tracer le graphique.

## Personnalisation de l'affichage des données historiques
{: #customize_historical_display}

Le répertoire contenant le code de visualisation graphique pour les données historiques des terminaux est `public/js/historian`. La logique de création de graphiques peut être personnalisée en éditant `public/js/historian/historianGraph.js`.

Le fichier qui contrôle les appels d'API REST pour la collecte des données historiques des terminaux est `public/js/historian/historian.js`.

Les données historiques sont transmises au fichier `historianGraph.js` pour tracer le graphique.

Un guide de développement plus détaillé est disponible sur le wiki Github iot-visualization.
