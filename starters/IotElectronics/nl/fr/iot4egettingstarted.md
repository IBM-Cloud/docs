---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# Création d'applications avec le module de démarrage {{site.data.keyword.iotelectronics}}

{{site.data.keyword.iotelectronics_full}} est une solution de bout en bout intégrée qui permet à vos applications de communiquer avec, de contrôler, d'analyser et de mettre à jour des appareils connectés. Le module de démarrage comprend une application de démarrage que vous pouvez utiliser pour créer des appareils simulés, ainsi qu'un modèle d'application mobile que vous pouvez utiliser pour contrôler ces appareils depuis votre périphérique mobile.
{:shortdesc}

## Avant de commencer

Avant de commencer, vous devez déployer une instance d'{{site.data.keyword.iotelectronics}} dans votre organisation {{site.data.keyword.Bluemix_notm}}. Cette opération entraîne le déploiement automatique des services et des applications de composant du module de démarrage.

 Vous [trouverez le module de démarrage {{site.data.keyword.iotelectronics}}](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}.

## Initiation à {{site.data.keyword.iotelectronics}}
Pour commencer, effectuez les tâches suivantes :

1. [Créez des appareils simulés](iot4ecreatingappliances.html) à l'aide de l'application Web de démarrage
{{site.data.keyword.iotelectronics}}. Comme exemple, des machines à laver sont utilisées en tant qu'appareils simulés dans le module de démarrage {{site.data.keyword.iotelectronics}}. Vous pouvez connecter comme appareil tout type de périphérique électronique intelligent.
2. (Facultatif) [Configurez des options de connexion mobiles avec {{site.data.keyword.appid_full}}](https://console.ng.bluemix.net/docs/services/appid/index.html). Vous pouvez personnaliser l'apparence de l'écran de connexion qui s'affiche dans l'application mobile. Vous pouvez également activer ou désactiver l'utilisation des données d'identification de login social. Par défaut, {{site.data.keyword.appid_short_notm}} active l'autorisation par Facebook et Google+, et les utilisateurs d'applications mobiles peuvent utiliser leurs propres données d'identification de login social ou ignorer le processus de connexion et essayer l'application sans se connecter. 
3. [Téléchargez et connectez](iotelectronics_config_mobile.html) le modèle d'application mobile.


## Etapes suivantes
Découvrez ce que vous pouvez faire avec {{site.data.keyword.iotelectronics}}.

- [Explorez l'application de démarrage](iot4ecreatingappliances.html) pour découvrir comment un fabricant peut surveiller les appareils qui sont connectés à {{site.data.keyword.iot_short_notm}}.
- [Explorez le modèle d'application mobile](iotelectronics_config_mobile.html) pour découvrir comment les propriétaires d'appareil peuvent enregistrer leurs appareils et interagir avec eux.
- [Explorez et gérez des données](iotelectronics_dashboard.html) pour vos appareils enregistrés dans {{site.data.keyword.iot_short_notm}}.
- [Explorez les API ![Icône de lien externe](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window} pour voir comment vous pouvez personnaliser et développer vos propres applications {{site.data.keyword.iotelectronics}}.
