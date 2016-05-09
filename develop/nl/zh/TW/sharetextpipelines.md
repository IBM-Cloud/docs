---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#在 {{site.data.keyword.jazzhub_short}} 專案範例中共用以文字為基礎的管線 {: #share-pipeline}

*前次更新：2015 年 12 月 7 日* 

針對透過「部署至 {{site.data.keyword.Bluemix_notm}}」按鈕而部署至 {{site.data.keyword.Bluemix_notm}} 的專案範例，您可以定義 {{site.data.keyword.jazzhub_short}} 管線配置作為 YAML 檔案。可以共用定義為文字的管線，以便分出您的專案的人不必自行配置管線。此特性仍在開發中：YAML 格式和實作可能會隨時變更。目前，此特性只適用於具有 Git 及 GitHub 儲存庫且以 {{site.data.keyword.Bluemix_notm}} 為目標的專案。
{: shortdesc} 

在專案範例的根目錄中，您必須有名為 `.bluemix` 的資料夾，其中包含 `pipeline.yml` 檔案。

使用「部署至 {{site.data.keyword.Bluemix_notm}}」按鈕複製專案時，{{site.data.keyword.jazzhub_short}} 會建立以 `pipeline.yml` 檔案為基礎的管線。 

範例：
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

YAML 檔案格式是單一 YAML 文件，其中包含管線規格。下列範例 {{site.data.keyword.jazzhub_short}} 管線會在某一個階段中使用 Ant 建置 Java 應用程式。然後在另一個階段，管線會將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。 

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

##YAML 檔案語法 {: #yaml-syntax}

任何管線都可以使用下列語法以文字方式代表。

管線：
```
---
stages:
<sequence of stages>
```
{: codeblock} 

階段：
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

輸入：
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

觸發程式：
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
內容：
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

工作：
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

目標：
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

##延伸工作及延伸定義 {: #extension-jobs} 

延伸定義會定義延伸工作可以使用的內容集。當指定 `extension_id` 內容時，工作會被視為延伸工作。要找出延伸可用的內容，請參閱其文件。 

##使用 YAML 檔案與管線互動 {: #pipeline-yaml} 

**環境變數及解決方法** 
<!-- Formating for this? -->

從 `pipeline.yml` 檔案建立管線之前，「部署至 {{site.data.keyword.Bluemix_notm}}」功能會將檔案中的任何環境變數取代成您在 {{site.data.keyword.Bluemix_notm}} 介面中指定的資訊（例如您的組織）。YAML 值只會在它們單純由環境變數組成時才替換。 

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

在該範例中，目標組織會針對目標 URL 解析，而管線配置中持續保存的值是組織 GUID。部署 Script 內部的發生項目不會替換。

目標 URL 必須指定為環境變數或真實的值，且必須提供組織及空間的 GUID 或名稱。如果提供一個值，另一個值也會替換。

變數 | 說明
---------------- | ---------------- 
CF_TARGET_URL |	Bluemix 目標 URL
CF_ORGANIZATION	| 組織名稱
CF_ORGANIZATION_ID	| 組織 GUID
CF_SPACE |	空間名稱
CF_SPACE_ID |	空間 GUID
CF_APP	| 應用程式名稱

*表格 - 環境變數*

**從管線產生 YAML 檔案** 

您可以從管線產生 YAML 檔案。 

從現有的管線產生具有此格式之 URL 的檔案：

```
<DevOps Services domain>/pipeline/user/project/yaml
```
{: codeblock} 

這項呼叫不需要接受標頭。您可以從瀏覽器使用此呼叫。 

**附註：**為了安全因素，產生的管線 YAML 檔案中會省略 secure-stage 環境內容值。 

