---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}

{{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} fournit un kit d'outils polyvalent comportant des terminaux de passerelle, la gestion des terminaux et un accès puissant aux applications. {{site.data.keyword.iot_short_notm}} vous permet de collecter des données relatives à des terminaux connectés et d'effectuer des analyses sur des données temps réel à partir de votre organisation.
{:shortdesc}

## Avant de commencer
{: #byb}

Avant de connecter des terminaux et d'utiliser des données, inscrivez-vous à un compte {{site.data.keyword.Bluemix_notm}} et créez une instance du service {{site.data.keyword.iot_short_notm}} dans votre organisation {{site.data.keyword.Bluemix_notm}}. Vous pouvez créer une instance {{site.data.keyword.iot_short_notm}} directement depuis la page [{{site.data.keyword.iot_short_notm}} dans le catalogue de services Bluemix ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/internet-of-things-platform/){:new_window}.  

Pour obtenir des informations détaillées sur l'inscription à un compte {{site.data.keyword.Bluemix_notm}}, la configuration de régions et d'autres paramètres de gestion de compte, voir [Gestion de votre compte Bluemix](https://console.ng.bluemix.net/docs/admin/account.html#signup).

Vous pouvez définir et configurer votre instance {{site.data.keyword.iot_short_notm}} à partir du tableau de bord. Pour ouvrir le tableau de bord, accédez à votre instance de service {{site.data.keyword.iot_short_notm}} dans {{site.data.keyword.Bluemix_notm}}, puis cliquez sur **Lancer le tableau de bord**.

## Etape 1 : Connecter vos terminaux
{: #up_and_running}

Pour être rapidement opérationnel avec le service, examinez les options suivantes selon votre situation :

   |   Le service est déployé | Le service n'est pas déployé
  ------------- | -------------
  **J'ai un terminal à connecter** | [Connectez votre terminal à {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task).| Explorez la connexion de terminal dans la [démonstration Play organization ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **Je n'ai aucun terminal à connecter** | [Créer et connecter un simulateur de terminal Node-RED](nodereddevice_sample.html){:new_window} | Commencez à utiliser [Watson IoT Platform Starter](https://console.ng.bluemix.net/docs/starters/IoT/iot500.html).
Pour plus d'informations sur la connexion de types de terminal spécifiques à {{site.data.keyword.iot_short_notm}}, voir les [recettes developerWorks ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}.  

Pour la documentation du développeur de connexion de terminal, voir :
- [Connectivité MQTT pour les terminaux](devices/mqtt.html)
- [Connectivité MQTT pour les passerelles](gateways/mqtt.html)

## Etape 2 : Analyser vos données de terminal
{: #analyzing_data}

Commencez par explorer les données en temps réel envoyées par les terminaux à {{site.data.keyword.iot_short_notm}}.

{{site.data.keyword.iot_short_notm}} inclut les outils d'analyse suivants :  
- [Tableaux et cartes](data_visualization.html) pour visualiser vos données de terminal en temps réel
- [Règles et actions](analytics.html) déclenchées par les données de terminal en temps réel

Pour un exemple montrant comment démarrer rapidement, voir la recette developerWorks [Using Rules and Actions with IBM Watson IoT Platform Cloud Analytics ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window}. 

## Etape 3 : Créer des applications destinées à consommer vos données de terminal
{: #develop_applications}

Etendez les fonctions d'analyse de données de {{site.data.keyword.iot_short_notm}} en créant et en connectant vos propres applications afin qu'elles consomment des données de terminal historiques et en temps réel.

Pour plus d'informations, voir les rubriques suivantes :   
- Explorez la [documentation de développeur d'applications](applications/api.html) et la [{{site.data.keyword.iot_short_notm}}documentation d'API](reference/api.html).
- Explorez les [bibliothèques client {{site.data.keyword.iot_short_notm}} ](iot_platform_client_lib.html) qui fournissent des outils et des fichiers pour générer et développer du code afin d'intégrer et de connecter vos terminaux et vos applications.
- [Connectez un service {{site.data.keyword.cloudantfull}} ](cloudant_connector.html) à votre {{site.data.keyword.iot_short_notm}} pour stocker les données de terminal historiques.




# Liens connexes
{: #rellinks}
* [IBM Watson IoT Service Health Dashboard](https://status.internetofthings.ibmcloud.com){:new_window}

## Tutoriels et exemples
{: #samples}
* [Recettes relatives à la connexion de vos terminaux ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}
* [{{site.data.keyword.iot_short_notm}} Play organization ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM® mbed™ IoT Starter Kit ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## Informations de référence sur l'API
{: #api}
* [Documentation de l'API {{site.data.keyword.iot_short_notm}}](../reference/api.html)
* [Documentation de développeur](developer_doc_overview.html)
