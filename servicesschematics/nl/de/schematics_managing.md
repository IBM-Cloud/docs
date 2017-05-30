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

# Verwalten von Ressourcen in eigenen Umgebungen
{: #managing}

{{site.data.keyword.bplong}} vereinfacht die Verwaltung Ihrer Umgebungen. Sie können Ihre bereitgestellten Ressourcen ändern und Änderungen bei Bedarf wiederholt bereitstellen.

{:shortdesc}

Änderungen an Ihrer Umgebung können mit einem einfachen Prozess bereitgestellt werden. Wenn Sie ändern wollen, welche Ressourcen zugeordnet sind, codieren Sie Änderungen an Ihrer Konfiguration in deklarativer Syntax, d. h. Sie geben nur Ihr gewünschtes Ergebnis an. Mit {{site.data.keyword.bpshort}} können Sie eine Vorschau Ihrer Änderungen vor der Bereitstellung anzeigen.


## Aktualisieren von Ressourcen über die GUI
{: #gui}

Wenn Sie zur Verwaltung der Ressourcen in Ihren Umgebungen eine grafische Ansicht bevorzugen, können Sie das {{site.data.keyword.bpshort}}-Dashboard verwenden.
{:shortdesc}

Nachdem Sie Codeänderungen an Ihrer Konfiguration in GitHub publiziert oder Variablen in der GUI modifiziert haben, führen Sie die folgenden Schritte aus, um Aktualisierungen in Ihrer Umgebung bereitzustellen:

1. Wählen Sie im **{{site.data.keyword.bpshort}}**-Dashboard die Option **Umgebungen** aus.

2. Klicken Sie auf die Zeile der jeweiligen Umgebung, die Sie aktualisieren möchten.

3. Klicken Sie auf **Plan** und überprüfen Sie Ihr Planprotokoll auf Fehler. Die Umgebung ist gesperrt, bis Sie oder andere Mitarbeiter in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto den Plan anwenden oder abbrechen. 

4. Klicken Sie auf **Anwenden**, um die Aktualisierungen bereitzustellen. 


## Aktualisieren von Ressourcen über die CLI
{: #cli}

Mit der {{site.data.keyword.bpshort}}-CLI können Sie Ressourcen in Ihren Umgebungen programmgesteuert aktualisieren.
{:shortdesc}

Nachdem Sie Codeänderungen an Ihrer Konfiguration in GitHub veröffentlicht haben, führen Sie die folgenden Schritte aus, um Aktualisierungen in Ihrer Umgebung bereitzustellen:

1. Führen Sie den Befehl `plan` aus. Die {{site.data.keyword.bpshort}}-CLI extrahiert die aktualisierte Umgebungskonfiguration aus GitHub und gibt eine Vorschau aus, wie sich Ihre Ressourcen von der aktuellen Bereitstellung unterscheiden.

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. Zeigen Sie die Planausgabe im Aktivitätenprotokoll an.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. Stellen Sie Ihren Plan mit dem Befehl `Anwenden` bereit. 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Aktualisieren von Ressourcen mit der API
{: #api}

Mit der {{site.data.keyword.bpshort}}-API können Sie Ressourcen in Ihren Umgebungen programmgesteuert verwalten.
{:shortdesc}

Nachdem Sie Codeänderungen an Ihrer Konfiguration in GitHub veröffentlicht haben, führen Sie die folgenden Schritte aus, um Aktualisierungen in Ihrer Umgebung bereitzustellen:

1. Führen Sie den Aufruf `POST v1/environments/<environment_ID>/plan` aus. Die {{site.data.keyword.bpshort}}-API extrahiert die aktualisierte Umgebungskonfiguration aus GitHub und vergleicht sie mit der Terraform-Statusdatei, um darzustellen, wie sich Ihre Ressourcen von der aktuellen Bereitstellung unterscheiden.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  Beispielantwort:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. Zeigen Sie die Planausgabe im Aktivitätenprotokoll an.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Stellen Sie Ihren Plan bereit, indem Sie den Aufruf `PUT /v1/environments/<environment_ID>/apply` ausführen. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## Prüfung von Änderungen an Ihren Umgebungen
{: #auditing}

Konfigurationen können im Versionsverlauf Ihres Quellcodeverwaltungsrepositorys geprüft werden. Zur Überwachung von Bereitstellungen in Ihrer Umgebung oder zum Anzeigen vorheriger Bereitstellungen bietet {{site.data.keyword.bpshort}} folgende Optionen zur Anzeige Prüfprotokollen.

### Über das {{site.data.keyword.bpshort}}-Dashboard:
{: #auditing-gui}

1. Wählen Sie die Zeile der Umgebung, um auf die Seite für Umgebungsdetails zuzugreifen.

2. Überwachen Sie den Abschnitt **Kürzliche Aktivitäten**. Sie können auch Langzeitprotokolle vorheriger Pläne und Bereitstellungen anzeigen.

### Über die {{site.data.keyword.bpshort}}-CLI:
{: #auditing-cli}

1. Rufen Sie Ihre Umgebungs-ID ab.

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. Rufen Sie die Aktivitäts-IDs für Ihre Umgebung ab. Aktivitäts-IDs sind den Aktionen 'plan', 'apply', 'destroy' und 'delete' zugeordnet. Der folgende Befehl listet alle Aktivitäten auf, die für Ihre Umgebung ausgeführt wurden.

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. Rufen Sie die Daten zu einer bestimmten Aktivität ab, z. B. wer in einer Umgebung Änderungen vorgenommenen hat und wann.

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. Optional: Um ein detailliertes Protokoll anzuzeigen, z. B. die Ausgabe für 'plan' oder 'apply', führen Sie den Befehl `log` aus. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### Über die {{site.data.keyword.bpshort}}-API:
{: #auditing-api}

1. Rufen Sie Ihre Umgebungs-ID ab.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  Der Antworthauptteil enthält alle Umgebungen in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto. Suchen Sie den `id`-Wert der jeweiligen Umgebung, die Sie überprüfen möchten.

2. Rufen Sie die Aktivitäts-IDs für die Aktionen ab, die für Ihre Umgebung ausgeführt werden.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Rufen Sie eine bestimmte Aktivität für eine Umgebung ab. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Überprüfen Sie ein detailliertes Protokoll der Terraform-Ausgabe.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
