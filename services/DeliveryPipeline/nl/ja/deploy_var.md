---

copyright:
  years: 2016

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

# 環境プロパティーおよびリソース
{: #deliverypipeline_environment}
最終更新日: 2016 年 4 月 29 日
{: .last-updated}

IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} サービスと相互作用するには、環境プロパティーと事前にインストールされた
リソースを使用することができます。例えば、環境プロパティーと事前インストールされたリソースをジョブ・スクリプトまたはテスト・コマンドで使用することができます。
{:shortdesc}

次のプロパティーとリソースは、パイプライン環境においてデフォルトで使用可能です。

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
| ARCHIVE_DIR | アーカイブを保存またはダウンロードするディレクトリー。 |
| BUILD_ID | 現在のジョブ実行に固有の ID。  |
| BUILD_DISPLAY_NAME | 接頭部が「#」の BUILD_ID 値。 |
| BUILD_NUMBER | パイプライン UI に表示される増分ステージ ID。  |
| GIT_BRANCH | ジョブが入力データとして使用する Git ブランチ。このプロパティーは、Git リポジトリーを入力データとして使用するジョブでのみ使用可能です。 |
| GIT_COMMIT | ジョブが入力データとして使用する Git コミット。このプロパティーは、Git リポジトリーを入力データとして使用するジョブでのみ使用可能です。 |
| GIT_PREVIOUS_COMMIT | ジョブが最後に正常に実行されたときの Git コミット値。このプロパティーは、Git リポジトリーを入力データとして使用するジョブでのみ使用可能です。 |
| GIT_URL | ジョブが入力データとして使用する Git リポジトリー URL。このプロパティーは、Git リポジトリーを入力データとして使用するジョブでのみ使用可能です。 |
| IDS_JOB_ID | ジョブの構成に固有の ID。 |
| IDS_JOB_NAME | ジョブの構成名。 |
| IDS_OUTPUT_PROPS | ご使用のステージ環境プロパティーのコンマ区切りの名前。 |
| IDS_PROJECT_NAME | プロジェクトの名前 (例: <code>所有者 - プロジェクト名</code>) |
| IDS_STAGE_NAME | 現行ステージの名前。 |
| IDS_URL | 現行パイプラインの URL。 |
| IDS_VERSION | デプロイ中のビルドの番号または SCM ID。このプロパティーは、デプロイされるジョブでのみ使用可能です。
| JOB_NAME | 現行パイプラインのコンテキストに固有のジョブ ID。 |
| PIPELINE_STAGE_INPUT_JOB_ID | 現行ステージに入力されるジョブの ID。 |
| PIPELINE_STAGE_INPUT_REV | 現行ステージの入力の改訂。 |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | パイプラインの実行に固有の ID。 |
| TASK_ID | ジョブの現在の実行に固有の ID。 |
| TMPDIR | 一時ファイルが保管されるディレクトリーの場所。 |
| WORKSPACE | 現行作業ディレクトリーへのパス。 |

### ランタイムとツール・プロパティー

| 環境プロパティー | 説明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Apache Ant 1.9.2 へのパス。 |
| GRADLE_HOME | Gradle 1.11 へのパス。 |
| JAVA_HOME | IBM&reg; Java&trade; 7 へのパス。 |
| JAVA7_HOME | IBM Java 7 へのパス。 |
| JAVA8_HOME | IBM Java 8 へのパス。 |
| MAVEN_HOME | Apache Maven 3.2.1 へのパス。 |
| NODE_HOME | Node.js 0.10.29 へのパス。 |

### デプロイメント・プロパティー

| 環境プロパティー | 説明 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | デプロイメントに使用される、デプロイするアプリの名前。このプロパティーはデプロイメントに
必要で、スクリプト自体、デプロイされるジョブの構成インターフェース、またはプロジェクトの `manifest.yml`
ファイルに指定することができます。 |
| CF_ORG | デプロイメントに使用される、デプロイ先の組織の名前。 |
| CF_ORGANIZATION_ID | デプロイメントに使用される、デプロイ先の組織の ID。 |
| CF_SPACE | デプロイメントに使用される、デプロイ先のスペースの名前。 |
| CF_SPACE_ID | デプロイメントに使用される、デプロイ先のスペースの ID。  |
| CF_TARGET_URL | デプロイメントに使用される、IBM Bluemix&reg; または Cloud Foundry の URL。 |
| IDS_VERSION | デプロイメントに使用される、デプロイ中のアプリのバージョンまたはソース ID。 |

## 事前インストール済みリソース
{: #deliverypipeline_resources}

複数のランタイム、ツール、および Node モジュールがパイプラインごとに事前にインストールされます。

### ランタイムとツール

*注:* すべてのリンクはホーム・ディレクトリーにあります。

| リソース | リンク・ネーム | ファイルパス |
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

IBM Node 0.10.40、0.12.7、および 4.2.2 の 64 ビット・バージョンは、パイプライン環境で使用可能です。
バージョンを選択するには、エクスポート・コマンドを使用します。

例えば、Node 0.12.7 を使用するには、コマンド
`export PATH=/opt/IBM/node-v0.12/bin:$PATH` を入力します。

Node 4.2.2 を使用するには、コマンド `export
PATH=/opt/IBM/node-v4.2/bin:$PATH` を入力します。

### Node モジュール

次の Node モジュールは、パイプライン環境でグローバルにインストールされます。

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
