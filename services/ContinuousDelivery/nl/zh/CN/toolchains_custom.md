---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 设置定制工具链（试验性）
{: #toolchains-custom}
上次更新时间：2016 年 4 月 27 日
{: .last-updated}

创建定制工具链可帮助您改进 DevOps 工作流程。您可以迅速着手使用其中一个现有工具链模板，以开始创建更有针对性的工具链。
{:shortdesc}

[创建和部署工具链](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}有多种方式。本指南将说明创建可以使用[部署到 {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window} 按钮进行部署的定制工具链的步骤。经过一些配置后，您能够在 {{site.data.keyword.Bluemix_notm}} 中通过可部署的工具链轻松共享 GitHub 项目。


## 入门
{: #toolchains_custom_gettingstarted}

要创建定制工具链，首先应克隆工具链模板。克隆现有模板将为您迅速提供可开始进行定制的起始点。

1. 使用所选的 Git 客户机，输入以下命令来克隆 GitHub 中的[简单工具链](https://github.com/open-toolchain/simple-toolchain){: new_window}模板。

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 此模板从单个 GitHub 存储库部署基本 Hello World 应用程序，并包含已针对持续交付、源代码控制、问题跟踪和联机编辑预配置的简单工具链。

2. **（可选）**：如果您希望从更复杂的工具链模板开始，那么可以首先克隆[微型服务的云本机工具链](https://github.com/open-toolchain/toolchain-demo){: new_window}。

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 此模板将部署由三个微型服务组成的网上商店，每个微型服务都包含在其自己的 GitHub 存储库中。此外，还包含更复杂的工具链，此工具链已针对持续交付、源代码控制、蓝绿部署、功能测试、问题跟踪、联机编辑和消息传递进行预配置。

不管选择哪个模板，本指南中概述的定制工具链创建原则都类似。

克隆模板后，您将具有基本 GitHub 存储库，该存储库具有 *Readme* 文件和 `.bluemix` 目录，该目录中包含使工具链正常运行所需的所有配置文件。`.bluemix` 目录至少应该包含以下文件：

* toolchain.yml
* deploy.json
* pipeline.yml

以下各部分将说明上述每一个文件以及随着工具链发展可能需要添加的某些其他配置。

## 了解配置文件
{: #toolchains_custom_config_files}

工具链模板配置文件主要由 YAML 格式的文件组成。每个文件都包含元数据，并描述工具链的不同方面。这包括有关工具链的常规描述性信息，要包含的 GitHub 存储库，有关应该如何构建代码和应该将代码部署到何处的详细信息，以及将在工具链中包含的各种工具的配置详细信息。随着工具链变得越来越复杂，配置文件也需相应跟上。重要的一点是，文件应保持正确的格式，以降低引入错误的风险。

处理 YAML 文件时，须牢记下面几条准则：

* 不允许使用制表符。只应使用空格。
* 所有属性和列表都必须缩进一个或多个空格。
* 所有键和属性都是区分大小写的。

为了复查工作，您可能希望使用简单 YAML 验证程序（例如，此 [YAML 解析器](http://wiki.ess3.net/yaml/){: new_window}）以避免存在任何此类错误。

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

`toolchain.yml` 文件是工具链的核心。此文件中概述了完整的工具链细节，包括要拉入的存储库、要包含的服务和构建详细信息。为了理解此文件的内容，可以将其分解成若干部分。

1\. **工具链介绍性信息：**

 此部分提供有关工具链的简单详细信息，这些信息将在工具链创建页面上向用户显示。应该包含工具链的名称以及描述，描述中说明工具链的用途或工具链部署后将执行的操作。此外，还可以包含图像，以显示工具链的徽标或可视化描述。

 除了提供工具链的介绍性内容外，此部分还包含名为 `required` 的键，用于定义可以在工具链创建页面上创建时配置的工具集成。允许在创建时对工具进行配置，能使您创建可轻松复用或重新确定用途的工具链。对于可以在工具链创建页面上配置的每一个工具，将 `toolchain.yml` 文件中定义的工具父键添加为 `required` 键的属性。

 以下片段显示了此部分的示例：

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

 **注：**图像必须先使用类似 [AskApache](http://www.askapache.com/online-tools/base64-image-converter/) 的工具转换为基本 64 位表示。

2\. **GitHub 存储库定义：**

 工具链可以持续交付任意数量的 GitHub 存储库。应该在 `toolchain.yml` 文件的此部分中定义每个存储库。

 首先，对于将添加到工具链的每个 GitHub 存储库，使用以下属性来添加表示 GitHub 存储库名称的父键：

| 项 | 键/属性 | 值 | 描述 |
|------|--------------|-------|-------------|
| repo-name | 键 |  | 存储库名称 |
| service_id | 属性 | <`githubpublic` 或 `githubprivate`> | GitHub 存储库的类型 |
| parameters: | 键 |  |  |
| repo_name | 属性 |  | **注释：应该如何对此项进行定义** |
| repo_url | 属性 |  | GitHub 存储库的 URL |
| type | 属性 | <`new`、`fork`、`clone` 或 `link`> | 应该如何创建存储库 |
| has_issues | 属性 | <`true` 或 `false`> | 使用 GitHub Issues |

 **注：**如果定义了多个存储库，并将其配置为 `has_issues: true`，那么 GitHub Issues 跟踪程序的单个实例将添加到工具链，用于跟踪已将此项设置为 `true` 的所有存储库的问题。

 以下片段显示了此部分的示例：

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

3\. **管道信息：**

 持续交付可在管道中使用。此部分定义用于在每个 GitHub 存储库中构建和部署代码的配置详细信息。

 首先，对于已在工具链中定义的每个 GitHub 存储库，添加表示其管道名称的父键。最好从 GitHub 存储库的名称中派生此键。添加以下属性：

| 项 | 键/属性 | 值 | 描述 |
|------|--------------|-------|-------------|
| pipeline-name | 键 |  | 管道的名称 |
| service_id | 属性 | <`pipeline`> | 要使用的服务的名称 |
| parameters | 键 |  |  |
| name | 属性 | <`repo_name`> | 与在 #Github 存储库部分中定义的名称相同 |
| ui-pipeline | 属性 | <`true` 或 `false`> |  |
| configuration | 键 |  |  |
| content | 属性 | <`$file(pipeline.yml)`> | 用于定义管道定义的文件 |
| env | 键 |  |  |
| REPO_NAME | 键 | <`repo-name-key`> | 与 GitHub 存储库父键相同 |
| CF_APP_NAME |  属性 | <`"{{deploy.parameters.repo-name-key}}"`> | Cloud Foundry 使用的名称。应该包含 GitHub 存储库父键名称 |
| PROD_SPACE_NAME | 属性 | <`"{{deploy.parameters.prod-space}}"`> | 要部署到的 {{site.data.keyword.Bluemix_notm}} 空间的名称 |
| PROD_ORG_NAME | 属性 | <`"{{deploy.parameters.prod-organization}}"`> | 要部署到的 {{site.data.keyword.Bluemix_notm}} 组织的名称 |
| PROD_REGION_ID | 属性 | <`"{{deploy.parameters.prod-region}}"`> | 要部署到的 {{site.data.keyword.Bluemix_notm}} 区域的名称 |
| execute | 属性 | <`true` 或 `false`> | 创建后启动管道 |
| services | 属性 | <`repo-name-key`> |  GitHub 存储库父键 |
| hidden | 属性 | <`[form, description]`> |  |

 有关创建 `pipeline.yml` 文件的信息，请参阅[后面的部分](#toolchains_custom_pipeline_yml)。

 以下片段显示了此部分的示例：

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

4\. **部署详细信息：**

 在持续交付过程中，工具链可以设置为将应用程序部署到部署工具链的用户有权访问的任何 {{site.data.keyword.Bluemix_notm}} 区域、组织或空间。具体部署工具链的位置的详细信息可以从工具链创建页面中进行选择。  

 ![Delivery Pipeline 配置设置](images/deploy_configuration.png)

 `toolchain.yml` 文件的此部分定义可从工具链创建页面进行配置的管道阶段。

 首先，父键 `deploy` 用于确定部署配置属性。以下属性构成了此部分的剩余内容：

| 项 | 键/属性 | 值 | 描述 |
|------|--------------|-------|-------------|
| deploy | 键 |  | 部署部分的名称 |
| schema | 属性 | <`deploy.json`> | 定义用于配置部署详细信息的 UI 的布局的文件 |
| service-category | 属性 | <`pipeline`> | 将使用部署配置的服务 |
| parameters | 键 |  |  |
| prod-region | 属性 | <`"{{region}}"`> | 为生产阶段定义 {{site.data.keyword.Bluemix_notm}} 区域 |
| prod-organization | 属性 | <`"{{organization}}"`> | 为生产阶段定义 {{site.data.keyword.Bluemix_notm}} 组织 |
| prod-space | 属性 | <`prod`> | 为生产阶段定义 {{site.data.keyword.Bluemix_notm}} 空间 |
| github-repo-name | 属性 | <`"{{repo-name-key.parameters.repo_name}}"`> | 用于将 GitHub 存储库名称传递到工具链创建页面的变量 |

 有关创建 `deploy.json` 文件的信息，请参阅[后面的部分](#toolchains_custom_deploy_json)。

 下面提供的示例定义了部署到生产环境的单个阶段。

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

 大多数情况下，代码示例可以按原样使用，只需略作修改。要定制此部分，应该更新 `github-repo-name`，使其与您存储库名称一致。此外，还需要更新 [`deploy.json`](#toolchains_custom_deploy_json) 文件内的详细信息。

 要创建包含开发、QA 和生产阶段的更复杂管道，可以替换 `parameters` 键下的以下属性。

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

5\. **工具配置**

 配置工具链的核心组件后，可以开始包含其他工具集成，这些工具集成将帮助向工具链添加更多功能，使工具链更加有用。所有工具都将具有必须添加到 `toolchain.yml` 文件的一个条目，另外有些工具还需要单独的 YAML 配置文件；YAML 配置文件应该在 `.bluemix` 目录内进行创建。

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

`pipeline.yml` 文件包含管道各阶段的所有配置详细信息。`pipeline.yml` 文件可以通过两种方式创建。

1. 手动创建 `pipeline.yml` 文件。有关创建 `pipeline.yml` 文件的详细信息和语法，请参阅[共享 DevOps Services 样本项目中基于文本的管道](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}。

2. 从现有 DevOps Services 项目生成 `pipeline.yml` 文件。为此，请执行以下操作：
	
	1. 创建新的 [DevOps Services 项目](https://hub.jazz.net/create){: new_window}。
	
	2. 打开该项目，并单击**构建和部署**。
	
	3. 配置管道所需的全部阶段。
	
	4. 在浏览器的地址栏中，将 `/yaml` 附加到项目的 URL，然后按 Enter 键。
	
	5. 将生成的 `pipeline.yml` 文件保存到 GitHub 存储库的 `.bluemix` 目录中。

如果工具链包含多个管道，请为每个 `pipeline.yml` 文件提供唯一名称。

下面是 `pipeline.yml` 文件的示例：

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

从工具链创建页面上的“可配置的集成”部分中选择 Delivery Pipeline 时，此部分会展开以显示可为该工具配置的以下项：

	* 应用程序名称
	* 将部署管道阶段的区域、组织和空间。

![Delivery Pipeline 配置设置](images/deploy_configuration.png)

UI 中此部分的布局由 `deploy.json` 模式进行定义。

在该模式内，应该更新以下属性以便与应用程序的详细信息相匹配：

	* Title
	* 描述
	* LongDescription
	* 应修改 `hello-world-name` 的所有实例及关联详细信息以便与应用程序的相应信息相匹配。

下面是 `deploy.json` 文件的示例：

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
