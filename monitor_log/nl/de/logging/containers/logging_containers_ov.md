---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Protokollierung für den IBM Bluemix Container Service
{: #logging_containers_ov}

In {{site.data.keyword.Bluemix}} können Sie Containerprotokolle über das {{site.data.keyword.Bluemix_notm}}-Dashboard, in Kibana und über die Befehlszeile anzeigen, filtern und analysieren.
{:shortdesc}

Containerprotokolle werden von außerhalb der Container mithilfe von Crawlern überwacht und weitergeleitet. Die Daten werden von den Crawlern an eine Multi-Tenant-Elasticsearch-Instanz in {{site.data.keyword.Bluemix_notm}} gesendet.

**Hinweis:** Sie können Containerprotokolle in {{site.data.keyword.Bluemix_notm}} für Docker-Container analysieren, die in der von {{site.data.keyword.IBM}} verwalteten Cloud-Infrastruktur bereitgestellt sind.

Die folgende Abbildung gibt eine allgemeine Übersicht über die Protokollierung für den {{site.data.keyword.containershort}}:

![Allgemeine Übersicht über die Komponenten für Container](images/logging_containers_ov.jpg "Allgemeine Übersicht über die Komponenten für Container")

Die Containerprotokollierung wird automatisch aktiviert, wenn Sie den betreffenden Container in {{site.data.keyword.Bluemix_notm}} bereitstellen.


## Methoden zur Analyse von Containerprotokollen
{: #logging_containers_ov_methods}
 
Sie können eine der folgenden Methoden zur Analyse der Protokolle Ihres Containers auswählen:

* Analysieren Sie das Protokoll in {{site.data.keyword.Bluemix_notm}}, um die letzten Aktivitäten des Containers anzuzeigen.
    
    Sie können Protokolle über die Registerkarte **Überwachung und Protokolle** anzeigen, filtern und analysieren, die für jeden Container verfügbar ist. Weitere Informationen finden Sie unter [Protokolle über das Bluemix-Dashboard analysieren](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analysieren Sie Protokolle in Kibana, um erweiterte Analysetasks durchzuführen.
    
    Sie können Kibana, eine quelloffene Analyse- und Visualisierungsplattform, dazu verwenden, Ihre Daten in einer Reihe von Darstellungsarten, wie zum Beispiel Diagrammen und Tabellen, zu überwachen, zu durchsuchen, zu analysieren und zu visualisieren. Weitere Informationen finden Sie unter [Protokolle in Kibana analysieren](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analysieren Sie Protokolle über die Befehlszeilenschnittstelle mit Befehlen zur programmgesteuerten Protokollverwaltung.
    
    Sie können Protokolle über die Befehlszeilenschnittstelle (CLI) mit dem Befehl **cf ic logs** anzeigen, filtern und analysieren. Weitere Informationen finden Sie unter [Protokolle über die Befehlszeilenschnittstelle analysieren](../logging_view_cli.html#analyzing_logs_cli).

## Für Container erfasste Protokolle
{: #logging_containers_ov_logs_collected}

Die folgenden Protokolle werden standardmäßig erfasst:

<table>
  <caption>Tabelle 1. Protokolle</caption>
  <tbody>
    <tr>
      <th align="center">Protokoll</th>
      <th align="center">Beschreibung</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> Docker-Nachrichten werden standardmäßig im Ordner '/var/log/messages' des Containers gespeichert. Dieses Protokoll enthält Systemnachrichten.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">Dieses Protokoll ist das Docker-Protokoll. <br> Die Docker-Protokolldatei wird nicht als Datei innerhalb des Containers gespeichert, jedoch trotzdem erfasst. Diese Protokolldatei wird standardmäßig erfasst, da sie die Docker-Standardkonvention zur Bereitstellung der Informationen der Standardausgabe (stdout) und der Standard-Fehlerausgabe (stderr) für den Container darstellt. Wenn ein Containerprozess Informationen an die Standardausgabe oder Standard-Fehlerausgabe sendet, werden diese Informationen erfasst. 
      </td>
     </tr>
  </tbody>
</table>

Zur Erfassung zusätzlicher Protokolle fügen Sie die Umgebungsvariable **LOG_LOCATIONS** mit einem Pfad zur Protokolldatei hinzu, wenn Sie den Container erstellen. Sie können mehrere Protokolldateien hinzufügen, indem Sie sie durch Kommas getrennt angeben. Weitere Informationen finden Sie unter [Vom Standard abweichende Protokolldaten aus einem Container erfassen](logging_containers_other_logs.html#logging_containers_collect_data).



## Protokollspeicherung
{: #logging_containers_ov_log_retention}

Beachten Sie die folgenden Informationen zur Protokollspeicherung:

* Es werden maximal 1 GB an Daten pro Bereich und Tag gespeichert. Alle Protokolle, die die 1-GB-Begrenzung überschreiten, werden verworfen. Die Zuordnung der Obergrenze wird jeden Tag um 12:30 Uhr (UTC) zurückgesetzt. 

    Sie können sich an den Support wenden, um Ihre Obergrenze erhöhen zu lassen. Geben Sie in Ihrem Support-Ticket Ihre Bereichs-ID für die Anforderung der Obergrenzenerhöhung, die neue Obergrenze und den Grund für die Anforderung an.

* Bis zu 7 GB an Daten können maximal 7 Tage lang durchsucht werden. In die Protokolldaten wird wieder erneut von vorn geschrieben (First In, First Out), wenn entweder die Begrenzung von 7 GB an Daten oder die Dauer von 7 Tagen erreicht wird.

