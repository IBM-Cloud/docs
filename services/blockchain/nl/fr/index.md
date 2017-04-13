---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation
{: #gettingstartedtemplate}

**ATTENTION :** Avant d'utiliser un plan IBM Blockchain sur Bluemix, vous devez lire les informations techniques de la [clause de protection](needtoknow.html).
{:shortdesc}

## IBM Blockchain sur Bluemix

Le service {{site.data.keyword.blockchainfull}} on Bluemix&reg; comporte trois plans de réseau de blockchain. Le dernier plan, **High Security Business Network (HSBN) vNext bêta**, repose sur le codebase Hyperledger Fabric v1.0 et exploite une architecture modulaire pour offrir de nouvelles fonctionnalités. Les plans IBM Blockchain on Bluemix permettent aux développeurs d'écrire et de tester immédiatement les applications de code blockchain, sans qu'il soit nécessaire de concevoir et de configurer un réseau de blockchain privé. Le code blockchain est le moteur sous-jacent à l'échange sécurisé et efficace d'actifs sur les réseaux de code blockchain Fabric, et l'enregistrement permanent de ces transactions dans le registre.

## Plans de l'offre

Les nouveaux abonnés IBM Blockchain on Bluemix peuvent désormais s'inscrire au plan **HSBN vNext bêta**. Cette offre toute récente repose sur Hyperledger Fabric v1.0, qui garantit une sécurité de nouvelle génération, intégrité, évolutivité et performances. Le tableau 1 décrit les plans Bluemix :

Table 1: Plans IBM Blockchain on Bluemix  

| Plan Bluemix      | Statut       | Disponible pour les nouveaux membres  | Version Hyperledger Fabric
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext bêta** (1)   | Bêta     | Oui |  v1.0 |
| HSBN (2) |  Disponibilité générale (GA) |  Oui |  v0.6 |
| Starter Developer (3)    | Bêta     | Oui | v0.6 |

(1) Le plan **High Security Business Network (HSBN) vNext bêta** fournit une méthode facile pour l'accès aux organisations Bluemix et la génération d'un réseau de blockchain distribué.  
(2) Le plan **High Security Business Network (HSBN) GA** fournit un environnement LinuxONE on z Systems hautement sécurisé, à service exclusif, avec un isolement de code utilisant [IBM Secure Service Container](etn_ssc.html).  
(3) Le plan Starter Developer bêta fournit une environnement de développement uniquement à service partagé.   

## Détails des plans de l'offre

Le tableau 2 fournit une comparaison détaillée des plans de l'offre IBM Blockchain on Bluemix. Les nouveaux abonnés IBM Blockchain on Bluemix doivent choisir le plan **HSBN vNext bêta**. Les plans HSBN et Starter Developer sont fermés aux nouveaux abonnés mais ils sont toujours pris en charge par IBM :

Tableau 2 : Détails des plans IBM Blockchain on Bluemix  

| Plan Bluemix :      | Starter Developer Network       | High Security Business Network       | High Security Business Network (HSBN) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| Statut :    | Bêta     | Disponibilité générale (GA) | Bêta |
| Objectif :  |  Développement et test des niveaux de sécurité, performance et disponibilité |  Simulation d'un réseau d'entreprise, et test des niveaux de sécurité, performance et disponibilité |  Configuration d'un réseau métier d'entreprise avec une sécurité, des performances et une disponibilité de niveau production |
| Noeuds :    | 4 homologues + autorité de certification     | 4 homologues + autorité de certification | Gestion dynamique de composants réseau |
| Moniteur du Tableau de bord : | [Oui](ibmblockchainmonitor.html) | [Oui](ibmblockchainmonitor.html) | [Oui](v10_dashboard.html) |
| Environnement :     | partagé et à service partagé | Isolé et à service exclusif | Plusieurs niveaux d'isolement |

# Liens connexes
{: #rellinks}
## Tutoriels et exemples
{: #samples}
* [Démo IBM Marbles (GitHub)](https://github.com/IBM-Blockchain/marbles) - v0.6 & v1.0
* [Démo IBM Commercial Paper (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - v0.6
* [Démo IBM Car Lease (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - v0.6
* [Démo Art Auction (Github)](https://github.com/ITPeople-Blockchain/auction) v0.6 - v1.0 (exécution en local)

## Informations de référence sur l'API
{: #api}
* [API Hyperledger Fabric (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [Logiciel SDK HFC pour Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Liens connexes
{: #general}
* [Code Fabric](https://github.com/hyperledger/fabric)
* [Composeur Fabric](https://fabric-composer.github.io/)
* [Docs Fabric v1.0](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Docs Fabric v0.6](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [Dépassement de la capacité de pile](http://stackoverflow.com/questions/tagged/hyperledger)
* [Nouveautés dans les services Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
