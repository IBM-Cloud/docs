---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Dashboard für Serviceadministration
{: #service-dashboard}


Im Dashboard für Serviceadministration können Sie den Status einer {{site.data.keyword.geospatialshort_Geospatial}}-Serviceinstanz anzeigen und die Serviceinstanz stoppen bzw. erneut starten. Wenn Sie das Dashboard für Serviceadministration aufrufen möchten, klicken Sie auf die Kachel {{site.data.keyword.geospatialshort_Geospatial}} im {{site.data.keyword.geospatialshort_Geospatial}}-Dashboard. Wenn Sie die Beispielanwendung verwenden und die Serviceinstanz den Ereignisgrenzwert erreicht und stoppt wird, können Sie den Service erneut starten. Beim Stoppen des Service wird der Ereignisgrenzwert gelöscht. Das Empfangen der Ereignisse wird fortgesetzt, bis Sie den Service stoppen. Im Dashboard für Serviceadministration werden auch der Status der Serviceinstanz und ihre Statistikdaten angezeigt.
{:shortdesc}

##{{site.data.keyword.geospatialshort_Geospatial}} - Regionsüberprüfungen

Mit {{site.data.keyword.geospatialshort_Geospatial}} werden Geräte überwacht,
während diese aktiv sind, und zwar mittels Internet of Things. Jedes überwachte Gerät sendet Gerätenachrichten mit einer eindeutigen ID
sowie seiner aktuellen Position, die aus Breitengrad und Längengrad besteht. Die Geräteposition
wird mit den Koordinaten der einzelnen definierten geografischen Regionen abgeglichen. Der Service produziert dann
Ereignisse, sobald Geräte in eine bestimmte Region eintreten (Entry-Ereignis), aus einer bestimmten Region austreten (Exit-Ereignis) oder
sich in einer bestimmten Region aufhalten (Hangout-Ereignis).

Eine Regionsüberprüfung wird als Einheit zum Messen der Nutzung von {{site.data.keyword.geospatialfull}} verwendet. Für jede
Gerätenachricht wird eine einzige Regionsüberprüfung durchgeführt, wenn für die Region die Entry- und/oder die Exit-Erkennung
angegeben ist. Für jede
Gerätenachricht wird eine einzige Regionsüberprüfung durchgeführt, wenn für die Region die Hangout-Erkennung
angegeben ist. Sind keine Regionen definiert, wird für jede Gerätenachricht eine einzige Regionsüberprüfung
gezählt, wie wenn es 1 Region gäbe. Dies bedeutet, dass wenn Sie eine Überprüfung für 100 Regionen definiert haben (Entry, Exit und Hangout), eine einzige
Gerätenachricht 200 Regionsüberprüfungen produzieren würde.
