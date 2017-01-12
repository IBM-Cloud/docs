---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à IBM {{site.data.keyword.blockchain}}
{: #gettingstartedtemplate}
Dernière mise à jour : 10 novembre 2016
{: .last-updated}

**ATTENTION :** Avant d'utiliser le plan développeur du module de démarrage (Starter Developer) (Beta) ou le Plan du réseau d'entreprise de haute sécurité (High Security Business Network) (GA), vous devez lire les informations techniques et de support dans [Ce que vous devez savoir](needtoknow.html).
<br><br>

## Statut des plans de l'offre

Le plan Starter Developer est une version bêta, et il fournit un environnement de développement à service partagé. 
Le plan High Security Business Network est une édition en
disponibilité générale. Le plan High Business Network fournit un environnement LinuxONE on z hautement sécurisé, à service exclusif, avec un isolement de code utilisant [IBM Secure Service Container](etn_ssc.html).
<br><br>

## IBM Blockchain on Bluemix

Avec le service {{site.data.keyword.blockchainfull}},
vous accédez d'un simple clic à deux réseaux de
blockchain de développement et de test composé de quatre noeuds. Au lieu de créer un tout nouveau réseau de blockchain, les développeurs peuvent immédiatement commencer à écrire des applications et à déployer du code blockchain. 
Le service IBM Blockchain sur Bluemix est un réseau privé d'égal à
égal, bâti à partir du code
[Hyperledger
Fabric v0.6.1](https://github.com/hyperledger/fabric/tree/v0.6) du projet Hyperledger de Linux Foundation.
{:shortdesc}

Les réseaux de blockchain sont utilisés pour permettre l'échange et le suivi à la fois sécurisé et efficace des actifs numériques, et enregistrer de manière définitive toutes les transactions dans le registre partagé. Pour plus de détails sur la chaîne de blocs, voir la rubrique [A propos de la chaîne de blocs](ibmblockchain_overview.html) .
<br><br>

## Choix de votre plan de réseau

Vous avez le choix entre deux plans IBM Blockchain sur Bluemix : **Starter Developer Network** ou **High Security Business Network**. Utilisez le tableau de comparaison ci-dessous pour choisir l'environnement adapté à votre profil.

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Plan Bluemix :      | Starter Developer Network       | High Security Business Network
| ------------------------- |:--------------------------:|:-----:|
| Statut :    | Bêta     | Disponibilité générale (GA) |
| Objectif :  |  Développement et test des niveaux de sécurité, performance et disponibilité |  Simulation d'un réseau d'entreprise, et test des niveaux de sécurité, performance et disponibilité |
| Noeuds :    | 4 noeuds + Autorité de certification     | 4 noeuds + Autorité de certification |
| [Moniteur du Tableau de bord :](ibmblockchainmonitor.html) | Oui | Oui |
| Transactions confidentielles : | Oui | Oui |
| [Consensus :](etn_pbft.html) | PBFT | PBFT |
| Environnement :     | partagé et à service partagé | Isolé et à service exclusif |
| [IBM Secure Service Container :](etn_ssc.html) | Non | Oui |

<br>
## Lancement de votre plan de réseau

Procédez comme suit pour créer et déployer une instance de
service non lié de réseau de blockchain.  Votre réseau inclut un environnement de développement avec des noeuds de validation et un observation technique. Il vous permet également de déployer du code blockchain, d'afficher des journaux et de générer des applications :

1. Depuis la page [{{site.data.keyword.blockchain}} Service ](https://console.ng.bluemix.net/catalog/services/blockchain/), remplissez le formulaire **Add Service** dans le volet de droite :
  - **Space:** Sélectionnez **dev**.
  - **App:** Sélectionnez **Leave unbound**, ou pour lier votre service à l'une de vos applications Bluemix.org, **Select an application**.
  - **Service name:** Entrez un nom ou une valeur unique, par exemple **Blockchain Test Net123**.
  - **Credential name:** Conservez la valeur par défaut.
  - **Selected Plan:** Choisissez **Starter Developer** ou **High Security**.
  - Cliquez sur le bouton **CREATE**.
2.  Vous êtes maintenant à l'écran **Service Dashboard** de vote nouveau service. Depuis cet écran, vous pouvez **gérer** votre instance du réseau. Cliquez sur **LAUNCH** pour utiliser votre moniteur de chaîne de blocks.
3.  Le moniteur de chaîne de blocs affiche les détails du réseau, les journaux en temps réel, l'état actuel du registre, les API et les modèles de code blockchain. Utilisez ce tableau de bord pour exécuter les fonctions suivantes :
  - Accédez à la Reconnaissance et aux routes d'API pour les homologues du réseau.
  - Affichez les conteneurs de code blockchain en cours d'exécution.
  - Affichez les journaux en temps réel et le code blockchain de dépannage.
  - Affichez l'état global du registre.
  - Accéder à l'interface utilisateur swagger et interagissez avec votre réseau via l'API REST.
  - Déployez l'un des trois exemples de code blockchain.


# Liens connexes
{: #rellinks}
## Tutoriels et exemples
{: #samples}
* [Démo IBM Marbles (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Car Lease Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Art Auction Demo (Github)](https://github.com/ITPeople-Blockchain/auction)

## Informations de référence sur l'API
{: #api}
* [Interface utilisateur swagger](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [API de matrice Hyperledger (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* 
[Logiciel
SDK HFC pour Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Liens connexes
{: #general}
* [Code matrice](https://github.com/hyperledger/fabric)
* [Livre blanc](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Spécifications de protocole et doc associée](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [Dépassement de la capacité de pile](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Nouveautés dans les services Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
