---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Condivisione di pipeline basate sul testo nei progetti di esempio {{site.data.keyword.jazzhub_short}} {: #share-pipeline}

*Ultimo aggiornamento: 7 dicembre 2015* 

Per i progetti di esempio distribuiti a {{site.data.keyword.Bluemix_notm}} mediante
il pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}},
puoi definire delle configurazioni pipeline {{site.data.keyword.jazzhub_short}} come
file YAML. Le pipeline definite come testo possono essere condivise; in questo modo, gli utenti che
biforcano il tuo progetto non devono configurare le loro pipeline. Questa funzione è in fase di sviluppo: il formato e l'implementazione YAML
potrebbero subire modifiche in qualsiasi momento. Attualmente, questa funzione è disponibile solo per i
progetti con repository Git e GitHub mirati a {{site.data.keyword.Bluemix_notm}}. 
{: shortdesc} 

Nella directory root del progetto di esempio, devi avere una cartella denominata
`.bluemix` che contiene un file `pipeline.yml`.

Quando un progetto viene clonato utilizzando il pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}, {{site.data.keyword.jazzhub_short}} crea una pipeline basata sul file `pipeline.yml`. 

Esempio: 
``` 
<root esempio>
	.bluemix
		pipeline.yml
	<altro contenuto di esempio>
```
{: codeblock} 

Il formato file YAML è un singolo documento YAML che contiene una
specifica di pipeline. La seguente pipeline {{site.data.keyword.jazzhub_short}} di esempio crea un'applicazione Java con Ant in una singola fase. Quindi, in un'altra fase, la pipeline distribuisce l'applicazione a {{site.data.keyword.Bluemix_notm}}. 

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

##Sintassi del file YAML {: #yaml-syntax}

Qualsiasi pipeline può essere rappresentata testualmente utilizzando la seguente sintassi.

Pipeline:
```
---
stages:
<sequence of stages>
```
{: codeblock} 

Stage: 
```
---
name: <name>
[inputs: 
	<sequence of inputs>] 
[triggers:   
	<sequence of triggers>] 
[properties:   
	<sequence of properties>] 
[jobs:   
	<sequence of jobs>]
```
{: codeblock} 

Input:
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

Trigger:
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
Proprietà:
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

Lavoro:
```
[name: <job name>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <extension id>] ;extension jobs only
[working_dir: <working dir path>] ;builder and tester only
[artifact_dir: artifact path>] ;builder only
[build_type: <build type>] ;builder only
[script: <script>] ;not for extension jobs
[enable_tests: 'true' | 'false'] ;builder and tester only
[test_file_pattern: <pattern>] ;builder and tester only
[target: <target>] ;deployer and extension jobs only
*[<extension property name>: <value>] ;extension jobs only
```
{: codeblock} 

Destinazione:
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

##Lavori di estensione e definizioni di estensione {: #extension-jobs} 

Le definizioni di estensione definiscono l'insieme di proprietà disponibili per
i lavori di estensione. Un lavoro viene trattato come un lavoro di estensione quando
viene specificata la proprietà `extension_id`. Per scoprire quali
proprietà sono disponibili per un'estensione, consulta la sua documentazione. 

##Interazione con le pipeline utilizzando un file YAML {: #pipeline-yaml} 

**VARIABILI DI AMBIENTE E RISOLUZIONI** 
<!-- Formating for this? -->

Prima della creazione della pipeline da un file `pipeline.yml`, la funzionalità Distribuisci a {{site.data.keyword.Bluemix_notm}} sostituisce tutte le variabili di ambiente contenute nel file con le informazioni da te specificate nell'interfaccia {{site.data.keyword.Bluemix_notm}} (ad esempio, la tua organizzazione). I valori YAML vengono sostituiti solo se
consistono esclusivamente in una variabile di ambiente. 

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

In questo esempio, l'organizzazione di destinazione viene
risolta rispetto all'URL di destinazione e il valore che permane nella configurazione
della pipeline è il GUID dell'organizzazione. La ricorrenza all'interno dello script
di distribuzione non viene sostituita.

L'URL di destinazione deve essere specificato come una variabile
di ambiente o un valore reale e devono essere forniti i GUID
o i nomi dell'organizzazione e dello spazio. Se viene fornito un valore, viene sostituito
anche l'altro.

Variabile | Descrizione 
---------------- | ---------------- 
CF_TARGET_URL |	URL di destinazione Bluemix
CF_ORGANIZATION	| Nome dell'organizzazione
CF_ORGANIZATION_ID	| GUID organizzazione
CF_SPACE |	Nome spazio
CF_SPACE_ID |	GUID spazio
CF_APP	| Nome applicazione

*Tabella - Variabili di ambiente*

**GENERAZIONE DI UN FILE YAML DA UNA PIPELINE** 

Puoi generare un file YAML da una pipeline. 

Genera il
file da una pipeline esistente con un URL in questo formato:

```
<DevOps Services domain>/pipeline/user/project/yaml
```
{: codeblock} 

Questa chiamata
non richiede un'intestazione Accept. Puoi utilizzare questa chiamata da un browser. 

**Nota:** per motivi di sicurezza, i valori della proprietà di ambiente secure-stage sono omessi dai file YAML pipeline generati. 

