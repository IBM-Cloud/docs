---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Cloudant-Paket verwenden
{: #openwhisk_catalog_cloudant}
Das Paket `/whisk.system/cloudant` ermöglicht Ihnen die Arbeit mit einer Cloudant-Datenbank. Es enthält die folgenden Aktionen und Feeds.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | Paket | dbname, host, username, password | Dient zur Arbeit mit einer Cloudant-Datenbank. |
| `/whisk.system/cloudant/read` | Aktion | dbname, id | Liest ein Dokument aus einer Datenbank. |
| `/whisk.system/cloudant/write` | Aktion | dbname, overwrite, doc | Schreibt ein Dokument in eine Datenbank. |
| `/whisk.system/cloudant/changes` | Feed | dbname, maxTriggers | Aktiviert Auslöserereignisse bei Änderungen an einer Datenbank. |

In den folgenden Abschnitten werden die Einrichtung einer Cloudant-Datenbank, die Konfiguration eines zugeordneten Pakets sowie die Verwendung der Aktionen und Feeds im Paket `/whisk.system/cloudant` schrittweise erläutert.

## Cloudant-Datenbank in Bluemix einrichten
{: #openwhisk_catalog_cloudant_in}

Wenn Sie OpenWhisk über Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Cloudant-Serviceinstanzen. Verwenden Sie OpenWhisk und Cloudant nicht über Bluemix, fahren Sie mit dem nächsten Schritt fort.

1. Erstellen Sie eine Cloudant-Serviceinstanz in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).

  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.

2. Stellen Sie sicher, dass sich Ihre OpenWhisk-Befehlszeilenschnittstelle (CLI, Command-Line Interface) in dem Namensbereich befindet, der der Bluemix-Organisation und dem Bereich entspricht, die Sie im vorherigen Schritt verwendet haben.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Alternativ können Sie mit dem Befehl `wsk property set --namespace` den Namensbereich mithilfe einer Liste der für sie zugänglichen Namensbereiche festlegen.

3. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Cloudant-Serviceinstanz, die Sie erstellt haben.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_testCloudant_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 private binding
  ```

  Es wird der vollständig qualifizierte Name der Paketbindung angezeigt, die Ihrer Bluemix-Cloudant-Serviceinstanz entspricht.

4. Prüfen Sie, ob die zuvor erstellte Paketbindung mit dem Host und den Berechtigungsnachweisen für Ihre Bluemix-Cloudant-Serviceinstanz konfiguriert ist.

  ```
  wsk package get /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 parameters
  ```
  {: pre}
  ```
  ok: got package /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1, displaying field parameters
  ```
  ```json
  [
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
  ]
  ```

## Cloudant-Datenbank außerhalb von Bluemix einrichten
{: #openwhisk_catalog_cloudant_outside}

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie Ihre Cloudant-Datenbank außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihr Cloudant-Konto erstellen. Sie benötigen den Hostnamen, den Benutzernamen und das Kennwort des Cloudant-Kontos.

1. Erstellen Sie eine Paketbindung, die für Ihr Cloudant-Konto konfiguriert ist.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. Prüfen Sie, ob die Paketbindung vorhanden ist.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```


## Änderungen an einer Cloudant-Datenbank empfangen
{: #openwhisk_catalog_cloudant_listen}

Mit dem Feed `changes` können Sie einen Service konfigurieren, der bei jeder Änderung an Ihrer Cloudant-Datenbank einen Auslöser aktiviert. Die folgenden Parameter sind verfügbar:

- `dbname`: Name der Cloudant-Datenbank.
- `maxTriggers`: Stoppt die Aktivierung von Auslösern, wenn dieser Grenzwert erreicht wird. Standardwert: unbegrenzt.


1. Erstellen Sie einen Auslöser mit dem Feed `changes` in der Paketbindung, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```

2. Fragen Sie Aktivierungen mit der Pollingfunktion ab.

  ```
  wsk activation poll
  ```
  {: pre}

3. Ändern Sie in Ihrem Cloudant-Dashboard ein vorhandenes Dokument oder erstellen Sie ein neues Dokument.

4. Beobachten Sie die neuen Aktivierungen für den Auslöser `myCloudantTrigger` für jede Dokumentänderung.
  
  **Hinweis:** Wenn Sie keine neuen Aktivierungen beobachten können, lesen Sie die nachfolgenden Abschnitte über das Lesen und Schreiben in einer Cloudant-Datenbank. Durch Testen der nachfolgenden Schritte zum Lesen und Schreiben können Sie prüfen, ob Ihre Cloudant-Berechtigungsnachweise korrekt sind.
  
  Sie können jetzt Regeln erstellen und diese Aktionen zuordnen, um auf die Dokumentaktualisierungen zu reagieren.
  
  Der Inhalt der generierten Ereignisse weist die folgenden Parameter auf:
  
  - `id`: Die Dokument-ID.
  - `seq`: Die von Cloudant generierte Sequenz-ID.
  - `changes`: Ein Array von Objekten, die jeweils ein Feld `rev` haben, das die Revisions-ID des Dokuments enthält.
  
  Die JSON-Darstellung des Auslöserereignisses sieht wie folgt aus:
  
  ```json
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```
  
## In eine Cloudant-Datenbank schreiben
{: #openwhisk_catalog_cloudant_write}

Sie können eine Aktion verwenden, um ein Dokument in einer Cloudant-Datenbank mit dem Namen `testdb` speichern. Stellen Sie sicher, dass diese Datenbank in Ihrem Cloudant-Konto vorhanden ist.

1. Speichern Sie ein Dokument mit der Aktion `write` in der Paketbindung, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  ```
  ```json
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```

2. Prüfen Sie, ob das Dokument vorhanden ist, indem Sie in Ihrem Cloudant-Dashboard danach suchen.

  Die Dashboard-URL für die Datenbank `testdb` sieht in etwa wie folgt aus: `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


## Aus einer Cloudant-Datenbank lesen
{: #openwhisk_catalog_cloudant_read}

Sie können eine Aktion verwenden, um ein Dokument aus einer Cloudant-Datenbank mit dem Namen `testdb` abzurufen. Stellen Sie sicher, dass diese Datenbank in Ihrem Cloudant-Konto vorhanden ist.

- Rufen Sie ein Dokument mit der Aktion `read` in der Paketbindung ab, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myCloudant` durch Ihren Paketnamen ersetzen.

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```json
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3",
    "name": "Walter White"
  }
  ```

## Aktionssequenz und Änderungsauslöser zur Verarbeitung eines Dokuments aus einer Cloudant-Datenbank verwenden
{: #openwhisk_catalog_cloudant_read_change notoc}
Sie können eine Aktionssequenz in einer Regel verwenden, um das Dokument, das einem Cloudant-Änderungsereignis zugeordnet ist, abzurufen und zu verarbeiten.

Im Folgenden ist ein Beispielcode einer Aktion aufgeführt, die zur Verarbeitung eines Dokuments dient:
```javascript
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```

Erstellen Sie die Aktion, um das Dokument aus Cloudant zu verarbeiten:
```
wsk action create myAction myAction.js
```
{: pre}

Um ein Dokument aus der Datenbank zu lesen, können Sie die Aktion `read` aus dem Cloudant-Paket verwenden.
Die Aktion `read` kann mit `myAction` zusammengesetzt werden, um eine Aktionsfolge zu erstellen.
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

Die Aktion `sequenceAction` kann in einer Regel verwendet werden, mit der die Aktion bei neuen Cloudant-Auslöserereignissen aktiviert wird.
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Hinweis:** Mit dem Cloudant-Auslöser `changes` wurde der Parameter `includeDoc` unterstützt, der nun nicht mehr unterstützt wird.
  Sie müssen Auslöser, die zuvor mit `includeDoc` erstellt wurden, erneut erstellen. Führen Sie die folgenden Schritte aus, um den Auslöser erneut zu erstellen:
  ```
  wsk trigger delete myCloudantTrigger
  ```
  {: pre}
  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  Das oben dargestellte Beispiel kann verwendet werden, um eine Aktionsfolge zu erstellen, um das geänderte Dokument zu lesen und die vorhandenen Aktionen aufzurufen.
  Denken Sie daran, Regeln zu inaktivieren, die möglicherweise nicht mehr gültig sind, und erstellen Sie mit dem Aktionsfolgemuster neue Regeln.

