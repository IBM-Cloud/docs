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

# Einführung in Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Mit einem umfassenden ANSI SQL 99-Subset und einem umfangreichen Subset an eigenen Erweiterungen wie JSON-Dokument, Volltextsuche und aktualisierbaren Ansichten, bietet MySQL Anwendungsentwicklern eine breite Palette zur Nutzung ihrer Anwendungen. Administratoren steht außerdem eine breite Auswahl an Datenbank-Management-Tools zur Verfügung, die mit MySQL funktionieren. Mithilfe von {{site.data.keyword.composeForMySQL_full}} werden die Funktionen von MySQL dahingehend erweitert, dass die Verwaltung für Sie übernommen wird und Sie ein einfaches Bereitstellungssystem zur automatischen Skalierung für eine hohe Verfügbarkeit und Redundanz sowie automatisierte Backups angeboten bekommen.
{:shortdesc}

**Anmerkung:** {{site.data.keyword.composeForMySQL_full}} gewährt keinen Zugriff auf die Compose-Benutzerschnittstelle. Weitere Details finden Sie unter [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support).

Führen Sie zum Einstieg in {{site.data.keyword.composeForMySQL}} die folgenden Schritte aus:

1. [Erstellen Sie eine {{site.data.keyword.composeForMySQL}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Wenn Sie eine Instanz des Service erstellen, wählen Sie sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis aus. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden.  Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt "Verfügbare Berechtigungsnachweise" aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForMySQL}}-Service her.

  Um eine Anwendung mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden.

  Laden Sie die Beispielanwendung [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung der Bluemix-Konsole auf **App anzeigen**.

  Die Beispielanwendung veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForMySQL}}-Service.


## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `mysql`.
`name`|Der Name der Datenbankimplementierung.
`uri_cli`|Eine `mysql`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Das Zertifikat ist base64-codiert.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`uri`|Die bei der Herstellung einer Verbindung zum Service verwendete URI, die Folgendes enthält: Schema (`mysql:`), Benutzername und Kennwort des Administrators, Hostname des Servers sowie die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, und der vhost-Name.
{: caption="Table 1. {{site.data.keyword.composeForMySQL}} - Berechtigungsnachweise" caption-side="top"}


# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
* [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
