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

# {{site.data.keyword.bpshort}}-CLI-Plug-in für die {{site.data.keyword.Bluemix_notm}}-CLI
{: #cli}

Nutzen Sie die {{site.data.keyword.bpshort}}-Befehle für die {{site.data.keyword.Bluemix}}-CLI zum Verwalten Ihrer Umgebungen und Durchführen weiterer Operationen in {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Vor der Verwendung der CLI-Befehle:

* Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} mit `bx login [ -- sso]` an, um Ihre Sitzung zu authentifizieren. Benutzer mit einer eingebundenen ID müssen das Flag `--sso` verwenden, um einen einmaligen Kenncode zu generieren.

Um eine Liste der Befehle anzuzeigen, können Sie den Befehl `bx schematics help` ausführen.

<table id="manage_environments" summary="Verwalten Sie Ihre Umgebungen mit den 'bx schematics environment'-Befehlen.">
<caption>Tabelle 1. Verfügbare Befehle für die Verwaltung Ihrer Umgebung. Die Befehle folgen der Syntax <code>bx schematics environment</code>.
</caption>
 <thead>
 <th colspan="5">Verwaltung der eigenen Umgebung</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="Aktualisieren Sie die Ressourcen, die von Ihrer Umgebung bereitgestellt werden, mit den 'bx schematics action'-Befehlen.">
 <caption>Tabelle 2. Verfügbare Befehle, um Ressourcen in Ihrer Umgebung zu aktualisieren. Die Befehle folgen der Syntax <code>bx schematics action</code>.
 </caption>
  <thead>
  <th colspan="5">Aktualisieren eigener Ressourcen</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="Prüfung von Aktivitäten, die mit den 'bx schematics activity'-Befehlen für Ihre Umgebung ausgeführt wurden.">
  <caption>Tabelle 3. Verfügbare Befehle, um die Aktivitäten zu prüfen, die Sie für Ihre Umgebung ausgeführt haben. Die Befehle folgen der Syntax <code>bx schematics activity</code>.
  </caption>
   <thead>
   <th colspan="5">Prüfung Ihrer Umgebung</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

Erstellen Sie eine Umgebung in {{site.data.keyword.Bluemix_notm}} aus Ihrer Konfiguration.

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### Parameter

<dl>
<dt>--file FILE_NAME</dt>
<dd>Die JSON-Datei, die verwendet wird, um Details zu Ihrer Umgebung zu übergeben.
<p>
<p>JSON-Beispiel mit allen verfügbaren Werten:
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
}</pre></dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe im JSON-Format.</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

Entfernen der Konfiguration aus {{site.data.keyword.Bluemix_notm}}. Dieser Befehl wird nur für Umgebungen ohne aktive Ressourcen empfohlen. Wenn Sie eine Umgebung mit aktiven Ressourcen löschen, müssen Sie jede Ressource in den jeweiligen Service-Dashboards verwalten.

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### Parameter

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--force</dt>
<dd>Fortschritt des Befehls ohne eine Ja/Nein-Bestätigung erzwingen.</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

Rufen Sie eine Liste aller vorhandenen Umgebungen in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto ab.

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### Parameter
<dl>
<dt>--count VALUE</dt>
<dd>Die Anzahl der in Ihrer Rückgabe einzugrenzenden Umgebungen.</dd>
<dt>--offset VALUE</dt>
<dd>Der Offset in der Liste der Umgebungen.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe im JSON-Format.</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

Abrufen von Informationen zu einer vorhandenen Umgebung.

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe im JSON-Format.</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

Aktualisieren der Details zu einer vorhandenen Umgebung, z. B. Umgebungsnamen oder GitHub-URL. Zum Aktualisieren der Anzahl der Ressourcen, die in der Umgebung zugeordnet sind, siehe [bx schematics action plan](#action-plan).

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--file FILE_NAME</dt>
<dd>Die JSON-Datei, die verwendet wird, um Details zu Ihrer Umgebung zu übergeben. Siehe [bx schematics environment create](#environment-create) für einen JSON-Beispielausschnitt mit zulässigen Werten.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe im JSON-Format.</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

Stellen Sie Ihre Umgebungskonfiguration bereit. Der Befehl `apply` durchsucht die Konfigurationen, die in Ihrem GitHub-Repository gespeichert sind, und führt sie aus.

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--force</dt>
<dd>Fortschritt des Befehls ohne eine Ja/Nein-Bestätigung erzwingen.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe für 'apply' im JSON-Format.</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

Vernichten der eigenen Umgebung und der Ressourcen. Der Befehl `destroy` zerstört Ihre Umgebung einschließlich der aktiven Ressourcen. Diese Aktion wird normalerweise nur für temporäre Umgebungen, z. B. eine QA-Umgebung, mit der Absicht verwendet, die Umgebung für einen begrenzten Zeitraum bereitzustellen. Das Vernichten der Produktionsumgebungen wird nicht empfohlen. Die Aktion `destroy` kann nicht rückgängig gemacht werden und sollte mit Vorsicht verwendet werden.

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--force</dt>
<dd>Fortschritt des Befehls ohne eine Ja/Nein-Bestätigung erzwingen.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe von 'destroy' im JSON-Format.</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

Vergleichen der eigenen Umgebungskonfiguration mit der bereitgestellten Konfiguration. Der Befehl `plan` durchsucht die Konfiguration in Ihrem GitHub-Repository und führt einen Vergleich mit der Statusdatei durch, die Ihrer bereitgestellten Umgebung zugeordnet ist. Die Ausgabe für 'plan' zeigt, welche Ressourcen hinzugefügt oder entfernt werden würden, wenn Sie Ihre Umgebungskonfiguration mit dem Befehl `apply` bereitstellen würden. 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--file FILE_NAME</dt>
<dd>Die optionale JSON-Datei, die verwendet wird, um Parameter für die Aktion 'plan' zu übergeben. Sie können den Parameter <code>sourcesha</code> übergeben, um auf eine bestimmte Git-Verzweigung für die Terraform-Konfiguration der Umgebung zu verweisen. Die Git-Verzweigung muss als Kopfverweis, z. B. <code>refs/heads/BRANCH_NAME</code>, angegeben werden. Wenn kein Parameter angegeben ist, ist der Standardwert der Kopf der Master-Verzweigung, also <code>refs/heads/master</code>.<p>
<p>JSON-Beispielausschnitt mit Wert:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe von 'plan' im JSON-Format.</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

Auflisten der Daten aus Terraform-Aktivitäten, die für eine Umgebung ausgeführt wurden.

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>Die eindeutige Kennung für die Umgebung. Sie können diesen Wert durch Ausführen von <code>bx schematics environment list</code> abrufen.</dd>
<dt>--count VALUE</dt>
<dd>Die Anzahl der Aktivitäten, die zurückgegeben werden sollen.</dd>
<dt>--offset VALUE</dt>
<dd>Der Offset in der Liste.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe von 'plan' im JSON-Format.</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

Zeigt detaillierte Aktivitätenprotokolle für Aktionen an, die für eine Umgebung ausgeführt werden.

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### Parameter
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>Das Flag für die Rückgabe von Details zu einer bestimmten Aktivität. Sie können eine Liste der Aktivitäts-IDs pro Umgebung mit dem Befehl <code>bx schematics activity list --id ENVIRONMENT_ID</code> abrufen.</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

Anzeigen von 'plan'-Dateien für eine Umgebung.

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### Parameter
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>Das Flag für die Rückgabe von Details zu einer bestimmten Aktivität. Sie können eine Liste der Aktivitäts-IDs pro Umgebung mit dem Befehl <code>bx schematics activity list --id ENVIRONMENT_ID</code> abrufen.</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

Abrufen der Details zu einer bestimmten Aktivität, die für eine Umgebung ausgeführt wurde.

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### Parameter
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>Das Flag für die Rückgabe von Details zu einer bestimmten Aktivität. Sie können eine Liste der Aktivitäts-IDs pro Umgebung mit dem Befehl <code>bx schematics activity list --id ENVIRONMENT_ID</code> abrufen.</dd>
<dt>--json</dt>
<dd>Drucken der Ausgabe von 'plan' im JSON-Format.</dd>
</dl>
