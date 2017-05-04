---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokollierung in Bluemix
{: #logging_bmx_ov}

Die {{site.data.keyword.Bluemix}}-Protokollierungsfunktionen sind in die Plattform integriert und die Erfassung von Daten wird für Cloudressourcen automatisch aktiviert. {{site.data.keyword.Bluemix_notm}} erfasst standardmäßig Protokolle für Ihre Apps, App-Laufzeiten und Verarbeitungslaufzeiten, in denen diese Apps ausgeführt werden. 
{:shortdesc}

Mithilfe der Protokollierungsfunktionen in {{site.data.keyword.Bluemix_notm}} können Sie das Verhalten der Cloudplattform und der Ressourcen, die in ihr ausgeführt werden, untersuchen. Zur Erfassung des Standardausgabeprotokolls und des Standardfehlerprotokolls ist keine besondere Ausstattung erforderlich. Anhand von Protokollen können Sie zum Beispiel ein Prüfprotokoll für eine Anwendung bereitstellen, Probleme in Ihrem Service ermitteln, Sicherheitslücken aufdecken, eine Fehlerermittlung für App-Bereitstellungen und das Laufzeitverhalten durchführen, Probleme in der Infrastruktur, in der Ihre App ausgeführt wird, erkennen, Ihre App komponentenübergreifend auf der Cloudplattform verfolgen sowie Muster erkennen, die es Ihnen ermöglichen, präemptive Aktionen durchzuführen, die sich auf Ihr Service-SLA auswirken könnten.

Wenn Sie Ihre Apps in der Cloud ausführen, können Sie möglicherweise nicht über SSH oder FTP auf die Protokolle in der Infrastruktur zugreifen, in der Ihre Apps ausgeführt werden, zum Beispiel wenn Ihre App in Cloud Foundry ausgeführt wird. Andererseits können Sie Ihre App in {{site.data.keyword.containershort}} ausführen, einer anderen Verarbeitungslaufzeit, die in {{site.data.keyword.Bluemix_notm}} verfügbar ist. Dort können Sie über SSH auf die Protokolle zugreifen. Unabhängig von der Verarbeitungslaufzeit ist der Zugriff auf Protokolle von entscheidender Bedeutung und {{site.data.keyword.Bluemix_notm}} stellt allgemeine Möglichkeiten zur Visualisierung und Analyse von Protokollen auf Ihrer Cloudplattform zur Verfügung.

{{site.data.keyword.Bluemix_notm}} zeichnet Protokolldaten auf, die von der Cloud Foundry-Plattform und von Cloud Foundry-Anwendungen generiert werden. In den Protokollen können Sie die Fehler, Warnungen und Informationsnachrichten prüfen, die für Ihre App generiert wurden. Weitere Informationen zur Protokollierung in Cloud Foundry finden Sie unter [Protokollierung für Cloud Foundry-Apps in Bluemix](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} zeichnet Protokolldaten auf, die durch {{site.data.keyword.containershort}} generiert werden. Weitere Informationen zur Protokollierung in {{site.data.keyword.containershort}} finden Sie unter [Protokollierung für den IBM Bluemix Container Service](containers/logging_containers_ov.html#logging_containers_ov).    


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
