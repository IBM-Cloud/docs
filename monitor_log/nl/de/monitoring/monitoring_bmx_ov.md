---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Überwachung in Bluemix
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}} erfasst standardmäßig Leistungsmetriken für CPU-Nutzung, Speicherauslastung und Ein-/Ausgabeoperationen über das Netz. Diese Metriken stellen Informationen über die Leistung einzelner Cloudressourcen bereit. Sie können die Leistung dieser Ressourcen in Ihrer Cloudumgebung über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle (UI) überwachen. Sie können echtzeitnahe Daten und gespeicherte Langzeitdaten anzeigen.
{:shortdesc}

Mithilfe der Überwachungsfunktionen in {{site.data.keyword.Bluemix_notm}} können Sie Schlüsselmesswerte aus Ihrer Umgebung und Ihren Anwendungen automatisch erfassen und messen. Zur Erfassung der Metriken ist keine besondere Ausstattung erforderlich. Anhand der Informationen, die durch Leistungsmetriken bereitgestellt werden,  können Sie zum Beispiel die Funktionsweise eines Service in der Cloud überwachen, Ressourcenengpässe erkennen und das Service Level Agreement (SLA) im Auge behalten. Durch die Analyse der Leistungsdaten für einen Service können Sie Situationen erkennen, die zu einem Ressourcenengpass führen und in der Folge Ihr Service-SLA für Ihre Kunden beeinträchtigen können. Auf diese Weise lassen sich Situationen, die sich negativ auf Ihr Geschäft auswirken können, durch frühzeitige Maßnahmen vermeiden.  

Sie können weitere Leistungsmetriken konfigurieren und überwachen. Sie können diese Metriken außerhalb von {{site.data.keyword.Bluemix_notm}} visualisieren und analysieren. Sie können zum Beispiel Grafana zur Überwachung weiterer Metriken verwenden, wenn Sie Ihre App in {{site.data.keyword.containershort}} ausführen. Sie können Dashboards auf Containerinstanzebene oder Bereichsebene anpassen, in denen Sie die Leistungsdaten visualisieren und analysieren.

![Grafana-Überwachungsansicht für einen Container in {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg "Grafana-Überwachungsansicht für einen Container in Bluemix")

Sie können die Überwachung der {{site.data.keyword.Bluemix_notm}}-Plattform zu folgenden Zwecken verwenden:

* Untersuchung von Anwendungsoperationen, um zum Beispiel potenzielle Engpässe zu erkennen oder festzustellen, wann Upgrades erforderlich sind.
* Definieren von Trends, die Sie zur Planung zukünftiger App-Anforderungen in Ihrer Cloudplattform verwenden können.

Weitere Informationen zur Überwachung von Apps, die in Cloud Foundry ausgeführt werden, finden Sie unter [Überwachung von Apps, die in Cloud Foundry ausgeführt werden](monitoring_cf_apps.html#monitoring_bluemix_apps).

Weitere Informationen zur Überwachung in {{site.data.keyword.containershort}} finden Sie unter [Überwachung in {{site.data.keyword.containershort}}](containers/monitoring_containers_ov.html#monitoring_bmx_containers_ov).
