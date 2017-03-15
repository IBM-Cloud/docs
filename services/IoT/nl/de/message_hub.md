---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Archivierungsfunktion mithilfe von {{site.data.keyword.messagehub}} verbinden und konfigurieren  
{: #messagehub_main}

Durch eine Verbindung zwischen {{site.data.keyword.messagehub_full}} und {{site.data.keyword.iot_short}} wird ein skalierbarer Nachrichtenbus mit hohem Durchsatz für die Speicherung archivierter Daten bereitgestellt. {{site.data.keyword.messagehub}} basiert auf Apache Kafka, das ein Open-Source-Nachrichtenübertragungssystem mit hohem Durchsatz ist, das eine Plattform mit kurzer Latenzzeit zum Handhaben von Feeds mit Echtzeitdaten bietet.

## Vorbereitende Schritte  
{: #byb}

Führen Sie vor dem Herstellen einer Verbindung von {{site.data.keyword.messagehub}} zu Ihrem {{site.data.keyword.iot_short}}-Service folgende Tasks aus:

- Richten Sie {{site.data.keyword.messagehub}} mithilfe des {{site.data.keyword.Bluemix_notm}}-Katalogs im selben {{site.data.keyword.Bluemix_notm}}-Bereich ein, in dem auch {{site.data.keyword.iot_short_notm}} vorhanden ist. Weitere Informationen zu {{site.data.keyword.messagehub}} finden Sie in [Einführung in {{site.data.keyword.messagehub}}](https://console.{DomainName}/docs/services/MessageHub/index.html).

- Stellen Sie sicher, dass Sie innerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation über Entwicklerberechtigungen verfügen und dass Sie über {{site.data.keyword.Bluemix_notm}} angemeldet sind. Wenn Sie nicht über {{site.data.keyword.Bluemix_notm}} angemeldet sind oder innerhalb dieser {{site.data.keyword.Bluemix_notm}}-Organisation nicht über Entwicklerberechtigungen verfügen, können Sie die Bindung zwischen {{site.data.keyword.messagehub}} und {{site.data.keyword.iot_short_notm}} nicht autorisieren.

## Verbindung herstellen

Gehen Sie wie folgt vor, um {{site.data.keyword.messagehub}} für die Speicherung von archivierten Daten zu verbinden:

1. Klicken Sie in Ihrem {{site.data.keyword.iot_short}}-Dashboard in der Navigationsleiste auf **Erweiterungen**.
2. Klicken Sie auf der Kachel für die Archivdatenspeicherung auf **Einrichten**.
4. Wählen Sie den {{site.data.keyword.messagehub}}-Service aus, für den Sie eine Verbindung herstellen möchten.  
Alle verfügbaren {{site.data.keyword.messagehub}}-Services, die sich innerhalb desselben {{site.data.keyword.Bluemix_notm}}-Bereichs wie Ihr {{site.data.keyword.iot_short}}-Service befinden, werden im Abschnitt 'Speicherung archivierter Daten konfigurieren' aufgelistet.
5. Wählen Sie die Konfigurationsoptionen für {{site.data.keyword.messagehub}} aus:
 1. Wählen Sie eine Zeitzone aus.  
 Die Zeitmarken der an {{site.data.keyword.messagehub}} gesendeten Gerätedaten werden in die ausgewählte Zeitzone konvertiert.
 2. Wählen Sie ein Standardthema aus.  
 Geräteereignisse werden an das Standardthema gesendet, sofern ein solches hier definiert ist. Zum Verwenden von Themazuordnungen mit höherer Granularität lassen Sie das Standardthema leer und fügen Sie angepasste Weiterleitungsregeln hinzu.
 3. Optional: Geben Sie angepasste Weiterleitungsregeln an.  
 Geben Sie zusätzliche Regeln für das Weiterleiten von Geräteereignissen an. Nur Ereignisse, die mit den angepassten Weiterleitungsregeln übereinstimmen, werden weitergeleitet.  
 **Hinweis:** Ein Ereignis kann mit mehreren Weiterleitungsregeln übereinstimmen und an mehrere {{site.data.keyword.messagehub}}-Themen weitergeleitet werden.
 4. Optional: Konfigurieren Sie Themen.  
 Zum Erstellen der Themen mit mehr als den standardmäßigen zwei Partitionen können Sie die Partitionskonfiguration angeben.
 5. Klicken Sie auf **Fertig**.
5. Klicken Sie auf **Berechtigen**.
6. Klicken Sie im Dialogfeld 'Berechtigung' auf die Option **Bestätigen**.

Ihre Gerätedaten werden nun in Ihrer {{site.data.keyword.messagehub}}-Instanz gespeichert.
