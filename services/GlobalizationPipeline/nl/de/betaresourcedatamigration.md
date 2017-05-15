---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ressourcendaten aus Betaversion migrieren
{: #globalizationpipeline_betaresourcedatamigration}

*Letzte Aktualisierung: 14. Oktober 2016*
{: .last-updated}

Die Betaversion von {{site.data.keyword.GlobalizationPipeline_full}} steht nach dem Release der GA-Version (GA, General Announcement) nur noch eine bestimmte Zeitdauer zur Verfügung. Benutzerdaten in Instanzen der Betaversion werden nicht in die GA-Serviceinstanzen verschoben. Um die Daten nach dem GA beizubehalten, können Sie Ressourcendaten in Dateien exportieren und anschließend in die neue Instanz importieren. Bitte beachten Sie, dass Sie diese Operation nicht mithilfe des Service-Dashboards ausführen können. Auch der Export von Daten in eines der Ressourcendateiformate führt nicht dazu, dass andere Metadaten, die zu diesen Ressourcendaten gehören, beibehalten werden.

Um die Datenmigration von einer Betaversion zu einer GA-Version zu unterstützen, wurde ein Feature zum Java-Befehlszeilentool von {{site.data.keyword.GlobalizationPipeline_short}} hinzugefügt. Die Quelle des Tools ist unter https://github.com/IBM-Bluemix/gp-java-tools gehostet und das zugehörige Binärrelease steht ebenfalls im github-Repository zur Verfügung. Der letzte Entwicklungssnapshot wurde veröffentlicht. [Download.](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

Das Tool verwendet eine REST-API, die nach der Betaversion für ***das Hochladen von Ressourceneinträgen*** verbessert wurde. Daher muss die Zielserviceinstanz die GA-Version sein. 
* Quelle: Beta- oder GA-Version
* Ziel: Nur GA-Version

Um alle Bundledaten in einer Globalisierungsserviceinstanz in eine andere Instanz zu kopieren, verwenden Sie den unten stehenden Befehl:

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url` und andere Parameterwerte befinden sich in den Berechtigungsnachweisen für die Quelle bzw. das Ziel des Service. Zum Beispiel: 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
Ferner wird die gesamte GP-CLI aktualisiert, um die Berechtigungsnachweise im JSON-Format zusätzlich zu einzelnen Optionen `(-s / -i / -u / -p)` zu unterstützen. Sie können eine JSON-Datei mit einem ähnlichen Inhalt wie unten erstellen: 

creds.json 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"

} 
```
Anschließend können Sie die Datei durch `-j <json-file>` angeben. Im Befehl `copy/copy-all-bundles` können Sie folgende Zeile ersetzen:

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

durch

`-j creds.json `
 
Alternativ können Sie Bundle von einer Position mithilfe des folgenden Befehls an eine andere Position kopieren: 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**Hinweis:** Sie können zwei weitere Parameter: `-b <source-bundle-id>` und `-d <dest-bundle-id>` zusätzlich zu den Parametern zum Kopieren aller Bundle (copy-all-bundles) verwenden. Dieser Befehl kann verwendet werden, um ein Bundle innerhalb derselben Instanz zu kopieren. In diesem Fall können Sie die Zielparameter der Berechtigungsnachweise `(--dest-*)` weglassen.


Die Befehle oben extrahieren vorhandene Bundledaten und Ressourceneintragsdaten und laden diese an die neue Position hoch. Während dieses Vorgangs werden einige Felder, die vom REST-Server gesteuert werden, aktualisiert. (Dazu gehören die Felder updatedBy/updatedAt). Da diese Befehle die Servicebindung und die Konfigurationsdaten nicht kopieren, müssen Sie möglicherweise die MT-Services in der Zielinstanz konfigurieren.


Die Betaversion unterstützt zum Beispiel die Übersetzung von Arabisch durch Watson Language Translator. In der GA-Version wird die Übersetzung von Arabisch nicht mehr kostenlos angeboten. Wenn Sie Daten der Betaversion in die neue GA-Instanz kopieren, werden bereits übersetzte arabische Inhalte beibehalten. Eine Änderung der Quellensprache führt nicht automatisch dazu, dass Arabisch übersetzt wird. Es sei denn, Sie konfigurieren die Watson-Bindung, um die Übersetzung von Arabisch zu aktivieren. Dies trifft auch zu, wenn die Quelleninstanz die GA-Version ist. Eine externe MT-Servicebindung ist für die GP-Instanz spezifisch. Die Bindung/Konfiguration von anderen Instanzen wird nicht automatisch portiert. 

