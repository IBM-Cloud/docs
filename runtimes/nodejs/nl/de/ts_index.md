---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Fehlerbehebung bei SDK for Nodejs
{: #ts}


Es folgen die Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von SDK for Nodejs in {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Das Starten der Anwendung schlug mit der Nachricht über fehlenden Speicherplatz auf der Einheit fehl: “No space left on device”.
{: #no_space_left_on_device}


Das Starten einer Nodejs-Anwendung schlug mit der Nachricht über fehlenden Speicherplatz auf der Einheit fehl: “No space left on device”. Der Fehler kann in den Protokollen beispielsweise wie folgt aussehen: {: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Nodejs-Anwendungen, die NPM-Versionen vor Version 3 verwenden, verbrauchen mehr Speicherplatz beim Herunterladen von Abhängigkeiten.
{: tsCauses}

Ändern Sie die Datei 'package.json' für Ihre Anwendung, um eine NPM Version zu verwenden, die höher als Version 3 ist.
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}
