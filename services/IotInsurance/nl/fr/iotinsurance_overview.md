---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# A propos d'{{site.data.keyword.iotinsurance_short}}
{: #about}

{{site.data.keyword.iotinsurance_full}} est une instance de production IoT intégrée qui collecte et analyse des données provenant d'assurés
dans leur contexte afin de proposer des évaluations personnalisées des risques, une protection en temps réel et des réductions sur les coûts d'assurance.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} fournit une vue d'ensemble des actifs et de la situation d'un assuré, y compris des informations sur
la localisation, la météo, le trafic ou le bien-être général. Une analyse approfondie de ces informations permet aux assureurs de proposer une évaluation personnalisée des risques et une protection en temps réel à leurs assurés. L'assuré bénéficie ainsi de la possibilité d'éviter les risques en étant prévenu à l'avance et de conseils personnalisés, et la mise en place et le
traitement
de ses demandes d'indemnisations sont rationalisés. L'assureur,
quant à lui, peut veiller à la satisfaction du client et le fidéliser, ainsi que réduire ses coûts en évitant les demandes d'indemnisation et en
automatisant le traitement.

## Architecture
{: #architecture}

![Architecture {{site.data.keyword.iotinsurance_short}}. Ce
diagramme est décrit dans le corps principal de la rubrique.](images/IoT4I_architecture.svg "Architecture {{site.data.keyword.iotinsurance_short}}")

Les composants {{site.data.keyword.iotinsurance_short}} fonctionnent ensemble comme décrit dans la présente section. Cette organisation est également illustrée dans le diagramme d'architecture. Le tableau de bord {{site.data.keyword.iotinsurance_short}} affiche les données stockées dans {{site.data.keyword.iot_short_notm}} et dans la base de données {{site.data.keyword.cloudantfull}}. Les terminaux intelligents de l'utilisateur peuvent être connectés via le cloud ou directement à {{site.data.keyword.iot_short_notm}}. S'ils sont connectés via le cloud, ils envoient des données au transformateur, lequel traite ces dernières et les envoie à {{site.data.keyword.iot_short_notm}}. Les données de {{site.data.keyword.weatherfull}} peuvent également être extraites dans le transformateur de données Weather Company d'{{site.data.keyword.iotinsurance_short}}, puis dans {{site.data.keyword.iot_short_notm}}. Les données sont traitées par le moteur de bouclier, qui génère un événement de bouclier et l'envoie au moteur des actions via des API. Le moteur des actions peut éventuellement utiliser {{site.data.keyword.mobilepushfull}} pour envoyer des notifications à l'application mobile de l'utilisateur. L'utilisateur peut également se servir de l'application mobile pour répondre aux alertes ou aux offres.

**Remarque** : Les versions antérieures d'{{site.data.keyword.iotinsurance_short}} utilisaient le service {{site.data.keyword.amafull}} pour traiter les réponses et les renvoyer via les API à {{site.data.keyword.iot_short_notm}}, puis au tableau de bord {{site.data.keyword.iotinsurance_short}}. Ce processus continue de fonctionner pour les instances des versions antérieures d'{{site.data.keyword.iotinsurance_short}}. Toutefois, les nouvelles instances d'{{site.data.keyword.iotinsurance_short}} n'incluent pas {{site.data.keyword.amashort}}, ni {{site.data.keyword.mobilepushshort}}. Pour utiliser l'application mobile, vous devez créer un processus d'authentification personnalisé. Vous pouvez également, si vous le souhaitez, créer et lier une [instance {{site.data.keyword.mobilepushshort}}](../mobilepush/index.html) à l'API afin d'activer les notifications push.

## Tableau de bord des assurances
{: #insurance_dashboard}
Le tableau de bord des assurances propose aux utilisateurs des compagnies d'assurance, comme les agents, une vue complète de la situation des actifs
assurés de leurs
clients. Ces utilisateurs peuvent afficher les boucliers et les événements pour un pays, un état ou un compte.

L'exemple de tableau de bord des assurances est chargé avec des données simulées afin de montrer le type d'informations que vous pouvez collecter et
analyser.

## Modèle d'application mobile
{: #mobileapp}
C'est dans le modèle d'application mobile que les titulaires de contrat d'assurance, comme les propriétaires, affichent les informations
qu'{{site.data.keyword.iotinsurance_short}} envoie depuis les capteurs situés chez eux et y répondent.

A l'aide d'un terminal mobile, les propriétaires autorisent le service à se connecter au cloud du fournisseur de capteurs pour l'envoi et la
réception de données. Par exemple, un propriétaire peut recevoir une notification dans l'application de démarrage mobile si le capteur détecte une
fuite d'eau. Pour plus d'informations, voir [Installation et connexion du modèle d'application mobile](iotinsurance_mobile_app.html).

## API REST et en temps réel
{: #rest_api}
Les API REST sont utilisées par l'application de démarrage mobile, le tableau de bord des assurances, le moteur de bouclier et le contrôleur de risques. Elles
permettent aux utilisateurs de prendre connaissance des associations qui existent entre les terminaux, les boucliers et les actions. A l'aide des API, les programmeurs peuvent créer des utilisateurs, générer des données d'événement, créer et enregistrer de nouveaux boucliers, et extraire des
données d'événement.

L'API à laquelle vous accédez depuis la console du service est personnalisée pour votre instance d'{{site.data.keyword.iotinsurance_short}}.

Sur la page de l'API, vous pouvez  
  - Afficher tous les appels API disponibles ainsi que la documentation associée.
  - Tester des appels API individuels.  Sélectionnez un appel API afin d'afficher toutes les informations, puis cliquez sur **Essayez !**.

Les exemples d'API permettent de vous initier avec des scénarios courants. Pour plus d'informations, voir [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).


## Transformer
{: #transformer}
Le composant Transformer demande de nouvelles informations à l'API du serveur Cloud et les transforme pour qu'elles correspondent aux données
figurant dans
{{site.data.keyword.iotinsurance_short}}. Ensuite,
ces données sont publiées pour que le reste de l'implémentation d'{{site.data.keyword.iotinsurance_short}} puisse les utiliser. Les utilisateurs doivent autoriser le composant Transformer à accéder aux données du cloud de capteurs et à traiter les données enregistrées. {{site.data.keyword.iotinsurance_short}} prend en charge plusieurs fournisseurs de cloud et terminaux. Pour connaître la liste complète des fournisseurs de cloud pris en charge et les instructions de connexion à {{site.data.keyword.iotinsurance_short}}, voir [Terminaux et fournisseurs pris en charge](iotinsurance_supporteddevices.html).

## Transformateur de données Weather Company
{: #wcdtransformer}
L'application Weather Company injecte des données météorologiques pertinentes issues du service de données Weather Company dans le flux de données IoT4I. Ces données peuvent ensuite servir à construire des boucliers activés pour la météo.

**Remarque** : Le transformateur de données Weather Company est pris en charge en tant que démonstration de faisabilité ou aperçu technique uniquement et n'est pas destiné à une utilisation en production.

## Moteur de bouclier
{: #shield_engine}
A partir des informations stockées dans un événement, le moteur de bouclier détermine si un risque, par exemple une fuite d'eau, existe. Si un risque est
identifié, il est transmis au moteur des actions.

Un bouclier est une protection spécifique qu'un client acquiert auprès d'un assureur. Par exemple, un propriétaire souscrit une assurance habitat pour
protéger son logement en cas d'incendie, de dégât des eaux, de vol et d'autres risques. La solution {{site.data.keyword.iotinsurance_short}} fournit
un bouclier intégré en cas de dégât des eaux. Les clients sont prévenus et peuvent répondre lorsqu'un événement impliquant l'eau menace leur
logement. A l'aide de l'API REST, les développeurs peuvent ajouter davantage de boucliers.  

Ceux-ci s'exécutent dans le moteur d'analyse
d'{{site.data.keyword.iotinsurance_short}}. Le moteur d'analyse identifie le type de risque (par exemple, *Eau détectée*), le compte
utilisateur du capteur qui a signalé le risque, et les boucliers qui sont associés au compte. Une action peut être effectuée en fonction de ces
informations. Vous pouvez utiliser ou modifier les boucliers inclus dans la bibliothèque de boucliers {{site.data.keyword.iotinsurance_short}}, ou vous pouvez créer et implémenter vos propres boucliers. Pour plus d'informations sur les boucliers et la [bibliothèque de boucliers {{site.data.keyword.iotinsurance_short}} ![Icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}, voir [Kit d'outils de bouclier](iotinsurance_shield_toolkit.html).

## Moteur des actions
{: #action_engine}
Le moteur des actions détermine les actions à exécuter à partir des informations spécifiées dans le bouclier.

Vous pouvez créer des boucliers dans JavaScript à l'aide de l'API {{site.data.keyword.iotinsurance_short}}.



# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}
* [Code du modèle d'application mobile dans GitHub![Icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Référence d'API
{: #api}
* [API {{site.data.keyword.iotinsurance_short}} ![Icône de lien externe](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemples d'API {{site.data.keyword.iotinsurance_short}} ![Icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Liens connexes
{: #general}
* [Documentation d'{{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Forum de support des développeurs ![Icône de lien externe](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix]){:new_window}
* [Forum de support Stack Overflow ![Icône de lien externe](../../icons/launch-glyph.svg)](http://stackoverflow.com/questions/tagged/ibm-bluemix){:new_window}
