---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.composeForEtcd}}
{: #getting-started-with-compose-for-etcd}

"etcd" ist ein Schlüssel/Wert-Speicher mit den immer korrekten Daten, die Sie zum Koordinieren und Verwalten Ihres Server-Clusters für die Konfigurationsverwaltung für verteilte Server benötigen. "etcd" verwendet den RAFT-Datenkonsistenzalgorithmus zur Sicherstellung der Konsistenz in Ihrem Cluster. Er erzwingt die Reihenfolge der Operationen an den Daten, sodass jeder Knoten im Cluster auf demselben Weg zum selben Ergebnis kommt. {{site.data.keyword.composeForEtcd_full}} fügt automatische Sicherungen Ihrer Konfigurationsdaten durch, die in "etcd" gespeichert sind. Über eine intuitive Verwaltungsschnittstelle können Sie Ihre Bereitstellung mit Leichtigkeit überwachen, skalieren und verwalten.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForEtcd}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForEtcd}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForEtcd}}-Service her.

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForEtcd}}-Service.

Laden Sie die Beispiel-App [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**, um den Inhalt von *examples* anzuzeigen.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine App eine Verbindung zum geeigneten Server herstellt. Das Zertifikat ist base64-codiert. Vor seiner Verwendung muss der Schlüssel decodiert werden, wie in der Beispiel-App gezeigt.
`deployment_id`|Eine interne ID für den Service, wie in Compose erstellt.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `etcd`.
`name`|Der Name der Datenbankimplementierung.
`uri`|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. `uri` enthält das Schema (`amqps:), Administrator-Benutzernamen und Kennwort, den Hostnamen des Servers, die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, sowie den Namen des `virtuellen Hosts.
{: caption="Table 1. {{site.data.keyword.composeForEtcd}} - Berechtigungsnachweise" caption-side="top"}

# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
* [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
