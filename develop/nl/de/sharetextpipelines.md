---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Textbasierte Pipelines in Beispielprojekten von {{site.data.keyword.jazzhub_short}} gemeinsam nutzen {: #share-pipeline}

*Letzte Aktualisierung: 7. Dezember 2015* 

Für Beispielprojekte, die in {{site.data.keyword.Bluemix_notm}} über die Schaltfläche 'In {{site.data.keyword.Bluemix_notm}} bereitstellen' bereitgestellt werden, können Sie {{site.data.keyword.jazzhub_short}}-Pipelinekonfigurationen
als YAML-Dateien definieren. Pipelines, die als Text definiert sind, können gemeinsam genutzt werden,
sodass Personen, die über Verzweigungen mit Ihrem Projekt arbeiten, keine eigenen Pipelines konfigurieren müssen. Dieses Feature befindet sich im Entwicklungsstadium: Das YAML-Format und dessen Implementierung
können sich zu jedem beliebigen Zeitpunkt ändern. Zurzeit steht dieses Feature nur für Projekte mit Git- und GitHub-Repositorys zur Verfügung,
die {{site.data.keyword.Bluemix_notm}} als Ziel verwenden. 
{: shortdesc} 

Im Stammverzeichnis des Beispielprojekts muss sich ein Ordner mit dem Namen `.bluemix` befinden, der die Datei `pipeline.yml` enthält.

Wenn ein Projekt über die Schaltfläche 'In {{site.data.keyword.Bluemix_notm}} bereitstellen' geklont wird, erstellt {{site.data.keyword.jazzhub_short}} eine Pipeline auf der Basis der Datei `pipeline.yml`. 

Beispiel: 
``` 
<Beispielstammverzeichnis>
	.bluemix
		pipeline.yml
	<sonstiger Beispielinhalt>
```
{: codeblock} 

Das YAML-Dateiformat besteht aus einem einzelnen YAML-Dokument, das eine Pipelinespezifikation enthält. Mit der folgenden {{site.data.keyword.jazzhub_short}}-Beispielpipeline
wird eine Java-App mit Ant in einer Stage erstellt. In einer weiteren Stage stellt dann die Pipeline die App in {{site.data.keyword.Bluemix_notm}} bereit. 

``` 
---
stages:
- name: Build Stage
  inputs:
  - type: git
    branch: master
  triggers:
  - type: commit
  properties:
  - name: APP_VERSION
    value: '1.0'
    type: text
  jobs:
  - name: Build
    type: builder
    artifact_dir: output
    build_type: ant
    script: |-
      #!/bin/bash
      ant
    enable_tests: true
    test_file_pattern: tests/TEST-*.xml
- name: Deploy Stage
  inputs:
  - type: job
    stage: Build Stage
    job: Build
  triggers:
  - type: stage
  jobs:
  - name: Deploy to dev
    type: deployer
    target:
      url: https://api.ng.bluemix.net
      organization: uateam@ca.ibm.com
      space: dev
      application: JavaSampleUnitTest
    script: |
      cf push "${CF_APP}"
      # View logs
      #cf logs "${CF_APP}" --recent
```
{: codeblock} 

##YAML-Dateisyntax {: #yaml-syntax}

Jede beliebige Pipeline kann mithilfe der folgenden Syntax in Textformat dargestellt werden.

Pipeline:
```
---
stages:
<Stagefolge>
```
{: codeblock} 

Stage: 
```
---
name: <Name>
[inputs:
	<Eingabefolge>]
[triggers:   
	<Auslöserfolge>]
[properties:   
	<Eigenschaftenfolge>]
[jobs:   
	<Jobfolge>]
```
{: codeblock} 

Eingabe:
```
type: 'git' | 'job'
[branch: <Zweigname>] ;nur für Git-Eingaben
stage: <Stagename>		  ;nur für Job-Eingaben
job: <Jobname>			   	;nur für Job-Eingaben
```
{: codeblock} 

Trigger:
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true, wenn keine Angabe gemacht wird
```
{: codeblock} 	
	
Eigenschaft:
```
name: <Eigenschaftsname>
value: <Eigenschaftswert>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text, wenn keine Angabe gemacht wird
```
{: codeblock} 

Job:
```
[name: <Jobname>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <Erweiterungs-ID>] ;nur Erweiterungsjobs
[working_dir: <Pfad des Arbeitsverzeichnisses>] ;nur Builder und Tester
[artifact_dir: <Artefaktpfad>] ;nur Builder
[build_type: <Build-Typ>] ;nur Builder
[script: <script>] ;nicht für Erweiterungsjobs
[enable_tests: 'true' | 'false'] ;nur Builder und Tester
[test_file_pattern: <Muster>] ;nur Builder und Tester
[target: <Ziel>] ;nur Deployer und Erweiterungsjobs
*[<Name der Erweiterungseigenschaft>: <Wert>] ;Nur Erweiterungsjobs
```
{: codeblock} 

Ziel:
```
url: <Ziel-URL>
organization: <Organisationsname>
space: <Bereichsname>
[application: <Anwendungsname>]
```
{: codeblock} 

##Erweiterungsjobs und Erweiterungsdefinitionen {: #extension-jobs} 

Mit Erweiterungsdefinitionen wird die Gruppe von Eigenschaften definiert, die
den Eigenschaftsjobs zur Verfügung stehen. Ein Job wird als Erweiterungsjob behandelt, wenn die Eigenschaft `extension_id` angegeben ist. Informationen zu den für eine Erweiterung verfügbaren Eigenschaften finden Sie in der zugehörigen Dokumentation. 

##Interaktion mit Pipelines mithilfe einer YAML-Datei {: #pipeline-yaml} 

**Umgebungsvariablen und Auflösung** 
<!-- Formating for this? -->

Bevor die Pipeline aus einer Datei des Typs `pipeline.yml` erstellt wird, werden durch die Funktion 'In {{site.data.keyword.Bluemix_notm}} bereitstellen' alle Umgebungsvariablen in der Datei durch Informationen ersetzt, die Sie in der {{site.data.keyword.Bluemix_notm}}-Schnittstelle angeben (z. B. Ihre Organisation betreffend). YAML-Werte werden nur verwendet, wenn sie ausschließlich aus einer Umgebungsvariablen bestehen. 

```
{
  "project_id": "_ljkahfliasdlk",
  "env": {
     "CF_ORGANIZATION" : "user@se.ibm.com"
  },
  "config": {
    "format" : "yaml",
    "content" : "
      ...
        target:
          url: http://api.ng.bluemix.net
          organization: ${CF_ORGANIZATION}
        script: \"echo ${CF_ORGANIZATION}\"                
      ...
    "
  }
}
```
{: codeblock} 

In diesem Beispiel wird die Zielorganisation anhand der Ziel-URL aufgelöst
und beim dem in der Pipelinekonfiguration erhaltenen Wert handelt es sich um die Organisations-GUID. Für das Vorkommen im Bereitstellungsscript findet keine Ersetzung statt.

Die Ziel-URL muss als Umgebungsvariable oder als realer Wert angegeben werden und
es müssen entweder die GUIDs oder die Namen der Organisation und des Bereichs angegeben werden. Wird ein Wert angegeben, wird auch der andere ersetzt.

Variable | Beschreibung 
---------------- | ---------------- 
CF_TARGET_URL |	Bluemix-Ziel-URL
CF_ORGANIZATION	| Organisationsname
CF_ORGANIZATION_ID	| Organisations-GUID
CF_SPACE |	Bereichsname
CF_SPACE_ID |	Bereichs-GUID
CF_APP	| App-Name

*Tabelle - Umgebungsvariablen*

**YAML-Datei aus einer Pipeline generieren** 

Sie können eine YAML-Datei aus einer Pipeline generieren. 

Generieren Sie die Datei aus einer vorhandenen
Pipeline mit einer URL im folgenden Format:

```
<DevOps Services-Domäne>/pipeline/user/project/yaml
```
{: codeblock} 

Dieser Aufruf erfordert keinen Header 'Accept'. Sie können diesen Aufruf in einem Browser verwenden. 

**Hinweis:** Aus Sicherheitsgründen sind die Umgebungseigenschaftswerte für die Stage 'secure'
nicht in den generierten Pipeline-YAML-Dateien enthalten. 

