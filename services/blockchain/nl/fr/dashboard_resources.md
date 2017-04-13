---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Ressources
{: #dashboard_resources}
Dernière mise à jour : 16 mars 2017
{: .last-updated}

Cet écran comporte d'importantes données réseau et des informations d'état en temps réel concernant vos composants de blockchain.  Ces
composants incluent votre homologue, l'autorité de certification et le noeud de commande. Chaque composant comporte quatre en-têtes
distincts : **Nom**, **URL**, **Etat** et **Actions**.
{:shortdesc}

La **Figure 1** illustre l'écran de tableau de bord initial qui affiche vos composants réseau :

![Réseau de blockchain](images/myresources.png "Mes ressources")
*Figure 1. Mes ressources*

#### Nom

L'en-tête "Nom" affiche le nom au niveau système formel pour votre composant. Nos composants s'intitulent ici
`order01`, `peer01` et `ca01`.  

#### URL

L'en-tête "URL" affiche le noeud final d'API pour chaque composant. Ces noeuds finaux sont requis pour
cibler les composants réseau spécifiques d'une application côté client, et leurs définitions résident généralement
dans un fichier de configuration modélisé JSON qui est fourni avec l'application. Si vous personnalisez une application
qui nécessite l'adhésion d'homologues qui ne font pas partie de votre organisation, vous devrez obtenir ces
adresses IP auprès du ou des administrateurs dans le cadre d'une opération externe. Les clients doivent pouvoir se connecter aux
homologues dont ils attendent une réponse.

#### Statut

L'en-tête "Statut" affiche l'état réseau actuel de chaque composant (En cours d'exécution ou Arrêté, par exemple).

#### Actions

L'en-tête "Actions" comporte des boutons permettant de démarrer ou d'arrêter vos composants. Il contient également un menu déroulant
qui permet d'accéder aux journaux de composant. Ces journaux présentent les appels de procédure distante qui ont lieu
entre les différents composants réseau et s'avèrent utiles pour le débogage et le traitement des incidents. Vous pouvez les tester
en arrêtant un homologue et en le ciblant avec une transaction ; vous verrez alors des erreurs de connectivité gRPC. Redémarrez ensuite l'homologue et relancez la transaction ; vous verrez qu'une connexion est réussie. Vous
pouvez aussi arrêter un homologue pendant une longue période alors que vos canaux continuent à effectuer des transactions. Lorsque
l'homologue est redémarré, vous remarquez une synchronisation du registre via le protocole gossip. Une fois que
l'homologue a complètement synchronisé le registre, vous pouvez procéder à des appels et des requêtes normaux.  

#### Données d'identification pour le service

Dans la partie supérieure droite de cet écran, vous voyez un onglet Données d'identification pour le service. Cliquez sur cet onglet pour exposer un
fichier JSON contenant des données réseau de bas niveau pour chacun de vos composants
(ID d'inscription/Enregistrer un secret pour votre autorité de certification, par exemple). Il s'agit de l'intégralité des infos de configuration dont
vous aurez besoin pour une application. Notez, cependant, que ce fichier contient uniquement votre IP homologue. Si vous devez cibler
d'autres homologues, vous aurez besoin d'obtenir ces noeuds finaux.   
