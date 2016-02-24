# Bluemix-CLI 'dev_mode'
Der Entwicklungsmodus ist ein Bluemix-Feature, das Sie für die Arbeit mit Ihren Apps nutzen können, während diese in der Cloud aktiv sind. Der Entwicklungsmodus schließt die Befehlszeilenschnittstelle 'dev_mode' ein. Die CLI 'dev_mode' wurde als cf-CLI-Plug-in aufgebaut und unterstützt sowohl Liberty- als auch IBM Node.js-Apps.

Die CLI 'dev_mode' stellt die folgenden Features zur Verfügung:
- Wechseln der App zwischen Entwicklungsmodus und normalem Modus.
- Inkrementelles Aktualisieren der Anwendungsdateien ohne neue Push-Operation.
- Starten, Stoppen oder Neustarten Ihrer App im vorhandenen Container.

## Einführung
**Voraussetzung:** Zuerst müssen Sie die Cloud Foundry-CLI installieren. Details hierzu finden Sie unter [Start coding with Cloud Foundry command line interface](https://github.com/cloudfoundry/cli). 


Installieren Sie das Befehlszeilentool 'dev_mode' über eine der folgenden Methoden:
- Lokale Installation.
  1. Laden Sie das dev_mode-Plug-in für Ihre Plattform aus dem [IBM Bluemix-CLI-Plug-in-Repository](http://plugins.ng.bluemix.net) herunter.
  2. Installieren Sie das dev_mode-Plug-in mithilfe des Befehls 'cf install-plugin':
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Installation aus dem Bluemix-CLI-Repository.
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

## Verwendung
**Um alle Befehle der CLI 'dev_mode' anzuzeigen, verwenden Sie den folgenden Befehl:**

```
cf plugins
```

### Befehle für dev_mode

### mode

```
cf mode <App-Name> <dev|normal>
```

Ändern des App-Modus.

### status

```
cf status <App-Name>
```

Anzeigen des App-Modus und des Laufzeitstatus.

### update-file

```
cf update-file <ferner Pfad> <localPath> [Befehlsoptionen]
```

Aktualisieren von Anwendungsdateien in der Cloud.

Befehlsoptionen:

**expand**

Gibt an, ob die hochgeladenen Dateien aus der ZIP-Datei extrahiert werden müssen.

**restart**

Die App-Laufzeit wird nach der Dateiaktualisierung neu gestartet.
  
### delete-file

```
cf delete-file <ferner Pfad> [Befehlsoptionen]
```

Löschen von Anwendungsdateien in der Cloud.

Befehlsoptionen:

**restart**

Die App-Laufzeit wird nach der Dateilöschung neu gestartet.

### start-inplace

```
cf start-inplace <App-Name>
```

Die App wird im vorhandenen Container gestartet.

### stop-inplace

```
cf stop-inplace <App-Name>
```

Die App wird im vorhandenen Container gestoppt.

### restart-inplace

```
cf restart-inplace <App-Name>
```

Die App wird im vorhandenen Container neu gestartet.



### help

```
cf help <Befehlsname>
```
Es wird Hilfetext zu einem Befehl angezeigt.
