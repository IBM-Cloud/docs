---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Benutzerschnittstelle (CLI) für Autoskalierung
{: #autoscalingcli}

*Letzte Aktualisierung: 25. Februar 2016*

Sie können den Service {{site.data.keyword.autoscaling}} unter Verwendung der {{site.data.keyword.autoscaling}}-CLI für {{site.data.keyword.Bluemix_notm}} konfigurieren. Die {{site.data.keyword.autoscaling}}-CLI unterstützt Linux64, Win64 und OSX und stellt eine ähnliche Funktionalität wie die REST-konforme API für Autoskalierung (Auto-Scaling RESTful API) bereit.
{: shortdesc}

Bevor Sie beginnen, müssen Sie die {{site.data.keyword.Bluemix_notm}}-CLI installieren. Anweisungen hierzu enthält das Dokument zum [Download der {{site.data.keyword.Bluemix_notm}}-CLI](http://plugins.{DomainName}/ui/home.html){: new_window}.

## {{site.data.keyword.Bluemix_notm}}-CLI-Plug-in hinzufügen

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

## Autoskalierungsrichtlinie zuordnen

Sie können eine Autoskalierungsrichtlinie einer bestimmten App zuordnen. Führen Sie den folgenden Befehl aus:

```bx as policy-attach <APP_NAME> -p <policy_file>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, der Sie eine Autoskalierungsrichtlinie zuordnen möchten.</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">Der Name der JSON-Datei, die die Autoskalierungsrichtlinie beschreibt. Detaillierte Informationen hierzu enthält die Dokumentation zur <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">{{site.data.keyword.autoscaling}}-RESTful-API</a>.</dd>
</dl>


## Autoskalierungsrichtlinie generieren

Sie können eine Autoskalierungsrichtlinie erstellen, indem Sie die Fragen in der Befehlszeilenschnittstelle beantworten. Entsprechend Ihrer Eingabe wird eine JSON-Datei mit der Definition der Autoskalierungsrichtlinie mit dem von Ihnen eingegebenen Namen gespeichert. Wenn Sie den Dateinamen nicht eingeben, wird der Richtlinieninhalt direkt in der Befehlszeile ausgegeben und nicht in einer Datei gespeichert. Führen Sie den folgenden Befehl aus:

```bx as policy-create```
{: codeblock}


## Autoskalierungsrichtlinie anzeigen

Sie können die Autoskalierungsrichtlinie einer App anzeigen. Der Inhalt der Richtlinie wird direkt in der Befehlszeile ausgegeben. Führen Sie den folgenden Befehl aus:

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die die Autoskalierungsrichtlinie angezeigt werden soll. Standardmäßig wird die JSON-Struktur in eine Serie von lesbarer Ausgabe übersetzt.</dd>
</dl>

**Tipp:** Sie können auch die Option **--json** verwenden, um eine Quelltextformatierung der ursprünglichen JSON-Antwort zu erstellen.


## Zuordnung einer Autoskalierungsrichtlinie aufheben

Sie können eine Autoskalierungsrichtlinie von einer App entfernen. Führen Sie den folgenden Befehl aus:

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die die Zuordnung zur Autoskalierungsrichtlinie aufgehoben werden soll.</dd>
</dl>


## Autoskalierungsrichtlinie aktivieren oder inaktivieren

Sie können die Autoskalierungsrichtlinie einer bestimmten App aktivieren oder inaktivieren. Führen Sie den folgenden Befehl aus:

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die die Autoskalierungsrichtlinie aktiviert oder inaktiviert werden soll.</dd>
</dl>


## Autoskalierungsprotokoll einer App anzeigen

Sie können das Protokoll der Autoskalierungsaktivität einer bestimmten App anzeigen. In der Befehlszeilenschnittstelle wird eine Tabelle der Autoskalierungsprotokolleinträge angezeigt.

```bx as history-show <APP_NAME>  [--start-date=<start_timestamp>][--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Der Name der App, für die das Protokoll der Autoskalierungsrichtlinie angezeigt werden soll.
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">Die Zeitmarke für den Beginn des Protokollbereichs. Die unterstützten Formate sind `jjjj-MM-ttTHH:mm:ss+/-hhmm, jjjj-MM-ttTHH:mm:ssZ`. Standardmäßig ist die Zeitmarke auf 50 Stunden vor der aktuellen Uhrzeit eingestellt. Detaillierte Informationen zum Zeitmarkenformat enthält der <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C-Standard 'Date and Time Formats'</a>. 
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">Die Zeitmarke für das Ende des Protokollbereichs. Die unterstützten Formate sind `jjjj-MM-ttTHH:mm:ss+/-hhmm, jjjj-MM-ttTHH:mm:ssZ`. Standardmäßig ist die Zeitmarke auf die aktuelle Uhrzeit eingestellt. Detaillierte Informationen zum Zeitmarkenformat enthält der <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C-Standard 'Date and Time Formats'</a>. 
</dl>

**Tipp:** Sie können auch die Option **--json** verwenden, um eine Quelltextformatierung der ursprünglichen JSON-Antwort zu erstellen.

# Zugehörige Links
## Allgemein
* [{{site.data.keyword.autoscaling}}-Service](../../../services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}}-CLI](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C-Standard 'Date and Time Formats'](https://www.w3.org/TR/NOTE-datetime){: new_window}


