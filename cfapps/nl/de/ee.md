---

 

copyright:

  years: 2015，20166

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Szenario: End-to-End-Entwicklung
{: #ee}

*Letzte Aktualisierung: 18. April 2016*

Sie können die {{site.data.keyword.Bluemix}}-Benutzerschnittstelle, -Plattform und eine Auswahl von Tools verwenden, wenn Sie Ihre Apps erstellen, ausführen und bereitstellen. Befolgen Sie dieses umfassende Entwicklungsszenario, um zu beginnen.
{:shortdesc}

## Registrieren
{: #ee_start}

Bevor Sie beginnen können, müssen Sie sich unter [https://console.ng.bluemix.net/](https://console.ng.bluemix.net/) für eine IBM ID registrieren. Anschließend melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und starten Ihre kostenlose 30-tägige Testversion. {{site.data.keyword.Bluemix_notm}} stellt im Rahmen Ihrer kostenlosen Testversion ein Volumen von 2 GB Laufzeitspeicher und 10 Serviceinstanzen bereit.

## Web-App mithilfe der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle erstellen
{: #ee_appui}

Nachdem Sie sich registriert haben, beginnen Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle mit dem Erstellen Ihrer ersten App.

In {{site.data.keyword.Bluemix_notm}} werden Apps Organisationen und Bereichen zugeordnet. Eine Organisation wird von mehreren Mitarbeitern verwendet, die ihr Eigner sind. Zunächst erhalten Sie eine Standardorganisation, die nach Ihrem Benutzernamen benannt ist, und Sie sind der einzige Mitarbeiter. Sie erhalten auch einen Bereich innerhalb dieser Organisation. Der Bereich ist eine Umgebung, in der Ihre Apps ausgeführt werden. Beispiel: Sie können einen Entwicklungsbereich als Entwicklungsumgebung verwenden, einen Testbereich als Testumgebung und einen Produktionsbereich als Produktionsumgebung. Darüber hinaus gehört jede Umgebung zu einer Region. Mit {{site.data.keyword.Bluemix_notm}} können Sie Ihre Anwendungen in einer bestimmten geografischen Region bereitstellen, um die Netzlatenz zu verringern und den Datenschutz und die Verfügbarkeit zu verbessern. Details finden Sie unter 'Regionen'.

In diesem Szenario möchten Sie mithilfe von Node.js eine Web-App entwickeln. Sie befinden sich in den USA, ebenso wie die meisten Ihrer App-Benutzer. Sie entscheiden sich, Ihre App in der Nähe Ihrer Benutzerbasis zu erstellen und auszuführen, sodass Sie von der geringeren Netzlatenz profitieren können. Klicken Sie nach dem Anmelden bei {{site.data.keyword.Bluemix_notm}} in der oberen, rechten Ecke auf Ihren Kontonamen und wählen Sie die Region **Vereinigte Staaten (Süden)** aus. Führen Sie anschließend die folgenden Schritte zum Erstellen einer App aus:

  1. Klicken Sie auf die Schaltfläche mit dem Pluszeichen.
  2. Wählen Sie **Compute**>**CF-Anwendungen**>**SDK for Node.js** aus.
  3. Geben Sie einen eindeutigen Namen für Ihre App ein. Zum Beispiel: TestNode. Klicken Sie anschließend auf **Erstellen**. Der Name der App muss in der gesamten {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.
  
Jetzt werden die **Coding beginnen**-Anweisungen angezeigt. Sie können die Anweisungen befolgen, um den Startercode von TestNode herunterzuladen, zu ändern und bereitzustellen.

Der App ist standardmäßig ein Kontingent von 1 Instanz und 512 MB Speicher zugewiesen. Sie können den
Speicher vergrößern oder weitere Instanzen hinzufügen, um für Ihre App eine hohe Verfügbarkeit zu erreichen, z. B. 3 Instanzen mit jeweils 1 GB Speicher. Klicken Sie auf **App-Übersicht anzeigen**, um Ihr
Kontingent an App-Instanzen und Speicher anzugeben. Beispiel: Geben Sie als Kontingent 3 Instanzen und 1 GB Speicher
ein und klicken Sie auf **Speichern**. Sie können auch die Dateien, Protokolle und
Umgebungsvariablen anzeigen, um Probleme zu beheben.

## Service mithilfe der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle binden
{: #ee_bindui}

Nachdem Sie Ihre App erstellt haben, stellen Sie mit der App eine Verbindung zur Datenbank her. Auf diese
Weise können Sie die App-Daten mithilfe der Datenbankabfragesprache speichern und beobachten. In diesem Szenario
entscheiden Sie sich dafür, den Service {{site.data.keyword.cloudant}}, der
von {{site.data.keyword.Bluemix_notm}} bereitgestellt wird, zu verwenden.

Um Services in der Anwendung verwenden zu können, müssen Sie eine entsprechende Serviceinstanz erstellen und Ihre Anwendung an die Serviceinstanz binden, indem Sie die folgenden Schritte ausführen:
  1. Klicken Sie auf der Übersichtsseite der App auf **Service oder API hinzufügen**.
  2. Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Katalog den Service {{site.data.keyword.cloudant}} aus.
  3. Geben Sie einen eindeutigen Namen für die Serviceinstanz ein oder verwenden Sie den Standardnamen, der von {{site.data.keyword.Bluemix_notm}} generiert wird, und klicken Sie auf **Erstellen**.
  4. Das Fenster 'Erneutes Staging für Anwendung' wird angezeigt. Klicken Sie auf **Erneutes Staging**, um für Ihre App ein erneutes Staging durchzuführen.
  
Nun wird Ihre App an den Service {{site.data.keyword.cloudant}} gebunden. In der Umgebungsvariablen VCAP_SERVICES finden Sie alle erforderlichen Daten für die Kommunikation zwischen der Anwendung und der Serviceinstanz. Beispiel: Da {{site.data.keyword.Bluemix_notm}} mehrere Anwendungen auf derselben virtuellen Maschine hostet, können Anwendungen
nicht dieselbe HTTP-Portnummer verwenden, um eingehende Anforderungen zu empfangen. Um Konflikte zu vermeiden, erhält jede Anwendung eine eindeutige Portnummer. Diese Portnummer wird über die Variable VCAP_APP_PORT zur Verfügung gestellt.

Klicken Sie auf der Übersichtsseite der App auf **Umgebungsvariablen**, um die gesamte VCAP_SERVICES-Liste anzuzeigen und weitere Informationen zu erhalten:
```
{
   "cloudantNoSQLDB": [
      {
         "name": "Cloudant NoSQL DB-tx",
         "label": "cloudantNoSQLDB",
         "plan": "Shared",
         "credentials": {
            "username": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix",
            "password": "b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424",
            "host": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com",
            "port": 443,
            "url": "https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com"
         }
      }
   ]
}
```

**Hinweis:** Bei dieser Umgebungsvariablen handelt es sich um die Serialisierung eines JSON-Objekts mit einem Eintrag pro Serviceinstanz, an die die App gebunden ist. Die Datenmenge und der Datentyp, die von den einzelnen Serviceinstanzen bereitgestellt werden, hängen
vom jeweiligen Service ab. Wenn Ihre App keinen Service verwendet, ist VCAP_SERVICES ein leeres
JSON-Objekt. Diese Umgebungsvariable wird nur verwendet, wenn Sie Ihrer App einen Service hinzufügen.

## App mithilfe der Befehlszeilenschnittstelle 'cf' erstellen
{: #ee_cf}

In {{site.data.keyword.Bluemix_notm}} werden verschiedene Tools bereitgestellt, mit denen Sie mit dem Codieren Ihrer App beginnen können, zum Beispiel die Befehlszeilenschnittstelle 'cf' und Eclipse-Tools. Sie können die Befehlszeilenschnittstelle 'cf' auswählen, um mit dem Codieren Ihrer App
TestNode zu beginnen.

  1. Laden Sie als erstes den Code Ihrer App herunter und entwickeln Sie ihn.
  
    1. Wechseln Sie zur Seite 'Coding beginnen' Ihrer App. klicken Sie auf die Schaltfläche **Startercode herunterladen**, um den Code für Ihre App herunterzuladen.
    2. Extrahieren Sie die heruntergeladene Datei in ein Verzeichnis, z. B. `C:\test`.
    3. Entwickeln Sie den Code mit Ihrer lokalen integrierten Entwicklungsumgebung.
	
  2. Installieren Sie die Befehlszeilenschnittstelle (Command Line Interface, CLI) **cf**.
  
    1. Laden Sie das Installationsprogramm für das Befehlszeilentool 'cf' für Ihr Betriebssystem herunter.
    2. Befolgen Sie die Anweisungen im Assistenten des Tools, um die Installation auszuführen.
    3. Überprüfen Sie mithilfe des Befehls **cf -v** die Version der Befehlszeilenschnittstelle 'cf'. Beispiel:
	
	```
	cf -v
	```
	
    **Anforderung:** Vergewissern Sie sich, dass Sie stets die neueste Version des Befehlszeilentools 'cf' verwenden.
  3. Nach der Installation der Befehlszeilenschnittstelle **cf** müssen Sie angeben, mit welcher {{site.data.keyword.Bluemix_notm}}-Region Sie arbeiten wollen, indem Sie den Befehl **cf api** verwenden. Die Befehlszeilenschnittstelle **cf** verwendet *https://api.Bluemix-URL*, wobei *Bluemix-URL* die URL der Region ist. Die URL der Region 'Vereinigte Staaten (Süden)' lautet: {{Domain}}. Geben Sie den folgenden Befehl ein, um eine Verbindung zu
{{site.data.keyword.Bluemix_notm}} herzustellen:
  
  ```
  cf api https://api.ng.bluemix.net
  ```
  
  Weitere Informationen zum Herstellen einer Verbindung zu anderen {{site.data.keyword.Bluemix_notm}}-Regionen finden Sie im Abschnitt zu den {{site.data.keyword.Bluemix_notm}}-Regionen. Nach Angabe der {{site.data.keyword.Bluemix_notm}}-Region werden die von Ihnen angegebenen Positionsinformationen
gespeichert.
  
  4. Melden Sie sich als Nächstes bei {{site.data.keyword.Bluemix_notm}} an, indem Sie den Befehl 'cf login' verwenden.
  
  ```
  cf login -u eigene_benutzer-id -p ***** -o name_der_eigenen_organisation -s name_des_eigenen_bereichs
  ```
  
  5. Nachdem Sie sich bei {{site.data.keyword.Bluemix_notm}} angemeldet haben, können Sie Ihre App in {{site.data.keyword.Bluemix_notm}} bereitstellen. Geben Sie im Verzeichnis (`C:\test`) der App den folgenden Befehl ein:
  
  ```
  cf push TestNode
  ```
  
  Weitere Informationen zum Befehl **cf push** finden Sie unter 'Anwendung hochladen'.
  
  6. Nun können Sie auf die App zugreifen, indem Sie die folgende Anwendungs-URL in einen Browser eingeben:
  ```
  http://TestNode.mybluemix.net
  ```

Sie können auch andere Tools zum Erstellen der App verwenden, z. B. Eclipse-Tools. Weitere Informationen finden Sie auf der Seite 'Coding beginnen' Ihrer App in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle.

## Service mithilfe der Befehlszeilenschnittstelle 'cf' binden
{: #ee_cfbind}

In {{site.data.keyword.Bluemix_notm}} können Sie mithilfe der Bluemix-Benutzerschnittstelle einen Service hinzufügen, wie bereits in diesem Szenario beschrieben. Sie können
einen Service aber auch mithilfe der Befehlszeilenschnittstelle **cf** binden. In diesem Beispiel möchten Sie den
Service {{site.data.keyword.cloudant}} Ihrer App TestNode
mithilfe der Befehlszeilenschnittstelle 'cf' hinzufügen.

Um den Service {{site.data.keyword.cloudant}} in der App verwenden zu können, müssen Sie eine Cloudant-Serviceinstanz erstellen und Ihre App an die Serviceinstanz binden, bevor Sie die Serviceinstanz anschließend verwenden. Dasselbe Verfahren gilt auch für alle anderen Services.

  1. Erstellen Sie eine Cloudant NoSQL DB-Serviceinstanz.
  
  Verwenden Sie den Befehl 'cf create-service', um eine neue Instanz eines Service zu erstellen. Beispiel:
  
  ```
  cf create-service cloudantNoSQLDB Shared cloudant100
  ```
  
  Sie können auch den Befehl 'cf services' verwenden, um eine Liste der Serviceinstanzen anzuzeigen, die Sie erstellt haben.
  
  ```
  cf services
  ```
  
  Nach Erstellung einer Serviceinstanz ist diese Instanz für alle Ihre Anwendungen verfügbar und kann entsprechend gebunden und verwendet werden.
  
  2. Binden Sie die Serviceinstanz an Ihre App.
  
  Um eine Serviceinstanz verwenden zu können, müssen Sie die Instanz an Ihre Anwendung binden. Verwenden Sie den Befehl
'cf bind-service', um eine Serviceinstanz an eine Anwendung zu binden, indem Sie den Anwendungsnamen und die erstellte Serviceinstanz
angeben.
  
  ```
  cf bind-service TestNode cloudant100
  ```
  
  Durch das Binden einer Serviceinstanz an eine Anwendung kann {{site.data.keyword.Bluemix_notm}} mit dem Service kommunizieren und angeben, dass eine neue Anwendung mit der betreffenden Serviceinstanz kommunizieren wird. Die Verarbeitung der Anwendung und der Serviceinstanz durch
{{site.data.keyword.Bluemix_notm}} während der Bindung kann je nach Service unterschiedlich
sein. Beispiel: Einige Services erstellen unter Umständen für jede Anwendung, die mit der Serviceinstanz kommuniziert, einen neuen Tenant. Der Service gibt eine
Rückmeldung an {{site.data.keyword.Bluemix_notm}} mit Informationen wie beispielsweise den Berechtigungsnachweisen, die
an die Anwendung übergeben werden müssen, um die Kommunikation zwischen der Anwendung und dem Service zu ermöglichen.

  **Hinweis:** Ist die Anwendung gerade aktiv, wenn sie an eine Serviceinstanz gebunden wird, so wird die Umgebungsvariable
VCAP_SERVICES erst nach einem Neustart der Anwendung aktualisiert. Verwenden Sie den Befehl
'cf restart', um Ihre Anwendung erneut zu starten.
  
  3. Verwenden Sie die Serviceinstanz.
  
  In diesem Szenario enthält die Umgebungsvariable VCAP_SERVICES Informationen wie beispielsweise die folgenden Elemente, die eine Anwendung
verwenden kann, um eine Verbindung zu dieser Instanz von {{site.data.keyword.cloudant}} herzustellen:
  
  <dl><dt>username (Benutzername)</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password (Kennwort)</dt>
  <dd>b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424</dd>
  <dt>url (URL)</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dt></dl>
  
  Beispiel: Ihre Node.js-App könnte wie folgt auf diese Informationen zugreifen:
  ```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['"cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```
  
  **Hinweis:** Wie der Beispielcode zeigt, kann zur Herstellung einer Verbindung mit einer Serviceinstanz von {{site.data.keyword.cloudant}} zunächst überprüft werden, ob die
Umgebungsvariable VCAP_SERVICES vorhanden ist. Ist die Umgebungsvariable vorhanden, kann die
Anwendung die Eigenschaften der Variablen 'cloudant' verwenden, um auf die Datenbank zuzugreifen. Ist
die Umgebungsvariable VCAP_SERVICES hingegen nicht vorhanden, wird die lokale Serviceinstanz von {{site.data.keyword.cloudant}} mit den bereitgestellten Standardwerten verwendet.
  
  4. Interagieren Sie mit der Serviceinstanz.
  
  Sie können mit einer Serviceinstanz interagieren, indem Sie die entsprechenden Berechtigungsnachweisinformationen verwenden. Zu den möglichen Aktionen gehören Lese-, Schreib- und Aktualisierungsvorgänge. Das folgende Beispiel veranschaulicht, wie ein JSON-Objekt in die Serviceinstanz von
{{site.data.keyword.cloudant}} eingefügt wird:
  ```
  // Neue Nachricht erstellen
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // Nachrichtendatensatz erstellen
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```
  
  5. **Optional:** Heben Sie die Bindung einer Serviceinstanz auf oder löschen Sie die Serviceinstanz.
  
  Möglicherweise möchten Sie eine Serviceinstanz löschen oder ihre Bindung aufheben, wenn sie nicht mehr verwendet wird oder Sie Speicher freigeben möchten. Um die Bindung einer Serviceinstanz an Ihre App aufzuheben, verwenden Sie den Befehl
**cf unbind-service**; um eine Serviceinstanz zu löschen, verwenden Sie den Befehl **cf delete-service**.

  Weitere Informationen zu Services finden Sie unter 'Services'. Weitere Informationen zu den **cf**-Optionen, die Sie zum Verwalten Ihrer Anwendungen in der
{{site.data.keyword.Bluemix_notm}}-Umgebung verwenden können, erhalten Sie, indem Sie den Befehl **cf --help** in der Befehlszeilenschnittstelle **cf** ausgeben.

  **Hinweis:** Vergewissern Sie sich vor dem Löschen einer Serviceinstanz, dass Sie diese Serviceinstanz auch tatsächlich nicht mehr benötigen. Beim Löschen einer Serviceinstanz werden sämtliche Daten entfernt, die der betreffenden Instanz des Service zugeordnet sind. Die Umgebungsvariable
VCAP_SERVICES von Anwendungen, die an einen gelöschten Service gebunden sind, kann erst nach einem Neustart der betreffenden Anwendung
aktualisiert werden.

## App-Kosten berechnen
{: #ee_billing}

Ihre kostenlose 30-tägige Testversion ist abgelaufen, aber Sie möchten {{site.data.keyword.Bluemix_notm}} weiterhin verwenden. Sie müssen Ihre Kreditkarteninformationen für ein nutzungsorientiertes Konto oder ein Subskriptionskonto
hinzufügen, um {{site.data.keyword.Bluemix_notm}} weiterhin nutzen zu können. Jedoch stellt {{site.data.keyword.Bluemix_notm}} weiterhin Gratisleistungen für die meisten Laufzeit-Frameworks und Services bereit, selbst wenn Sie das Konto in ein Zahlungskonto umwandeln. Sie müssen keine Gebühr an
{{site.data.keyword.Bluemix_notm}} zahlen, es sei denn, die Nutzung übersteigt das kostenlose Kontingent.

{{site.data.keyword.Bluemix_notm}} stellt einen Schätzer und eine Berechnungsfunktion zum Anzeigen Ihrer App-Kosten zur Verfügung. Sie können die Kosten von TestNode folgendermaßen anzeigen:

  * Klicken Sie in Ihrem Dashboard auf TestNode. Klicken Sie anschließend auf der Übersichtsseite auf **Kosten dieser Anwendung schätzen**, um den Preis für die Laufzeit **SDK for Node.js** und den monatlichen Gesamtpreis der App anzuzeigen.
  
  * Geben Sie alternativ auf der Seite 'Preisliste' die monatliche Nutzung
der Laufzeit und Services Ihrer App ein. Beispiel: 3 Instanzen von **SDK for Node.js** mit 1 GB Speicher pro Instanz. Der monatliche Preis wird berechnet und angezeigt.

Sie können die App-Kosten auch manuell berechnen, indem Sie die Preise der Laufzeiten und Services zusammenrechnen und die kostenlosen Gratisleistungen abziehen. Weitere Informationen finden Sie unter 'Kosten manuell schätzen'.

## Apps entfernen
{: #ee_removing}

Beim Erstellen immer weiterer Apps erreicht möglicherweise das Kontingent das zulässige Limit. Einige Apps, die Sie nicht mehr verwenden, können jedoch immer noch das Kontingent belegen. Es ist einfach, Apps zu löschen, um jederzeit Speicherplatz in
{{site.data.keyword.Bluemix_notm}} freizugeben.

Wechseln Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle auf die Übersichtsseite der App, klicken Sie auf das Symbol **Menü** und löschen Sie die App, die Sie nicht mehr benötigen. Sie können auch den Befehl **cf delete** zum Löschen von Apps verwenden.
