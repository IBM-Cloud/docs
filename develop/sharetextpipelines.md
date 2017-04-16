---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-16"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Sharing text-based pipelines in sample projects {: #share-pipeline}

For sample projects that are deployed to {{site.data.keyword.Bluemix_notm}} through the Deploy to {{site.data.keyword.Bluemix_notm}} button, you can define pipeline configurations as YAML files. Pipelines that are defined as text can be shared so that the people who fork your project don't have to configure their own pipelines. This feature is under development: the YAML format and implementation might change at any time. Currently, this feature is available only for projects with Git and GitHub repositories that target {{site.data.keyword.Bluemix_notm}}. 
{: shortdesc} 

In the sample project's root directory, you must have a folder named `.bluemix` that contains a `pipeline.yml` file.

When a project is cloned by using the Deploy to {{site.data.keyword.Bluemix_notm}} button, a pipeline that is based on the `pipeline.yml` file is created. 

Example: 
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

The YAML file format is a single YAML document that contains a pipeline specification. The following sample pipeline builds a Java app with Ant in one stage. Then, in another stage, the pipeline deploys the app to {{site.data.keyword.Bluemix_notm}}. 

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

## YAML file syntax {: #yaml-syntax}

Any pipeline can be represented textually by using the following syntax.

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
	
Property:
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

Job:
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

Target:
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

## Extension jobs and extension definitions {: #extension-jobs} 

Extension definitions define the set of properties that are available to extension jobs. A job is treated as an extension job when the `extension_id` property is specified. To find out which properties are available for an extension, consult its documentation. 

## Interacting with pipelines by using a YAML file {: #pipeline-yaml} 

**ENVIRONMENT VARIABLES AND RESOLUTION** 
<!-- Formating for this? -->

Before the pipeline is created from a `pipeline.yml` file, the Deploy to {{site.data.keyword.Bluemix_notm}} capability replaces any environment variables in the file with information you specify in the {{site.data.keyword.Bluemix_notm}} interface (for example, your organization). YAML values are substituted only if they solely consist of an environment variable. 

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

In that example, the target org is resolved against the target URL, and the value that persists in the pipeline configuration is the org GUID. The occurrence inside of the deployment script is not substituted.

The target URL must be specified as an environment variable or a real value, and either the GUIDs or the names of the org and space must be provided. If one value is provided, the other is also substituted.

Variable | Description 
---------------- | ---------------- 
CF_TARGET_URL |	Bluemix target URL
CF_ORGANIZATION	| Org name
CF_ORGANIZATION_ID	| Org GUID
CF_SPACE |	Space name
CF_SPACE_ID |	Space GUID
CF_APP	| App name
{: caption="Table 1. Environment variables" caption-side="top"}

**GENERATING A YAML FILE FROM A PIPELINE** 

You can generate a YAML file from a pipeline. 

Generate the file from an existing pipeline with a URL in this format:

```
<domain>/pipeline/user/project/yaml
```
{: codeblock} 

This call does not require an accept header. You can use this call from a browser. 

**Note:** For safety reasons, secure-stage environment property values are omitted from generated pipeline YAML files. 
