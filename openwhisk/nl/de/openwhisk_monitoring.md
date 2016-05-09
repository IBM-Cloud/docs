---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Aktivität mit dem {{site.data.keyword.openwhisk_short}}-Dashboard überwachen
*Letzte Aktualisierung: 9. Februar 2016*

Das [{{site.data.keyword.openwhisk}}-Dashboard](https://{DomainName}/whisk/dashboard/) stellt eine grafische Zusammenfassung Ihrer Aktivität bereit. Verwenden Sie das Dashboard, um die Leistung und den Status Ihrer {{site.data.keyword.openwhisk_short}}-Aktionen zu ermitteln. 
{:shortdesc}

Sie können jeder Zeit auf die Option zum erneuten Laden ('Reload') klicken, um das Dashboard mit den neuesten Aktivierungsprotokolldaten zu aktualisieren.

## Aktivitätenzusammenfassung
{: #summary}

Die Ansicht der Aktivitätszusammenfassung stellt eine allgemeine Zusammenfassung Ihrer {{site.data.keyword.openwhisk_short}}-Umgebung bereit. Verwenden Sie die Ansicht **Aktivitätenzusammenfassung** zur Überwachung des allgemeinen Zustands und der Leistung Ihres für {{site.data.keyword.openwhisk_short}} eingerichteten Service. Die Metriken in dieser Ansicht bieten Ihnen die folgenden Möglichkeiten:
* Sie können die Nutzungsrate der für {{site.data.keyword.openwhisk_short}} eingerichteten Aktionen Ihres Service ermitteln, indem Sie die Häufigkeit anzeigen, mit der sie aufgerufen wurden.
* Sie können die Gesamtrate von Fehlern über alle Aktionen hinweg ermitteln. Wenn Sie einen Fehler erkennen, können Sie die Services oder Aktionen eingrenzen, die Fehler hatten, indem Sie die Ansicht **Aktivitätenhistogramm** anzeigen. Sie können die Fehler selbst eingrenzen, indem Sie das **Aktivitätenprotokoll** anzeigen.
* Sie können die Leistung Ihrer Aktionen ermitteln, indem Sie die durchschnittliche Ausführungszeit anzeigen, die mit jeder Aktion verbunden ist. 

<!-- For tips on improving performance, see troubleshooting? -->

## Aktivitätenzeitachse
{: #timeline}

Die Ansicht **Aktivitätenzeitachse** zeigt ein vertikales Balkendiagramm an, um die Aktivitäten der vergangenen und gegenwärtigen Aktionen darzustellen. Die Farbe Rot weist auf Fehler in den betreffenden Aktionen hin. Korrelieren Sie diese Ansicht mit dem **Aktivitätenprotokoll**, um weitere Details zu Fehlern zu ermitteln.

## Aktivitätenhistogramm
{: #histogram}

Die Ansicht **Aktivitätenhistogramm** zeigt ein horizontales Diagramm an, um die Aktivitäten der vergangenen und gegenwärtigen Aktionen darzustellen. Die Farbe Rot weist auf Fehler in den betreffenden Aktionen hin. Korrelieren Sie diese Ansicht mit dem **Aktivitätenprotokoll**, um weitere Details zu Fehlern zu ermitteln.

## Aktivitätenprotokoll
{: #log}

Diese Ansicht zeigt eine formatierte Version des Aktivierungsprotokolls an. Sie zeigt die Details zu jeder Aktivierung an, prüft jedoch einmal pro Minute durch Polling auf neue Aktivierungen. Klicken Sie auf eine Aktion, um ein detailliertes Protokoll anzuzeigen. 
**Hinweis:** Wenn Sie Ausgabe, die im Aktivitätenprotokoll angezeigt wird, über die CLI abrufen wollen, verwenden Sie den folgenden Befehl: 

  ```
  wsk activation poll
  ```
  {: pre} 

## Filteroptionen
{: #filtering}

Wählen Sie das gewünschte Aktionsprotokoll aus und wählen Sie den Zeitrahmen der protokollierten Aktivität aus. 

**Hinweis:** Diese Filter werden auf alle Ansichten im Dashboard angewendet.
