---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Setting up custom toolchains (Experimental)
{: #toolchains-custom}
Last updated: 27 April 2016
{: .last-updated}

Creating a custom toolchain can help you improve your DevOps workflow. You can get started quickly with one of the existing toolchain templates, or customize one of the templates to create a more tailored toolchain to start from.
{:shortdesc}

There are many ways to [create and deploy a toolchain](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}.  This guide will explain the steps to create a custom toolchain that can be deployed using a [Deploy to {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window} button. After some configuration, you will be able to easily share a GitHub project with a deployable toolchain in {{site.data.keyword.Bluemix_notm}}.


## Getting started
{: #toolchains_custom_gettingstarted}

To create a custom toolchain, we'll begin by cloning a toolchain template.  Cloning an existing template will quickly give you a starting point to begin your customization from.

1. Using the Git client of your choice, enter the following command to clone the [Simple Toolchain](https://github.com/open-toolchain/simple-toolchain){: new_window} template in GitHub.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 This template deploys a basic Hello World application from a single GitHub repository and includes a simple toolchain that is preconfigured for continuous delivery, source control, issue tracking, and online editing.

2. **(Optional)**: If you would prefer to start with a more complex toolchain template, you can start by cloning the [Cloud-native Toolchain for Microservices](https://github.com/open-toolchain/toolchain-demo){: new_window}.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 This template deploys an online store that is comprised of three microservices, each contained in their own GitHub repository.  A more complex toolchain is also included that is preconfigured for continuous delivery, source control, blue-green deployments, functional testing, issue tracking, online editing, and messaging.

Regardless of which template is chosen, the principals outlined in this guide for creating a custom toolchain will be similar.

After cloning the template, you will have a basic GitHub repository that has a *Readme* file and a `.bluemix` directory that contains all of the configuration files that are required to make your toolchain function.  At a minimum, the `.bluemix` directory should contain the following:

* toolchain.yml
* deploy.json
* pipeline.yml

Each of these files will be explained in the following sections along with some additional configurations that may need to be added as your toolchain evolves.

## Understanding the configuration files
{: #toolchains_custom_config_files}

The toolchain template configuration files are comprised primarily of YAML formatted files.  Each file contains metadata that describes different aspects of the toolchain.  This includes general descriptive info about the toolchain, the GitHub repositories to be included, details on how code should be built and where it should be deployed, and configuration details for the various tools that you will included in the toolchain.  As your toolchain becomes more complex, the configuration files will also follow suit.  It is important that the files remain well formatted to reduce the risk of errors being introduced.

A few guidelines to keep in mind when working within a YAML file:

* Tabs are not allowed.  Only spaces should be used.
* All properties and lists must be indented with one or more spaces.
* All keys and properties are case-sensitive.

To double check your work, you may want to use a simple YAML validator such as this [YAML Parser](http://wiki.ess3.net/yaml/){: new_window} to avoid any such errors.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

The `toolchain.yml` file is the heart of your toolchain. The specifics of your toolchain, including repositories to pull in, services to include, and build details are all outlined in this file. To make sense of it's contents, it can be broken up into several sections.

1\. **Introductory toolchain information:**

 This section provides simple details about your toolchain that are presented to the user on the toolchain creation page. You should include a name for your toolchain along with a description that explains the purpose of the toolchain or what it will do when it is deployed. An image can also be included to display a logo or a visual depiction of your toolchain.

 In addition to providing introductory content for your toolchain, this section also includes a key named `required` that defines tool integrations that can be configured at the time of creation on the toolchain creation page.  Allowing a tool to be configured at the time of creation allows you to create a toolchain that can easily be reused or re-purposed.  For each tool that can be configured on the toolchain creation page, add the tools parent key as defined within the `toolchain.yml` file as a property of the `required` key.

 This snippet shows an example of this section:

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

 **Note:** Images must first be converted to a base 64 representation by using a tool like [AskApache](http://www.askapache.com/online-tools/base64-image-converter/).

2\. **GitHub repository definitions:**

 A toolchain can provide continuous delivery for any number of GitHub repositories.  This section of the `toolchain.yml` file is where each repository should be defined.

 To start, for each GitHub repository that will be added to the toolchain, add a parent key that represents the name of your GitHub repository with the following properties:

| Item | Key/Property | Value | Description |
|------|--------------|-------|-------------|
| repo-name | key |  | Repository name |
| service_id | property | <`githubpublic` , `githubprivate`> | Type of GitHub repository |
| parameters: | key |  |  |
| repo_name | property |  | **COMMENT:  How should this be defined** |
| repo_url | property |  | URL of the GitHub repository |
| type | property | <`new` , `fork` , `clone` , `link`> | How the repository should be created |
| has_issues | property | <`true` , `false`> | Use GitHub Issues |

 **Note:** If you define multiple repositories and configure them as `has_issues: true`, a single instance of GitHub Issue tracker will be added to the toolchain that will track issues for all repositories that have been set to `true`.

 This snippet shows an example of this section:

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

3\. **Pipeline information:**

 Continuous delivery is made possible with the pipeline.  This section defines the configuration details that are used to build and deploy the code in each of your GitHub repositories.

 To start, for each GitHub repository that has been defined in your toolchain, add a parent key that represents a name of its pipeline.  Deriving this key from the name of your GitHub repository is a good idea.   Add the following properties:

| Item | Key/Property | Value | Description |
|------|--------------|-------|-------------|
| pipeline-name | key |  | Name for the pipeline |
| service_id | property | <`pipeline`> | Name of service to be used |
| parameters | key |  |  |
| name | property | <`repo_name`> | Same as name defined in the #Github repos section for |
| ui-pipeline | property | <`true` , `false`> |  |
| configuration | key |  |  |
| content | property | <`$file(pipeline.yml)`> | File that defines your pipeline definition |
| env | key |  |  |
| REPO_NAME | key | <`repo-name-key`> | The same name as your GitHub repository parent key |
| CF_APP_NAME |  property | <`"{{deploy.parameters.repo-name-key}}"`> | Name used by Cloud Foundry.  Should include your GitHub repository parent key name |
| PROD_SPACE_NAME | property | <`"{{deploy.parameters.prod-space}}"`> | Name of {{site.data.keyword.Bluemix_notm}} space to deploy to |
| PROD_ORG_NAME | property | <`"{{deploy.parameters.prod-organization}}"`> | Name of {{site.data.keyword.Bluemix_notm}} organization to deploy to |
| PROD_REGION_ID | property | <`"{{deploy.parameters.prod-region}}"`> | Name of {{site.data.keyword.Bluemix_notm}} region to deploy to |
| execute | property | <`true` , `false`> | Start pipeline after creation |
| services | property | <`repo-name-key`> |  GitHub repository parent key |
| hidden | property | <`[form, description]`> |  |

 Information about creating a `pipeline.yml` file can be found in a [later section.](#toolchains_custom_pipeline_yml)

 This snippet shows an example of this section:

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

4\. **Deployment details:**

 As part of the continuous delivery process, a toolchain can be set up to deploy your application into any {{site.data.keyword.Bluemix_notm}} Region, Organization, or Space that the user deploying the toolchain has access too.  The specific details of where to deploy your application can be selected from the toolchain creation page.  

 ![Delivery Pipeline Configuration settings](images/deploy_configuration.png)

 This section of the `toolchain.yml` file defines the pipeline stages that are available to be configured from the toolchain creation page.

 To start, the parent key `deploy` is used to identify the deployment configuration properties.  The following properties make up the rest of the section:

| Item | Key/Property | Value | Description |
|------|--------------|-------|-------------|
| deploy | key |  | Name of deploy section |
| schema | property | <`deploy.json`> | File that defines the layout of the UI for configuring your deployment details |
| service-category | property | <`pipeline`> | Service that will use the deployment configurations |
| parameters | key |  |  |
| prod-region | property | <`"{{region}}"`> | Defines {{site.data.keyword.Bluemix_notm}} region for production stage |
| prod-organization | property | <`"{{organization}}"`> | Defines {{site.data.keyword.Bluemix_notm}} organization for production stage |
| prod-space | property | <`prod`> | Defines {{site.data.keyword.Bluemix_notm}} space for production stage |
| github-repo-name | property | <`"{{repo-name-key.parameters.repo_name}}"`> | Variable to pass the GitHub repository name to the toolchain creation page |

 Information about creating a `deploy.json` file can be found in a [later section.](#toolchains_custom_deploy_json)

 The example provided below defines a single stage that deploys to a production environment.

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

 The code example can be used mostly as is and requires only slight modification.  To customize this section, the `github-repo-name` should be updated to be consistent with your repository name.  Details within the [`deploy.json`](#toolchains_custom_deploy_json) file will also need updated.

 To create a more complex pipeline that includes a dev, QA, and Prod stage, the following properties can be substituted under the `parameters` key.

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

5\. **Tool configurations**

 After configuring the core components of your toolchain, you can begin including other tool integrations that will help add additional functionality and usefulness to your toolchain.  All tools will have an entry that must be added to the `toolchain.yml` file, and some will also require a separate YAML configuration file that should be created within the `.bluemix` directory.

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

The `pipeline.yml` file contains all of the configuration details for the stages of your pipeline.  The `pipeline.yml` file can be created two different ways.

1. Create the `pipeline.yml` file manually.  The details and syntax for creating the `pipeline.yml` file can be found in [Sharing text-based pipelines in DevOps Services sample projects](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}.

2. Generate the `pipeline.yml` file from an existing DevOps Services project.  To do so.
	
	1. Create a new [DevOps Services project](https://hub.jazz.net/create){: new_window}.
	
	2. Open the project and click **BUILD & DEPLOY**
	
	3. Configure all of the stages needed for your pipeline.
	
	4. In your browser's address bar, append `/yaml` to the project's URL and press enter.
	
	5. Save the resulting `pipeline.yml` file to the `.bluemix` directory in your GitHub repository.

If your toolchain contains more than one pipeline, provide unique names for each `pipeline.yml` file.

The following is an example of a `pipeline.yml` file:

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

On the toolchain creation page, when Delivery Pipeline is selected from the Configurable Integrations section, the section expands to display the following items which can be configured for that tool:

	* The applications name
	* The Region, Organization, and Space that your pipeline stages will deploy too.

![Delivery Pipeline Configuration settings](images/deploy_configuration.png)

The layout of this section in the UI is defined by the `deploy.json` schema.

Within the schema, the following properties should be updated to match the details of your application:

	* Title
	* Description
	* LongDescription
	* All instances of `hello-world-name` and associated details should be modified to match that of your application.

The following is an example of a `deploy.json` file:

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
