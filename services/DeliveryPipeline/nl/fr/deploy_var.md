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

# Propriétés et ressources d'environnement
{: #deliverypipeline_environment}
Dernière mise à jour : 29 avril 2016
{: .last-updated}

Vous pouvez utiliser des propriétés d'environnement et des
ressources pré-installées pour interagir avec le service IBM&reg; Bluemix&reg;
{{site.data.keyword.deliverypipeline}}. Par exemple, vous
pouvez les utiliser dans un script de travail ou une commande de test. {:shortdesc}

Les propriétés et ressources suivantes sont disponibles par
défaut dans les environnements de pipeline.

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## Propriétés d'environnement
{: #deliverypipeline_envprop}

### Propriétés générales

| Propriété d'environnement | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | Répertoire dans lequel archiver ou télécharger les archives. |
| BUILD_ID | ID unique pour l'exécution de travail en cours.  |
| BUILD_DISPLAY_NAME | Valeur BUILD_ID, préfixée de "#". |
| BUILD_NUMBER | ID d'étape incrémentielle qui est affiché dans l'interface utilisateur du pipeline.  |
| GIT_BRANCH | Branche Git utilisée par le travail en entrée. Cette propriété est uniquement disponible dans les travaux qui utilisent un référentiel Git en entrée. |
| GIT_COMMIT | Validation Git utilisée par le travail en entrée. Cette propriété est uniquement disponible dans les travaux qui utilisent un référentiel Git en entrée. |
| GIT_PREVIOUS_COMMIT | Valeur de validation Git de la dernière exécution réussie du travail. Cette propriété est uniquement disponible dans les travaux qui utilisent un référentiel Git en entrée. |
| GIT_URL | URL de référentiel Git utilisée par le travail en entrée. Cette propriété est uniquement disponible dans les travaux qui utilisent un référentiel Git en entrée. |
| IDS_JOB_ID | ID unique de la configuration du travail. |
| IDS_JOB_NAME | Nom de la configuration du travail. |
| IDS_OUTPUT_PROPS | Noms séparés par des virgules des propriétés d'environnement de votre étape. |
| IDS_PROJECT_NAME | Nom du projet, par exemple, <code>Propriétaire - Nom du projet</code>. |
| IDS_STAGE_NAME | Nom de l'étape en cours. |
| IDS_URL | URL du pipeline en cours. |
| IDS_VERSION | Numéro de la génération qui est déployée ou identificateur SCM. Cette propriété est disponible uniquement pour les travaux de déploiement.
| JOB_NAME | ID de travail unique dans le contexte du pipeline en cours. |
| PIPELINE_STAGE_INPUT_JOB_ID | ID du travail en entrée pour l'étape en cours. |
| PIPELINE_STAGE_INPUT_REV | Révision de l'entrée pour l'étape en cours. |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | ID unique pour l'exécution du pipeline. |
| TASK_ID | ID unique de l'exécution en cours du travail. |
| TMPDIR | Emplacement du répertoire dans lequel sont stockés les fichiers temporaires. |
| WORKSPACE | Chemin d'accès au répertoire de travail en cours. |

### Propriétés d'exécution et d'outil

| Propriété d'environnement | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Chemin d'accès à Apache Ant 1.9.2. |
| GRADLE_HOME | Chemin d'accès à Gradle 1.11. |
| JAVA_HOME | Chemin d'accès à IBM&reg; Java&trade; 7. |
| JAVA7_HOME | Chemin d'accès à IBM Java 7. |
| JAVA8_HOME | Chemin d'accès à IBM Java 8. |
| MAVEN_HOME | Chemin d'accès à Apache Maven 3.2.1. |
| NODE_HOME | Chemin d'accès à Node.js 0.10.29. |

### Propriétés de déploiement

| Propriété d'environnement | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | Pour les déploiements, nom de l'application à déployer. Cette propriété est obligatoire pour le déploiement et elle peut être spécifiée dans le script lui-même, l'interface de configuration du travail de déploiement ou le fichier `manifest.yml` du projet. |
| CF_ORG | Pour les déploiements, nom de l'organisation (org) dans laquelle effectuer le déploiement. |
| CF_ORGANIZATION_ID | Pour les déploiements, nom de l'organisation dans laquelle effectuer le déploiement.  |
| CF_SPACE | Pour les déploiements, nom de l'espace dans lequel effectuer le déploiement.  |
| CF_SPACE_ID | Pour les déploiements, ID de l'espace dans lequel effectuer le déploiement.   |
| CF_TARGET_URL | Pour les déploiements, URL d'IBM Bluemix&reg; ou de Cloud Foundry. |
| IDS_VERSION | Pour les déploiements, version de l'application qui est déployée ou identificateur source. |

## Ressources préinstallées
{: #deliverypipeline_resources}

Plusieurs environnements d'exécution, outils et modules de noeud sont préinstallés dans chaque pipeline.

### Environnements d'exécution et outils

*Remarque :* Tous les liens figurent dans le répertoire de base.

| Ressource | Nom du lien | Chemin d'accès |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|Cloud Foundry CLI 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java (par défaut)|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|IBM Rational Team Concert&trade; SCM Tools |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

Les versions 64 bits d'IBM Node 0.10.40, 0.12.7 et 4.2.2 sont disponibles dans l'environnement de pipeline. Pour choisir une version, utilisez la commande export.

Par exemple, pour utiliser Node 0.12.7, entrez la commande suivante :
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

Pour utiliser Node 4.2.2, entrez la commande suivante :
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### Modules de noeud

Les modules de noeud suivants sont sont installés globalement dans l'environnement de pipeline :

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
