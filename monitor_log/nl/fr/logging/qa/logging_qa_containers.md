---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Questions et réponses fréquentes
{: #logging_qa}

Ci-après figurent des réponses sur des questions fréquentes concernant l'utilisation des fonctionnalités de journalisation de {{site.data.keyword.Bluemix}}. {:shortdesc}

* [Que faire si je ne vois pas de journaux JSON générés par mon conteneur dans Kibana ?](logging_qa.html#logging_qa_no_JSON_data_kibana)


## Que faire si je ne vois pas de journaux JSON générés par mon conteneur dans Kibana ?
{: #logging_qa_no_JSON_data_kibana}

Lorsque des journaux JSON sont envoyés aux journaux Docker sous la sortie standard (stdout), ils ne sont pas analysés
en tant que fichiers JSON, et, par conséquent, ne peuvent pas être triés d'après la zone @timestamp pour modifier leur ordre.  

Les valeurs @timestamp affichées correspondent à leur horodatage lors de leur réception par ElasticSearch.  

Les horodatages correspondant à la génération de ces
journaux dans le conteneur sont affichés dans le cadre de la zone de message.

Pour scinder la zone de message en plusieurs zones, consignez le contenu JSON dans un fichier au lieu de l'envoyer vers la sortie standard
(stdout). Ensuite, triez les journaux dans Kibana.
