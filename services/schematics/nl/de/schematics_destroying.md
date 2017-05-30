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

# Vernichten von Ressourcen im temporären Umgebungen
{: #destroying}

Sie können {{site.data.keyword.bplong}} verwenden, um Ihre Ressourcen zu vernichten. Wenn Sie Ihre Ressourcen vernichten, zerstören Sie damit Ihre Umgebung und alle zugehörigen Ressourcen.  
{:shortdesc}

**Achtung**: Wenn Sie Ressourcen vernichten, kann die Aktion nicht rückgängig gemacht werden. Das Vernichten von Ressourcen wird für Produktionsumgebungen nicht empfohlen, kann aber für temporäre Umgebungen wie Test- oder Qualitätssicherungsumgebungen hilfreich sein.

Bevor Sie Ihre Ressourcen vernichten, beachten Sie die folgenden Richtlinien: 
* Stellen Sie sicher, dass der Datenverkehr nicht in Ihre Ressourcen weitergeleitet wird.
* Stellen Sie sicher, dass alle Daten, die Sie benötigen könnten, gesichert sind. 


## Vernichten von Ressourcen über die GUI
{: #gui}

Sie können das {{site.data.keyword.bpshort}}-Dashboard verwenden, um für temporäre Umgebungen den Betrieb aufzunehmen oder diese zu zerstören.
{:shortdesc}

1. Wählen Sie im **{{site.data.keyword.bpshort}}**-Dashboard die Registerkarte **Umgebungen** aus.

2. Klicken Sie auf die Zeile der jeweiligen Umgebung, die Sie entfernen möchten. 

3. Wählen Sie im Menü "Optionen" **Ressourcen vernichten** oder **Umgebung löschen** aus. Weder die Aktion 'Löschen' noch die Aktion 'Vernichten' kann rückgängig gemacht werden. Um festzustellen, welche Option ausgewählt werden sollte, ist zu überlegen, ob Sie über aktive Ressourcen verfügen.
  * Wählen Sie **Ressourcen vernichten** aus, wenn Sie Ihre aktiven Ressourcen stoppen und entfernen möchten. Es wird empfohlen, vor der Vernichtung einen Plan auszuführen, um zu überprüfen, ob die Ressourcen, die der Umgebung zugeordnet sind, entfernt werden dürfen.
  * Wählen Sie **Umgebung löschen** aus, wenn Sie die Umgebungskonfiguration aus dem {{site.data.keyword.bpshort}}-Service entfernen möchten. Diese Option wird in der Regel verwendet, wenn die Umgebung nicht bereitgestellt ist und keine aktive Ressourcen besitzt. Wenn Sie diese Option mit aktiven Ressourcen auswählen, können Sie nicht mehr den {{site.data.keyword.bpshort}}-Service verwenden, um Änderungen an Ihrer Umgebung zu verfolgen oder bereitzustellen. Die aktiven Ressourcen müssen über ihre Service-Dashboards einzeln verwaltet werden.
  
  Befolgen Sie die Anweisungen auf dem Bildschirm, um Ihre Auswahl zu bestätigen. 


## Vernichten von Ressourcen über die CLI
{: #cli}

Sie können die {{site.data.keyword.bpshort}}-CLI verwenden, um für temporäre Umgebungen den Betrieb aufzunehmen oder diese zu zerstören.
{:shortdesc}

1. Führen Sie den Befehl `destroy` aus, um Ihre Umgebung und die Ressourcen zu zerstören.

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. Optional: Führen Sie den Befehl `delete` aus, um Ihre Konfiguration aus dem Service zu entfernen.

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Vernichten von Ressourcen über die API
{: #api}

Sie können die {{site.data.keyword.bpshort}}-API verwenden, um für temporäre Umgebungen den Betrieb aufzunehmen oder diese zu zerstören.
{:shortdesc}

1. Führen Sie den Aufruf `PUT v1/environments/<environment_ID>/destroy` aus, um Ihre Ressourcen zu vernichten.

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. Optional: Führen Sie den Aufruf `DELETE v1/environments/<environment_ID>` aus, wenn Sie Ihre Konfiguration aus dem {{site.data.keyword.bpshort}}-Service entfernen möchten.

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
