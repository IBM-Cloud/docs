---

copyright:
  years: 2016
lastupdated: "2016-11-17"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Risorse e proprietà dell'ambiente
{: #deliverypipeline_environment}

Puoi utilizzare le proprietà dell'ambiente e le risorse preinstallate per interagire con il servizio IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}. Ad esempio, puoi incorporarle in uno script del lavoro o in un comando di verifica.
{:shortdesc}

Puoi aggiungere le tue proprie proprietà dell'ambiente a una fase dalla relativa scheda **PROPRIETÀ AMBIENTE**. Le proprietà dell'ambiente sono disponibili per ogni lavoro in una fase.

Puoi aggiungere quattro tipi di proprietà dalla scheda Proprietà ambiente:
* **Testo**: una chiave della proprietà con un valore a singola riga.
* **Area di testo**: una chiave della proprietà con un valore a più righe.
* **Sicurezza**: una chiave della proprietà con un valore a singola riga. Il valore viene visualizzato come degli asterischi.
* **Proprietà**: un file nel repository del progetto. Questo file può contenere più proprietà. Ogni proprietà deve essere sulla propria riga. Per coppie di valore-chiave separate, utilizzare il segno uguale (=).


Le seguenti proprietà e risorse sono disponibili per impostazione predefinita negli ambienti della pipeline.

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## Proprietà dell'ambiente
{: #deliverypipeline_envprop}

### Proprietà di ambito generale

| Proprietà ambiente | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | La directory per archiviare o in cui scaricare gli archivi. |
| BUILD_ID | L'ID univoco per l'esecuzione del lavoro corrente.  |
| BUILD_DISPLAY_NAME | Il valore BUILD_ID, con prefisso "#". |
| BUILD_NUMBER | L'ID della fase incrementale visualizzato nella IU della pipeline.  |
| GIT_BRANCH | Il ramo Git che il lavoro utilizza come input. Questa proprietà è disponibile nei lavori che utilizzano un repository Git come input. |
| GIT_COMMIT | Il commit Git che il lavoro utilizza come input. Questa proprietà è disponibile nei lavori che utilizzano un repository Git come input. |
| GIT_PREVIOUS_COMMIT | Il valore di commit Git dell'ultima esecuzione del lavoro con esito positivo. Questa proprietà è disponibile solo nei lavori che utilizzano un repository Git come input. |
| GIT_URL | L'URL del repository Git che il lavoro utilizza come input. Questa proprietà è disponibile nei lavori che utilizzano un repository Git come input. |
| IDS_JOB_ID | L'ID univoco della configurazione del lavoro. |
| IDS_JOB_NAME | Il nome della configurazione del lavoro. |
| IDS_OUTPUT_PROPS | I nomi separati da virgole delle tue proprietà dell'ambiente della fase. |
| IDS_PROJECT_NAME | Il nome del progetto, ad esempio <code>Owner - Project Name</code>. |
| IDS_STAGE_NAME | Il nome della fase corrente. |
| IDS_URL | L'URL della pipeline corrente. |
| IDS_VERSION | Il numero per la build che sta venendo distribuita o dell'identificativo SCM. Questa proprietà è disponibile solo per i lavori di distribuzione.
| JOB_NAME | L'ID del lavoro univoco nel contesto della pipeline corrente. |
| PIPELINE_STAGE_INPUT_JOB_ID | L'ID del lavoro che è l'input della fase corrente. |
| PIPELINE_STAGE_INPUT_REV | La revisione dell'input della fase corrente. |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | L'ID univoco per l'esecuzione della pipeline. |
| TASK_ID | L'ID univoco per l'esecuzione corrente del lavoro. |
| TMPDIR | Un'ubicazione della directory in cui i file temporanei vengono archiviati. |
| WORKSPACE | Il percorso della directory di lavoro corrente. |

### Proprietà di runtime e dello strumento

| Proprietà ambiente | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Il percorso a Apache Ant 1.9.2. |
| GRADLE_HOME | Il percorso a Gradle 1.11. |
| JAVA_HOME | Il percorso a IBM&reg; Java&trade; 7. |
| JAVA7_HOME | Il percorso a IBM Java 7. |
| JAVA8_HOME | Il percorso a IBM Java 8. |
| MAVEN_HOME | Il percorso a Apache Maven 3.2.1. |
| NODE_HOME | Il percorso a Node.js 0.10.29. |

### Proprietà di distribuzione

| Proprietà ambiente | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | Per le distribuzioni, il nome dell'applicazione da distribuire. Questa proprietà è obbligatoria per la distribuzione e può essere specificata nello script stesso, nell'interfaccia di configurazione del lavoro di distribuzione o nel file `manifest.yml` del progetto. |
| CF_ORG | Per le distribuzioni, il nome dell'organizzazione (org) a cui distribuire. |
| CF_ORGANIZATION_ID | Per le distribuzioni, l'ID dell'organizzazione a cui distribuire. |
| CF_SPACE | Per le distribuzioni, il nome dello spazio a cui distribuire. |
| CF_SPACE_ID | Per le distribuzioni, l'ID dello spazio a cui distribuire.  |
| CF_TARGET_URL | Per le distribuzioni, l'URL di IBM Bluemix&reg; o Cloud Foundry. |
| IDS_VERSION | Per le distribuzioni, la versione dell'applicazione che sta venendo distribuita o dell'identificativo della risorsa. |

## Risorse pre-installate
{: #deliverypipeline_resources}

Molti moduli Node, strumenti e runtime sono pre-installati in ogni pipeline.

### Runtime e strumenti

*Nota:* tutti i link sono alla directory home.

| Risorsa | Nome link | Percorso |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|CLI Cloud Foundry 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java (predefinito)|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|Strumenti IBM Rational Team Concert&trade; SCM |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

Le versioni a 64 bit di IBM Node 0.10, 0.10.48, 0.12, 0.12.17, 4.2, 4.4.5, 4.6.0, 6.2.2 e 6.7.0 sono disponibili nell'ambiente della pipeline. Per scegliere una versione, utilizza il comando export.

Ad esempio, per utilizzare Node 0.12.7, immetti questo comando:
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

Per utilizzare Node 4.2.2, immetti questo comando:
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### Moduli Node

I seguenti moduli Node sono globalmente installati nell'ambiente della pipeline:

* grunt@0.4.5
* grunt-cli@0.1.13
* grunt-contrib-concat@0.4.0
* grunt-contrib-jshint@0.10.0
* grunt-contrib-nodeunit@0.4.1
* grunt-contrib-qunit@0.5.1
* grunt-contrib-uglify@0.5.0
* grunt-contrib-watch@0.6.1
* karma@0.12.23
* karma-cli@0.0.4
* karma-jasmine@0.1.5
* karma-phantomjs-launcher@0.1.4
* phantomjs@1.9.10
