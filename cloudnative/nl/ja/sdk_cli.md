---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# SDK Generator プラグイン
{: #sdk-cli}

{{site.data.keyword.IBM}} SDK Generator プラグインは、[{{site.data.keyword.Bluemix_notm}} CLI ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/cli/reference/bluemix_cli/index.html) にインストールできます。

{{site.data.keyword.Bluemix_notm}} の開発者は、このプラグインを使用して [Open API 仕様 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.openapis.org/) 準拠の REST API 定義から SDK を生成することができます。REST API 定義を変更する際は、プロジェクト全体を再生成するのではなく、このプラグインを使用して SDK だけを再生成することができます。

また、特定のスペース内の Cloud Foundry アプリが、SDK 生成に有効な REST API 定義を持っているかどうかも確認することができます。最後に、{{site.data.keyword.IBM_notm}} SDK Generator プラグインを使用して REST API 定義を検証し、それらが SDK 生成プログラムの要件に従っていることを確認できます。

この {{site.data.keyword.IBM_notm}} SDK Generator プラグインにより、生成された SDK を使用してバックエンド・サービスをアプリに容易に統合することができます。REST API に対する変更が行われた場合は、SDK を再生成し、古い SDK を置換してシームレスな SDK アップグレードを行うことができます。また、CLI を devops パイプラインに統合し、アプリをビルドするたびに SDK が API 仕様と常に整合されるようにすることができます。

REST API 定義は、有効でなければならず、稼働中のサーバー・エンドポイントでホストされているか、またはシステム上のローカル・ファイルでなければなりません。REST API 定義がホストされている場合は、`OPENAPI_SPEC` 環境変数に相対 URL が定義されている必要があります。


## 必要条件
{: #prereqs}

以下の要件を満たしていることを確認してください。

* [{{site.data.keyword.Bluemix_notm}} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net) アカウントを持っている
* [Open API ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.openapis.org/) 仕様に準拠した有効な API 定義


## インストール
{: #installation}

1. [{{site.data.keyword.Bluemix}} CLI ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://clis.ng.bluemix.net/ui/home.html) をインストールします。

2. [プラグイン ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in) をインストールします。

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## コマンド
{: #commands}

以下のコマンドを使用して、SDK を生成したり、Open API 定義ファイルを検証したり、Cloud Foundry アプリをリストしたりします。


### SDK の生成
{: #gen}

`bluemix sdk generate [arguments...][command options]` を使用します。


#### 引数
{: #gen-args}

* `APP_NAME` - 現在のスペース内の Cloud Foundry アプリの名前
* `OPENAPI_DOC_LOCATION` - ロー REST API 定義 JSON または Yaml の URL または相対ファイル・パス
* `GENERATED_SDK_NAME` (オプション) - 生成済み SDK の名前


#### オプション
{: #gen-options}

* `PLATFORM` (必要)
   * `--android` - Android SDK を生成する
   * `--ios` - iOS Swift SDK を生成する
   * `--swift` - Swift サーバー SDK を生成する
* `--output "YOUR_RELATIVE_PATH"` (オプション) - 生成された SDK を、`YOUR_RELATIVE_PATH` によって指定されたディレクトリー内に配置する (既存の SDK がある場合は上書きする)
* `--unzip` (オプション) - 生成された SDK を解凍する (既存の SDK 成果物がある場合は上書きする)


#### 使用法
{: #gen-usage}

{{site.data.keyword.Bluemix_notm}} で稼働中の Cloud Foundry アプリから SDK を生成するには、そのアプリの名前を CLI のパラメーターとして使用することができます。以下のコマンドは、アプリの名前を `SDK_Name` として使用しています。

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

Open API 定義ファイルの URL、あるいはローカルの JSON ファイルまたは Yaml ファイルから SDK を生成するには、以下のコマンドを使用します。

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### Open API 定義の検証
{: #validating}

`bluemix sdk validate [argument]` を使用します。


#### 引数
{: #val-args}

* `APP_NAME` - 現在のスペース内の Cloud Foundry アプリの名前
* `OPENAPI_DOC_LOCATION` - ロー REST API 定義 JSON または Yaml の URL または相対ファイル・パス


#### 使用法
{: #val-usage}

{{site.data.keyword.Bluemix_notm}} で稼働中の Cloud Foundry アプリの API 仕様を検証するには、そのアプリの名前を CLI のパラメーターとして使用することができます。

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

API 仕様文書の URL、あるいはローカルの JSON ファイルまたは Yaml ファイルから SDK を検証するには、以下のコマンドを使用します。

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### アプリのリスト (Cloud Foundry)
{: #list-apps}

`bluemix sdk list [argument][option]` を使用して、アプリをリストし、API 仕様を検証します。`OPENAPI_SPEC` 環境変数を、仕様をホストしている相対 URL パスに設定する必要があります。


#### 引数
{: #list-args}

* `SPACE_NAME` (オプション) - アプリを検索する現行組織内の Cloud Foundry スペースの名前。指定されない場合、現行スペースが検索されます。


#### オプション
{: #list-options}

* `--url` (オプション) - リスト内の各アプリの Open API 定義の完全形式の URL を表示します。


#### 使用法
{: #list-usage}

現行スペース内のアプリをリストするには、以下のコマンドを使用します。

```
bluemix sdk list
```
{: codeblock}

現行スペース内のアプリをリストし、API 仕様の URL を表示するには、以下のコマンドを使用します。

```
bluemix sdk list --url
```
{: codeblock}

特定スペース内のアプリをリストするには、以下のコマンドを使用します。

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

特定スペース内のアプリをリストし、API 仕様の URL を表示するには、以下のコマンドを使用します。

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
