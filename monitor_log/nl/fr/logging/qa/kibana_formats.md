---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Formats de journal Kibana
{: #kibana_formats}

Vous pouvez configurer Kibana pour afficher sur la page *Discover* différentes zones pour chaque entrée de journal.
{:shortdesc}



## Format de journal Kibana pour les applications Cloud Foundry
{: #kibana_log_format_cf}

Vous pouvez configurer Kibana pour afficher sur la page *Discover* les zones suivantes pour chaque entrée de journal :

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
| message | Message émis par le composant. <br> Le message varie en fonction du contexte. |
| message_type | Flux dans lequel le message de journal est écrit. <br> * **OUT** fait référence au flux stdout. <br> * **ERR** fait référence au flux stderr. |
| org_id | ID unique de votre organisation {{site.data.keyword.Bluemix_notm}}. |
| org_name | Nom de l'organisation {{site.data.keyword.Bluemix_notm}} dans laquelle votre application est constituée en préproduction. |
| origin | Composant ayant généré l'événement. |
| source_id | Composant qui génère les journaux. <br> La liste suivante décrit les journaux provenant de chaque composant : <br> * **API** : Réponses consignées à des appels d'API qui requièrent une modification de l'état de votre application. <br> * **APP** : Réponses consignées depuis votre application. <br> * **CELL** : Réponses consignées depuis la cellule Diego et qui indique quand une application démarre, s'arrête ou tombe en panne. <br> * **LGR** : Réponses consignées depuis loggregator et qui indique des problèmes affectant le processus de journalisation. <br> * **RTR**:  Réponses consignées depuis le composant Router quand il achemine des demandes HTTP à votre application. <br> * **SSH** : Réponses consignées depuis la cellule Diego lorsqu'un utilisateur accède à un conteneur d'application à l'aide de la commande `cf ssh. <br> * **STG** : Réponses consignées depuis la cellule Diego ou l'agent DEA (Droplet Execution Agent) quand votre application est  constituée ou reconstituée. |
| space_name | Nom de l'espace {{site.data.keyword.Bluemix_notm}} dans lequel votre application est constituée en préproduction. |
| timestamp | Heure à laquelle l'événement a été consigné. L'horodatage est défini à la milliseconde près. |
{: caption="Tableau 1. Zones des applications Cloud Foundry" caption-side="top"}



## Format de journal Kibana pour les conteneurs Docker
{: #kibana_log_format_containers}

Vous pouvez configurer Kibana pour afficher sur la page *Discover* les zones suivantes pour chaque entrée de journal :

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


## Format de journal Kibana pour Message Hub
{: #kibana_log_format_messagehub}

Vous pouvez configurer Kibana pour afficher sur la page *Discover* les zones suivantes pour chaque entrée de journal :

| Zone | Description |
|-------|-------------|
| @timestamp | `yyyy-MM-jjTHH:mm:ss:SS-0500`  <br> Heure à laquelle l'événement a été consigné. <br> L'horodatage est défini à la milliseconde près. |
| @version | Version de l'événement. |
| ALCH_TENANT_ID | ID de l'espace {{site.data.keyword.Bluemix_notm}}. |
| \_id | ID unique de votre document de journal. |
| \_index | Index de votre entrée de journal. |
| \_type | Type de journal, par exemple, *syslog*. |
| loglevel | Gravité de l'événement consigné. Par exemple, **Info**. |
| module | Cette zone est définie sur **MessageHub**. |
{: caption="Tableau 1. Zones des événements de concentrateur de messages" caption-side="top"}

Exemple d'entrée de journal :

```
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
