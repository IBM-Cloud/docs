---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Présentation
{: #index}

Vous pouvez gérer les API de manière native dans {{site.data.keyword.Bluemix}}, qu'elles soient associées à une action {{site.data.keyword.openwhisk_short}} ou à une liste croissante de services {{site.data.keyword.Bluemix_notm}} intégrés, comme le service {{site.data.keyword.appconserviceshort}}. La gestion des API vous permet de contrôler l'utilisation, d'accroître l'adoption et d'assurer le suivi des statistiques. 

Comme indiqué dans le diagramme suivant, la gestion des API s'effectue grâce à l'insertion d'une passerelle légère et rapide devant des noeuds finaux du cloud existants. Cette passerelle, appelée Passerelle d'API dans le diagramme, est chargée de répondre aux appels API entrants provenant des applications. La passerelle d'API fournit un ensemble complet de règles d'API pour la sécurité, la gestion du trafic, la médiation, l'accélération et la prise en charge des protocoles autres que HTTP.

![Flux de la passerelle d'API](images/bluemix-native-apim-flow_ow.png "Flux de gestion des API")

Lorsque vous exposez une API, vous la mettez à disposition d'autres personnes pour qu'elles l'utilisent. Cela signifie souvent que vous accordez aux utilisateurs l'API un accès limité aux informations situées sur les serveurs que vous gérez. Cet accès offre une expérience client plus transparente pour l'utilisateur final car il peut accéder directement aux informations à partir de l'interface en cours. 

Il peur arriver que vous souhaitiez contrôler l'activité sur vos serveurs. Par exemple, en cas d'un nombre trop important de demandes API sur un serveur pendant une courte durée, le serveur peut connaître une surcharge et s'arrêter. Pour éviter de telles situations, vous pouvez gérer la fréquence des appels API grâce à la gestion d'API. La passerelle légère associée à l'API assure le suivi du nombre d'appels envoyés à votre API et applique des limites sur le nombre d'appels acceptés. La gestion d'API vous permet également de suivre le volume d'appels API provenant d'une source en particulier en enregistrant sa clé d'API. La clé d'API est une chaîne unique que l'équipe de développement de l'API fournit à l'équipe de consommation de l'API et qui permet au développeur de l'API de surveiller les statistiques liées aux appels générés par les demandes de l'équipe de consommation.   

Les fonctions suivantes sont disponibles la gestion d'API {{site.data.keyword.Bluemix_notm}} :
## Analyse des API
{: #basic_analytics notoc}

Si vous souhaitez monétiser l'utilisation de vos API, vous pouvez utiliser la fonction d'analyse afin d'effectuer le suivi de l'utilisation des appels. Vous avez également la possibilité de surveiller l'utilisation afin de comprendre comment vos API sont employées et prendre ainsi des décisions éclairées concernant la mise à jour de vos API dans le but d'augmenter leur adoption.

Vous pouvez visualiser les statistiques suivantes sur vos API : 
* le nombre de réponses et le temps de réponse moyen au cours de la dernière heure, ou de l'intervalle de temps que vous indiquez, 
* le nombre d'appels API par minute,
* les 100 dernières réponses.

## Limite par abonnement (clé d'API)
{: #rate_limit notoc}

Vous pouvez appliquer une limite de fréquence permettant de gérer le nombre d'appels que les applications peuvent effectuer auprès de vos API. Vous pouvez indiquer une limite de fréquence afin de n'autoriser qu'un nombre défini d'appels par seconde, par minute ou par heure afin d'éviter la surcharge de votre système de back-end. Cette limite peut être définie globalement pour les API, ou pour chaque clé d'API.

## OAuth
{: #oauth notoc}

Pour éviter toute utilisation non voulue des données que vous fournissez, veillez à ce que seuls les utilisateurs disposant de l'authentification correcte puissent accéder à vos API. Vous pouvez contrôler l'accès à vos API grâce à l'autorisation standard OAuth. OAuth est un protocole d'autorisation basé sur des jetons, qui permet à des sites Web ou des applications tiers d'accéder à des données sans que l'utilisateur doive partager des informations personnelles.

## CORS
{: #cors notoc}

CORS permet aux scripts imbriqués d'une page Web d'appeler l'API dans les limites du domaine. Cela profite à l'utilisateur de l'API car cette dernière peut extraire des informations provenant d'un autre domaine lorsqu'il est appelé par l'API. Si CORS n'est pas activé, l'extraction de contenu est limitée au même domaine que celui de la demande d'origine. Pour plus d'informations sur CORS et sur son implémentation, voir [HTTP access control (CORS) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS.html){: new_window}.

## Options supplémentaires de gestion d'API
{: #add_mgt_options notoc}

Ces fonctions de gestion d'API sont disponibles dans l'onglet API Management de votre tableau de bord {{site.data.keyword.openwhisk_short}} ou App Connect. Pour avoir accès à des solutions de gestion plus complexes, vous pouvez effectuer une mise à niveau vers le service complet {{site.data.keyword.apiconnect_full}} afin de bénéficier de fonctions supplémentaires, telles que l'analyse détaillée et les stratégies de conditionnement des API, ou à un portail de développeur qui permet de diffuser vos API sur les réseaux sociaux. Pour plus d'informations sur le service {{site.data.keyword.apiconnect_full}}, voir [Getting started with API Connect](https://console.ng.bluemix.net/docs/services/apiconnect/index.html){: new_window}.

Pour plus d'informations sur la mise à niveau des API que vous gérez dans {{site.data.keyword.Bluemix_notm}} vers le service {{site.data.keyword.apiconnect_short}}, voir [Accès à des fonctions de gestion d'API supplémentaires](upgrade.html).

