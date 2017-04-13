---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Tests supplémentaires
{: #etn_next}


Les tests ci-après ont été effectués dans l'environnement High Security Business Network (sauf indication contraire) afin de tester la fonction de code blockchain, le registre, les exécutions longues, les accès concurrents et les transactions complexes.  Les valideurs et les noeuds de services aux membres ont été exécutés en tant que machines virtuelles invitées au sein du conteneur de services sécurisé sur le système d'exploitation LinuxONE.  Les valeurs utilisées ont été choisies à partir de données entrées par les clients et ne doivent pas être considérées à tort comme les valeurs maximum. (Remarque : certains de ces tests sont répétés dans les sections [Logiciel SDK Node.js](etn_txn.html) et [Tests du consensus et de la disponibilité](etn_pbft.html).)

{:shortdesc}

1. Fonction de code blockchain - Des interfaces de code blockchain ont été expérimentées pour garantir que les transactions `Deploy`, `Invoke` et `Query` fonctionnent correctement à partir de l'API REST et de l'interface de ligne de commande. L'API REST et l'interface de ligne de commande ont toutes deux été utilisées pour tester toutes les fonctions de noeud final (notamment, Block, Blockchain, Chaincode, Network, Registrar et Transactions), comme décrit dans la spécification de protocole Hyperledger.
2. Registre - Création de 20 000 enregistrements de contenus de 1K dans le registre en fonction de différents environnement de conduite des tests. Les tests incluaient un client créant des enregistrements de 20K en série.
3. Exécutions longues - Ces tests ont été effectués par l'envoi d'appels, de hauteur de chaîne et de requêtes entre plusieurs noeuds pendant 72 heures en utilisant la démo de code blockchain example02.
4. Logiciel SDK Node.js - Le logiciel SDK Node.js amélioré a été utilisé pour l'enregistrement et l'inscription d'utilisateurs, ainsi que pour l'exécution de déploiements, d'appels et de requêtes sur un homologue à la fois en mode développement (en démarrant l'homologue avec : `peer node start –peer -chaincodedev`) et en mode réseau (en démarrant l'homologue avec : `peer node start`).
5. Accès concurrents de base - Ces tests ont été effectués par l'envoi d'appels concurrents vers chacun des quatre homologues pendant une durée de 10 minutes, avec des contenus de 1KB, la mesure de hauteur de chaîne et l'interrogation de l'état du registre.
6. Transactions complexes - Ces tests ont été effectués par la soumission aléatoire d'un mélange de requêtes et d'appels de différentes tailles de contenus, de 10k à 500K, vers les différents homologues, pendant une durée de 10 minutes. La hauteur de chaîne et l'interrogation de l'état global ont été mesurées pour garantir la synchronisation du registre partagé sur les homologues réseau.
