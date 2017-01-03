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
Dernière mise à jour : 10 novembre 2016
{: .last-updated}

**ATTENTION :** Vous devez prendre connaissance des informations suivantes avant d'utiliser IBM Blockchain dans le plan Bluemix : Starter Developer (Beta) ou High Security Business Network (GA).
<br><br>

## Déclaration du support IBM

IBM est depuis longtemps chef de file en matière d'innovation, et cela se poursuit avec les dernières offres IBM Blockchain. La chaîne blocs (ou Blockchain) est une technologie qui connaît un essor rapide et qui promet de perturber un certain nombre de secteurs, de la finance à la logistique. Dans le cadre de programmes d'adoption précoces, les clients et partenaires commerciaux IBM influencent d'ores et déjà l'orientation future de la chaîne de blocs. IBM Blockchain on Bluemix est l'un de ces
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
liés à l'adoption de cette technologie peuvent se poser. Au cours du
cycle *Incubation*, les clients peuvent utiliser
Hyperledger Fabric v0.6 pour des tests et des simulations réseau,
mais **IBM met en garde contre l'application d'actifs
financiers de valeur directement sur un réseau de chaîne de bloc
Hyperledger Fabric v0.6**.  
<br>

## Déclaration Open source

IBM Blockchain sur Bluemix (à la fois le plan Starter Developer
et le plan High Business Network) utilise le code open source
Hyperledger Fabric v0.6.1 de Linux Foundation. Les membres Hyperledger Project, dont IBM, contribuent au code pour la matrice, laquelle est ensuite vérifiée, validée et testée par la communauté. 
Hyperledger Fabric v0.6.1 est actuellement à l'état
*Incubation*. Les détails relatifs à l'état
*Incubation*, et à l'intégralité du cycle de vie pour
Hyperledger Project, sont disponibles à l'adresse
https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Déclaration du support du code blockchain

IBM Blockchain ne prend pas en charge le code blockchain non
déterministe, qui introduit un risque pour la cohérence et
l'intégrité des données sur un réseau de blockchain. Avant de déployer du nouveau code blockchain sur votre réseau IBM Blockchain sur Bluemix, passez en revue les détails relatifs au [code blockchain non déterministe](nondeterministic.html).

Outre le [code blockchain non déterministe](nondeterministic.html), les pratiques en matière de codage suivantes ne sont PAS pris en charge sur les réseaux IBM Blockchain :

1. Utilisation de tableaux associatifs avec itération (l'ordre est aléatoire en Go).
2. Lecture d'une liste d'éléments d'une table KVS (l'ordre n'est pas garanti).
3. Ecriture de code blockchain dangereux (query et invoke peuvent être appelés en parallèle).
4. Substitution de mémoire globale ou de mémoire cache pour les variables d'état du grand livre dans le code blockchain.
5. Accès à des services externes, comme les bases de données, directement depuis le code blockchain.
6. Utilisation de bibliothèques ou de variables globales qui
pourraient introduire du non déterminisme (utilisation de "random" ou
"time", par exemple).
7. Itération à l'aide de GetRows.  

La bibliothèque d'exemples comporte des exemples de code
blockchain ; le répertoire contient des exemples écrits en
Go et en Java.
<br><br>

## Remarques liées à la migration

Plusieurs modifications de programmation doivent être
implémentées pour que le code développé dans
Hyperledger Fabric
v0.5-developer-preview puisse fonctionner avec le programme
d'arrière plan Bluemix (généré à partir de
Hyperledger Fabric v0.6.1). Pour plus de détails sur les nouvelles
fonction et les modifications de code, consultez la section
[Migration
considerations](http://hyperledger-fabric.readthedocs.io/en/v0.6/v0.6_migration/) dans la documentation Hyperledger
Fabric.   

## Problèmes connus de HSBN 

1. Lors de l'utilisation de High Security Business
Network, qui utilise Hyperledger Fabric v0.6.1, il est
conseillé de réinitialiser régulièrement le réseau s'il y a environ
une cinquantaine
de déploiements de code blockchain. Cette réinitialisation
permet de supprimer le code blockchain et les données qui ont
été collectées. Le code blockchain plus ancien peut ainsi
éventuellement être remplacé par des améliorations effectuées au
cours d'une phase du développement itératif.  Si vous êtes en phase
de post-développement, le nombre de déploiements de code
blockchain doit être surveillé afin d'affecter la capacité au
code blockchain le plus important. 
2. Erreurs sporadiques "503 Service Unavailable" et "502 Bad Gateway"
reçues lors de l'exécution d'une interrogation d'état du réseau et
des homologues.
3. Des messages "Server.Serve failed to complete
security
handshake" peuvent figurer dans les journaux de vp1. Il ne s'agit
pas d'une erreur fatale et elle n'est pas liée aux opérations réseau.
4. La zone **Données d'identification pour le
service** peut ne pas se remplir automatiquement ; dans ce
cas, générez ces données d'identification du service comme suit :

 a) Depuis le tableau de bord de votre service, cliquez sur
l'onglet **Données d'identification pour le service** :

  ![HSBN Données d'identification pour le service](images/hsbn.png "HSBN Données d'identification pour le service")

 b) Sous l'onglet **Données d'identification pour le service**,
cliquez sur le bouton **Nouvelles données d'identification**:

  ![HSBN Nouvelles données d'identification](images/hsbn1.png "HSBN Nouvelles données d'identification")

c) Une nouvelle fenêtre intitulée
**Ajouter des données d'identification** s'affiche
; cliquez sur le bouton **Ajouter** au bas de
la fenêtre :

  ![HSBN Ajouter des données d'identification](images/hsbn2.png "HSBN Ajouter des données d'identification")

 d) A présent, votre écran doit être similaire à
l'exemple suivant. Un clic sur **Afficher les données
d'identification** permet d'afficher un contenu
JSON contenant les données d'identification de service pour
votre instance HSBN.  

  ![HSBN Données d'identification générées](images/hsbn3.png "Données d'identification générées")



## Obtention d'aide

Pour obtenir du support et de l'aide sur votre réseau IBM Blockchain on Bluemix, voir [Obtention de support](ibmblockchain_support.html).
