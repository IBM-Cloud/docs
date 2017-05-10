---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Format de journal Kibana pour Message Hub
{: #kibana_log_format_messagehub}

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
