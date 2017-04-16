---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-30"

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

# Managing pipelines
{: #deliverypipeline_managing}

You can administer, configure, and extend IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} integrations.
{:shortdesc}

Complete the following tasks to administer, configure, and extend a pipeline.

## Controlling access
{: #deliverypipeline_access}

You can restrict who is able to run stages or modify a pipeline. To do so, go to the Pipeline Settings page, which you can reach by clicking the **Stage Configuration** icon on the Pipeline: All Stages page.

![The pipeline settings gear icon](images/pipeline_settings.png)

## Environment properties and resources
{: #deliverypipeline_envprop}

You can use environment properties and pre-installed resources to interact with the {{site.data.keyword.deliverypipeline}} service. For example, you might incorporate them into a job script or test command. For more information, see [Environment properties and resources for the {{site.data.keyword.deliverypipeline}} service](/docs/services/DeliveryPipeline/deploy_var.html).

You can add your own environment properties to a stage from its **ENVIRONMENT PROPERTIES** tab. Environment properties are available to every job in a stage.

You can add four types of properties from the Environment Properties tab:
* **Text**: A property key with a single-line value.
* **Text Area**: A property key with a multi-line value.
* **Secure**: A property key with a single-line value. The value is displayed as asterisks.
* **Properties**: A file in the project's repository. This file can contain multiple properties. Each property must be on its own line. To separate key-value pairs, use the equals sign (=).

## Extending the capabilities of your pipeline
{: #deliverypipeline_extend}

You can extend the capabilities of your Build & Deploy pipeline by configuring your jobs to use supported services. For example, test jobs can run static code scans and build jobs can globalize strings.

For more information on extending pipeline capabilities, see [Extending the {{site.data.keyword.deliverypipeline}} service's capabilities](/docs/services/DeliveryPipeline/deliverypipeline_extension.html).
