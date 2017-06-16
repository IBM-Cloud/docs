---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Häufige Fragen und Antworten
{: #logging_qa}

In diesem Abschnitt finden Sie die Antworten auf häufige Fragen zu Protokollfunktionen von {{site.data.keyword.Bluemix}}. {:shortdesc}

* [Was kann ich tun, wenn in Kibana keine JSON-Protokolle angezeigt werden, die von meinem Container generiert wurden?](logging_qa.html#logging_qa_no_JSON_data_kibana)


## Was kann ich tun, wenn in Kibana keine JSON-Protokolle angezeigt werden, die von meinem Container generiert wurden?
{: #logging_qa_no_JSON_data_kibana}

Wenn JSON-Protokolle über die Standardausgabe (STDOUT) an die Docker-Protokolle gesendet werden, werden sie nicht als JSON-Daten geparst und können daher nicht nach dem Feld @timestamp sortiert werden, um die Reihenfolge zu ändern. 

Die Werte im Feld @timestamp, die angezeigt werden, sind die Zeitmarken für die Zeitpunkte, zu denen die Protokolle von ElasticSearch empfangen wurden. 

Die Zeitmarken, die die Zeitpunkte angeben, zu denen die Protokolle im Container generiert wurden, werden im Nachrichtenfeld angezeigt.

Wenn das Nachrichtenfeld in mehrere Felder unterteilt werden soll, protokollieren Sie JSON-Daten in einer Datei und senden Sie nicht an die Standardausgabe. Anschließend können Sie die Protokolle in Kibana sortieren.
