---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in DevOps Insights (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} wendet Analysen für Entwickler, Teams und die Bereitstellung auf Ihre wichtigsten DevOps-Projekte an. Mithilfe dieser Komponente können Sie ermitteln, wie konform Ihr Team mit DevOps und Entwicklerverfahren arbeitet. Außerdem ist sie ideal für das Risikomanagement Ihrer Codebasis und die automatische Durchsetzung von Qualitätsstandards in Continuous Delivery-Projekten.
{:shortdesc}

{{site.data.keyword.DRA_short}} umfasst mehrere verschiedene Leistungsmerkmale:

   * Mit Developer Insights können Sie den Entwicklungsstand (Reife) Ihres Projekts umfassend untersuchen. Sie können fehlerträchtige Dateien ermitteln und eine Konformitätsansicht des Projekts im Hinblick auf die Entwicklerverfahren erhalten. 

   * Team Dynamics verwendet soziale Codeanalysen, mit denen Sie feststellen können, wie gut Ihr Team zusammenarbeitet und wie diese Zusammenarbeit noch verbessert werden kann. 

   * Deployment Risk ist wie ein Sicherheitsnetz für Continuous Delivery. Die Komponente analysiert die Ergebnisse aus Komponententests, Funktionstests, Anwendungsscans und Codeabdeckungstools an bestimmten Gates in Ihrem Entwicklungsprozess und verhindert, dass riskante Änderungen freigegeben werden. 

   * Mit Delivery Insights können Sie Bereitstellungsstatistiken, Metriken und weitere Informationen zu Ihrer IBM UrbanCode Deploy-Installation anzeigen. Beispielsweise können Diagramme über den Bereitstellungszeitraum, über erfolgreiche und fehlgeschlagene Bereitstellungen angezeigt werden, die alle nach logisch gruppierten Umgebungen sortiert sind. Weitere Informationen finden Sie in [Integration von DevOps Insights mit IBM UrbanCode Deploy](/docs/services/DevOpsInsights/uc_insights_overview.html). 

Bei {{site.data.keyword.DRA_short}} handelt es sich um eine Integration mit dem offenen Toolchain-Katalog von Bluemix. Weitere Informationen zu Toolchains finden Sie in [Arbeiten mit Toolchains](/docs/services/ContinuousDelivery/toolchains_working.html). 

Um {{site.data.keyword.DRA_short}} verwenden zu können, müssen Sie die Komponente zu einer Toolchain hinzufügen. Viele Toolchain-Vorlagen enthalten bereits {{site.data.keyword.DRA_short}}. [Fügen Sie die Komponenten außerdem unbedingt zu Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation als Service hinzu](/docs/services/reqnsi.html), damit Sie Informationen zu {{site.data.keyword.DRA_short}} anzeigen und über das {{site.data.keyword.Bluemix_notm}}-Dashboard auf einige der Toolchain-Vorlagen zugreifen können, die {{site.data.keyword.DRA_short}} enthalten.   

## DevOps Insights zu einer Toolchain hinzufügen
{: #catalog}

{{site.data.keyword.DRA_short}} ist eine Komponente von {{site.data.keyword.contdelivery_short}}. Sie können {{site.data.keyword.DRA_short}} zu jeder Toolchain hinzufügen, indem Sie die Komponente aus dem Toolintegrationskatalog auswählen. 

{{site.data.keyword.DRA_short}} ist zudem in vielen Toolchain-Vorlagen enthalten. Wenn Sie eine Toolchain aus einer Vorlage erstellen, die {{site.data.keyword.DRA_short}} enthält, stellen Sie sicher, dass {{site.data.keyword.DRA_short}} auf **Erweitert** gesetzt ist. Erstellen Sie dann die Toolchain und fahren Sie mit dem Abschnitt [Insights verwenden](/docs/services/DevOpsInsights/index.html#using) fort. 

Führen Sie die folgenden Schritte aus, um {{site.data.keyword.DRA_short}} zu einer Toolchain hinzuzufügen:

1. Klicken Sie auf **Tool hinzufügen**. 

2. Klicken Sie auf **{{site.data.keyword.DRA_short}}**.

3. Um alle Funktionen von {{site.data.keyword.DRA_short}} zu Ihrer Toolchain hinzuzufügen, wählen Sie **Erweitert** aus und stellen Sie sicher, dass das Kontrollkästchen zum Aktivieren von Developer Insights aktiviert ist. Um nur Deployment Risk hinzuzufügen, wählen Sie die Option **Standard** aus.  

4. Klicken Sie auf **Integration erstellen**.

{{site.data.keyword.DRA_short}} ist nun auf der Übersichtsseite Ihrer Toolchain verfügbar. 

## DevOps Insights verwenden
{: #using}

Wenn Ihre Toolchain GitHub, GitLab oder JIRA enthält, stellt Ihnen {{site.data.keyword.DRA_short}} automatisch nach einer anfänglichen Datenerfassung und -analyse Informationen zu Ihrer Codebasis und Ihrem Team bereit. Wenn Ihre Toolchain keine dieser Integrationen umfasst, fügen Sie eine dieser Integrationen hinzu und führen Sie dann die folgenden Schritte aus:

1. Klicken Sie auf der Übersichtsseite der Toolchain auf **{{site.data.keyword.DRA_short}}**. 

2. Klicken Sie in der linken Navigationsleiste auf **Team Dynamics** oder **Developer Insights** und wählen Sie dann eine Datenkategorie aus. 

3. Untersuchen Sie die Projektdaten, indem Sie die Dashboards in der Datenkategorie anzeigen. Wenn Sie mehr über ein Diagramm oder darüber wissen möchten, wie Sie die darin enthaltenen Informationen verarbeiten sollen, klicken Sie auf **Informationen** oder **Anweisungen**. 

Nachdem Sie Team Dynamics und Developer Insights untersucht haben, [konfigurieren Sie Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html), um Codequalität durchsetzen zu können. Deployment Risk ist sowohl mit der {{site.data.keyword.contdelivery_short}} Pipeline als auch mit Jenkins kompatibel.    

Standardmäßig enthält {{site.data.keyword.DRA_short}} weder Developer Insights noch Team Dynamics. Führen Sie die folgenden Schritte durch, um diese Leistungsmerkmale nach der Konfiguration zu Ihrer Toolchain hinzuzufügen:

1. Wechseln Sie zur Übersichtsseite der Toolchain. 
2. Klicken Sie auf der {{site.data.keyword.DRA_short}}-Karte auf das Aktionsmenü. 
3. Klicken Sie auf **Konfigurieren**. 
4. Wählen Sie für den Typ die Option **Erweitert** und aktivieren Sie das entsprechende Kontrollkästchen. 
5. Klicken Sie auf **Integration speichern**. 

Nach dem Speichern der Konfiguration scannen Developer Insights und Team Dynamics automatisch Ihr Repository und das Problemverfolgungssystem. 
