---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Nouveautés
{: #whatsnew}

Le plan **HSBN vNext bêta** repose sur une validation stable du codebase en open source de [Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window}. Hyperledger Fabric v1.0 implémente une architecture modulaire qui fournit une plateforme solide, sécurisée et personnalisable pour la génération de réseau blockchain d'entreprise.  
{: shortdesc}

Le service **HSBN vNext bêta** s'étend au-delà d'un simple environnement de bac à sable pour fournir un réseau de blockchain distribué avec des groupes de ressources s'étendant sur plusieurs organisations Bluemix. Pour plus d'informations sur l'architecture de réseau, consultez la rubrique [Présentation](v10_netoverview.html).

## Nouvelle architecture en version 1.0
{:why}

L'architecture d'Hyperledger Fabric a considérablement évoluée en version 1.0 pour offrir la puissance nécessaire aux réseaux
de niveau entreprise axés sur la sécurité, l'évolutivité, la confidentialité et les performances. Les homologues sont répartis dans
deux environnements d'exécution distincts : **avalisant** et **validant**, et la responsabilité en matière de commande de transaction
est représentée dans un composant distinct. Les questions relatives à la vie privée et à la confidentialité sont traitées via des canaux, lesquels
assurent la séparation des données. Des registres existent pour chaque canal, de sorte que les réseaux puissent être personnalisés pour
la prise en charge de différentes combinaisons de transactions bilatérales, multilatérales ou mêmes publiques.

Pour plus d'informations sur la topologie de réseau et l'interaction, consultez la section [Hyperledger architecture deep dive](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window}.

## Modifications supplémentaires

Le plan HSBN vNext bêta inclut également les modifications suivantes :
* Le [nouveau tableau de bord](v10_dashboard.html) permet aux abonnés de créer un réseau de
blockchain, d'inviter des membres, de rejoindre un autre réseau et de gérer des ressources et des actifs.
* La [nouvelle application en exemple de code blockchain Marbles pour la version 1.0](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} permet de tester le codebase le plus récent.
* Le nouveau [flux de transactions](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html) dans Hyperledger Fabric v1.0 garantit
la cohérence et l'intégrité des données par l'implémentation de plusieurs points de contrôle tout au long du traitement de transaction.
