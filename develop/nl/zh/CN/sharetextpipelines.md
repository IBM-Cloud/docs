---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#共享 {{site.data.keyword.jazzhub_short}} 样本项目中基于文本的管道 {: #share-pipeline}

*上次更新时间：2015 年 12 月 7 日* 

对于通过“部署到 {{site.data.keyword.Bluemix_notm}}”按钮部署到 {{site.data.keyword.Bluemix_notm}} 的样本项目，可以将 {{site.data.keyword.jazzhub_short}} 管道配置定义为 YAML 文件。定义为文本的管道可以共享，这样派生您项目的人员就不必对自己的管道进行配置。此功能正在开发中：YAML 格式和实现可能会随时更改。目前，此功能仅可用于具有以 {{site.data.keyword.Bluemix_notm}} 为目标的 Git 和 GitHub 存储库的项目。
{: shortdesc} 

在样本项目的根目录中，必须具有名为 `.bluemix` 且包含 `pipeline.yml` 文件的文件夹。

使用“部署到 {{site.data.keyword.Bluemix_notm}}”按钮克隆项目后，{{site.data.keyword.jazzhub_short}} 会创建一个基于 `pipeline.yml` 文件的管道。 

示例：
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

YAML 文件格式是包含管道规范的单个 YAML 文档。以下样本 {{site.data.keyword.jazzhub_short}} 管道在一个阶段中使用 Ant 构建了 Java 应用程序。然后，在另一个阶段中，该管道将该应用程序部署到 {{site.data.keyword.Bluemix_notm}}。 

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
      # 查看日志
      #cf logs "${CF_APP}" --recent
```
{: codeblock} 

##YAML 文件语法 {: #yaml-syntax}

任何管道都可以使用以下语法以文本形式进行表示。

管道：
```
---
stages:
<sequence of stages>
```
{: codeblock} 

阶段：
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

输入：
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

触发器：
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
属性：
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

作业：
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

目标：
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

##扩展作业和扩展定义 {: #extension-jobs} 

扩展定义用于定义可供扩展作业使用的属性集。指定了 `extension_id` 属性时，作业被视为是扩展作业。要找出哪些属性可用于扩展，请查阅其文档。 

##通过使用 YAML 文件与管道交互 {: #pipeline-yaml} 

**环境变量和解决方法** 
<!-- Formating for this? -->

通过 `pipeline.yml` 文件创建管道之前，“部署到 {{site.data.keyword.Bluemix_notm}}”功能会将该文件中的所有环境变量替换为您在 {{site.data.keyword.Bluemix_notm}} 界面中指定的信息（例如，您所在的组织）。仅当 YAML 值只由环境变量构成时，才会替换这些值。 

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

在该示例中，目标组织根据目标 URL 进行解析，持久存储在管道配置中的值为组织 GUID。在部署脚本内部出现的值不会进行替换。

目标 URL 必须指定为环境变量或实际值，并且必须提供组织和空间的 GUID 或名称。如果提供其中一个值，那么另一个值也会替换。

变量 | 描述
---------------- | ---------------- 
CF_TARGET_URL |	Bluemix 目标 URL
CF_ORGANIZATION	| 组织名称
CF_ORGANIZATION_ID	| 组织 GUID
CF_SPACE |	空间名称
CF_SPACE_ID |	空间 GUID
CF_APP	| 应用程序名称

*表 - 环境变量*

**从管道生成 YAML 文件** 

可以从管道生成 YAML 文件。 

从现有管道生成带有以下格式 URL 的文件：

```
<DevOps Services domain>/pipeline/user/project/yaml
```
{: codeblock} 

此调用无需 accept 头。可以从浏览器使用此调用。 

**注：**出于安全原因，会在生成的管道 YAML 文件中省略安全阶段环境属性值。 

