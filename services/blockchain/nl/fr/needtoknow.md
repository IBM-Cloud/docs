---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Clause de protection
{: #etn_overview}

**ATTENTION :** Vous devez prendre connaissance des informations suivantes avant d'utiliser un plan IBM Blockchain on Bluemix.

## Déclaration du support IBM

IBM est depuis longtemps chef de file en matière d'innovation, et cela se poursuit avec les offres du plan IBM Blockchain on Bluemix. La chaîne de blocs (ou Blockchain) est une technologie qui connaît un essor rapide et qui promet de perturber un certain nombre de secteurs, de la finance à la logistique en passant par la chaîne d'approvisionnement. Dans le cadre de programmes d'adoption précoces, les clients et partenaires commerciaux IBM étudient la blockchain en tant que solution industrielle. IBM Blockchain on Bluemix est l'un de ces
programmes. **Comme pour toute nouvelle technologie, les utilisateurs d'IBM Blockchain on Bluemix doivent se préparer à des changements rapides et essentiels**.  
{:shortdesc}

L'architecture d'IBM Blockchain repose sur le projet Hyperledger Fabric de Linux Foundation. Hyperledger Fabric est actuellement à l'état *Actif* et connaît un développement continu. Chaque contribution de la communauté open source renforce le projet Hyperledger Fabric, mais des défis liés à l'adoption de cette technologie peuvent se poser. Pendant le cycle *Actif* du projet, les clients peuvent utiliser Hyperledger Fabric v1.0 à des fins de tests et de simulation réseau. **IBM met en garde contre toute définition ou échange d'actifs financiers, ou tout actif de valeur, directement sur un réseau de blockchain Hyperledger Fabric**.  

## Déclaration Open source

Le plan **High Security Business Network (HSBN) vNext bêta** repose sur le code open source Hyperledger Fabric v1.0 de Linux Foundation. Les plans Starter Developer and High Security Business Network (HSBN) reposent sur le code Hyperledger Fabric v0.6. Les membres du projet Hyperledger, y compris IBM, continuent à contribuer au code source, après quoi il est passé en revue, certifié et testé par la communauté. Hyperledger Fabric v1.0 est actuellement à l'état *Actif* ; pour plus de détails sur l'état *Actif*, et sur le cycle de vie du projet Hyperledger, consultez le site https://wiki.hyperledger.org/community/project-lifecycle.  

## Déclaration du support du code blockchain

Les pratiques en matière de codage suivantes ne sont PAS prises en charge sur les réseaux IBM Blockchain :

1. Utilisation de tableaux associatifs avec itération (l'ordre est aléatoire en Go).
2. Lecture d'une liste d'éléments d'une table KVS (l'ordre n'est pas garanti).
3. Ecriture de code blockchain dangereux (query et invoke peuvent être appelés en parallèle).
4. Substitution de mémoire globale ou de mémoire cache pour les variables d'état du registre dans le code blockchain.
5. Accès à des services externes, comme les bases de données, directement depuis le code blockchain.
6. Utilisation de bibliothèques ou de variables globales qui
pourraient introduire du non déterminisme (utilisation de "random" ou
"time", par exemple).
7. Itération à l'aide de GetRows.  

En outre, les plans HSBN et Starter (Hyperledger Fabric v0.6) ne prennent pas en charge le code blockchain non déterministe, qui introduit un risque pour la cohérence et l'intégrité des données ; pour plus de détails, voir la section [Code blockchain non déterministe](nondeterministic.html).
