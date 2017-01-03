---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 設定自訂工具鏈（實驗性）
{: #toolchains-custom}
前次更新：2016 年 4 月 27 日
{: .last-updated}

建立自訂工具鏈可協助您改善 DevOps 工作流程。您可以快速開始使用其中一個現有工具鏈範本，或自訂其中一個範本來建立更適合開始使用的工具鏈。
{:shortdesc}

有許多方式可以[建立及部署工具鏈](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}。本手冊將說明下列作業的步驟：建立可使用[部署至 {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window} 按鈕部署的自訂工具鏈。進行部分配置之後，您就可以在 {{site.data.keyword.Bluemix_notm}} 中輕鬆地共用 GitHub 專案與可部署工具鏈。


## 開始使用
{: #toolchains_custom_gettingstarted}

若要建立自訂工具鏈，請從複製工具鏈範本開始。複製現有範本，可讓您快速開始進行自訂。

1. 使用所選擇的 Git 用戶端，在 GitHub 中輸入下列指令來複製[簡式工具鏈](https://github.com/open-toolchain/simple-toolchain){: new_window}範本。

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 此範本部署來自單一 GitHub 儲存庫的基本 Hello World 應用程式，並包括可預先配置以進行持續交付、來源控制、問題追蹤及線上編輯的簡式工具鏈。

2. **（選用）**：如果您偏好使用較複雜的工具鏈範本，可以從複製[微服務的雲端原生工具鏈](https://github.com/open-toolchain/toolchain-demo){: new_window}開始。

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 此範本會部署包含三個微服務（各自包含在其專屬 GitHub 儲存庫中）的線上儲存庫。也會包括較複雜的工具鏈，並且已預先配置以進行持續交付、來源控制、藍綠部署、功能測試、問題追蹤、線上編輯及傳訊。

不論選擇哪一個範本，本手冊中所概述用於建立自訂工具鏈的主體都會類似。

複製範本之後，您將會有內含 *Readme* 檔案及 `.bluemix` 目錄的基本 GitHub 儲存庫，而該目錄包含讓工具鏈運作所需的所有配置檔。`.bluemix` 目錄最少應該包含下列項目：

* toolchain.yml
* deploy.json
* pipeline.yml

下列各節將會說明上述每一個檔案，以及在工具鏈發展時可能需要新增的一些其他配置。

## 瞭解配置檔
{: #toolchains_custom_config_files}

工具鏈範本配置檔主要包含 YAML 格式化檔案。每一個檔案都包含可說明工具鏈不同層面的 meta 資料。這包括工具鏈的一般敘述性資訊、要包括的 GitHub 儲存庫、程式碼建置方式及部署位置的詳細資料，以及要內含在工具鏈中的各種工具的配置詳細資料。隨著工具鏈變得更為複雜，配置檔也會變得更為適合。檔案一定要保持良好的格式，才能降低造成錯誤的風險。

處理 YAML 檔案時，需要記住一些準則：

* 不容許使用定位點。應該只使用空格。
* 所有內容及清單都必須縮排一個以上的空格。
* 所有機碼及內容都區分大小寫。

若要再次確認您的工作，您可以使用簡式 YAML 驗證器（例如此 [YAML 剖析器](http://wiki.ess3.net/yaml/){: new_window}）來避免所有這類錯誤。

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

`toolchain.yml` 檔案是工具鏈的核心。此檔案會概述工具鏈的所有特性（包括要取回的儲存庫、要包括的服務及建置詳細資料）。為了讓其內容更具意義，將會分成數個區段。

1\. **介紹工具鏈資訊：**

 此區段提供工具鏈建立頁面上向使用者呈現的工具鏈簡單詳細資料。您應該包括工具鏈名稱及說明，而說明會說明工具鏈用途或部署時所執行的作業。也可以包括影像，以顯示工具鏈的標誌或視覺化描述。

 除了提供工具鏈的介紹內容之外，此區段也包括名為 `required` 的機碼，以定義在建立時可在工具鏈建立頁面上配置的工具整合。容許要在建立時配置的工具，可讓您建立可輕鬆地重複使用或重新提出的工具鏈。針對可在工具鏈建立頁面上配置的每一個工具，將 `toolchain.yml` 檔案內所定義的工具母機碼新增為 `required` 機碼的內容。

 此 Snippet 顯示此區段的範例：

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

 **附註：**必須先使用 [AskApache](http://www.askapache.com/online-tools/base64-image-converter/) 這類工具，將影像轉換成 Base 64 表示法。

2\. **GitHub 儲存庫定義：**

 工具鏈可以提供任意數目 GitHub 儲存庫的持續交付。`toolchain.yml` 檔案的這個區段就是應該定義每一個儲存庫的位置。

 若要開始，針對將新增至工具鏈的每一個 GitHub 儲存庫，新增代表具有下列內容的 GitHub 儲存庫名稱的母機碼：

| 項目 | 機碼/內容 | 值 | 說明 |
|------|--------------|-------|-------------|
| repo-name | 機碼 |  | 儲存庫名稱 |
| service_id | 內容 | <`githubpublic`、`githubprivate`> | GitHub 儲存庫的類型 |
| parameters: | 機碼 |  |  |
| repo_name | 內容 |  | **註解：應該如何定義此項目** |
| repo_url | 內容 |  | GitHub 儲存庫的 URL |
| type | 內容 | <`new`、`fork`、`clone`、`link`> | 應該如何建立儲存庫 |
| has_issues | 內容 | <`true`、`false`> | 使用 GitHub Issues |

 **附註：**如果您定義多個儲存庫，並將它們配置成 `has_issues: true`，則會將 GitHub 問題追蹤系統的單一實例新增至工具鏈，工具鏈將追蹤已設為 `true` 的所有儲存庫的問題。

 此 Snippet 顯示此區段的範例：

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

3\. **管線資訊：**

 持續交付可以使用管線進行。此區段定義用來在每一個 GitHub 儲存庫中建置及部署程式碼的配置詳細資料。

 若要開始，針對工具鏈中已定義的每一個 GitHub 儲存庫，新增代表其管線名稱的母機碼。建議您從 GitHub 儲存庫名稱衍生此機碼。新增下列內容：

| 項目 | 機碼/內容 | 值 | 說明 |
|------|--------------|-------|-------------|
| pipeline-name | 機碼 |  | 管線的名稱 |
| service_id | 內容 | <`pipeline`> | 要使用的服務名稱 |
| parameters | 機碼 |  |  |
| name | 內容 | <`repo_name`> | 與 #Github repos 區段中定義的名稱相同 |
| ui-pipeline | 內容 | <`true`、`false`> |  |
| configuration | 機碼 |  |  |
| content | 內容 | <`$file(pipeline.yml)`> | 定義管線定義的檔案 |
| env | 機碼 |  |  |
| REPO_NAME | 機碼 | <`repo-name-key`> | 與 GitHub 儲存庫母機碼的名稱相同 |
| CF_APP_NAME |  內容 | <`"{{deploy.parameters.repo-name-key}}"`> | Cloud Foundry 所使用的名稱。應該包括 GitHub 儲存庫母機碼名稱 |
| PROD_SPACE_NAME | 內容 | <`"{{deploy.parameters.prod-space}}"`> | 要部署到其中的 {{site.data.keyword.Bluemix_notm}} 空間的名稱 |
| PROD_ORG_NAME | 內容 | <`"{{deploy.parameters.prod-organization}}"`> | 要部署到其中的 {{site.data.keyword.Bluemix_notm}} 組織的名稱 |
| PROD_REGION_ID | 內容 | <`"{{deploy.parameters.prod-region}}"`> | 要部署到其中的 {{site.data.keyword.Bluemix_notm}} 地區的名稱 |
| execute | 內容 | <`true`、`false`> | 在建立之後，啟動管線 |
| services | 內容 | <`repo-name-key`> |  GitHub 儲存庫母機碼 |
| hidden | 內容 | <`[form, description]`> |  |

 您可以在[後面的區段](#toolchains_custom_pipeline_yml)中找到建立 `pipeline.yml` 檔案的相關資訊。

 此 Snippet 顯示此區段的範例：

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

4\. **部署詳細資料：**

 在進行持續交付處理程序期間，可以設定工具鏈，以將應用程式部署至部署工具鏈的使用者也有權存取的任何 {{site.data.keyword.Bluemix_notm}}「地區」、「組織」或「空間」。您可以從工具鏈建立頁面中選取應用程式部署位置的特定詳細資料。  

 ![Delivery Pipeline 配置設定](images/deploy_configuration.png)

 `toolchain.yml` 檔案的這個區段定義可從工具鏈建立頁面配置的管線階段。

 若要開始，母機碼 `deploy` 可用來識別部署配置內容。下列內容構成本區段的其餘部分：

| 項目 | 機碼/內容 | 值 | 說明 |
|------|--------------|-------|-------------|
| deploy | 機碼 |  | deploy 區段的名稱 |
| schema | 內容 | <`deploy.json`> | 定義用於配置部署詳細資料的使用者介面佈置的檔案 |
| service-category | 內容 | <`pipeline`> | 將使用部署配置的服務 |
| parameters | 機碼 |  |  |
| prod-region | 內容 | <`"{{region}}"`> | 定義正式作業階段的 {{site.data.keyword.Bluemix_notm}} 地區 |
| prod-organization | 內容 | <`"{{organization}}"`> | 定義正式作業階段的 {{site.data.keyword.Bluemix_notm}} 組織 |
| prod-space | 內容 | <`prod`> | 定義正式作業階段的 {{site.data.keyword.Bluemix_notm}} 空間 |
| github-repo-name | 內容 | <`"{{repo-name-key.parameters.repo_name}}"`> | 要將 GitHub 儲存庫名稱傳遞給工具鏈建立頁面的變數 |

 您可以在[後面的區段](#toolchains_custom_deploy_json)中找到建立 `deploy.json` 檔案的相關資訊。

 下面提供的範例定義部署至正式作業環境的單一階段。

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

 程式碼範例大部分會依現狀使用，而且只需要稍微進行修改。若要自訂此區段，`github-repo-name` 應該更新成與儲存庫名稱一致。也需要更新 [`deploy.json`](#toolchains_custom_deploy_json) 檔案內的詳細資料。

 若要建立包括 dev、QA 及 Prod 階段的更複雜的管線，可以替換 `parameters` 機碼下的下列內容。

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

 配置工具鏈的核心元件之後，您可以開始包括其他工具整合，以協助將其他功能及實用性新增至工具整合。所有工具都會有必須新增至 `toolchain.yml` 檔案的項目，而且有些也需要應該在 `.bluemix` 目錄內建立的不同 YAML 配置檔。

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

`pipeline.yml` 檔案包含管線階段的所有配置詳細資料。您可以使用兩種不同的方式來建立 `pipeline.yml` 檔案。

1. 手動建立 `pipeline.yml` 檔案。您可以在[在 DevOps Services 範例專案中共用文字型管線](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}中找到建立 `pipeline.yml` 檔案的詳細資料及語法。

2. 從現有 DevOps Services 專案產生 `pipeline.yml` 檔案。若要這樣做，請執行下列動作：
	
	1. 建立新的 [DevOps Services 專案](https://hub.jazz.net/create){: new_window}。
	
	2. 開啟專案，然後按一下**建置並部署**
	
	3. 配置管線所需的所有階段。
	
	4. 在瀏覽器的位址列中，將 `/yaml` 附加至專案的 URL，然後按 Enter 鍵。
	
	5. 將產生的 `pipeline.yml` 檔案儲存至 GitHub 儲存庫中的 `.bluemix` 目錄。

如果您的工具鏈包含多個管線，請為每一個 `pipeline.yml` 檔案提供唯一的名稱。

下列是 `pipeline.yml` 檔案範例：

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

在工具鏈建立頁面上，從「可配置的整合」區段中選取 Delivery Pipeline 時，這個區段會展開以顯示下列可針對該工具配置的項目：

	* 應用程式名稱
	* 管線階段將部署到其中的「地區」、「組織」及「空間」。

![Delivery Pipeline 配置設定](images/deploy_configuration.png)

使用者介面中此區段的佈置是透過 `deploy.json` 綱目所定義。

在此綱目內，應該更新下列內容以符合應用程式的詳細資料：

	* 標題
	* 說明
	* LongDescription
	* 應該修改所有 `hello-world-name` 實例及關聯的詳細資料，以符合應用程式的詳細資料。

下列是 `deploy.json` 檔案範例：

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
