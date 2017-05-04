---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana-Protokollformat für Message Hub
{: #kibana_log_format_messagehub}

Sie können Kibana so konfigurieren, dass für jeden Protokolleintrag die folgenden Felder auf der Seite *Discover* angezeigt werden:
{:shortdesc}

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
_id:
    AVqu6vJl1zcfr8KYMI95
_type:
    logs
_index:
    logstash-2017.03.08

```
