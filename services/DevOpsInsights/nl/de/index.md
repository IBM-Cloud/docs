---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.DRA_short}} (Experimentell)
{: #gettingstarted}

Mit {{site.data.keyword.DRA_full}} können Sie Risiken für Ihre Builds und Bereitstellungen ermitteln.
{:shortdesc}

{{site.data.keyword.DRA_short}} aggregiert und analysiert die Ergebnisse aus Komponententests, Funktionstests und Codeabdeckungstools, um zu bestimmen, ob Ihr Code den vordefinierten Richtlinien bei angegebenen Gates in Ihrem Bereitstellungsprozess entspricht. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden. Sie können {{site.data.keyword.DRA_short}} als Sicherheitsnetz für Ihre Continuous Delivery-Umgebung, als Möglichkeit der Implementierung und Verbesserung der Qualitätsstandards über einen Zeitraum hinweg sowie als Datenvisualisierungstool für Informationen zum Projektstatus verwenden.

Bei {{site.data.keyword.DRA_short}} handelt es sich um ein experimentelles Angebot und wird auf As-is-Basis nur zu Entwicklungs- und Versuchszwecken bereitgestellt. Für die Verwendung von {{site.data.keyword.DRA_short}} müssen Sie diese Komponente zu einer beliebigen Toolchain hinzufügen, die mit der {{site.data.keyword.deliverypipeline}} arbeitet.

{: #catalog}
Führen Sie für den Zugriff auf die Benutzerschnittstelle von {{site.data.keyword.DRA_short}} die folgenden Schritte in einer vorhandenen Toolchain aus:

1. Klicken Sie auf die Schaltfläche **Tool hinzufügen**.

2. Klicken Sie auf **{{site.data.keyword.DRA_short}}**.

3. Klicken Sie auf **Integration erstellen**.

4. Klicken Sie auf die Kachel für **{{site.data.keyword.DRA_short}}**.

5. Vervollständigen Sie Ihr Setup mit den verbliebenen Tasks:

	1. [Konfigurieren Sie Ihre {{site.data.keyword.deliverypipeline}}-Integration](./pipeline_integration.html).
	2. Führen Sie die Pipeline aus und [überprüfen Sie die {{site.data.keyword.deliverypipeline}}-Dashboards](./pipeline_decision_reports.html).
	3. [Definieren Sie Richtlinien](./create_criteria.html) für die {{site.data.keyword.DRA_short}}-Verwaltung.
	4. Führen Sie die Pipeline erneut aus, um zu prüfen, ob Ihr Projekt Ihre Richtlinien berücksichtigt.


# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Wahrscheinlichkeit erfolgreicher Bereitstellungen mithilfe von Analysen feststellen](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## Zugehörige Links
{: #general}

* [Einführung in Toolchains](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Einführung in Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [IBM Bluemix-Preisstruktur](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [IBM Bluemix - Voraussetzungen](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
