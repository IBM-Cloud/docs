---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Einführung in {{site.data.keyword.product-insights_short}}
{: #product-insights}

{{site.data.keyword.product-insights_full}} stellt eine Verbindung zu lokalen IBM Softwareprodukten her, um so einen produktübergreifenden Bestand einzurichten und Einblicke in und Informationen zu den Produktnutzungsmetriken bereitzustellen.

{:shortdesc}

Der Service {{site.data.keyword.product-insights_short}} wird innerhalb von IBM Bluemix ausgeführt; er empfängt Informationen aus den aktivierten lokalen IBM Softwareprodukten. Diese Informationen werden dann im Dashboard der Serviceinstanz angezeigt. Um den Service nutzen zu können, benötigen Sie ein Bluemix-Konto; außerdem müssen Sie den Service in einer Organisation und einem Bereich einrichten. Die Produkt- und Nutzungsinformationen für Ihre aktivierten lokalen Produkte werden im Gültigkeitsbereich bzw. im Kontext dieses eindeutigen Service sicher gespeichert und angezeigt. 

Tipp: Zur Vereinfachung können Sie anfänglich eine einzelne Serviceinstanz verwenden.

Führen Sie zur Einführung in {{site.data.keyword.product-insights_short}} die folgenden Schritte aus:

1.  Klicken Sie auf der Registerkarte **Verwalten** auf die Schaltfläche zum Registrieren eines Produkts, um eine Liste der unterstützten Produkte sowie den erforderlichen Versionsstand anzuzeigen. Zu jedem Produkttyp werden Anweisungen bereitgestellt, sodass Sie eine Verbindung zwischen Ihren lokalen Produktinstanzen und dem Service {{site.data.keyword.product-insights_short}} herstellen können. Falls dies erforderlich sein sollte, aktualisieren Sie Ihre aktivierten lokalen IBM Softwareprodukte auf den vorausgesetzten Mindestversionsstand. Für ein Produkt, für das ein unterstützter Mindestversionsstand erforderlich ist, müssen Sie das Fixpack oder den vorläufigen Fix installieren, um die Integration mit {{site.data.keyword.product-insights_short}} zu ermöglichen. 
2.  Stellen Sie eine Verbindung zwischen Ihren aktivierten lokalen IBM Softwareprodukten und Ihrem {{site.data.keyword.product-insights_short}}-Service her. Für den Konfigurationsprozess der einzelnen Produkte benötigen Sie die Serviceberechtigungsnachweise (d. h. den API-Schlüssel sowie den API-Host). Sie finden die Serviceberechtigungsnachweise auf der Registerkarte **Serviceberechtigungsnachweise** Ihres Service-Dashboards. 
3.  Nach der Aktivierung der einzelnen Produktinstanzen und nach dem Herstellen einer Verbindung zu diesen ist möglicherweise ein Start oder Neustart der Produkte oder Produktinstanzen erforderlich, damit diese dem Service {{site.data.keyword.product-insights_short}} die Produkt- und Nutzungsinformationen bereitstellen können. 

Details zu den Aktivierungsprodukten, dem für jedes Produkt erforderlichen Mindestversionsstand sowie zur Vorgehensweise beim Aktivieren der einzelnen Produkte zur Integration mit {{site.data.keyword.product-insights_short}} finden Sie bei der [technischen Community](https://developer.ibm.com/product-insights/) zu {{site.data.keyword.product-insights_full}}.

Sie können Ihren Bestand anzeigen, indem Sie die Option **Verwalten** im Service-Dashboard auswählen.  

* Im Service-Dashboard werden die Namen der Produkte, zu denen eine Verbindung hergestellt wurde, im Fenster **Produkte** aufgeführt. 
* Wählen Sie die Option **Alle anzeigen** aus, um alle Produktinstanzen anzuzeigen. Um die Produktinstanzen für ein Produkt anzuzeigen, wählen Sie das Produkt im Fenster **Produkte** aus; sie werden dann im Fenster **Instanzen** angezeigt.
* Wählen Sie zum Anzeigen der Details einer einzelnen Produktinstanz diese Produktinstanz im Fenster **Instanzen** aus. Das Fenster **Details** wird dann mit diesen Angaben gefüllt. Im Fenster **Details** werden Details der Produktinstanz sowie die Nutzungsinformationen angezeigt, die von der Instanz gesendet wurden.
* Auf der Registerkarte **Nutzung** werden Informationen zur Produktnutzung im grafischen Format angezeigt. In Abhängigkeit von dem Produkt können Sie den Typ von Informationen, die Sie anzeigen möchten, sowie den Stichprobenzeitraum angeben.
* Auf der Registerkarte **Details** werden die Produktinstanzinformationen angezeigt; dazu gehören auch die Produktinformationen, die Umgebungsinformationen sowie die Komponenteninformationen.
* Auf der Registerkarte **Services** der Registerkarte **Advisor** werden Details zu zusätzlichen Services bereitgestellt, die in Bezug auf die aktuelle Produktinstanz von Nutzen sein können. Auf der Registerkarte mit den Aktualisierungen werden Informationen zum Versionsstand der Produktinstanz sowie zu dessen Aktualität angegeben.










