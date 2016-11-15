---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Ce que vous devez savoir
{: #etn_overview}
Dernière mise à jour : 13 octobre 2016
{: .last-updated}

**ATTENTION :** Vous devez prendre connaissance des informations suivantes
avant d'utiliser IBM Blockchain dans le plan Bluemix :
Starter Developer (Beta) ou High Security Business Network (GA).
<br><br>

## Déclaration du support IBM

IBM est depuis longtemps chef de file en matière d'innovation,
et cela se poursuit avec les dernières offres IBM Blockchain. La
chaîne blocs (ou Blockchain) est une technologie qui connaît un
essor rapide et qui promet de perturber un certain nombre de
secteurs, de la finance à la logistique. Dans le cadre de
programmes d'adoption précoces, les clients et partenaires
commerciaux IBM influencent d'ores et déjà l'orientation future
de la chaîne de blocs. IBM Blockchain on Bluemix est l'un de ces
programmes. **Comme pour toute nouvelle
technologie, les utilisateurs d'IBM Blockchain
on Bluemix doivent se préparer à des changements rapides et
essentiels**.  
{:shortdesc}

L'architecture d'IBM Blockchain repose sur le projet
Hyperledger de Linux Foundation. Hyperledger Fabric est un projet en
open source en cours de développement, actuellement à l'état
*Incubation*. Chaque contribution de la communauté
open source renforce le projet Hyperledger Fabric, mais des défis
liés à l'adoption de cette technologie peuvent se poser. Au
cours du cycle *Incubation*, les clients peuvent
utiliser Hyperledger Fabric v0.5 pour des tests et des
simulations réseau,
mais **IBM met en garde contre l'application d'actifs
financiers de valeur directement sur un réseau de chaîne de
bloc Hyperledger Fabric
v0.5**.  
<br>

## Déclaration Open source

IBM Blockchain sur Bluemix (à la fois le plan Starter Developer
et le plan High Business Network) utilise le code open source
Hyperledger Fabric v0.5 de Linux Foundation. Les membres Hyperledger Project, dont IBM, contribuent au code pour la matrice, laquelle est ensuite vérifiée, validée et testée par la communauté. 
Hyperledger Fabric v0.5 est actuellement à l'état
*Incubation*. Les détails relatifs à l'état
*Incubation*, et à l'intégralité du cycle de vie
pour Hyperledger Project, sont disponibles à l'adresse
https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Déclaration du support du code blockchain

IBM Blockchain ne prend pas en charge le [code blockchain non déterministe](ibmblockchain_tutorials.html#ndcc), qui introduit un risque pour la cohérence et l'intégrité des données sur un réseau de blockchain. Avant de déployer du nouveau code blockchain sur votre réseau IBM Blockchain sur Bluemix, passez en revue les détails relatifs au [code blockchain non déterministe](ibmblockchain_tutorials.html#ndcc).

Outre le [code blockchain non déterministe](ibmblockchain_tutorials.html#ndcc), les pratiques en matière de codage suivantes ne sont PAS pris en charge sur les réseaux IBM Blockchain :

1. Utilisation de tableaux associatifs avec itération (l'ordre est aléatoire en Go).
2. Lecture d'une liste d'éléments d'une table KVS (l'ordre n'est pas garanti).
3. Ecriture de code blockchain dangereux (query et invoke peuvent être appelés en parallèle).
4. Substitution de mémoire globale ou de mémoire cache pour les variables d'état du grand livre dans le code blockchain.
5. Accès à des services externes, comme les bases de données, directement depuis le code blockchain.
6. Utilisation de bibliothèques ou de variables globales qui pourraient introduire du non déterminisme (utilisation de “random” ou "time", par exemple).
<br><br>

## Obtention d'aide

Pour obtenir du support et de l'aide sur votre réseau IBM Blockchain on Bluemix, voir [Obtention de support](ibmblockchain_support.html).
