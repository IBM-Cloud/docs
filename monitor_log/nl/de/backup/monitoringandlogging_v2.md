---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Überwachung und Protokollierung
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} ist die Cloud-Computing-Plattform von {{site.data.keyword.IBM_notm}} zur Erstellung, Ausführung und Verwaltung von Apps und Services. In {{site.data.keyword.Bluemix_notm}} werden Platform as a Service (PaaS) und Infrastructure as a Service (IaaS) kombiniert. Zusätzlich bietet {{site.data.keyword.Bluemix_notm}} einen umfassenden Katalog von Cloud-Services, die sich leicht in PaaS und IaaS integrieren lassen, sodass Geschäftsanwendungen unter geringem Zeitaufwand erstellt werden können. {{site.data.keyword.Bluemix_notm}} enthält integrierte Protokollierungs- und Überwachungsservices für die gesamte Plattform. 
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} bietet Protokollierungs- und Überwachungsservices für verschiedene Computer-Services an, wie zum Beispiel für den Cloud Foundry-Service und {{site.data.keyword.containershort}}. Sie können Anwendungen in einer beliebigen Computer-Laufzeit entwickeln, ausführen und verwalten, ohne dazu über die komplexe Infrastruktur mit dem entsprechenden Verwaltungsaufwand verfügen zu müssen, die in der Regel zum Entwickeln und Starten einer App gehört. 

**Hinweis:** Überwachungs- und Protokollierungsfunktionen sind den Regionen 'Vereinigte Staaten (Süden)' und 'Vereintes Königreich' verfügbar.

Mithilfe der Überwachungsfunktionen in {{site.data.keyword.Bluemix_notm}} können Sie Schlüsselmesswerte aus Ihrer Umgebung und Ihren Anwendungen automatisch erfassen und messen. Zur Erfassung der Metriken ist keine besondere Ausstattung erforderlich. Anhand der Informationen, die durch Leistungsmetriken bereitgestellt werden,  können Sie zum Beispiel die Funktionsweise eines Service in der Cloud überwachen, Ressourcenengpässe erkennen und das Service Level Agreement (SLA) im Auge behalten. Zum Beispiel können Sie durch die Analyse der Leistungsdaten für einen Service Situationen erkennen, die zu einem Ressourcenengpass führen und in der Folge Ihr Service-SLA für Ihre Kunden beeinträchtigen können. Auf diese Weise lassen sich Situationen, die sich negativ auf Ihr Geschäft auswirken können, durch frühzeitige Maßnahmen vermeiden.  

Mithilfe der Protokollierungsfunktionen in {{site.data.keyword.Bluemix_notm}} können Sie das Verhalten der Cloudplattform und der Ressourcen, die in ihr ausgeführt werden, untersuchen. Zur Erfassung des Standardausgabeprotokolls und des Standardfehlerprotokolls ist keine besondere Ausstattung erforderlich. Anhand von Protokollen können Sie zum Beispiel ein Prüfprotokoll für eine Anwendung bereitstellen, Probleme in Ihrem Service ermitteln, Sicherheitslücken aufdecken, eine Fehlerermittlung für App-Bereitstellungen und das Laufzeitverhalten durchführen, Probleme in der Infrastruktur, in der Ihre App ausgeführt wird, erkennen, Ihre App komponentenübergreifend auf der Cloudplattform verfolgen sowie Muster erkennen, die es Ihnen ermöglichen, präemptive Aktionen durchzuführen, die sich auf Ihr Service-SLA auswirken könnten.

## Computer-Infrastrukturressourcen überwachen
{: #monitoring_sl_ov}

Jeder {{site.data.keyword.Bluemix_notm}}-Server stellt Überwachungsfunktionen und leicht lesbare Berichte bereit, die stets verfügbar sind. Weitere Informationen finden Sie unter [Infrastrukturüberwachung & Berichterstellung ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}.


## Überwachung in {{site.data.keyword.Bluemix}} für Computer-Services
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}} erfasst standardmäßig Leistungsmetriken für CPU-Nutzung, Speicherauslastung und Ein-/Ausgabeoperationen über das Netz. Diese Metriken stellen Informationen über die Leistung einzelner Cloudressourcen bereit. Sie können die Leistung dieser Ressourcen in Ihrer Cloudumgebung über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle (UI) überwachen. Sie können echtzeitnahe Daten und gespeicherte Langzeitdaten anzeigen. 

Sie können weitere Leistungsmetriken konfigurieren und überwachen. Sie können diese Metriken außerhalb von {{site.data.keyword.Bluemix_notm}} visualisieren und analysieren. Sie können zum Beispiel Grafana zur Überwachung weiterer Metriken verwenden, wenn Sie Ihre App in {{site.data.keyword.containershort}} ausführen. Sie können Dashboards auf Containerinstanzebene oder Bereichsebene anpassen, in denen Sie die Leistungsdaten visualisieren und analysieren.

![Grafana-Überwachungsansicht für einen Container in {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

Sie können die Überwachung der {{site.data.keyword.Bluemix_notm}}-Plattform zu folgenden Zwecken verwenden:

* Sie können Anwendungsoperationen untersuchen, um zum Beispiel potenzielle Engpässe zu erkennen oder festzustellen, wann Upgrades erforderlich sind.
* Sie können Trends definieren, die Sie zur Planung zukünftiger App-Anforderungen in Ihrer Cloudplattform verwenden können.

Weitere Informationen zur Überwachung von Apps, die in Cloud Foundry ausgeführt werden, finden Sie unter [Überwachung von Apps, die in Cloud Foundry ausgeführt werden](monitoring_cf_apps.html#monitoring_bluemix_apps).

Weitere Informationen zur Überwachung in {{site.data.keyword.containershort}} finden Sie unter [Überwachung in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

## Protokollierung in {{site.data.keyword.Bluemix}}
{: #logging_bmx_ov}

Die {{site.data.keyword.Bluemix_notm}}-Protokollierungsfunktionen sind in die Plattform integriert und die Erfassung von Daten wird für Cloudressourcen automatisch aktiviert. {{site.data.keyword.Bluemix_notm}} erfasst standardmäßig Protokolle für Ihre Apps, App-Laufzeiten und Verarbeitungslaufzeiten, in denen diese Apps ausgeführt werden. 

Wenn Sie Ihre Apps in der Cloud ausführen, können Sie möglicherweise nicht über SSH oder FTP auf die Protokolle in der Infrastruktur zugreifen, in der Ihre Apps ausgeführt werden, zum Beispiel wenn Ihre App in Cloud Foundry ausgeführt wird. Andererseits können Sie Ihre App in {{site.data.keyword.containershort}} ausführen, einer anderen Verarbeitungslaufzeit, die in {{site.data.keyword.Bluemix_notm}} verfügbar ist. Dort können Sie über SSH auf die Protokolle zugreifen. Unabhängig von der Verarbeitungslaufzeit ist der Zugriff auf Protokolle von entscheidender Bedeutung und {{site.data.keyword.Bluemix_notm}} stellt allgemeine Möglichkeiten zur Visualisierung und Analyse von Protokollen auf Ihrer Cloudplattform zur Verfügung.

{{site.data.keyword.Bluemix_notm}} zeichnet Protokolldaten auf, die von der Cloud Foundry-Plattform und von Cloud Foundry-Anwendungen generiert werden. In den Protokollen können Sie die Fehler, Warnungen und Informationsnachrichten prüfen, die für Ihre App generiert werden. Weitere Informationen zur Protokollierung in Cloud Foundry finden Sie unter [Protokollierung für Cloud Foundry-Apps in {{site.data.keyword.Bluemix}}](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} zeichnet Protokolldaten auf, die durch {{site.data.keyword.containershort}} generiert werden. Weitere Informationen zur Protokollierung in {{site.data.keyword.containershort}} finden Sie unter [Protokollierung in {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


Die von {{site.data.keyword.Bluemix_notm}} bereitgestellte Protokollierungsfunktionalität bietet Ihnen folgende Möglichkeiten:

* Einsichtnahme in Ihre Cloudressourcen und deren Leistung und Ausführung
* Definition von Trends, die Ihnen beim Erkennen von Szenarios helfen, die Maßnahmen erfordern
* Definition von Prüfdatenlisten für eine App zum Beispiel für Protokollierungszwecke
* Verringerung des Zeit- und Arbeitsaufwands zur Ermittlung und Behebung eines Problems in einer App 
* Überwachung der Bereitstellung Ihrer Apps auf der Cloudplattform
* Erkennung, wann ein Service oder eine App inaktiv oder ausgefallen ist
* Verfolgung der Anwendungsausführung und des Datenflusses
* Ermittlung von Sicherheitslücken in Ihrer App
* Erkennung von Problemen in der Infrastruktur
* Erkennung von Problemen in der App-Laufzeit


