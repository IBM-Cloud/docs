---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana-Protokollformate
{: #kibana_formats}

Sie können Kibana so konfigurieren, dass für jeden Protokolleintrag verschiedene Felder auf der Seite *Discover* angezeigt werden.
{:shortdesc}



## Kibana-Protokollformat für Cloud Foundry-Anwendungen
{: #kibana_log_format_cf}

Sie können Kibana so konfigurieren, dass für jeden Protokolleintrag die folgenden Felder auf der Seite *Discover* angezeigt werden:

| Feld | Beschreibung |
|-------|-------------|
| @timestamp | `jjjj-MM-ttTHH:mm:ss:SS-0500`  <br> Der Zeitpunkt des protokollierten Ereignisses. <br> Die Zeitmarke ist bis auf die Millisekunde definiert. |
| @version | Die Version des Ereignisses. |
| ALCH_TENANT_ID | Die ID des {{site.data.keyword.Bluemix_notm}}-Bereichs. |
| \_id | Die eindeutige ID für Ihr Protokolldokument. |
| \_index | Der Index für Ihren Protokolleintrag. |
| \_type | Der Typ von Protokoll. Beispiel: *syslog*. |
| app_name | Der Name Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung. |
| application_id | Die eindeutige ID Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung. |
| host | Der Name Ihrer Anwendung, die die Protokolldaten generiert hat. |
| instance_id | Die Instanz-ID Ihrer Anwendungsinstanz, die die Protokolldaten generiert hat. |
| loglevel | Die Priorität des protokollierten Ereignisses. |
| message | Die Nachricht, die von der Komponente ausgegeben wird. <br> Die Nachricht variiert abhängig vom Kontext. |
| message_type | Der Datenstrom, in den die Protokollnachricht geschrieben wird. <br> * **OUT** verweist auf den Standardausgabedatenstrom (stdout). <br> * **ERR** verweist auf den Standard-Fehlerausgabedatenstrom (stderr). |
| org_id | Die eindeutige ID Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation. |
| org_name | Der Name der {{site.data.keyword.Bluemix_notm}}-Organisation, in der das Staging für Ihre App erfolgt. |
| origin | Die Komponente, aus der das Ereignis stammt. |
| source_id | Die Komponente, die Protokolle generiert. <br> In der folgenden Liste werden die Protokolle aus jeder Komponente beschrieben: <br> * **API**: Protokollierte Antworten auf API-Aufrufe, die eine Änderung an Ihrem App-Status anfordern. <br> * **APP**: Protokollierte Antworten aus Ihrer App. <br> * **CELL**: Protokollierte Antworten aus der Diego-Zelle, die den Zeitpunkt eines Starts, Stopps oder Absturzes einer App angeben. <br> * **LGR**: Protokollierte Antworten aus Loggregator, die auf Probleme mit dem Protokollierungsprozess hinweisen. <br> * **RTR**: Protokollierte Antworten aus dem Router, wenn er HTTP-Anforderungen an Ihre App leitet. <br> * **SSH**: Protokollierte Antworten aus der Diego-Zelle, wenn ein Benutzer auf einen App-Container mit dem Befehl `cf ssh` zugreift. <br> * **STG**: Protokollierte Antworten aus der Diego-Zelle oder dem Droplet Execution Agent (DEA), wenn ein Staging oder erneutes Staging für Ihre App erfolgt. |
| space_name | Der Name des {{site.data.keyword.Bluemix_notm}}-Bereichs, in dem das Staging für Ihre App erfolgt. |
| timestamp | Der Zeitpunkt des protokollierten Ereignisses. Die Zeitmarke ist bis auf die Millisekunde definiert. |
{: caption="Tabelle 1. Felder für CF-Apps" caption-side="top"}



## Kibana-Protokollformat für Docker-Container
{: #kibana_log_format_containers}

Sie können Kibana so konfigurieren, dass für jeden Protokolleintrag die folgenden Felder auf der Seite *Discover* angezeigt werden:

| Feld | Beschreibung |
|-------|-------------|
| @timestamp | `jjjj-MM-ttTHH:mm:ss:SS-0500`  <br> Der Zeitpunkt des protokollierten Ereignisses. <br> Die Zeitmarke ist bis auf die Millisekunde definiert. |
| @version | Die Version des Ereignisses. |
| ALCH_TENANT_ID | Die ID des {{site.data.keyword.Bluemix_notm}}-Bereichs. |
| \_id | Die eindeutige ID für Ihr Protokolldokument. |
| \_index | Der Index für Ihren Protokolleintrag. |
| \_type | Der Typ von Protokoll. Beispiel: *logs*. |
| group_id | Die Gruppen-ID. <br> * Für einen einzelnen Container ist der Wert **0000**. <br> * Für eine Containergruppe ist der Wert die GUID der Gruppe.  |
| host | Der Name des Hosts, auf dem der Container ausgeführt wird. |
| instance | Die GUID der Instanz für einen einzelnen Container. Die Liste der Instanz-IDs für eine Containergruppe.|
| log | Die Kurznachricht. |
| message | Die vollständige Nachricht. |
| path | Der Pfad und der Protokollname, unter dem sich das Protokoll in dem Container befindet. |
| stream | Gibt den Typ von Protokoll an: stdout, stderr |
| time | Das Datum und die Uhrzeit des Zeitpunkts für das Ereignis, als es auftrat. Die Zeitmarke ist bis auf die Millisekunde definiert.|
| timestamp | Das Datum und die Uhrzeit des protokollierten Ereignisses. Die Zeitmarke ist bis auf die Millisekunde definiert. |
{: caption="Tabelle 1. Felder für Docker-Container" caption-side="top"}


## Kibana-Protokollformat für Message Hub
{: #kibana_log_format_messagehub}

Sie können Kibana so konfigurieren, dass für jeden Protokolleintrag die folgenden Felder auf der Seite *Discover* angezeigt werden:

| Feld | Beschreibung |
|-------|-------------|
| @timestamp | `jjjj-MM-ttTHH:mm:ss:SS-0500`  <br> Der Zeitpunkt des protokollierten Ereignisses. <br> Die Zeitmarke ist bis auf die Millisekunde definiert. |
| @version | Die Version des Ereignisses. |
| ALCH_TENANT_ID | Die ID des {{site.data.keyword.Bluemix_notm}}-Bereichs. |
| \_id | Die eindeutige ID für Ihr Protokolldokument. |
| \_index | Der Index für Ihren Protokolleintrag. |
| \_type | Der Typ von Protokoll. Beispiel: *syslog*. |
| loglevel | Die Priorität des protokollierten Ereignisses. Beispiel: **Info**. |
| module | Dieses Feld ist auf den Wert **MessageHub** gesetzt. |
{: caption="Tabelle 1. Felder für Message Hub-Ereignisse" caption-side="top"}

Beispiel für einen Protokolleintrag:

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
