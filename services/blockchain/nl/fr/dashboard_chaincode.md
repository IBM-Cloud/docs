---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Code blockchain
{: #v10_dashboard}
Dernière mise à jour : 16 mars 2017
{: .last-updated}

Le code blockchain est un logiciel (actuellement écrit en Go ou Java) qui encapsule la logique métier et les instructions transactionnelles
pour la création et la modification des actifs. Il s'exécute dans un conteneur Docker associé à un homologue qui doit interagir avec lui.  
{:shortdesc}

Le code blockchain est tout d'abord installé sur le système de fichiers d'un homologue, puis il est instancié sur un canal. L'étape d'instanciation implique
l'initialisation des paire clé-valeur et le déploiement du conteneur de code blockchain. Tout homologue souhaitant interagir avec un
code blockchain doit avoir le code source installé sur son système de fichiers et un conteneur de code blockchain opérationnel. Toutefois, si un homologue
souhaite utiliser la même application de code blockchain sur plusieurs canaux, il n'a besoin que d'une seule instance du conteneur.  

La **Figure 8** illustre la présentation de l'installation du code blockchain :

![Réseau de blockchain](images/chaincode_install_overview.png "Installation du code blockchain")
*Figure 8. Présentation de l'installation du code blockchain*

* Utilisez le menu déroulant et sélectionnez un homologue sur lequel installer du code blockchain.  
* Cliquez sur le bouton **Installer le code blockchain** sur le côté droit de votre écran ; un nouveau panneau s'affiche.

La **Figure 9** illustre la fenêtre d'installation du code blockchain :

![Réseau de blockchain](images/chaincode_install.png "Installation du code blockchain")
*Figure 9. Fenêtre d'installation du code blockchain*

* Remplissez toutes les zones pour l'ID de code blockchain et la version de code blockchain. Soyez informé des schémas de dénomination, car ces chaînes seront utilisées dans les applications client pour l'interaction avec des codes blockchain particuliers.
* Cliquez sur le bouton de recherche et parcourez votre code système de fichiers local jusqu'à l'emplacement de stockage de la source de votre code blockchain. Sélectionnez un ou plusieurs fichiers à installer sur votre homologue. **Remarque **: Il est recommandé de télécharger uniquement le code blockchain écrit en Go ou en Java.  

Une fois qu'un code blockchain a été installé sur le système de fichiers d'un homologue, il doit ensuite être instancié sur un canal. Cette étape d'instanciation appelle la fonction `init` pour exécuter l'initialisation nécessaire du code blockchain. Cela implique souvent la définition de paires clé-valeur qui comprennent la base de données "world state" initiale d'un code blockchain.

La **Figure 10** illustre la fenêtre d'instanciation du code blockchain : 

![Réseau de blockchain](images/chaincode_instantiate.png "Instanciation de code blockchain")
*Figure 10. Fenêtre d'instanciation de code blockchain*

Notez que chacune des paires clé-valeur est définie avec la chaîne - `["a","b","200","250"]` - et qu'une fenêtre permet de sélectionner le canal sur lequel effectuer l'instanciation. Cet exemple illustre un code blockchain nommé `end2end` installé sur `fabric-peer1a` et instancié dans un canal nommé `mychannel`:

La combinaison installation/instanciation est une fonction puissante car elle permet à un homologue d'interagir avec le même conteneur de code blockchain sur plusieurs canaux. Le seul prérequis est que le source de code blockchain réel soit installé sur le système de fichiers de l'homologue. De cette façon, si un élément de code blockchain est utilisé sur des douzaines de canaux, un homologue n'aura besoin que d'un seul conteneur de code blockchain pour exécuter des opérations de lecture/écriture sur tous les registres de canal. Cette approche souple se révèle bénéfique pour les performances et le débit de calcul dès lors que l'échelle des réseaux et les applications de code blockchain deviennent plus élaborés.    
