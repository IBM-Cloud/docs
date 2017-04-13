---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Moniteur du tableau de bord
{: #blockchain_dashboard_monitor}


Le moniteur de tableau de bord fournit une vue d'ensemble de votre environnement de chaîne de blocs, notamment les données de performance et le code blockchain déployé. Il vous permet d'afficher les informations réseau : homologues, journaux, état du registre, API et code blockchain.  
{:shortdesc}

Comme illustré dans les exemples suivants, les onglets du moniteur
de tableau de bord comportent des vues uniques dans votre réseau de
blockchain :
  - Réseau
  - Chaîne de blocs
  - Exemple de code blockchain
  - API
  - Journaux
  - Statut
  - Support

**Onglet Réseau **: Vous pouvez surveiller l'état de vos homologues et les éventuels conteneurs de code blockchain en cours d'exécution, comme illustré dans la Figure 1. Accédez également à la Reconnaissance et aux routes d'API de vos homologues de validation et l'autorité de certification, qui sont les valeurs combinées de l'hôte de noeud et de port. Par exemple, le fragment de code JSON de vos **Données d'identification pour le service** Bluemix sur le **Tableau de bord des services** indique que `"discovery_host"` et `"discovery_port"` correspondent à la route affichée sous l'onglet **Réseau**. Ces valeurs sont utiles pour la connexion manuelle à Bluemix.

![](images/Console_Network.png "Onglet Réseau")
*Figure 1. Onglet Réseau*


**Onglet Blockchain **: Affichez l'état en cours de votre chaîne de blocs. Comme illustré dans la Figure 2, vous pouvez visualiser toutes les transactions, l'état en cours du registre et les données de performance du réseau :

![](images/Console_Blockchain.png "Onglet Chaîne de blocs")
*Figure 2. Onglet Blockchain*


**Onglet Exemple de code blockchain **: Découvrez et utilisez ces trois exemples de code blockchain pour vous entraîner à exécuter des transactions deploy et invoke sur votre réseau. Des instructions sont fournies pour vous guider tout au long du processus, comme illustré à la Figure 3. L'ensemble des déploiements et appels de code blockchain sont écrits dans le journal, ils peuvent aussi être consultés dans les journaux en temps réel, les onglets Blockchain et API.  

![](images/Console_DemoChaincode.png "Onglet Exemple de code blockchain")
*Figure 3. Onglet Exemple de code blockchain*


**Onglet API **: Utilisez l'interface utilisateur swagger pour interagir avec votre réseau de blockchain via l'API REST, comme illustré dans la Figure 4 :  

![](images/Console_APIs.png "Onglet API")
*Figure 4. Onglet API*


**Onglet Journaux **: Consultez les journaux des homologues de validation et des Services aux membres, qui contiennent les résultats de toutes les transactions sur le réseau. Vous pouvez utiliser les informations de journal pour inspecter les transactions et déboguer les code blockchain.  

![](images/Console_Logs.png "Onglet Journaux")
*Figure 5. Onglet Journaux*


**Onglet Statut **: Consultez les mesures de performance relatives aux services, au réseau et aux tests automatisés, comme illustré dans la Figure 6. Affichez les données du mois précédent. Cet onglet contient également des annonces de code, des forums généraux, des problèmes connus, ainsi que des notes sur l'édition pour IBM Blockchain.  

![](images/Console_Status.png "Onglet Statut")
*Figure 6. Onglet Statut*


**Onglet Support **: Signalez un problème et consultez l'état de votre Service, comme illustré à la Figure 7 :

![](images/Console_Support.png "Onglet Support")
*Figure 7. Onglet Support*
