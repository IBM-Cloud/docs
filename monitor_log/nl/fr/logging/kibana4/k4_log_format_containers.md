---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Format de journal Kibana pour les conteneurs Docker
{: #kibana_log_format_containers}

Vous pouvez configurer Kibana pour afficher sur la page *Discover* les zones suivantes pour chaque entrée de journal :
{:shortdesc}

| Zone | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-jjTHH:mm:ss:SS-0500`  <br> Heure à laquelle l'événement a été consigné. <br> L'horodatage est défini à la milliseconde près. |
| @version | Version de l'événement. |
| ALCH_TENANT_ID | ID de l'espace {{site.data.keyword.Bluemix_notm}}. |
| \_id | ID unique de votre document de journal. |
| \_index | Index de votre entrée de journal. |
| \_type | Type de journal. Par exemple, *logs*. |
| group_id | ID du groupe <br> *Pour un conteneur unique, sa valeur est **0000**. <br> * Pour un groupe de conteneurs, sa valeur est l'identificateur global unique (GUID) du groupe.  |
| hôte | Nom de l'hôte sur lequel le conteneur s'exécute. |
| instance | GUID de l'instance pour un conteneur unique. Liste des ID d'instance pour un groupe de conteneurs.|
| log | Message concis. |
| message | Message complet. |
| path | Chemin et nom du fichier journal dans le conteneur. |
| stream | Spécifie le type de journal : stdout, stderr |
| time | Date et heure à laquelle l'événement s'est produit. L'horodatage est défini à la milliseconde près.|
| timestamp | Date et heure de consignation de l'événement. L'horodatage est défini à la milliseconde près. |
{: caption="Tableau 1. Zones des conteneurs Docker" caption-side="top"}


