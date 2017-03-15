---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Développement de passerelles sur {{site.data.keyword.iot_short_notm}}
{: #gw_dev_index}

Si vos terminaux ne peuvent pas se connecter directement à Internet, vous pouvez générer un terminal de passerelle pour extraire et envoyer des données aux applications de votre organisation {{site.data.keyword.iot_full}}. Des bibliothèques client, des exemples et des informations vous sont fournis afin de vous aider à connecter des passerelles de terminaux à votre organisation et à vos applications {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Protocoles de connexion
Les passerelles se connectent à {{site.data.keyword.iot_short_notm}} à l'aide du protocole de messagerie MQTT. La connexion de passerelles à {{site.data.keyword.iot_short_notm}} à l'aide de la messagerie HTTP n'est pas prise en charge. Seuls les terminaux peuvent se connecter en utilisant la messagerie HTTP.

## Bibliothèques client
Les bibliothèques client pour le développement de passerelles pouvant se connecter à {{site.data.keyword.iot_short_notm}} sont disponibles dans les langues suivantes :

|Bibliothèque client |Lien vers la bibliothèque et autre documentation
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp](https://github.com/ibm-watson-iot/iot-cpp)
|C#|[https://github.com/ibm-watson-iot/iot-csharp](https://github.com/ibm-watson-iot/iot-csharp)
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc](https://github.com/ibm-watson-iot/iot-embeddedc)
|Java™|[https://github.com/ibm-watson-iot/iot-java](https://github.com/ibm-watson-iot/iot-java)
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs)
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered](https://github.com/ibm-watson-iot/iot-nodered)
|Python|[https://github.com/ibm-watson-iot/iot-python

](https://github.com/ibm-watson-iot/iot-python)

Pour plus d'informations et pour accéder à des liens vers les bibliothèques client disponibles, voir aussi [Bibliothèques client pour le développement {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

## Edge Analytics
{: #eaa_community}

La fonction {{site.data.keyword.iot_short_notm}} Edge Analytics vous permet d'exécuter {{site.data.keyword.iot_short_notm}} Analytics sur un terminal de passerelle. Utilisez Edge Analytics pour amener Analytics à analyser les données collectées au bord du réseau et à répondre à ces analyses. Vous pouvez également envoyer des données de terminal à {{site.data.keyword.iot_short_notm}} en vue d'un traitement d'analyse supplémentaire, d'une visualisation dans le tableau de bord, en tant que données d'entrée pour d'autres analyses ou afin d'être stockées dans un référentiel historique basé sur le cloud. 

Vous pouvez télécharger le logiciel SDK Edge Analytics à partir de la [page de la communauté IBM Edge Analytics](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true). Le logiciel SDK inclut le fichier JAR SDK, le javadoc, l'exemple de code, les liens de recette et les fichiers ReadMe. Dans la communauté, vous pouvez également regarder des vidéos pour devenir opérationnel avec Edge Analytics, et vous pouvez utiliser le forum de communauté pour poser des questions. 
