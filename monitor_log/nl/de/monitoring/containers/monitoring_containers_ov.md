---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Überwachung für den IBM Bluemix-Container-Service
{: #monitoring_bmx_containers_ov}

In {{site.data.keyword.Bluemix}} werden Containermetriken automatisch von außerhalb des Containers erfasst, ohne das Agenten innerhalb des Containers installiert und verwaltet werden müssen.
{:shortdesc}

Containerinterne Agenten können beträchtlichen Systemaufwand und lange Einrichtungszeiten für kurzlebige, schlanke Cloudinstanzen und Gruppen mit automatischer Skalierung verursachen, in denen Container rasch erstellt und gelöscht werden können. Dieser Ansatz einer ausgelagerten Datenerfassung beseitigt diese Aufwände und entbindet die Benutzer von der Aufgabe der Überwachung.

Ein Prozess, der auf dem Host ausgeführt wird, führt eine agentenlose Überwachung von Metriken aus. Dieser Prozess, der auch als Crawler bezeichnet wird, erfasst standardmäßig die folgenden Metriken kontinuierlich aus allen Containern:

* CPU
* Hauptspeicher
* Netzinformationen

Metrikdaten werden in Graphite erfasst und sowohl in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle als auch in Grafana angezeigt. 

Sie können Grafana über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder über einen Browser starten. Weitere Informationen finden Sie unter [Metriken in Grafana analysieren](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana).

Docker-Konventionen und Docker-Gruppenabrechnungsdaten werden als Basismechanismus für die Erfassung von Überwachungsdaten verwendet.

## Speicherung von Metrikdaten

Es wird bis zu einem Datenpunkt pro Minute erfasst. Containermetriken, in die über einen Zeitraum von sieben Tagen nicht geschrieben wurde, werden gelöscht.
    
## Sortierung von Metrikdaten

Die Daten werden nach Container-ID angezeigt und angeordnet. 

Sie können den Befehl `cf ic ps` über die Befehlszeile ausführen, um eine Liste der Container-IDs für die Container in Ihrer privaten {{site.data.keyword.Bluemix_notm}}-Image-Registry anzuzeigen.

