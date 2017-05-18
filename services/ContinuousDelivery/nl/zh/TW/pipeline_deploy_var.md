---

copyright:
  years: 2016
lastupdated: "2017-4-11"
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

# 環境內容及資源
{: #deliverypipeline_environment}

您可以使用環境內容及預先安裝的資源，以與 IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 服務互動。例如，您可以將它們包含在工作 Script 或測試指令中。
{:shortdesc}

您可以從階段的**環境內容**標籤中，將自己的環境內容新增至階段。階段中的每個工作都會有環境內容。

您可以從「環境內容」標籤中新增四種類型的內容：
* **文字**：具有單行值的內容索引鍵。
* **文字區**：具有多行值的內容索引鍵。
* **安全**：具有單行值的內容索引鍵。值會顯示為星號。
* **內容**：專案儲存庫中的檔案。此檔案可以包含多個內容。每一個內容都必須單獨一行。若要區隔索引鍵值組，請使用等號 (=)。


根據預設值，下列內容及資源可用於管線環境中。

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## 環境內容
{: #deliverypipeline_envprop}

### 一般用途的內容

| 環境內容 | 說明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | 要保存或下載保存檔用的目錄。 |
| BUILD_ID | 現行工作執行的唯一 ID。  |
| BUILD_DISPLAY_NAME | BUILD_ID 值，加上 "#" 字首。 |
| BUILD_NUMBER | 管線使用者介面中顯示的漸進式階段 ID。  |
| GIT_BRANCH | 工作用來作為輸入的 Git 分支。這個內容只適用於使用 Git 儲存庫作為輸入的工作中。 |
| GIT_COMMIT | 工作用來作為輸入的 Git 確定。這個內容只適用於使用 Git 儲存庫作為輸入的工作中。 |
| GIT_PREVIOUS_COMMIT | 工作前次成功執行的 Git 確定值。這個內容只適用於使用 Git 儲存庫作為輸入的工作中。 |
| GIT_URL | 工作用來作為輸入的 Git 儲存庫 URL。這個內容只適用於使用 Git 儲存庫作為輸入的工作中。 |
| IDS_JOB_ID | 工作配置的唯一 ID。 |
| IDS_JOB_NAME | 工作配置的名稱。 |
| IDS_OUTPUT_PROPS | 階段環境內容的逗點區隔名稱。 |
| IDS_PROJECT_NAME | 專案名稱，例如 <code>Owner - Project Name</code>。 |
| IDS_STAGE_NAME | 現行階段的名稱。 |
| IDS_URL | 現行管線的 URL。 |
| IDS_VERSION | 正在部署的建置號碼，或 SCM ID。此內容僅適用於部署工作。
| JOB_NAME | 現行管線環境定義中的唯一工作 ID。 |
| PIPELINE_STAGE_INPUT_JOB_ID | 現行階段的輸入工作 ID。 |
| PIPELINE_STAGE_INPUT_REV | 現行階段的輸入修訂。 |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | 管線執行作業的唯一 ID。 |
| TASK_ID | 工作現行執行作業的唯一 ID。 |
| TMPDIR | 儲存暫存檔的目錄位置。 |
| WORKSPACE | 現行工作目錄的路徑。 |

### 運行環境及工具內容

| 環境內容 | 說明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Apache Ant 1.9.2 的路徑。 |
| GRADLE_HOME | Gradle 1.11 的路徑。 |
| JAVA_HOME | IBM&reg; Java&trade; 7 的路徑。 |
| JAVA7_HOME | IBM Java 7 的路徑。 |
| JAVA8_HOME | IBM Java 8 的路徑。 |
| MAVEN_HOME | Apache Maven 3.2.1 的路徑。 |
| NODE_HOME | Node.js 0.10.29 的路徑。 |

### 部署內容

| 環境內容 | 說明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | 若為部署，此為要部署的應用程式名稱。此內容為部署所必要，且可以指定在 Script 本身中、部署工作配置介面，或專案的 `manifest.yml` 檔。 |
| CF_ORG | 若為部署，此為要部署到其中的組織名稱。 |
| CF_ORGANIZATION_ID | 若為部署，此為要部署到其中的組織 ID。 |
| CF_SPACE | 若為部署，此為要部署到其中的空間名稱。 |
| CF_SPACE_ID | 若為部署，此為要部署到其中的空間 ID。  |
| CF_TARGET_URL | 若為部署，此為 IBM Bluemix&reg; 或 Cloud Foundry 的 URL。 |
| IDS_VERSION | 若為部署，此為正在部署的應用程式版本或原始檔 ID。 |

## 預先安裝的資源
{: #deliverypipeline_resources}

在每個管線中，已預先安裝數個運行環境、工具及 Node 模組。

### 運行環境及工具

*附註：*所有鏈結都在起始目錄。

| 資源 | 鏈結名稱 | 路徑 |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|Cloud Foundry CLI 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java（預設）|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|IBM Rational Team Concert&trade; SCM Tools |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

64 位元版本的 IBM Node 0.10、0.10.48、0.12、0.12.17、4.2、4.4.5、4.6.0、6.2.2 及 6.7.0 可用於管線環境。若要選擇版本，請使用 export 指令。

例如，若要使用 Node 0.12.7，請輸入下列指令：`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

若要使用 Node 4.2.2，請輸入下列指令：`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### Node 模組

下列 Node 模組已廣域安裝在管線環境中：

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
