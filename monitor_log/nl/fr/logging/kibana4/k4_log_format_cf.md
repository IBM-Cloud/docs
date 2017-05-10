---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Format de journal Kibana pour les applications Cloud Foundry
{: #kibana_log_format_cf}

Vous pouvez configurer Kibana pour afficher sur la page *Discover* les zones suivantes pour chaque entrée de journal :
{:shortdesc}

| Zone | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-jjTHH:mm:ss:SS-0500`  <br> Heure à laquelle l'événement a été consigné. <br> L'horodatage est défini à la milliseconde près. |
| @version | Version de l'événement. |
| ALCH_TENANT_ID | ID de l'espace {{site.data.keyword.Bluemix_notm}}. |
| \_id | ID unique de votre document de journal. |
| \_index | Index de votre entrée de journal. |
| \_type | Type de journal, par exemple, *syslog*. |
| app_name | Nom de votre application {{site.data.keyword.Bluemix_notm}}. |
| application_id | ID unique de votre application {{site.data.keyword.Bluemix_notm}}. |
| hôte | Nom de l'application ayant produit les données de journal. |
| instance_id | ID d'instance de l'instance d'application ayant produit les données de journal. |
| loglevel | Niveau de gravité de l'événement consigné. |
| message | Message émis par le composant. <br> Il varie selon le contexte. |
| message_type | Flux dans lequel le message de journal est écrit. <br> * **OUT** fait référence au flux stdout. <br> * **ERR** fait référence au flux stderr. |
| org_id | ID unique de votre organisation {{site.data.keyword.Bluemix_notm}}. |
| org_name | Nom de l'organisation {{site.data.keyword.Bluemix_notm}} dans laquelle votre application est constituée en préproduction. |
| origin | Composant ayant généré l'événement. |
| source_id | Composant qui génère les journaux. <br> La liste suivante décrit les journaux provenant de chaque composant : <br> * **API** : Réponses consignées à des appels d'API qui requièrent une modification de l'état de votre application. <br> * **APP** : Réponses consignées depuis votre application. <br> * **CELL** : Réponses consignées depuis la cellule Diego et qui indique quand une application démarre, s'arrête ou tombe en panne. <br> * **LGR** : Réponses consignées depuis loggregator et qui indique des problèmes affectant le processus de journalisation. <br> * **RTR**:  Réponses consignées depuis le composant Router quand il achemine des demandes HTTP à votre application. <br> * **SSH** : Réponses consignées depuis la cellule Diego lorsqu'un utilisateur accède à un conteneur d'application à l'aide de la commande `cf ssh. <br> * **STG** : Réponses consignées depuis la cellule Diego ou l'agent DEA (Droplet Execution Agent) quand votre application est  constituée ou reconstituée. |
| space_name | Nom de l'espace {{site.data.keyword.Bluemix_notm}} dans lequel votre application est constituée en préproduction. |
| timestamp | Heure à laquelle l'événement a été consigné. L'horodatage est défini à la milliseconde près. |
{: caption="Tableau 1. Zones des applications Cloud Foundry" caption-side="top"}


