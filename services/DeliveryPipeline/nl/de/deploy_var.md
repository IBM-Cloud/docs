---

copyright:
  years: 2016

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

# Umgebungseigenschaften und Ressourcen
{: #deliverypipeline_environment}
Letzte Aktualisierung: 29. April 2016
{: .last-updated}

Sie können Umgebungseigenschaften und vorinstallierte Ressourcen verwenden, um mit dem Service IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} zu interagieren. Sie können sie beispielsweise in einem Job-Script oder einem Testbefehl verwenden.{:shortdesc}

Die folgenden Eigenschaften und Ressourcen sind in Pipeline-Umgebungen standardmäßig verfügbar.

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## Umgebungseigenschaften
{: #deliverypipeline_envprop}

### Eigenschaften mit allgemeinem Zweck

| Umgebungseigenschaft | Beschreibung |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | Das Verzeichnis zum Archivieren bzw. in das Archive herunterladen werden. |
| BUILD_ID | Die eindeutige ID für die aktuelle Jobausführung.  |
| BUILD_DISPLAY_NAME | Der Wert für BUILD_ID mit dem Präfix "#". |
| BUILD_NUMBER | Die inkrementelle Phasen-ID, die in der Benutzerschnittstelle der Pipeline angezeigt wird.  |
| GIT_BRANCH | Der Git-Zweig, den der Job als Eingabe verwendet. Diese Eigenschaft ist nur für Jobs verfügbar, die als Eingabe ein Git-Repository verwenden. |
| GIT_COMMIT | Die Git-Commitoperation, die der Job als Eingabe verwendet. Diese Eigenschaft ist nur für Jobs verfügbar, die als Eingabe ein Git-Repository verwenden. |
| GIT_PREVIOUS_COMMIT | Der Git-Commitwert der letzten erfolgreichen Ausführung des Jobs. Diese Eigenschaft ist nur für Jobs verfügbar, die als Eingabe ein Git-Repository verwenden. |
| GIT_URL | Die Git-Repository-URL, die der Job als Eingabe verwendet. Diese Eigenschaft ist nur für Jobs verfügbar, die als Eingabe ein Git-Repository verwenden. |
| IDS_JOB_ID | Die eindeutige ID der Jobkonfiguration. |
| IDS_JOB_NAME | Der Name der Jobkonfiguration. |
| IDS_OUTPUT_PROPS | Durch Kommas getrennte Namen Ihrer Phasenumgebungseigenschaften. |
| IDS_PROJECT_NAME | Der Name des Projekts, z. B. <code>Owner - Project Name</code>. |
| IDS_STAGE_NAME | Der Name der aktuellen Phase. |
| IDS_URL | Die URL der aktuellen Pipeline. |
| IDS_VERSION | Die Nummer des Builds, der bereitgestellt wird, oder die SCM-ID. Diese Eigenschaft ist nur für Bereitstellungsjobs verfügbar.
| JOB_NAME | Die eindeutige Job-ID im Kontext der aktuellen Pipeline. |
| PIPELINE_STAGE_INPUT_JOB_ID | Die ID des Jobs, der als Eingabe für die aktuelle Phase dient. |
| PIPELINE_STAGE_INPUT_REV | Die Überarbeitung der Eingabe für die aktuelle Phase. |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | Die eindeutige ID der Ausführung der Pipeline. |
| TASK_ID | Die eindeutige ID der aktuellen Jobausführung. |
| TMPDIR | Eine Verzeichnisposition, an der temporäre Dateien gespeichert werden. |
| WORKSPACE | Der Pfad zum aktuellen Arbeitsverzeichnis. |

### Laufzeit- und Tooleigenschaften

| Umgebungseigenschaft | Beschreibung |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Der Pfad zu Apache Ant 1.9.2. |
| GRADLE_HOME | Der Pfad zu Gradle 1.11. |
| JAVA_HOME | Der Pfad zu IBM&reg; Java&trade; 7. |
| JAVA7_HOME | Der Pfad zu IBM Java 7. |
| JAVA8_HOME | Der Pfad zu IBM Java 8. |
| MAVEN_HOME | Der Pfad zu Apache Maven 3.2.1. |
| NODE_HOME | Der Pfad zu Node.js 0.10.29. |

### Bereitstellungseigenschaften

| Umgebungseigenschaft | Beschreibung |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | Bei Bereitstellungen der Name der bereitzustellenden App. Diese Eigenschaft ist für die Bereitstellung erforderlich und kann im Script selbst, in der Schnittstelle zur Bereistellung der Jobkonfiguration oder in der Datei `manifest.yml` des Projekts angegeben werden. |
| CF_ORG | Bei Bereitstellungen der Name der Organisation, für die die Bereitstellung durchgeführt wird. |
| CF_ORGANIZATION_ID | Bei Bereitstellungen die ID der Organisation, für die Bereitstellung durchgeführt wird. |
| CF_SPACE | Bei Bereitstellungen der Name des Bereichs, für den die Bereitstellung durchgeführt wird. |
| CF_SPACE_ID | Bei Bereitstellungen die ID des Bereichs, für den die Bereitstellung durchgeführt wird.  |
| CF_TARGET_URL | Bei Bereitstellungen die URL von IBM Bluemix&reg; oder Cloud Foundry. |
| IDS_VERSION | Bei Bereitstellungen die Version der App, die bereitgestellt wird, oder die Quellenkennung. |

## Vorinstallierte Ressourcen
{: #deliverypipeline_resources}

In jeder Pipeline sind mehrere Laufzeiten, Tools und Node-Module vorinstalliert.

### Laufzeiten und Tools

*Anmerkung:* Alle Links befinden sich im Ausgangsverzeichnis.

| Ressource | Linkname | Pfad |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|Cloud Foundry CLI 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java (default)|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|IBM Rational Team Concert&trade; SCM Tools |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

64-Bit-Versionen von IBM Node 0.10.40, 0.12.7 und 4.2.2 sind in der Pipeline-Umgebung verfügbar. Verwenden Sie zum Auswählen einer Version den Exportbefehl.

Geben Sie beispielsweise für die Verwendung von Node 0.12.7 den folgenden Befehl ein:
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

Geben Sie für die Verwendung von Node 4.2.2 den folgenden Befehl ein:
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### Node-Module

Die folgenden Node-Module sind global in der Pipeline-Umgebung installiert:

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
