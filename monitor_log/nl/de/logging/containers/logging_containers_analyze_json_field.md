---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# JSON-Nachrichtenfeld in einem Container-Protokolleintrag analysieren
{: #logging_containers_analyze_json_field}

Wenn Sie Protokolldaten für Ihren Container in Kibana analysieren wollen, können Sie neue Suchen definieren und Filter auf Felder mit Zeichenfolgedatentypen anwenden, die in einem Nachrichtenfeld mit JSON-Format definiert sind.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um ein Feld im JSON-Formattyp in Kibana zu analysieren: 

1. Um ein JSON-Nachrichtenfeld in mehrere Felder zu unterteilen, protokollieren Sie die Nachricht im JSON-Format in einer Datei und senden sie nicht an die Standardausgabe (STDOUT).  

    Wenn JSON-Protokolleinträge an die Docker-Protokolldatei eines Containers über STDOUT gesendet werden, werden sie nicht als JSON-Daten geparst. Sie können Ihre Nachricht nicht nach dem Feld @timestamp sortieren, um die Reihenfolge zu ändern.   

2. Fügen Sie die Protokolldatei der Liste der nicht standardmäßigen Protokolle hinzu, die zur Analyse aus einem Container verfügbar sind. Weitere Informationen finden Sie unter [Vom Standard abweichende Protokolldaten aus einem Container erfassen](logging_containers_other_logs.html#logging_containers_collect_data). 

3. Analysieren Sie Ihr Protokoll in Kibana. Weitere Informationen finden Sie unter [Erweiterte Protokollanalyse mit Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana). 

    **Hinweis:** Wenn ein Feld als gültiges JSON-Format festgestellt wird, wird das Feld geparst und neue Felder werden aus diesem Feld erstellt. Nur Feldwerte eines Zeichenfolgetyps sind für die Filterung und Sortierung in Kibana verfügbar. 
    
    Der Wert des Felds @timestamp, der angezeigt wird, entspricht der Zeitmarke für den Zeitpunkt, zu dem der Protokolleintrag von ElasticSearch empfangen wurde. Die Zeitmarke, die den Zeitpunkt angibt, zu dem der Protokolleintrag im Container generiert wurde, wird in den Nachrichtenfeldern angezeigt. 
    


