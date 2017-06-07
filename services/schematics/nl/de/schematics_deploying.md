---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Bereitstellung von Ressourcen in Ihren Umgebungen
{: #deploying}

Mit {{site.data.keyword.bplong}} können Sie Ihre letzten Codeänderungen direkt über Ihren Quellcode bereitstellen. Wenn Sie Ihre Umgebung bereitstellen, stellen Sie die Ressourcen bereit, die von Ihrer Konfigurationsdateien definiert sind. Anschließend können Sie die Bereitstellung, die Orchestrierungen und den Lebenszyklus der Umgebung von {{site.data.keyword.bpshort}} aus verwalten.
{:shortdesc}

## Bereitstellung Ihrer Umgebungen über die GUI
{: #gui}

Wenn Sie für die Bereitstellung Ihrer Umgebung eine grafische Ansicht bevorzugen, können Sie das {{site.data.keyword.bpshort}}-Dashboard verwenden.
{:shortdesc}


### Voraussetzung
{: #gui-prereq}

* Speichern Sie eine Terraform-Konfiguration in der Quellcodeverwaltung. Konfigurationen können HashiCorp Configuration Language (HCL) oder der JSON-Syntax geschrieben werden. Lesen Sie die <a href="https://www.terraform.io/docs/configuration/index.html">Terraform-Konfigurationsdokumentation <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> hinsichtlich HCL-Syntax und Richtlinien zum Schreiben von Konfigurationen. Im <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud-Provider <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> finden Sie die verfügbaren Ressourcen.

Nach dem Speichern Ihrer Konfiguration:

1. Wählen Sie im **{{site.data.keyword.bpshort}}**-Dashboard die Option **Umgebungen** aus.

2. Klicken Sie auf **Umgebung erstellen**, um eine Umgebung hinzuzufügen, oder wählen Sie die Zeile einer vorhandenen Umgebung aus, die Sie bereitstellen möchten.

3. Klicken Sie auf **Plan**, um eine Vorschau anzuzeigen, welche Ressourcen bereitgestellt werden, wenn Sie Ihre Umgebung bereitstellen. Wenn Sie 'Plan' ausführen, extrahiert {{site.data.keyword.bpshort}} die Variablen in Ihren Umgebungsdetails und die aktuelle Version Ihrer Konfiguration aus der Quellcodeverwaltung. Die Ausgabe von 'Plan' zeigt, wie die Konfiguration im Vergleich zu dem aussieht, was entsprechend Ihrer Terraform-Statusdatei bereitgestellt wird. Ihre Umgebung wird für weitere Änderungen gesperrt, bis der Plan auf Ihre Umgebung angewendet oder abgebrochen wurde. 

4. Zeigen Sie das Protokoll im Abschnitt **Kürzliche Aktivität** an, um die Planausgabe zu überprüfen. Die Planausgabe zeigt an, ob Fehler vorhanden sind und welche Ressourcen der Service erstellen, ändern oder vernichten wird.

5. Wenn Sie bereit sind, Ihren Plan zu starten, klicken Sie auf **Anwenden**. Sie können das Aktivitätenprotokoll überwachen, um sicherzustellen, dass der Plan erfolgreich in der letzten Ausführung angewendet wird. 


## Bereitstellung Ihrer Umgebungen mit der CLI
{: #cli}

Sie können das {{site.data.keyword.bpshort}}-Plug-in für die {{site.data.keyword.Bluemix_notm}}-CLI verwenden, um Aktualisierungen für Ihre Umgebung bereitzustellen.
{:shortdesc}

### Voraussetzungen
{: #cli-prereq}

* Speichern Sie eine Terraform-Konfiguration in der Quellcodeverwaltung.
* Wenn noch nicht geschehen, installieren Sie die {{site.data.keyword.Bluemix_notm}}-CLI für Ihr Betriebssystem aus dem [{{site.data.keyword.Bluemix_notm}}-CLI-Repository](http://clis.ng.bluemix.net/ui/home.html).

Nachdem Sie sich an der {{site.data.keyword.Bluemix_notm}}-CLI angemeldet haben, gehen Sie folgendermaßen vor:

1. Installieren Sie das {{site.data.keyword.bpshort}}-CLI-Plug-in, indem Sie den folgenden Befehl ausführen.
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  Das {{site.data.keyword.bpshort}}-Plug-in wird unter `bx plugin list` angezeigt, wenn die Installation erfolgreich ist. 

2. Erstellen Sie eine Umgebung aus Ihrer Konfiguration. Wenn Sie Ihre Umgebung erstellen, verweisen Sie den Service an Ihre Quellcodeverwaltung, sodass er den neuesten Code extrahieren kann. 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="Beschreibung des Befehls 'environment create'.">
  <caption>Tabelle 1. Beschreibung des Befehls 'environment create'.
  </caption>
  <thead>
  <th colspan="1">Befehl</th>
  <th colspan="1">Was Sie tun</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>Die JSON-Datei, in der Details zu Ihrer Umgebung gespeichert werden.
  <p>
  <p>JSON-Beispiel:
  <pre>{
      "description": "(Optional) Beschreibung der Umgebung",
      "frozen": falsch,
      "name": "Name der Umgebung",
      "sourceurl": "Die GitHub-URL, die auf die Terraform-Konfiguration hinweist",
      "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Optional) variable_1",
          "secure": falsch,
          "value": "Sichtbarer Wert"
      },
      {
          "name": "(Optional) variable_2_secret",
          "secure": wahr,
          "value": "Gesicherter Wert"
      }]
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  Beachten Sie den zurückgegebenen `ID`-Wert. Die `ID` ist eine eindeutige Kennung, die Ihrer Umgebung zugeordnet und bei nachfolgenden Befehlen verwendet wird.
  
3. Führen Sie `plan` aus, um eine Vorschau anzuzeigen, wie sich Ihre Umgebung ändern würde. Der Befehl 'plan' zeigt an, welche Ressourcen sich ändern würden und in welcher Menge gegenüber dem, was bereitgestellt wird, jedoch werden die Änderungen erst wirksam, wenn Sie den Befehl `Anwenden` ausführen.
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Beschreibung des Befehls 'plan'.">
  <caption>Tabelle 2. Beschreibung des Befehls 'plan'.
  </caption>
  <thead>
  <th colspan="1">Befehl</th>
  <th colspan="1">Was Sie tun</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>Die spezifische Umgebung, für die ein Ausführungsplan ausgeführt werden soll. Sie können <code>bx schematics list</code> ausführen, wenn Sie den Wert für die Umgebungs-ID abrufen müssen.</td>
  </tbody></table>
  
  Eine `activity_id` wird dem Plan zugeordnet und im Aktivitätenprotokoll aufgezeichnet. 

4. Rufen Sie das Aktivitätenprotokoll ab, um die Ausgabe des Terraform-Plans anzuzeigen.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="Beschreibung des Befehls 'log'.">
  <caption>Tabelle 3. Beschreibung des Befehls 'log'.
  </caption>
  <thead>
  <th colspan="1">Befehl</th>
  <th colspan="1">Was Sie tun</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>Die spezifische Aktivität, die Sie für das Protokoll anzeigen möchten. Sie können <code>bx schematics activity list --id ENVIRONMENT_ID</code> ausführen, wenn Sie den Wert für die Aktivitäts-ID abrufen müssen.
  </td>
  </tbody></table>
  
5. Führen Sie den Befehl `apply` aus, um Ressourcen für Ihre Umgebung bereitzustellen.
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Beschreibung des Befehls 'apply'.">
  <caption>Tabelle 4. Beschreibung des Befehls 'apply'.
  </caption>
  <thead>
  <th colspan="1">Befehl</th>
  <th colspan="1">Was Sie tun</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>Die spezifische Umgebung, in der Sie Aktualisierungen bereitstellen möchten. Sie können <code>bx schematics list</code> ausführen, wenn Sie den Wert für die Umgebungs-ID abrufen müssen.</td>
  </tbody></table>
  
6. Überwachen Sie die Ausgabe von 'apply', um sicherzustellen, dass die Bereitstellung erfolgreich war. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  Eine erfolgreiche Bereitstellung gibt die folgende Zeile am Ende der Ausgabe zurück.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## Bereitstellung in Ihren Umgebungen mit der API
{: #api}

Sie können Ihre Umgebung mit der {{site.data.keyword.bpshort}}-API programmgesteuert bereitstellen.
{:shortdesc}

Aufrufe der <a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}}-API <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> verweisen auf den folgenden Basis-Endpunkt:

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### Voraussetzung
{: #api-prereq}

* Speichern Sie eine Terraform-Konfiguration in der Quellcodeverwaltung.

Führen Sie die folgenden Schritte aus, um Ressourcen in Ihrer Umgebung bereitzustellen:

1. Generieren Sie ein IAM OAuth-Token zur Verwendung in Ihrem Authentifizierungsheader. Der Befehl gibt ein UAA-Token und ein IAM-Token aus.
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  Beispiel für die Ausgabe:
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  Die Ausgabe `Bearer eyJraWQ...` ist ein abgeschnittenes Beispiel für das IAM-Token. Schließen Sie das vollständige Token in die Überschrift Ihrer API-Aufrufe ein.
  
2. Erstellen Sie eine Umgebung durch Ausführen des Aufrufs `POST v1/environments`.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Beschreibung der Umgebung",
    "frozen": falsch,
    "name": "Name der Umgebung",
    "sourceurl": "Die GitHub-URL, die auf die Terraform-Konfiguration verweist",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": falsch,
        "value": "Sichtbarer Wert"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": wahr,
        "value": "Gesicherter Wert"
    }]
  }'
  ```
  {: codeblock}
    
  Eine erfolgreiche Antwort gibt die folgende Ausgabe zurück.
  ```
  {
    "id": "Umgebungs-ID",
    "name": "Name der Umgebung",
    "description": "Beschreibung der Umgebung",
    "account": "{{site.data.keyword.Bluemix_notm}}-Konto-GUID",
    "owner": "Die IBM-ID des Benutzers, der die Umgebung erstellt hat",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": falsch,
    "sourceurl": "Die GitHub-URL, die auf die Konfiguration verweist",
    "statefile": "Verweis auf die Terraform-Statusdatei",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Sichtbarer Wert"
      }
    ]
  }
  ```
  {: screen}
    
  Beachten Sie den zurückgegebenen `id`-Wert. Die `id` ist eine eindeutige Kennung, die Ihrer Umgebung zugeordnet und in nachfolgenden Aufrufen verwendet wird.
  
3. Führen Sie den Aufruf `POST v1/environments/<environment_ID>/plan` aus, um eine Vorschau der Ressourcen anzuzeigen, die in Ihrer Umgebung bereitgestellt werden, wenn Sie Ihre Konfiguration anwenden. Pläne extrahieren die Umgebungskonfigurationen in der Master-Verzweigung Ihres Repositorys.
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  Eine erfolgreiche Antwort gibt eine `activityid` zurück. Die Aktivitäts-ID wird zur Anzeige von Protokollen benötigt, z. B. der Ausgabe für 'plan' und 'apply'.
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. Führen Sie den Aufruf `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` aus, um die Ausgabe für 'plan' anzuzeigen.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. Stellen Sie Ihre Umgebung mit dem Aufruf `PUT v1/environments/<environment_ID>/apply/` bereit.
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. Überwachen Sie die Bereitstellung durch Ausführen des Aufrufs `GET v1/environments/<environment_ID>/activities/<activity_ID>/log`, um die Ausgabe für 'apply' anzuzeigen.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  Eine erfolgreiche Bereitstellung gibt die folgende Zeile am Ende der Ausgabe zurück.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
