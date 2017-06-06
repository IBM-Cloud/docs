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

# 環境プロパティーとリソース
{: #deliverypipeline_environment}

環境プロパティーとあらかじめインストールされたリソースを使用して、IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} サービスと対話できます。たとえば、ジョブ・スクリプトやテスト・コマンドを取り込むことができます。{:shortdesc}

独自の環境プロパティーを、ステージの**「環境プロパティー (ENVIRONMENT PROPERTIES)」**タブからステージに追加します。環境プロパティーは、ステージのすべてのジョブに使用可能です。

「環境プロパティー (Environment Properties)」タブから、次の 4 つのタイプのプロパティーを追加できます。
* **「テキスト」**: 単一行の値を持つプロパティー・キー。
* **「テキスト域 (Text Area)」**: 複数行の値を持つプロパティー・キー。
* **「セキュア (Secure)」**: 単一行の値を持つプロパティー・キー。値はアスタリスクとして表示されます。
* **「プロパティー (Properties)」**: プロジェクトのリポジトリーにあるファイル。このファイルには、複数のプロパティーを含めることができます。プロパティーはそれぞれ独自の行で指定されている必要があります。キー値のペアを区切るには、等号 (=) を使用します。


パイプライン環境では、デフォルトで次のプロパティーとリソースを利用できます。

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## 環境プロパティー

{: #deliverypipeline_envprop}

### 汎用プロパティー

| 環境プロパティー | 説明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | アーカイブのアーカイブ先またはダウンロード先のディレクトリー。 |
| BUILD_ID | 現在のジョブ実行の固有 ID。  |
| BUILD_DISPLAY_NAME | 「#」をプレフィックスとして使用する BUILD_ID 値。 |
| BUILD_NUMBER | パイプライン UI に表示されるインクリメンタル・ステージ ID。  |
| GIT_BRANCH | ジョブが入力として使用する Git ブランチ。このプロパティーは、Git リポジトリーを入力として使用するジョブでのみ利用できます。 |
| GIT_COMMIT | ジョブが入力として使用する Git コミット。このプロパティーは、Git リポジトリーを入力として使用するジョブでのみ利用できます。 |
| GIT_PREVIOUS_COMMIT | ジョブが最後に正常に実行した Git コミットの値。このプロパティーは、Git リポジトリーを入力として使用するジョブでのみ利用できます。 |
| GIT_URL | ジョブが入力として使用する Git リポジトリーの URL。このプロパティーは、Git リポジトリーを入力として使用するジョブでのみ利用できます。 |
| IDS_JOB_ID | ジョブの構成の固有 ID。 |
| IDS_JOB_NAME | ジョブの構成の名前。 |
| IDS_OUTPUT_PROPS | ステージ環境プロパティーのコンマ区切りの名前。 |
| IDS_PROJECT_NAME | プロジェクトの名前 (例、<code>Owner - Project Name</code>)。 |
| IDS_STAGE_NAME | 現在のステージの名前。 |
| IDS_URL | 現在のパイプラインの URL。 |
| IDS_VERSION | デプロイ中のビルドの番号、または SCM ID。このプロパティーは、デプロイ・ジョブでのみ利用できます。
| JOB_NAME | 現在のパイプラインのコンテキストの固有ジョブ ID。 |
| PIPELINE_STAGE_INPUT_JOB_ID | 現在のステージの入力のジョブの ID。 |
| PIPELINE_STAGE_INPUT_REV | 現在のステージの入力のリビジョン。 |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | パイプラインの実行の固有 ID。 |
| TASK_ID | ジョブの現在の実行の固有 ID。 |
| TMPDIR | 一時ファイルが保存されるディレクトリーの場所。 |
| WORKSPACE | 現行の作業ディレクトリーのパス。 |

### ランタイムとツールのプロパティー

| 環境プロパティー | 説明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Apache Ant 1.9.2 のパス。 |
| GRADLE_HOME | Gradle 1.11 のパス。 |
| JAVA_HOME | IBM&reg; Java&trade; 7 のパス。 |
| JAVA7_HOME | IBM Java 7 のパス。 |
| JAVA8_HOME | IBM Java 8 のパス。 |
| MAVEN_HOME | Apache Maven 3.2.1 のパス。 |
| NODE_HOME | Node.js 0.10.29 のパス。 |

### デプロイメント・プロパティー


| 環境プロパティー | 説明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | デプロイメントにおける、デプロイするアプリの名前。これはデプロイメントに必須のプロパティーであり、スクリプト自体、デプロイ・ジョブ構成インターフェース、またはプロジェクトの `manifest.yml` ファイルで指定できます。 |
| CF_ORG | デプロイメントにおける、デプロイ先の組織の名前。 |
| CF_ORGANIZATION_ID | デプロイメントにおける、デプロイ先の組織の ID。 |
| CF_SPACE | デプロイメントにおける、デプロイ先のスペースの名前。 |
| CF_SPACE_ID | デプロイメントにおける、デプロイ先のスペースの ID。  |
| CF_TARGET_URL | デプロイメントにおける、IBM Bluemix&reg; または Cloud  Foundry の URL。 |
| IDS_VERSION | デプロイメントにおける、デプロイされるアプリケーションのバージョン、またはソース ID。 |

## 事前にインストールされているリソース
{: #deliverypipeline_resources}

いくつかのランタイム、ツール、Node モジュールは、すべてのパイプラインにあらかじめインストールされています。

### ランタイムとツール

*注意:* すべてのリンクがホーム・ディレクトリー内にあります。

| リソース | リンク名 | パス |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|Cloud Foundry CLI 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java (デフォルト)|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|IBM Rational Team Concert&trade; SCM Tools |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

64 ビット・バージョンの IBM Node 0.10、0.10.48、0.12、0.12.17、4.2、4.4.5、4.6.0、6.2.2、6.7.0 がパイプライン環境で利用できます。バージョンを選択するには、export コマンドを使用します。

たとえば、Node 0.12.7 を使用するには、次のコマンドを入力します。
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

Node 4.2.2 を使用するには、次のコマンドを入力します。
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### ノード・モジュール

次のノード・モジュールが、パイプライン環境にグローバルにインストールされます。

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
