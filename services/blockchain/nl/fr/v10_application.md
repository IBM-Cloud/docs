---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Développement d'applications
{: #v10_dashboard}


Utilisez l'exemple de code blockchain marbles02 et l'application javascript correspondante comme modèle pour la création de votre propre solution métier.
{:shortdesc}


L'application tire parti des API SDK Node.js pour interagir avec vos composants réseau mis à disposition et cible finalement votre homologue avec des demandes de transaction. Localisez les noeuds finaux d'API de votre homologue, autorité de certification et service de commande réseau au sein de l'onglet **Données d'identification pour le service** à l'écran **Ressources** du Moniteur et incluez ces chaînes dans un fichier de configuration associé à votre application. Notez, cependant, que si vous voulez cibler des homologues supplémentaires dans le réseau (ce qui peut être le cas si vous avez besoin de l'adhésion d'un homologue n'appartenant pas à votre organisation), vous devrez obtenir les noeuds finaux d'API corrects de ces homologues. Vous devez aussi stocker le certificat de l'autorité de certification de l'autre organisation afin de vérifier les réponses retournées à votre application. Ces informations ne sont pas exposées dans votre vue **Ressources**, par conséquent vous devez contacter l'admin approprié de l'organisation Bluemix et acquérir ces données dans une opération externe. L'URL du service de commande est commune au sein du réseau ; vous n'avez besoin d'aucune information spécifique aux membres pour ce composant.  

Consultez le référentiel GitHub [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0) pour plus de détails sur le code source prérequis ; suivez les instructions du README et donnez vie à votre application.  

Explorez le [référentiel SDK](https://github.com/hyperledger/fabric-sdk-node) pour vous exercer aux tests de bout en bout et mieux connaître les API.
