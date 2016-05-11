---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Environment properties and resources
{: #deliverypipeline_environment}

*Last updated: 29 April 2016*

You can use environment properties and pre-installed resources to interact with the IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} service. For example, you might use them in a job script or test command.
{:shortdesc}

The following properties and resources are available by default in pipeline environments.

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## Environment properties
{: #deliverypipeline_envprop}

### General purpose properties

| Environment property | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | The directory to archive or to download archives into. |
| BUILD_ID | The unique ID for the current job execution.  |
| BUILD_DISPLAY_NAME | The BUILD_ID value, prefixed with "#". |
| BUILD_NUMBER | The incremental stage ID that is shown in the pipeline UI.  |
| GIT_BRANCH | The Git branch that the job uses as input. This property is only available in jobs that use a Git repository as input. |
| GIT_COMMIT | The Git commit that the job uses as input. This property is only available in jobs that use a Git repository as input. |
| GIT_PREVIOUS_COMMIT | The Git commit value of the job's last successful run. This property is only available only in jobs that use a Git repository as input. |
| GIT_URL | The Git repository URL that the job uses as input. This property is only available in jobs that use a Git repository as input. |
| IDS_JOB_ID | The unique ID of the job's configuration. |
| IDS_JOB_NAME | The name of the job's configuration. |
| IDS_OUTPUT_PROPS | Comma-separated names of your stage environment properties. |
| IDS_PROJECT_NAME | The name of the project, for example, <code>Owner &#124; Project Name</code>. |
| IDS_STAGE_NAME | The name of the current stage. |
| IDS_URL | The URL for the current pipeline. |
| IDS_VERSION | The number for the build that is being deployed or the SCM identifier. This property is available only for deploy jobs.
| JOB_NAME | The unique job ID in the context of the current pipeline. |
| PIPELINE_STAGE_INPUT_JOB_ID | The ID of the job that is input for the current stage. |
| PIPELINE_STAGE_INPUT_REV | The revision of the input for the current stage. |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | The unique ID for the run of the pipeline. |
| TASK_ID | The unique ID of the job's current run. |
| TMPDIR | A directory location where temporary files are stored. |
| WORKSPACE | The path for the current working directory. |

### Runtime and tool properties

| Environment property | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | The path to Apache Ant 1.9.2. |
| GRADLE_HOME | The path to Gradle 1.11. |
| JAVA_HOME | The path to IBM&reg; Java&trade; 7. |
| JAVA7_HOME | The path to IBM Java 7. |
| JAVA8_HOME | The path to IBM Java 8. |
| MAVEN_HOME | The path to Apache Maven 3.2.1. |
| NODE_HOME | The path to Node.js 0.10.29. |

### Deployment properties

| Environment property | Description |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | For deployments, the name of the app to deploy. This property is required for deployment and can be specified in the script itself, the deploy job configuration interface, or the project's `manifest.yml` file. |
| CF_ORG | For deployments, the name of the organization (org) to deploy to. |
| CF_ORGANIZATION_ID | For deployments, the ID of the org to deploy to. |
| CF_SPACE | For deployments, the name of the space to deploy to. |
| CF_SPACE_ID | For deployments, the ID of the space to deploy to.  |
| CF_TARGET_URL | For deployments, the URL of IBM Bluemix&reg; or Cloud Foundry. |
| IDS_VERSION | For deployments, the version of the app that is being deployed or the source identifier. |

## Pre-installed resources
{: #deliverypipeline_resources}

Several runtimes, tools, and Node modules are pre-installed in every pipeline.

### Runtimes and tools

*Note:* All links are in the home directory.

| Resource | Link name | Path |
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

64-bit versions of IBM Node 0.10.40, 0.12.7, and 4.2.2 are available in the pipeline environment. To choose a version, use the export command.

For example, to use Node 0.12.7, enter this command:
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

To use Node 4.2.2, enter this command:
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### Node modules

The following Node modules are globally installed in the pipeline environment:

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
