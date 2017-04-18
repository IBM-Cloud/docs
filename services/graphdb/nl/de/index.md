---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
Letzte Aktualisierung: 27. Juli 2016
{: .last-updated}

{{site.data.keyword.graphfull}} ist ein vollständig verwalteter Grafikdatenbankservice,
auf den über eine REST-basierte HTTP-API-Schnittstelle zugegriffen werden kann.
Mit diesem Service können Sie Ihre mobilen Anwendungen und Ihre Webanwendungen erstellen, für die Grafikdatenbankfunktionen erforderlich sind.
{:shortdesc}

{{site.data.keyword.graphfull}} basiert auf dem Stack [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;,
das für die Erstellung von leistungsfähigen Grafikanwendungen verwendet wird, die eine v3-kompatible API nutzen.
Mit dem Stack verfügen Sie über zusätzliche Flexibilität und zusätzliche Funktionen, deren Grundlage eine gewohnte Umgebung ist.
Mit dem {{site.data.keyword.Bluemix}}-Dashboard
können Sie den {{site.data.keyword.graphfull}}-Service problemlos mit Ihren {{site.data.keyword.Bluemix_short}}-Anwendungen integrieren.

Für die Arbeit mit {{site.data.keyword.graphfull}} stehen Ihnen zwei Möglichkeiten zur Verfügung:

*	Verwendung der vereinfachten {{site.data.keyword.graphfull}}-API-Befehle.
*	Verwendung der vollständigen Apache TinkerPop v3-Abfragesprache (Gremlin).

Die {{site.data.keyword.graphfull}}-Features stehen als API zur Verfügung; hierzu werden HTTP-REST-Endpunkte verwendet.
Diese Endpunkte sind eine einfache Möglichkeit, Ihre Anwendungen mit dem {{site.data.keyword.graphfull}}-Service zu verbinden und diesen zu verwenden;
hierzu werden über HTTP API-Anforderungen vorgenommen und Ergebnisse abgerufen.
Verwenden Sie die über die von Ihnen ausgewählte Anwendungsprogrammiersprache bereitgestellten HTTP-Funktionen, um auf die Endpunkte zuzugreifen.
Alternativ dazu können Sie hierfür eine Befehlsschnittstelle oder ein Script des Typs `curl` verwenden.
In der API-Referenz werden die unterschiedlichen vom Service {{site.data.keyword.graphfull}} bereitgestellten Funktionen
zusammen mit Beispielen für ihre Nutzung beschrieben.

Ihre Anwendung kann auch die Apache TinkerPop-Abfragesprache Gremlin
für Tasks verwenden,
die den {{site.data.keyword.graphfull}}-Service nutzen.
Nehmen Sie die Gremlin-Abfrage in ein JSON-Dokument auf
und übergeben Sie das Dokument anschließend an den Serviceendpunkt `/gremlin`.
Beispiele für die Verwendung von Gremlin mit {{site.data.keyword.graphfull}} sind in der vollständigen Dokumentation enthalten.

Führen Sie die folgenden Schritte für eine Einführung in den Service {{site.data.keyword.graphfull}} aus:

1.	[Erstellen Sie eine Instanz](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) des Service {{site.data.keyword.graphfull}}.
2.	Vermerken Sie die drei zentralen Werte, die bei der Erstellung der Instanz generiert werden. Die Werte sind auf der Registerkarte `Serviceberechtigungsnachweise` verfügbar, wenn Sie zuvor auf die Kachel für die Services geklickt haben.
	*	IBM Graph-Endpunkt: `apiURL`.
	*	Benutzername für die Serviceinstanz `Benutzername`.
	*	Kennwort für die Serviceinstanz `Kennwort`.
3.	Verwenden Sie für die {{site.data.keyword.graphfull}}-Tasks die drei zentralen Werte in Ihren Anwendungen oder Scripts. Beispiele sind in der vollständigen Dokumentation enthalten.

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Beispiele](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## API-Referenz
{: #api}

* [REST-API für IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Gremlin mit IBM Graph verwenden](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Zugehörige Links
{: #general}

* [Vollständige Dokumentation](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
