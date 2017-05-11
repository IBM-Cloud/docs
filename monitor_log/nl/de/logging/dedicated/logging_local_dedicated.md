---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokollierung für Cloud Foundry-Apps in Dedicated und Local
{: #hybrid_apps_logs_ov}

In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} werden Cloud Foundry-Apps mit integrierter Protokollierung bereitgestellt. Die Daten, die aus Ihren Apps erfasst werden, können Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole prüfen.
{:shortdesc}

Cloud Foundry-Apps verwenden Cloud Foundry Loggregator, um Protokolle außerhalb der App zu überwachen und weiterzuleiten. Innerhalb der App müssen keine Agenten installiert werden.

## Hardwarevoraussetzungen


| **Voraussetzung** |    **1 Knoten**     | **3 Knoten für Hochverfügbarkeit** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Hauptspeicher | 80 GB | 240 GB |
| Lokaler Speicher | 2,98 TB | 8,94 TB |
{: caption="Tabelle 2. Hardwarevoraussetzungen für die Protokollierung für {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

## Konfiguration

In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} sind Protokolle standardmäßig für alle Apps aktiv. Informationen zum Lesen der Standardprotokolle finden Sie unter [Protokollierung für Apps, die in Cloud Foundry ausgeführt werden](../logging_cf_apps.html#logging_bluemix_cf_apps). In Umgebungen mit {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} kann darüber hinaus eine erweiterte Protokollierung aktiviert werden.

* Zum Aktivieren der erweiterten Protokollierung in Ihrer {{site.data.keyword.Bluemix_dedicated_notm}}- und {{site.data.keyword.Bluemix_local_notm}}-Umgebung führen Sie die Schritte im Abschnitt [Protokolle anzeigen](#hybrid_apps_logs_dash) aus. Falls die Schaltfläche **Erweiterte Ansicht** nicht angezeigt wird, ist diese Funktion nicht aktiviert.

* Die Schritte, mit denen Sie die erweiterte Protokollierung zu Ihrer Umgebung hinzufügen, sind in der Dokumentation für [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) bzw. [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) beschrieben.

## Protokollspeicherung

In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} werden Protokolldaten für Cloud Foundry-Apps standardmäßig 30 Tage gespeichert.

## Protokolle für Cloud Foundry-Apps in Dedicated und Local anzeigen
{: #hybrid_apps_logs_dash}

Für die Apps, die Sie unter {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} ausführen, können Sie Protokolle prüfen.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um die Protokolle für Ihre Apps anzuzeigen.
1. Wählen Sie eine aktive App aus.
2. Klicken Sie auf **Protokolle**. In der Ansicht **Protokolle** können Sie die Protokolle für Ihre aktive App einsehen.
4. Klicken Sie auf die Schaltfläche **Erweiterte Ansicht**. Die **erweiterte Ansicht** zeigt mehr Details der Protokolle und verwendet hierzu Kibana, ein Visualisierungstool, das mithilfe von Protokollen und Daten mit Zeitmarken angepasste Visualisierungen erstellt. Weitere Informationen zur Verwendung der erweiterten Ansicht enthält die Dokumentation zu [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Als Nächstes können Sie ein Kibana-Dashboard anpassen. Weitere Informationen finden Sie unter [Protokolle in Kibana analysieren](../logging_view_kibana3.html#analyzing_logs_Kibana3).
