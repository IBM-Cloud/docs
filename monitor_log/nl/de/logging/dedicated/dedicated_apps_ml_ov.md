---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Überwachung und Protokollierung für Cloud Foundry-Apps in Dedicated und Local
{: #dedicated_apps_ml_ov}


In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm:}} werden Cloud Foundry-Apps mit integrierter Protokollierung bereitgestellt. Die Daten, die aus Ihren Apps erfasst werden, können Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole prüfen.
{:shortdesc}

Cloud Foundry-Apps verwenden Cloud Foundry Loggregator, um Protokolle außerhalb der App zu überwachen und weiterzuleiten. Innerhalb der App müssen keine Agenten installiert werden.

## Hardwarevoraussetzungen


| **Voraussetzung** |    **1 Knoten**     | **3 Knoten für Hochverfügbarkeit** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
Hauptspeicher | 80 GB | 240 GB |
Lokaler Speicher | 2,98 TB | 8,94 TB |
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"}

## Konfiguration

In {{site.data.keyword.Bluemix}} Dedicated und {{site.data.keyword.Bluemix}} Local sind Protokolle standardmäßig für alle Apps aktiv. Informationen zum Lesen der Standardprotokolle finden Sie unter 'Protokollierung für Apps, die in Cloud Foundry ausgeführt werden'. In Umgebungen mit {{site.data.keyword.Bluemix}} Dedicated und {{site.data.keyword.Bluemix}} Local kann darüber hinaus eine erweiterte Protokollierung aktiviert werden.

## Protokollspeicherung

In {{site.data.keyword.Bluemix}} Dedicated und {{site.data.keyword.Bluemix}} Local werden Protokolldaten für Cloud Foundry-Apps standardmäßig 30 Tage gespeichert.

## Protokolle für Cloud Foundry-Apps in {{site.data.keyword.Bluemix}} Dedicated und {{site.data.keyword.Bluemix}} Local anzeigen
{: #dedicated_apps_ml_logs_dash}

Für die Apps, die Sie unter {{site.data.keyword.Bluemix_notm}} Dedicated und {{site.data.keyword.Bluemix_notm}} Local ausführen, können Sie Protokolle prüfen.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um die Protokolle für Ihre Apps anzuzeigen.
1. Wählen Sie eine aktive App aus.
2. Klicken Sie auf **Protokolle**. In der Ansicht **Protokolle** können Sie die Protokolle für Ihre aktive App einsehen.
4. Klicken Sie auf die Schaltfläche **Erweiterte Ansicht**. Die **erweiterte Ansicht** zeigt mehr Details der Protokolle und verwendet hierzu Kibana, ein Visualisierungstool, das mithilfe von Protokollen und Daten mit Zeitmarken angepasste Visualisierungen erstellt. Weitere Informationen zur Verwendung der erweiterten Ansicht enthält die Dokumentation zu [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Als Nächstes können Sie ein Kibana-Dashboard anpassen. Weitere Informationen finden Sie unter [Anzeige von Protokollen in einem Kibana-Dashboard anpassen](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom).

<!-- audience blue staging only end comment -->
