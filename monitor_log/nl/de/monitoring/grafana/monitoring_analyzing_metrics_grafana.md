---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Metriken in Grafana analysieren
{:#analyzing_metrics_grafana}

In {{site.data.keyword.Bluemix}} können Sie mit Grafana, einer quelloffenen Analyse- und Visualisierungsplattform, Ihre Metriken in verschiedenen Aufbereitungen, wie zum Beispiel Diagrammen und Tabellen, überwachen, durchsuchen, analysieren und visualisieren. Verwenden Sie Grafana zur Ausführung erweiterter Analysetasks.
{:shortdesc}

Sie können Grafana auf eine beliebige der folgenden Arten starten:

* Über {{site.data.keyword.Bluemix_notm}}

    Sie können Grafana mit den bestimmten Docker-Container-Metriken im Kontext des betreffenden Containers starten. 
    
    Weitere Informationen finden Sie unter [Zum Grafana-Dashboard über das {{site.data.keyword.Bluemix_notm}}-Dashboard navigieren](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix).

* Über einen direkten Browser-Link

    Sie können Grafana so starten, dass die angezeigten Daten Protokolle aus Services in einem angegebenen {{site.data.keyword.Bluemix_notm}}-Bereich aggregieren.
    
    Weitere Informationen finden Sie unter [Zum Grafana-Dashboard über einen Web-Browser navigieren](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser). 
    
Weitere Informationen zu Grafana finden Sie in der Veröffentlichung [Grafana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://docs.grafana.org/guides/getting_started/){: new_window}.


##  Zum Grafana-Dashboard über das Bluemix-Dashboard navigieren
{: #launch_grafana_from_bluemix}

Die Abfrage, durch die die Daten gefiltert werden, die in Grafana angezeigt werden, ruft Daten für den {{site.data.keyword.Bluemix_notm}}-Container von der Position aus ab, an der Sie Grafana starten. 

Führen Sie die folgenden Schritte aus, um die Metriken eines Docker-Containers in Grafana anzuzeigen:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie auf den Container im {{site.data.keyword.Bluemix_notm}}-Dashboard. 
    
2. Klicken Sie in der Navigationsleiste auf **Überwachung und Protokolle**. Die Registerkarte für die Überwachung wird geöffnet. 
    
3. Klicken Sie auf **Erweiterte Ansicht**. Das **Grafana**-Dashboard wird geöffnet.


##  Zum Grafana-Dashboard über einen Web-Browser navigieren
{: #launch_grafana_from_browser}

Die Abfrage, durch die die Daten gefiltert werden, die in Grafana angezeigt werden, ruft Daten für einen Bereich in der {{site.data.keyword.Bluemix_notm}}-Organisation ab. Die Metrikdaten, die in Grafana angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt wurden, an der Sie angemeldet sind.

Führen Sie die folgenden Schritte aus, um Grafana über einen Browser zu starten:

1. Öffnen Sie [https://logmet.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span>](https://logmet.{DomainName}), um sich bei der Grafana-Benutzerschnittstelle anzumelden.

2. Wählen Sie **Grafana** aus.
     

