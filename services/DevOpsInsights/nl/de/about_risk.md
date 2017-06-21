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

# Informationen zu  Deployment Risk

{{site.data.keyword.DRA_short}} stellt eine Fülle von Informationen zu Ihren Bereitstellungen, insbesondere zu Risiken, bereit. Mit dieser Komponente können Sie den Qualitätsschutz in Ihrer Delivery Pipeline mithilfe von Richtlinien und Gates automatisieren. 
{:shortdesc}

Klicken Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} über die Toolchain auf **Deployment Risk**. Dort erhalten Sie einen Überblick über die Anwendungen in Ihren Staging- und Produktionsumgebungen. Außerdem können Sie Drilldowns durchführen, um mehr zu Codeabdeckung, Testleistung und Sicherheitsberichten zu erfahren. Die Dashboards werden automatisch mit den aktuellen Informationen aus den {{site.data.keyword.DRA_short}}-Tests der Pipelines gefüllt.

Mit Deployment Risk können Sie Qualitätsstandards in Ihrer Toolchain mithilfe von Richtlinien und Gates durchsetzen. Richtlinien umfassen Regeln; Gates setzen Richtlinien um. Sie können beispielsweise eine Richtlinie "Komponententest und Testumfang" erstellen, die verlangt, dass Builds Standards für Komponententests und Testumfang einhalten. Sie fügen dann ein Gate hinzu, das die Richtlinie zu Ihrem Continuous Delivery-Prozess referenziert. Builds, die nicht der Richtlinie entsprechen, werden am Gate gestoppt. 

## Informationen zu Integrationen

Deployment Risk kann mit {{site.data.keyword.deliverypipeline}} integriert werden, das Bestandteil von {{site.data.keyword.contdelivery_full}} ist, sowie mit Jenkins-Projekten. Auf einer höheren Ebene ähneln sich die Anweisungen zur Verwendung beider Optionen.  

Wenn Sie {{site.data.keyword.deliverypipeline}} verwenden, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie Richtlinien und Regeln](risk_policies.html) für die {{site.data.keyword.DRA_short}}-Verwaltung.
2. [Bereiten Sie die Pipelinestufen vor](risk_cd.html), um sie mit {{site.data.keyword.DRA_short}} zu integrieren.
3. [Erstellen oder bearbeiten Sie Testjobs](risk_cd.html) in der Pipeline, mit denen Ergebnisse nach {{site.data.keyword.DRA_short}} hochgeladen werden.
4. [Fügen Sie Gates zu der Pipeline hinzu](risk_cd.html), die basierend auf diesen Ergebnissen und Ihren Richtlinien Entscheidungen zu Hochstufungen fällen.
5. Führen Sie die Pipeline aus und [zeigen Sie die Ergebnisse an](results.html).

Wenn Sie Jenkins verwenden, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie Richtlinien und Regeln](risk_policies.html) für die {{site.data.keyword.DRA_short}}-Verwaltung.
2. [Installieren Sie das Jenkins-Plug-in und konfigurieren Sie es](risk_jenkins.html).
3. [Erstellen Sie Testjobs und Gates gemäß den Anweisungen in der Plug-in-Anleitung](risk_jenkins.html). Die Tests laden Ergebnisse zum Analysieren nach {{site.data.keyword.DRA_short}} hoch und die Gates verwenden diese Ergebnisse für Hochstufungsentscheidungen.
4. Führen Sie das Projekt aus und [zeigen Sie die Ergebnisse an](results.html). 

Unabhängig davon, wie Sie Ihren Code erstellen und bereitstellen, sind die Ergebnisse gleich: Die Builds, die Standards entsprechen, passieren die Deployment Risk-Gates; Builds, die nicht den angegebenen Standards entsprechen, werden gestoppt. 

## Voraussetzungen
{: #prerequisites}

Für Deployment Risk sind neben der in [Einführung in {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html) beschriebenen Konfiguration einige zusätzliche Konfigurationsschritte erforderlich.

Für die Verwendung von Deployment Risk benötigen Sie zwei Dinge:

* Eine Instanz von {{site.data.keyword.deliverypipeline}} oder ein Jenkins-Projekt
* Tests, mit denen Sie Ihr Projekt bewerten möchten
