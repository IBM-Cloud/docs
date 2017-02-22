---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"



---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# (Veraltet) Befehlszeilenschnittstelle (CLI) für Entwicklungsmodus
{: #devmodecli}

**Diese Befehlszeilenschnittstelle wird nicht mehr verwendet.** Verwenden Sie anstelle der Befehlszeilenschnittstelle für den Entwicklungsmodus (dev_mode) IBM Eclipse Tools for Bluemix oder die DevOps-Web-IDE. Die dev_mode-CLI kann bis 30. Juni 2016 verwendet werden.

Die Bluemix-Befehlszeile für den Entwicklungsmodus (CLI 'dev_mode') ermöglicht das Aktualisieren Ihrer Apps, während sie in der Cloud ausgeführt werden. Die CLI 'dev_mode' wurde als cf-CLI-Plug-in aufgebaut und unterstützt sowohl Liberty- als auch IBM Node.js-Apps.
{: shortdesc}


Mit der CLI 'dev_mode' können Sie die folgenden Tasks ausführen:
- Wechseln der App zwischen Entwicklungsmodus und normalem Modus.
- Inkrementelles Aktualisieren der Anwendungsdateien ohne neue Push-Operation.
- Starten, Stoppen oder Neustarten Ihrer App im vorhandenen Container.

## Plug-in 'dev_mode' installieren
**Voraussetzung:** Zuerst müssen Sie die Cloud Foundry-CLI installieren. Details hierzu finden Sie unter [Start coding with Cloud Foundry command line interface](https://github.com/cloudfoundry/cli).


Installieren Sie das Befehlszeilentool 'dev_mode' über eine der folgenden Methoden:
- Lokale Installation.
  1. Laden Sie das dev_mode-Plug-in für Ihre Plattform aus dem [IBM Bluemix-CLI-Plug-in-Repository](http://plugins.ng.bluemix.net) herunter.
  2. Wechseln Sie zu dem Ordner mit dem dev_mode-Plug-in und installieren Sie das Plug-in mithilfe des Befehls 'cf install-plugin'. Beispiel:

        ```
        cf install-plugin dev_mode-linux64
        ```

- Installation aus dem Bluemix-CLI-Repository
  1. Fügen Sie das Repository 'bluemix-repo' zu den Cloud Foundry-CLI-Repositorys hinzu, indem Sie den folgenden Befehl verwenden:

        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Geben Sie 'cf repo-plugins' ein. Daraufhin wird das dev_mode-Plug-in im Repository 'bluemix-repo' angezeigt.

		```
        cf repo-plugins
        ```

  3. Installieren Sie das dev_mode-Plug-in in die Cloud Foundry-CLI-Plug-ins, indem Sie den folgenden Befehl verwenden:

        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Befehle der CLI 'dev_mode' anzeigen

Verwenden Sie den folgenden Befehl, um alle Befehle der CLI 'dev_mode' anzuzeigen:

```
cf plugins
```

## Index für Befehle der CLI 'dev_mode'
{: #dev_mode_cmds_index}

Verwenden Sie den Index in der folgenden Tabelle als Referenz für die häufig verwendeten Befehle der CLI 'dev_mode':

<table summary="Index der Befehle für dev_mode">
<caption>Tabelle 1. Befehle für dev_mode</caption>
 <thead>
 <th colspan="4">Befehle für dev_mode</th>
 </thead>
 <tbody>
 <tr>
 <td>[help](#help)</td>
 <td>[mode](#mode)</td>
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr>
 <tr>
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody>
 </table>


## help
{: #help}

Es wird Hilfetext zu einem Befehl angezeigt.

```
cf help <Befehlsname>
```


## mode
{: #mode}

Ändern des App-Modus.

```
cf mode <appName> <dev|normal>
```
<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>dev</dt>
   <dd>Entwicklungsmodus</dd>
   <dt>normal</dt>
   <dd>Produktionsmodus</dd>
   </dl>


## status
{: #status}

Anzeigen des App-Modus und des Laufzeitstatus.
```
cf status <App-Name>
```



## update-file
{: #update_file}

Aktualisieren von Anwendungsdateien in der Cloud.

```
cf update-file <ferner Pfad> <localPath> [Befehlsoptionen]
```


<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>expand</dt>
   <dd>Gibt an, ob die hochgeladenen Dateien aus der ZIP-Datei extrahiert werden müssen.</dd>
   <dt>restart</dt>
   <dd>Die App-Laufzeit wird nach der Dateiaktualisierung neu gestartet.</dd>
   </dl>



## delete-file
{: #delete_file}

Löschen von Anwendungsdateien in der Cloud.

```
cf delete-file <ferner Pfad> [Befehlsoptionen]
```


<strong>Befehlsoptionen</strong>:
 <dl>
   <dt>restart</dt>
   <dd>Die App-Laufzeit wird nach der Dateiaktualisierung neu gestartet.</dd>
  </dl>


## start-inplace
{: #start_inplace}
Die App wird im vorhandenen Container gestartet.

```
cf start-inplace <App-Name>
```



## stop-inplace
{: #stop_inplace}
Die App wird im vorhandenen Container gestoppt.

```
cf stop-inplace <App-Name>
```



## restart-inplace
{: #restart_inplace}

Die App wird im vorhandenen Container neu gestartet.

```
cf restart-inplace <App-Name>
```



# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}
* [Befehlszeilenschnittstelle (CLI) für Entwicklungsmodus ![Symbol für externen Link](../../../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){:new_window}
* [DevOps-Web-IDE ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://hub.jazz.net/docs/deploy/){:new_window}
