---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configurazione di toolchain personalizzate (sperimentale)
{: #toolchains-custom}
Ultimo aggiornamento: 27 aprile 2016
{: .last-updated}

La creazione di una toolchain personalizzata può aiutarti a migliorare il tuo flusso di lavoro DevOps. Puoi iniziare rapidamente con uno dei template di toolchain esistenti o puoi personalizzare uno di questi template per creare una toolchain più adeguata.
{:shortdesc}

Esistono diversi modi per [creare e distribuire una toolchain](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}.  Questa guida spiegherà la procedura per creare una toolchain personalizzata che può essere distribuita utilizzando un pulsante [Distribuisci a {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window}. Dopo alcune configurazioni, potrai condividere facilmente un progetto GitHub con una toolchain distribuibile in {{site.data.keyword.Bluemix_notm}}.


## Introduzione
{: #toolchains_custom_gettingstarted}

Per creare una toolchain personalizzata, cominciamo a clonare un template di toolchain. La clonazione di un template esistente ti fornisce rapidamente un punto di partenza per la personalizzazione.

1. Utilizzando il tuo client Git preferito, immetti il seguente comando per clonare il template [Simple Toolchain](https://github.com/open-toolchain/simple-toolchain){: new_window} in GitHub.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 Questo template distribuisce un'applicazione Hello World di base da un unico repository GitHub e include una toolchain semplice che è preconfigurata per la fornitura continua, il controllo dell'origine, la traccia dei problemi e la modifica in linea.

2. **(Facoltativo)**: se preferisci iniziare con il template di una toolchain più complessa, puoi clonare [Cloud-native Toolchain for Microservices](https://github.com/open-toolchain/toolchain-demo){: new_window}.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 Questo template distribuisce un negozio online composto da tre microservizi, ciascuno contenuto nel proprio repository GitHub.  È inclusa anche una toolchain più complessa preconfigurata per la fornitura continua, il controllo dell'origine, le distribuzioni blue-green, le verifiche funzionali, la traccia dei problemi, la modifica in linea e la messaggistica.

Indipendentemente dal template scelto, i principi descritti in questa guida per la creazione di una toolchain personalizzata saranno simili.

Dopo aver clonato il template, avrai un repository GitHub di base che include un file *Readme* e una directory `.bluemix` contenente tutti i file di configurazione necessari per rendere funzionante la tua toolchain.  Come minimo, la directory `.bluemix` deve contenere i seguenti file:

* toolchain.yml
* deploy.json
* pipeline.yml

Ciascuno di questi file verrà illustrato nelle seguenti sezioni insieme ad alcune ulteriori configurazioni che potrebbero dover essere aggiunte in seguito allo sviluppo della toolchain.

## Comprensione dei file di configurazione
{: #toolchains_custom_config_files}

I file di configurazione del template di toolchain sono composti principalmente da file in formato YAML.  Ogni file contiene dei metadati che descrivono i diversi aspetti della toolchain.  Ciò include informazioni descrittive generali sulla toolchain, i repository GitHub da includere, dettagli su come compilare il codice e su dove distribuirlo e dettagli di configurazione per i vari strumenti che includerai nella tua toolchain.  Man mano che la toolchain diventa più complessa, anche i file di configurazioni si adegueranno di conseguenza.  È importante che i file rimangano ben formattati per ridurre il rischio di introdurre errori.

Alcune linee guida da tenere a mente quando si utilizza un file YAML:

* Le schede non sono consentite.  Devono essere utilizzati solo gli spazi.
* Tutte le proprietà e tutti gli elenchi devono essere rientrati con uno o più spazi.
* Tutte le chiavi e proprietà sono sensibili al maiuscolo/minuscolo.

Per ricontrollare il tuo lavoro, può essere utile utilizzare un semplice validatore YAML come questo [Parser YAML](http://wiki.ess3.net/yaml/){: new_window} per evitare eventuali errori.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

Il file `toolchain.yml` è il cuore della tua toolchain. Le specifiche della toolchain, che includono i repository da richiamare, i servizi da includere e i dettagli di build, sono tutte descritte in questo file. Per dare un senso al suo contenuto, può essere suddiviso in più sezioni.

1\. **Informazioni introduttive sulla toolchain:**

 Questa sezione fornisce dei semplici dettagli sulla tua toolchain che vengono presentati all'utente nella pagina di creazione della toolchain. Devi fornire un nome per la tua toolchain insieme a una descrizione che ne spieghi lo scopo o la sua funzionalità una volta distribuita. Si può anche includere un'immagine per visualizzare un logo o una rappresentazione visiva della toolchain.

 Oltre a fornire informazioni introduttive per la tua toolchain, questa sezione include anche una chiave denominata `required` che definisce le integrazioni dello strumento che è possibile configurare durante la creazione della toolchain nella pagina relativa. La configurazione di uno strumento al momento della creazione ti permette di creare una toolchain che può essere facilmente riutilizzata o riproposta.  Per ogni strumento che può essere configurato nella pagina di creazione della toolchain, aggiungi la chiave principale degli strumenti definita nel file `toolchain.yml` come proprietà della chiave `required`.

 Il seguente frammento mostra un esempio di questa sezione:

 ```
 ---
 name: "Simple Toolchain"
 description: "Questa applicazione Hello World utilizza Node.js e include una toolchain che è preconfigurata per la fornitura continua, il controllo dell'origine, la traccia dei problemi e la modifica in line.\n\nPer iniziare, fai clic su **Crea**."
 version: 0.1
 # Genera la rappresentazione base64 dell'immagine in http://www.askapache.com/online-tools/base64-image-converter/
 image: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAA...
 required:
  - deploy
  - hello-world-repo
  ```
 {: codeblock}

 **Nota:** le immagini devono prima essere convertite in una rappresentazione base 64 utilizzando uno strumento come [AskApache](http://www.askapache.com/online-tools/base64-image-converter/).

2\. **Definizioni del repository GitHub:**

 Una toolchain può offrire la fornitura continua per un numero qualsiasi di repository GitHub.  Questa sezione del file `toolchain.yml` indica dove deve essere definito ciascun repository.

 Per iniziare, per ogni repository GitHub che verrà aggiunto alla toolchain, aggiungi una chiave principale che rappresenti il nome del tuo repository GitHub con le seguenti proprietà:

| Elemento | Chiave/Proprietà | Valore | Descrizione |
|------|--------------|-------|-------------|
| repo-name | chiave |  | Nome del repository |
| service_id | proprietà | <`githubpublic` , `githubprivate`> | Tipo di repository GitHub |
| parameters: | chiave |  |  |
| repo_name | proprietà |  | **COMMENTO:  come deve essere definito** |
| repo_url | proprietà |  | URL del repository GitHub |
| type | proprietà | <`new` , `fork` , `clone` , `link`> | Modalità di creazione del repository |
| has_issues | proprietà | <`true` , `false`> | Utilizza GitHub Issues |

 **Nota:** se definisci più repository e li configuri come `has_issues: true`, alla toolchain verrà aggiunta un'unica istanza del programma di traccia GitHub Issue che traccerà i problemi per tutti i repository impostati su `true`.

 Il seguente frammento mostra un esempio di questa sezione:

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

3\. **Informazioni sulla pipeline:**

 La fornitura continua è resa possibile dalla pipeline.  Questa sezione definisce i dettagli di configurazione utilizzati per creare e distribuire il codice nei tuoi repository GitHub.

 Per iniziare, per ogni repository GitHub che è stato definito nella tua toolchain, aggiungi una chiave principale che rappresenti un nome della sua pipeline.  Si consiglia di far derivare questa chiave dal nome del tuo repository GitHub.   Aggiungi le seguenti proprietà:

| Elemento | Chiave/Proprietà | Valore | Descrizione |
|------|--------------|-------|-------------|
| pipeline-name | chiave |  | Nome della pipeline |
| service_id | proprietà | <`pipeline`> | Nome del servizio da utilizzare |
| parameters | chiave |  |  |
| name | proprietà | <`repo_name`> | Stesso nome definito per la sezione #Github repos |
| ui-pipeline | proprietà | <`true` , `false`> |  |
| configuration | chiave |  |  |
| content | proprietà | <`$file(pipeline.yml)`> | File che definisce la definizione della tua pipeline |
| env | chiave |  |  |
| REPO_NAME | chiave | <`repo-name-key`> | Stesso nome della chiave principale del repository GitHub |
| CF_APP_NAME |  proprietà | <`"{{deploy.parameters.repo-name-key}}"`> | Nome utilizzato da Cloud Foundry.  Deve includere il nome della chiave principale del tuo repository GitHub |
| PROD_SPACE_NAME | proprietà | <`"{{deploy.parameters.prod-space}}"`> | Nome dello spazio {{site.data.keyword.Bluemix_notm}} in cui distribuire |
| PROD_ORG_NAME | proprietà | <`"{{deploy.parameters.prod-organization}}"`> | Nome dell'organizzazione {{site.data.keyword.Bluemix_notm}} in cui distribuire |
| PROD_REGION_ID | proprietà | <`"{{deploy.parameters.prod-region}}"`> | Nome della regione {{site.data.keyword.Bluemix_notm}} in cui distribuire |
| execute | proprietà | <`true` , `false`> | Avvia la pipeline dopo la creazione |
| services | proprietà | <`repo-name-key`> |  Chiave principale del repository GitHub |
| hidden | proprietà | <`[form, description]`> |  |

 Informazioni sulla creazione di un file `pipeline.yml` sono disponibili in una [sezione successiva.](#toolchains_custom_pipeline_yml)

 Il seguente frammento mostra un esempio di questa sezione:

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

4\. **Dettagli di distribuzione:**

 Come parte del processo di fornitura continua, è possibile impostare una toolchain per distribuire la tua applicazione in qualsiasi regione, organizzazione o spazio {{site.data.keyword.Bluemix_notm}} a cui ha anche accesso l'utente che distribuisce la toolchain.  I dettagli specifici di dove distribuire la tua applicazione possono essere selezionati dalla pagina di creazione della toolchain.  

 ![Impostazioni di configurazione di Delivery Pipeline](images/deploy_configuration.png)

 Questa sezione del file `toolchain.yml` definisce le fasi della pipeline che è possibile configurare dalla pagina di creazione della toolchain.

 Per iniziare, viene utilizzata la chiave principale `deploy` per identificare le proprietà di configurazione della distribuzione. Le seguenti proprietà compongono il resto della sezione:

| Elemento | Chiave/Proprietà | Valore | Descrizione |
|------|--------------|-------|-------------|
| deploy | chiave |  | Nome della sezione di distribuzione |
| schema | proprietà | <`deploy.json`> | File che definisce il layout dell'interfaccia utente per configurare i dettagli di distribuzione |
| service-category | proprietà | <`pipeline`> | Servizio che utilizzerà le configurazioni di distribuzione |
| parameters | chiave |  |  |
| prod-region | proprietà | <`"{{region}}"`> | Definisce la regione {{site.data.keyword.Bluemix_notm}} per la fase di produzione |
| prod-organization | proprietà | <`"{{organization}}"`> | Definisce la regione {{site.data.keyword.Bluemix_notm}} per la fase di produzione |
| prod-space | proprietà | <`prod`> | Definisce lo spazio {{site.data.keyword.Bluemix_notm}} per la fase di produzione |
| github-repo-name | proprietà | <`"{{repo-name-key.parameters.repo_name}}"`> | Variabile per passare il nome del repository GitHub alla pagina di creazione della toolchain |

 Informazioni sulla creazione di un file `deploy.json` sono disponibili in una [sezione successiva.](#toolchains_custom_deploy_json)

 L'esempio di seguito definisce una singola fase che distribuisce in un ambiente di produzione.

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

 L'esempio di codice può essere utilizzato in gran parte così com'è e richiede solo piccole modifiche. Per personalizzare questa sezione, occorre aggiornare `github-repo-name` affinché corrisponda al nome del tuo repository.  Dovranno essere aggiornati anche i dettagli all'interno del file [`deploy.json`](#toolchains_custom_deploy_json).

 Per creare una pipeline più complessa che includa una fase di sviluppo, QA e produzione, è possibile sostituire le seguenti proprietà sotto la chiave `parameters`.

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

5\. **Configurazioni dello strumento**

 Dopo aver configurato i componenti principali della tua toolchain, puoi iniziare a includere altre integrazioni dello strumento che permetteranno di aggiungere ulteriori funzionalità e utilità alla toolchain.  Tutti gli strumenti avranno una voce che deve essere aggiunta al file `toolchain.yml` e alcuni richiederanno anche un file di configurazione YAML separato da creare nella directory `.bluemix`.

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
	
 * **Eclipse Orion Web IDE**

	toolchain.yml
	```
	webide:
	  service_id: orion
	```
	{: codeblock}


## pipeline.yml
{: #toolchains_custom_pipeline_yml}

Il file `pipeline.yml` contiene tutti i dettagli di configurazione per le fasi della tua pipeline. È possibile creare il file `pipeline.yml` in due modi diversi.

1. Crea il file `pipeline.yml` manualmente.  I dettagli e la sintassi per creare il file `pipeline.yml` sono disponibili in [Condivisione di pipeline basate sul testo nei progetti di esempio DevOps Services](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}.

2. Genera il file `pipeline.yml` da un progetto DevOps Services esistente.  Per eseguire questa azione:
	
	1. Crea un nuovo [progetto DevOps Services](https://hub.jazz.net/create){: new_window}.
	
	2. Apri il progetto e fai clic su **CREA E DISTRIBUISCI**
	
	3. Configura tutte le fasi necessarie per la tua pipeline.
	
	4. Nella barra degli indirizzi del tuo browser, aggiungi `/yaml` all'URL del progetto e premi Invio.
	
	5. Salva il file `pipeline.yml` risultante nella directory `.bluemix` del repository GitHub.

Se la tua toolchain contiene più di una pipeline, fornisci dei nomi univoci per ciascun file `pipeline.yml`.

Di seguito è riportato un esempio di file `pipeline.yml`:

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

Nella pagina di creazione della toolchain, se si seleziona Delivery Pipeline nella sezione Integrazioni configurabili, vengono visualizzate le seguenti voci che è possibile configurare per tale strumento:

	* Il nome delle applicazioni
	* La regione, l'organizzazione e lo spazio in cui verranno distribuite le fasi della pipeline.

![Impostazioni di configurazione di Delivery Pipeline](images/deploy_configuration.png)

Il layout di questa sezione nell'interfaccia utente è definito dallo schema `deploy.json`.

All'interno dello schema, è necessario aggiornare le seguenti proprietà affinché corrispondano ai dettagli della tua applicazione:

	* Title
	* Description
	* LongDescription
	* Tutte le istanze di `hello-world-name` e i dettagli associati devono essere modificati in modo da farli corrispondere a quelli della tua applicazione.

Di seguito è riportato un esempio di file `deploy.json`:

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
