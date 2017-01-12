---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Angepasste Toolchains konfigurieren (Experimentell)
{: #toolchains-custom}
Letzte Aktualisierung: 27. April 2016
{: .last-updated}

Die Erstellung einer angepassten Toolchain kann zur Verbesserung des DevOps-Workflows beitragen. Verwenden Sie für einen schnellen Start eine der vorhandenen Toolchain-Vorlagen oder passen Sie eine der Vorlagen an, um eine Toolchain zu erstellen, die Ihren Anforderungen besser entspricht.
{:shortdesc}

Es gibt mehrere Möglichkeiten zur [Erstellung und Bereitstellung einer Toolchain](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}. In diesem Handbuch werden die Schritte zur Erstellung einer angepassten Toolchain erläutert, die mithilfe einer Schaltfläche zum [Bereitstellen in {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window} bereitgestellt werden kann. Nach einigen Konfigurationsschritten ist die gemeinsame Nutzung eines GitHub-Projekts mit einer bereitstellbaren Toolchain in {{site.data.keyword.Bluemix_notm}} möglich.


## Einführung
{: #toolchains_custom_gettingstarted}

Zur Erstellung einer angepassten Toolchain wird zunächst eine Toolchain-Vorlage geklont. Das Klonen einer vorhandenen Vorlage stellt eine schnelle Möglichkeit dar, um mit der Anpassung zu beginnen.

1. Geben Sie unter Verwendung eines Git-Clients Ihrer Wahl den folgenden Befehl ein, um die Vorlage [Einfache Toolchain](https://github.com/open-toolchain/simple-toolchain){: new_window} in GitHub zu klonen.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 Diese Vorlage stellt eine Hello World-Basisanwendung aus einem einzigen GitHub-Repository bereit und enthält eine einfache Toolchain, die für Continuous Delivery, Quellcodeverwaltung, Problemverfolgung und Onlinebearbeitung vorkonfiguriert ist.

2. **(Optional)**: Wenn Sie lieber mit einer komplexeren Toolchain-Vorlage beginnen möchten, können Sie auch die [cloud-native Toolchain für Microservices](https://github.com/open-toolchain/toolchain-demo){: new_window} klonen.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 Diese Vorlage stellt ein Onlinegeschäft bereit, das aus drei Microservices besteht, die jeweils in einem eigenen GitHub-Repository enthalten sind. Ferner ist eine komplexere Toolchain enthalten, die für Continuous Delivery, Quellcodeverwaltung,  Blue-Green-Deployments, Funktionstests, Problemverfolgung, Onlinebearbeitung und Messaging vorkonfiguriert ist.

Die in diesem Handbuch beschriebenen Richtlinien zur Erstellung angepasster Toolchains gelten unabhängig von der ausgewählten Vorlage.

Nach dem Klonen der Vorlage verfügen Sie über ein GitHub-Basisrepository mit einer *Readme-Datei* und einem Verzeichnis `.bluemix`, das alle für das Funktionieren der Toolchain erforderlichen Konfigurationsdateien enthält. Das Verzeichnis `.bluemix` sollte mindestens Folgendes enthalten:

* toolchain.yml
* deploy.json
* pipeline.yml

Diese Dateien werden in den folgenden Abschnitten zusammen mit einigen zusätzlichen Konfigurationsschritten beschrieben, die im Zuge der Weiterentwicklung der Toolchain möglicherweise erforderlich sind.

## Überblick über Konfigurationsdateien
{: #toolchains_custom_config_files}

Die Konfigurationsdateien der Toolchain-Vorlage bestehen hauptsächlich aus Dateien im YAML-Format. Jede Datei enthält Metadaten, die verschiedene Aspekte der Toolchain beschreiben. Dazu gehören allgemeine beschreibende Informationen zur Toolchain, die einzufügenden GitHub-Repositorys, Details zur Codeerstellung und zum Ort der Bereitstellung sowie Konfigurationsdetails zu den verschiedenen Tools, die Sie in die Toolchain einfügen. Mit zunehmender Komplexität der Toolchain werden auch die Konfigurationsdateien komplexer. Es ist wichtig, die Formatierung der Dateien zu überwachen, um das Fehlerrisiko zu verringern.

Beachten Sie beim Arbeiten mit YAML-Dateien die folgenden Richtlinien:

* Tabulatoren sind nicht zulässig. Es dürfen nur Leerzeichen verwendet werden.
* Alle Eigenschaften und Listen müssen mit einem oder mehreren Leerzeichen eingerückt werden.
* Bei allen Schlüsseln und Eigenschaften muss die Groß-/Kleinschreibung beachtet werden.

Zur Überprüfung Ihrer Arbeit können Sie ein einfaches YAML-Prüfprogramm wie den [YAML-Parser](http://wiki.ess3.net/yaml/){: new_window} verwenden, um Fehler dieser Art zu vermeiden.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

Die Datei `toolchain.yml` ist das Herzstück der Toolchain. In dieser Datei werden die Spezifikationen der Toolchain, die einzufügenden Repositorys und Services sowie die Builddetails beschrieben. Zum besseren Verständnis des Inhalts ist eine Aufteilung der Datei in mehrere Abschnitte möglich.

1\. **Einführende Informationen zu Toolchains:**

 In diesem Abschnitt werden einfache Details zu Ihrer Toolchain beschrieben, die dem Benutzer auf der Seite zum Erstellen der Toolchain angezeigt werden. Geben Sie einen Namen für die Toolchain sowie eine Beschreibung an, die den Zweck der Toolchain bzw. die Aufgaben der Toolchain nach der Bereitstellung erläutert. Ferner kann ein Bild für ein Logo oder eine grafische Darstellung der Toolchain eingefügt werden.

 Zusätzlich zu den einführenden Informationen zu Ihrer Toolchain enthält dieser Abschnitt einen Schlüssel namens `required`, der die Toolintegrationen definiert, die im Rahmen der Erstellung auf der Seite zum Erstellen der Toolchain konfiguriert werden können. Das Konfigurieren eines Tools im Rahmen der Erstellung ermöglicht das Erstellen einer Toolchain, die problemlos wiederverwendet oder einem neuen Zweck zugeführt werden kann. Fügen Sie für jedes Tool, das auf der Seite zum Erstellen der Toolchain konfiguriert werden kann, den jeweiligen übergeordneten Schlüssel gemäß den Angaben in der Datei `toolchain.yml` als Eigenschaft des Schlüssels `required` hinzu.

 Das folgende Snippet stellt ein Beispiel dieses Abschnitts dar:

 ```
 ---
 name: "Simple Toolchain"
 description: "This Hello World application uses Node.js and includes a toolchain that is preconfigured for continuous delivery, source control, issue tracking, and online editing.\n\nTo get started, click **Create**."
 version: 0.1
 # Generate base64 representation of image at http://www.askapache.com/online-tools/base64-image-converter/
 image: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAA...
 required: 
  - deploy
  - hello-world-repo
  ```
 {: codeblock}

 **Anmerkung:** Bilder müssen zuerst mit einem Tool wie [AskApache](http://www.askapache.com/online-tools/base64-image-converter/) in eine Base64-Darstellung konvertiert werden.

2\. **GitHub-Repository-Definitionen:**

 Eine Toolchain kann Continuous Delivery für eine beliebige Anzahl von GitHub-Repositorys bereitstellen. In diesem Abschnitt der Datei `toolchain.yml` werden die einzelnen Repositorys definiert.

 Fügen Sie zunächst für jedes GitHub-Repository, das in die Toolchain eingefügt wird, einen übergeordneten Schlüssel hinzu, der den Namen des GitHub-Repositorys mit den folgenden Eigenschaften angibt:

| Element | Schlüssel/Eigenschaft | Wert | Beschreibung |
|------|--------------|-------|-------------|
| repo-name | Schlüssel |  | Repository-Name. |
| service_id | Eigenschaft | <`githubpublic` , `githubprivate`> | Typ des GitHub-Repositorys. |
| parameters: | Schlüssel |  |  |
| repo_name | Eigenschaft |  | **Kommentar:  Wie soll dies definiert werden** |
| repo_url | Eigenschaft |  | URL des GitHub-Repositorys. |
| type | Eigenschaft | <`new` , `fork` , `clone` , `link`> | Gibt an, wie das Repository erstellt werden soll. |
| has_issues | Eigenschaft | <`true` , `false`> | Verwendung von GitHub Issues. |

 **Anmerkung:** Wenn Sie mehrere Repositorys definieren und diese mit der Angabe `has_issues: true` konfigurieren, wird eine einzelne Instanz des GitHub Issue-Trackers zur Toolchain hinzugefügt, der Probleme für alle Repositorys verfolgt, die auf `true` gesetzt wurden.

 Das folgende Snippet stellt ein Beispiel dieses Abschnitts dar:

 ```
 # Github repos
 hello-world-repo:
   service_id: githubpublic
   parameters:
 	repo_name: "hello-world-{{name}}"
 	repo_url: https://github.com/open-toolchain/node-hello-world
 	type: clone
 	has_issues: true
 ```
 {: codeblock}

3\. **Informationen zu Pipelines:**

 Die Pipeline macht Continuous Delivery möglich. In diesem Abschnitt werden die Konfigurationsdetails zur Erstellung und Bereitstellung des Codes in den einzelnen GitHub-Repositorys definiert.

 Fügen Sie zunächst für jedes GitHub-Repository, das in der Toolchain definiert wurde, einen übergeordneten Schlüssel hinzu, der den Namen der zugehörigen Pipeline angibt. Es ist sinnvoll, diesen Schlüssel vom Namen des GitHub-Repositorys abzuleiten. Fügen Sie die folgenden Eigenschaften hinzu:

| Element | Schlüssel/Eigenschaft | Wert | Beschreibung |
|------|--------------|-------|-------------|
| pipeline-name | Schlüssel |  | Name der Pipeline. |
| service_id | Eigenschaft | <`pipeline`> | Name des zu verwendenden Service. |
| parameters | Schlüssel |  |  |
| name | Eigenschaft | <`repo_name`> | Entspricht dem Namen, der im Abschnitt für GitHub-Repositorys definiert ist. |
| ui-pipeline | Eigenschaft | <`true` , `false`> |  |
| configuration | Schlüssel |  |  |
| content | Eigenschaft | <`$file(pipeline.yml)`> | Datei mit der Pipelinedefinition. |
| env | Schlüssel |  |  |
| REPO_NAME | Schlüssel | <`repo-name-key`> | Entspricht dem Namen des übergeordneten Schlüssels für das GitHub-Repository. |
| CF_APP_NAME |  Eigenschaft | <`"{{deploy.parameters.repo-name-key}}"`> | Von Cloud Foundry verwendeter Name. Sollte den Namen des übergeordneten Schlüssels für das GitHub-Repository enthalten. |
| PROD_SPACE_NAME | Eigenschaft | <`"{{deploy.parameters.prod-space}}"`> | Name des {{site.data.keyword.Bluemix_notm}}-Bereichs, in dem die Bereitstellung erfolgt. |
| PROD_ORG_NAME | Eigenschaft | <`"{{deploy.parameters.prod-organization}}"`> | Name der {{site.data.keyword.Bluemix_notm}}-Organisation, in der die Bereitstellung erfolgt. |
| PROD_REGION_ID | Eigenschaft | <`"{{deploy.parameters.prod-region}}"`> | Name der {{site.data.keyword.Bluemix_notm}}-Region, in der die Bereitstellung erfolgt. |
| execute | Eigenschaft | <`true` , `false`> | Pipeline nach der Erstellung starten. |
| services | Eigenschaft | <`repo-name-key`> |  Übergeordneter Schlüssel für das GitHub-Repository. |
| hidden | Eigenschaft | <`[form, description]`> |  |

 Informationen zur Erstellung der Datei `pipeline.yml` finden Sie in einem [späteren Abschnitt](#toolchains_custom_pipeline_yml).

 Das folgende Snippet stellt ein Beispiel dieses Abschnitts dar:

 ```
 # Pipelines
 hello-world-build:
   service_id: pipeline
   parameters:
 	name: "hello-world-{{name}}"
 	ui-pipeline: true
 	configuration: 
 	 content: $file(hello-world.pipeline.yml)
 	 env:
 	  HELLO_WORLD_REPO: "hello-world-repo"
 	  CF_APP_NAME: "{{deploy.parameters.hello-world-name}}"
 	  PROD_SPACE_NAME: "{{deploy.parameters.prod-space}}"
 	  PROD_ORG_NAME: "{{deploy.parameters.prod-organization}}"
 	  PROD_REGION_ID: "{{deploy.parameters.prod-region}}"
 	 execute: true
 	services: ["hello-world-repo"]
   hidden: [form, description]
 ```
 {: codeblock}

4\. **Informationen zur Bereitstellung:**

 Im Rahmen des Continuous Delivery-Prozesses kann eine Toolchain konfiguriert werden, um Ihre Anwendung in einer {{site.data.keyword.Bluemix_notm}}-Region oder -Organisation oder in einem Bluemix-Bereich bereitzustellen, auf die bzw. den der Benutzer, der die Toolchain bereitstellt, Zugriff hat. Einzelheiten dazu, wo die Anwendung bereitgestellt werden soll, können auf der Seite zum Erstellen der Toolchain ausgewählt werden.  

 ![Einstellungen für die Delivery Pipeline-Konfiguration](images/deploy_configuration.png)

 Dieser Abschnitt der Datei `toolchain.yml` definiert die Pipelinephasen, die auf der Seite zum Erstellen der Toolchain konfiguriert werden können.

 Zunächst werden mithilfe des übergeordneten Schlüssels `deploy` die Eigenschaften der Bereitstellungskonfiguration angegeben. Der restliche Abschnitt setzt sich aus den nachfolgenden Eigenschaften zusammen:

| Element | Schlüssel/Eigenschaft | Wert | Beschreibung |
|------|--------------|-------|-------------|
| deploy | Schlüssel |  | Name des Abschnitts für die Bereitstellung. |
| schema | Eigenschaft | <`deploy.json`> | Datei, die das Layout der Benutzerschnittstelle für die Konfiguration der Bereitstellungsdetails definiert. |
| service-category | Eigenschaft | <`pipeline`> | Service, der die Bereitstellungskonfigurationen verwendet. |
| parameters | Schlüssel |  |  |
| prod-region | Eigenschaft | <`"{{region}}"`> | Definiert die {{site.data.keyword.Bluemix_notm}}-Region für die Produktionsphase. |
| prod-organization | Eigenschaft | <`"{{organization}}"`> | Definiert die {{site.data.keyword.Bluemix_notm}}-Organisation für die Produktionsphase. |
| prod-space | Eigenschaft | <`prod`> | Definiert den {{site.data.keyword.Bluemix_notm}}-Bereich für die Produktionsphase. |
| github-repo-name | Eigenschaft | <`"{{repo-name-key.parameters.repo_name}}"`> | Variable zum Übergeben des GitHub-Repository-Namens an die Seite zum Erstellen der Toolchain. |

 Informationen zur Erstellung der Datei `deploy.json` finden Sie in einem [späteren Abschnitt](#toolchains_custom_deploy_json).

 Das folgende Beispiel definiert eine einzige Phase für die Bereitstellung in einer Produktionsumgebung.

 ```
 #Deployment
 deploy:
   schema: deploy.json
   service-category: pipeline
   parameters:
 	prod-region: "{{region}}"
 	prod-organization: "{{organization}}"
 	prod-space: prod
 	hello-world-name: "{{hello-world-repo.parameters.repo_name}}"
 ```
 {: codeblock}

 Das Codebeispiel kann nahezu unverändert übernommen werden und erfordert nur geringfügige Änderungen. Aktualisieren Sie zur Anpassung dieses Abschnitts das Element `github-repo-name` so, dass es mit dem Repository-Namen konsistent ist. Die Informationen in der Datei [`deploy.json`](#toolchains_custom_deploy_json) müssen ebenfalls aktualisiert werden.

 Zur Erstellung einer komplexeren Pipeline mit einer 'dev'-, 'qa'- und 'prod'-Phase können die folgenden Eigenschaften unter dem Schlüssel `parameters` ersetzt werden.

 ```
   parameters:
 	dev-region: "{{region}}"
 	qa-region: "{{region}}"
 	prod-region: "{{region}}"
 	dev-organization: "{{organization}}"
 	qa-organization: "{{organization}}"
 	prod-organization: "{{organization}}"
 	dev-space: dev
 	qa-space: qa
 	prod-space: prod
 ```
 {: codeblock}

5\. **Toolkonfigurationen**

 Nach der Konfiguration der Kernkomponenten der Toolchain können Sie weitere Toolintegrationen einfügen, mit deren Hilfe zusätzliche Funktionalität hinzugefügt und die Zweckmäßigkeit der Toolchain optimiert werden kann. Alle Tools verfügen über einen Eintrag, der in die Datei `toolchain.yml` eingefügt werden muss. Für einige Tools ist außerdem eine separate YAML-Konfigurationsdatei erforderlich, die im Verzeichnis `.bluemix` erstellt werden sollte.

 * **Slack**

	toolchain.yml
	```
	messaging:
	  service_id: slack
	  include: slack.yml
	```
	{: codeblock}
	
	slack.yml
	```
	---
	parameters:
	  api_token: ""
	  channel_name: ""
	```
	{: codeblock}
	
 * **Sauce Labs**

	toolchain.yml
	```
	test:
	  service_id: saucelabs
	  include: saucelabs.yml
	```
	{: codeblock}
	
	saucelabs.yml
	```
	---
	parameters:
	  username: ""
	  key: ""
	```
	{: codeblock}
	
 * **PagerDuty**

	toolchain.yml
	```
	alerting:
	  service_id: pagerduty
	  include: pagerduty.yml
	```
	{: codeblock}

	pagerduty.yml
	```
	---
	parameters:
	  site_name: ""
	  api_key: ""
	  service_name: ""
	  user_email: ""
	  user_phone: ""
	```
	{: codeblock}
	
 * **Web-IDE für Eclipse Orion**

	toolchain.yml
	```
	webide:
	  service_id: orion
	```
	{: codeblock}


## pipeline.yml
{: #toolchains_custom_pipeline_yml}

Die Datei `pipeline.yml` enthält sämtliche Konfigurationsdetails für die Phasen Ihrer Pipeline. Zur Erstellung der Datei `pipeline.yml` gibt es zwei Möglichkeiten.

1. Erstellen Sie die Datei `pipeline.yml` manuell. Weitere Informationen und die Syntax zur Erstellung der Datei `pipeline.yml` finden Sie unter [Textbasierte Pipelines in Beispielprojekten von DevOps Services gemeinsam nutzen](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}.

2. Generieren Sie die Datei `pipeline.yml` aus einem vorhandenen DevOps Services-Projekt. Gehen Sie wie folgt vor:
	
	1. Erstellen Sie ein neues [DevOps Services-Projekt](https://hub.jazz.net/create){: new_window}.
	
	2. Öffnen Sie das Projekt und klicken Sie auf **BUILD & DEPLOY**.
	
	3. Konfigurieren Sie alle für die Pipeline erforderlichen Phasen.
	
	4. Hängen Sie in der Adressleiste des Browsers `/yaml` an die Projekt-URL an und drücken Sie die Eingabetaste.
	
	5. Speichern Sie die erstellte Datei `pipeline.yml` im Verzeichnis `.bluemix` des GitHub-Repositorys.

Wenn Ihre Toolchain mehrere Pipelines enthält, geben Sie für jede Datei `pipeline.yml` einen eindeutigen Namen an.

Im Folgenden ist ein Beispiel für die Datei `pipeline.yml` dargestellt:

```
---
stages:
- name: BUILD
  inputs:
  - type: git
	branch: master
	service: ${HELLO_WORLD_REPO}
  triggers:
  - type: commit
  jobs:
  - name: Build
	type: builder
- name: DEPLOY
  inputs:
  - type: job
	stage: BUILD
	job: Build
  triggers:
  - type: stage
  properties:
  - name: CF_APP_NAME
	value: undefined
	type: text
  - name: APP_URL
	value: undefined
	type: text
  jobs:
  - name: Deploy
	type: deployer
	target:
	  region_id: ${PROD_REGION_ID}
	  organization: ${PROD_ORG_NAME}
	  space: ${PROD_SPACE_NAME}
	  application: ${CF_APP_NAME}
	script: |
	  #!/bin/bash
	  # Push app
	  export CF_APP_NAME="$CF_APP"
	  cf push "${CF_APP_NAME}"
	  export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
	  # View logs
	  #cf logs "${CF_APP_NAME}" --recent
```
{: codeblock}		


## deploy.json
{: #toolchains_custom_deploy_json}

Auf der Seite zum Erstellen der Toolchain wird bei Auswahl von 'Delivery Pipeline' im Abschnitt 'Konfigurierbare Integrationen' der Abschnitt erweitert, um die folgenden Elemente anzuzeigen, die für das Tool konfiguriert werden können:

	* Anwendungsname
	* Region, Organisation und Bereich, für die die Bereitstellung der Pipelinephasen erfolgt.

![Einstellungen für die Delivery Pipeline-Konfiguration](images/deploy_configuration.png)

Das Layout dieses Abschnitts in der Benutzerschnittstelle wird durch das Schema `deploy.json` definiert.

Aktualisieren Sie in diesem Schema die folgenden Eigenschaften, um sie mit den Details Ihrer Anwendung abzugleichen:

	* Title
	* Beschreibung
	* Langbeschreibung
	* Alle Instanzen von `hello-world-name` und die zugehörigen Details sollten mit der Anwendung abgeglichen werden.

Im Folgenden ist ein Beispiel für die Datei `deploy.json` dargestellt:

```
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Hello World Deploy Stage",
    "description": "hello-world simple toolchain",
    "longDescription": "The Delivery Pipeline for Devops Services allows you to automate your continuous deployment setup hello-world.",
    "type": "object",
    "properties": {
        "prod-region": {
            "description": "The bluemix region",
            "type": "string"
        },
        "prod-organization": {
            "description": "The bluemix org",
            "type": "string"
        },
       "prod-space": {
            "description": "The bluemix space",
            "type": "string"
        },
       "hello-world-name": {
            "description": "hello world app name",
            "type": "string"
        }
    },
    "required": ["prod-region", "prod-organization", "prod-space", "hello-world-name"],
    "form": [
       {
          "type": "validator",
          "url": "/devops/setup/bm-helper/helper.html"
       },        
        {
          "type": "text",
          "readonly": false,
          "title": "Hello World App Name",
          "key": "hello-world-name"
        },
        {
            "type": "table",
            "columnCount": 4,
            "widths": ["15%", "28%", "28%", "28%"],
            "items": [
                {
                  "type": "label",
                  "title": ""
                },
                {
                  "type": "label",
                  "title": "Region"
                },
                {
                  "type": "label",
                  "title": "Organization"
                },
                {
                  "type": "label",
                  "title": "Space"
                },
                {
                  "type": "label",
                  "title": "Prod Stage"
                },
                {
                  "type": "select",
                  "key": "prod-region"
                },
                {
                  "type": "select",
                  "key": "prod-organization"
                },
                {
                  "type": "select",
                  "key": "prod-space",
                  "readonly": false
                }
            ]
        }
    ]
}
```
{: codeblock}
