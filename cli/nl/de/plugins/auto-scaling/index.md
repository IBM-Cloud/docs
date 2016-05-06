{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Auto-Scaling-CLI
{: #autoscalingcli}

*Letzte Aktualisierung: 20. Januar 2015*

Sie können den Service {{site.data.keyword.autoscaling}} unter Verwendung der {{site.data.keyword.autoscaling}}-CLI für {{site.data.keyword.Bluemix_notm}} konfigurieren. Die {{site.data.keyword.autoscaling}}-CLI unterstützt Linux64, Win64 und OSX und stellt eine ähnliche Funktionalität wie die {{site.data.keyword.autoscaling}}-RESTful-API bereit.
{: shortdesc}

Bevor Sie beginnen, müssen Sie die {{site.data.keyword.Bluemix_notm}}-CLI installieren. Anweisungen hierzu enthält das Dokument zum [Download der {{site.data.keyword.Bluemix_notm}}-CLI](http://plugins.{DomainName}/ui/home.html){: new_window}.

## Plug-in für Auto-Scaling-CLI hinzufügen

Nach der Installation der {{site.data.keyword.Bluemix_notm}}-CLI können Sie das Plug-in für die {{site.data.keyword.autoscaling}}-CLI hinzufügen.

Führen Sie die folgenden Schritte aus, um das Repository hinzuzufügen und das Plug-in zu installieren:
1. Führen Sie den folgenden Befehl aus, um das Repository für das {{site.data.keyword.Bluemix_notm}}-CLI-Plug-in hinzuzufügen:
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um das Plug-in für die {{site.data.keyword.autoscaling}}-CLI zu installieren:
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Auto-Scaling-Richtlinie zuordnen

Sie können eine Auto-Scaling-Richtlinie einer bestimmten App zuordnen. Führen Sie dazu den folgenden Befehl aus:

```bx as policy-attach <APP_NAME> -p <richtliniendatei>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, der Sie eine Auto-Scaling-Richtlinie zuordnen möchten.</dd>
<dt class="pt dlterm">&lt;richtliniendatei&gt;</dt>
<dd class="pd">Der Name der JSON-Datei, die die Auto-Scaling-Richtlinie beschreibt. Detaillierte Informationen hierzu enthält die Dokumentation zur [{{site.data.keyword.autoscaling}}-RESTful-API](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html).</dd>
</dl>


## Auto-Scaling-Richtlinie erstellen

Sie können eine Auto-Scaling-Richtlinie erstellen, indem Sie die Fragen in der Befehlszeilenschnittstelle beantworten. Entsprechend Ihrer Eingabe wird eine JSON-Datei mit der Definition der Auto-Scaling-Richtlinie mit dem von Ihnen eingegebenen Namen gespeichert. Wenn Sie den Dateinamen nicht eingeben, wird der Richtlinieninhalt direkt in der Befehlszeile ausgegeben und nicht in einer Datei gespeichert. Führen Sie den folgenden Befehl aus:

```bx as policy-create```
{: codeblock}


## Auto-Scaling-Richtlinie anzeigen

Sie können die Auto-Scaling-Richtlinie einer App anzeigen. Der Inhalt der Richtlinie wird direkt in der Befehlszeile ausgegeben. Führen Sie den folgenden Befehl aus:

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die die Auto-Scaling-Richtlinie angezeigt werden soll. Standardmäßig wird die JSON-Struktur in eine Serie von lesbarer Ausgabe übersetzt.</dd>
</dl>

**Tipp:** Sie können auch die Option **--json** verwenden, um eine Quelltextformatierung der ursprünglichen JSON-Antwort zu erstellen.


## Zuordnung einer Auto-Scaling-Richtlinie aufheben

Sie können eine Auto-Scaling-Richtlinie von einer App entfernen. Führen Sie den folgenden Befehl aus:

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die die Zuordnung zur Auto-Scaling-Richtlinie aufgehoben werden soll.</dd>
</dl>


## Auto-Scaling-Richtlinie aktivieren oder inaktivieren

Sie können die Auto-Scaling-Richtlinie einer bestimmten App aktivieren oder inaktivieren. Führen Sie den folgenden Befehl aus:

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die die Auto-Scaling-Richtlinie aktiviert oder inaktiviert werden soll.</dd>
</dl>


## Auto-Scaling-Protokoll einer App anzeigen

Sie können das Protokoll der Auto-Scaling-Aktivität einer bestimmten App anzeigen. In der Befehlszeilenschnittstelle wird eine Tabelle der Auto-Scaling-Protokolleinträge angezeigt.

```bx as history-show <APP-NAME>  [--start-date=<start_zeitmarke>][--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP-NAME&gt;</dt>
<dd class="pd">Der Name der App, für die das Protokoll der Auto-Scaling-Richtlinie angezeigt werden soll. <dt class="pt dlterm">&lt;start_zeitmarke&gt;</dt>
<dd class="pd">Die Zeitmarke für den Beginn des Protokollbereichs. Die unterstützten Formate lauten `jjjj-MM-ttTHH:mm:ss+/-hhmm, jjjj-MM-ttTHH:mm:ssZ`. Standardmäßig ist die Zeitmarke auf 50 Stunden vor der aktuellen Uhrzeit eingestellt. Detaillierte Informationen zum Zeitmarkenformat enthält der [W3C-Standard 'Date and Time Formats'](https://www.w3.org/TR/NOTE-datetime){: new_window}.
<dt class="pt dlterm">&lt;ende_zeitmarke&gt;</dt>
<dd class="pd">Die Zeitmarke für das Ende des Protokollbereichs. Die unterstützten Formate lauten `jjjj-MM-ttTHH:mm:ss+/-hhmm, jjjj-MM-ttTHH:mm:ssZ`. Standardmäßig ist die Zeitmarke auf die aktuelle Uhrzeit eingestellt. Detaillierte Informationen zum Zeitmarkenformat enthält der [W3C-Standard 'Date and Time Formats'](https://www.w3.org/TR/NOTE-datetime){: new_window}.
</dl>

**Tipp:** Sie können auch die Option **--json** verwenden, um eine Quelltextformatierung der ursprünglichen JSON-Antwort zu erstellen.

# rellinks
## Allgemein
* [{{site.data.keyword.autoscaling}}-Service](../../services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}}-CLI](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C-Standard 'Date and Time Formats'](https://www.w3.org/TR/NOTE-datetime){: new_window}


