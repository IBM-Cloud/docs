---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokollierung für Cloud Foundry-Apps in Bluemix
{: #logging_bluemix_cf_apps}

In {{site.data.keyword.Bluemix}} können Sie Cloud Foundry-Protokolle (CF-Protokolle) über das {{site.data.keyword.Bluemix_notm}}-Dashboard, in Kibana und über die Befehlszeilenschnittstelle (CLI) anzeigen, filtern und analysieren. Darüber hinaus können Sie Protokolleinträge durch Streaming an ein externes Protokoll-Management-Tool übertragen. 
{:shortdesc}

Wenn Sie Ihre Apps in einer als Service bereitgestellten Cloudplattform (Platform-as-a-service, PaaS) wie Cloud Foundry in {{site.data.keyword.Bluemix_notm}} ausführen, können Sie nicht über SSH oder FTP auf die Protokolle in der Infrastruktur zugreifen, in der Ihre Apps ausgeführt werden. Die Plattform wird durch den Cloud-Provider gesteuert. Cloud Foundry-Apps, die in {{site.data.keyword.Bluemix_notm}} ausgeführt werden, verwenden die Komponente "Loggrerator", um Protokolleinträge aus der Cloud Foundry-Infrastruktur heraus weiterzuleiten. Loggregator erfasst automatisch STDOUT- und STDERR-Daten. Sie können diese Protokolle über das {{site.data.keyword.Bluemix_notm}}-Dashboard, über Kibana und über die Befehlszeilenschnittstelle visualisieren und analysieren.

Die folgende Abbildung zeigt eine Übersicht über die Protokollierung von Cloud Foundry-Apps in {{site.data.keyword.Bluemix_notm}}:

![Allgemeine Übersicht über die Komponenten für CF-Apps](../images/logging_cf_apps_ov.jpg "Allgemeine Übersicht über die Komponenten für CF-Apps")
 
Die Protokollierung von Cloud Foundry-Apps ist automatisch aktiviert, wenn Sie die Cloud Foundry-Infrastruktur zur Ausführung Ihrer Apps in {{site.data.keyword.Bluemix_notm}} verwenden. Wenn Sie Cloud Foundry-Laufzeitprotokolle anzeigen möchten, müssen Sie Ihre Protokolle in die Standardausgabe (STDOUT) und Standard-Fehlerausgabe (STDERR) schreiben. Weitere Informationen finden Sie unter [Laufzeitanwendungsprotokollierung durch CF-Apps](logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app).

{{site.data.keyword.Bluemix_notm}} bewahrt eine begrenzte Menge an Protokolldaten auf. Bei der Protokollierung von Daten werden die alten Informationen durch die neueren Daten ersetzt. Wenn Sie organisationsbedingte oder branchenspezifische Richtlinien einhalten müssen, die eine Aufbewahrung eines Teils oder aller Protokolldaten zu Prüfzwecken oder aus anderen Gründen vorsehen, können Sie Ihre Protokolle auf einen externen Protokollhost, wie zum Beispiel einen Protokoll-Management-Service eines anderen Anbieters, oder auf einen anderen Host durch Streaming übertragen. Weitere Informationen finden Sie unter [Externe Protokollhosts konfigurieren](../external/logging_external_hosts.html#thirdparty_logging).

## Methoden zur Analyse von CF-App-Protokollen
{: #logging_bluemix_cf_apps_log_methods}

Die folgenden Methoden stehen für die Analyse der Protokolle Ihrer Cloud Foundry-Anwendung zur Auswahl:

* Analysieren Sie das Protokoll in {{site.data.keyword.Bluemix_notm}}, um die letzte Aktivität der Anwendung anzuzeigen.
    
    In {{site.data.keyword.Bluemix_notm}} können Sie Protokolle über die Registerkarte **Protokolle** anzeigen, filtern und analysieren, die für jede Cloud Foundry-Anwendung verfügbar ist. Weitere Informationen finden Sie unter [CF-App-Protokolle über das Bluemix-Dashboard analysieren](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analysieren Sie Protokolle in Kibana, um erweiterte Analysetasks durchzuführen.
    
    In {{site.data.keyword.Bluemix}} können Sie Kibana, eine quelloffene Analyse- und Visualisierungsplattform, dazu verwenden, Ihre Daten in einer Reihe von Darstellungsarten, wie zum Beispiel Diagrammen und Tabellen, zu überwachen, zu durchsuchen, zu analysieren und zu visualisieren. Weitere Informationen finden Sie unter [Protokolle in Kibana analysieren](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analysieren Sie Protokolle über die Befehlszeilenschnittstelle mit Befehlen zur programmgesteuerten Protokollverwaltung.
    
    In {{site.data.keyword.Bluemix}} können Sie Protokolle über die Befehlszeilenschnittstelle (CLI) mithilfe des Befehls **cf logs** anzeigen, filtern und analysieren. Weitere Informationen finden Sie unter [Cloud Foundry-App-Protokolle über die Befehlszeile analysieren](../logging_view_cli.html#analyzing_logs_cli).


## Protokollquellen für CF-Apps
{: #logging_bluemix_cf_apps_log_sources}

Für Cloud Foundry-Anwendungen (CF-Anwendungen) sind die folgenden Protokollquellen verfügbar:
    
| Protokollquelle | Komponentenname | Beschreibung | 
|------------|----------------|-------------|
| LGR | Loggregator | Die LGR-Komponente stellt Informationen über den Cloud Foundry Loggregator bereit, der Protokolle aus Cloud Foundry heraus weiterleitet. |
| RTR | Router | Die RTR-Komponente stellt Informationen zu HTTP-Anforderungen an eine Anwendung bereit. | 
| STG | Staging | Die STG-Komponente stellt Informationen zum Staging und erneuten Staging einer Anwendung bereit. | 
| APP | Anwendung | Die APP-Komponente stellt Protokolle aus der Anwendung bereit. Hier wird die Standard-Fehlerausgabe (STDERR) und die Standardausgabe (STDOUT) in Ihrem Code angezeigt. | 
| API | Cloud Foundry-API | Die API-Komponente stellt Informationen zu den internen Aktionen bereit, die aus der Anforderung eines Benutzers zum Ändern des Status einer Anwendung resultieren. | 
| DEA | Droplet Execution Agent | Die DEA-Komponente stellt Informationen zum Start, Stopp oder Absturz einer Anwendung bereit. <br> Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf DEA basiert. | 
| CELL | Diego-Zelle | Die CELL-Komponente stellt Informationen zum Start, Stopp oder Absturz einer Anwendung bereit. <br> Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf Diego basiert.|
| SSH | SSH | Die SSH-Komponente stellt jedes Mal Informationen bereit, wenn ein Benutzer auf eine Anwendung mit dem Befehl **cf ssh** zugreift. Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf Diego basiert. |
{: caption="Tabelle 1. Protokollquellen" caption-side="top"}

Die folgende Abbildung zeigt die verschiedenen Komponenten (Protokollquellen) in einer Cloud Foundry-Architektur, die auf dem Droplet Execution Agent (DEA) basiert:
![Protokollquellen in einer DEA-Architektur.](../images/logging_F1.png "Komponenten (Protokollquellen) in einer Cloud Foundry-Architektur, die auf dem Droplet Execution Agent (DEA) basiert.")


