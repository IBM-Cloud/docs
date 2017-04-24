---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana-Protokollformat für Docker-Container
{: #kibana_log_format_containers}

Sie können Kibana so konfigurieren, dass für jeden Protokolleintrag die folgenden Felder auf der Seite *Discover* angezeigt werden:
{:shortdesc}

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



