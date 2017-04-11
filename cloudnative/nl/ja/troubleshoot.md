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
{:note:.deprecated}

# トラブルシューティング
{: #ts}

{{site.data.keyword.dev_cli_notm}} に関するいくつかの既知の問題を回避策とともに示します。
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## 既知の問題
{: #knownissues}

以下のセクションでは、既知の問題と、考えられる解決策について説明します。


### 非モバイル・パターンでプロジェクトを作成中に、ホスト名が使用されているというエラーが発生する
{: #hostname}

{{site.data.keyword.dev_cli_short}} を使用して Web アプリ、BFF、またはマイクロサービスのパターンからプロジェクトを作成する場合に、以下のエラーが発生することがあります。

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### 原因
{: #hostname-cause}
   
このエラーは、期限切れのログイン・トークンが原因です。


#### 解決策
{: #hostname-resolution}

もう一度ログインしてください。

```
bx login
```
{: codeblock}


### {{site.data.keyword.dev_cli_short}} での一般障害
{: #general}

{{site.data.keyword.dev_cli_short}} の create、delete、list、または code のコマンドを使用した場合に、以下のエラーが発生することがあります。

```
Failed to <command> project.
```
{: codeblock}


#### 原因
{: #hostname-cause}
   
このエラーは、期限切れのログイン・トークンが原因です。


#### 解決策
{: #hostname-resolution}

もう一度ログインしてください。

```
bx login
```
{: codeblock}


### {{site.data.keyword.objectstorageshort}} 機能を追加する際にサービス・ブローカー・エラーが発生する
{: #os}

{{site.data.keyword.dev_cli_short}} を使用して {{site.data.keyword.objectstorageshort}} 機能で 2 つのプロジェクトを作成する場合に、以下のエラーが発生することがあります。

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### 原因
{: #os-cause}
   
このエラーは、{{site.data.keyword.objectstorageshort}} サービスが、無料 {{site.data.keyword.objectstorageshort}} プランのインスタンスを 1 つしか許可しないことが原因です。


#### 解決策
{: #os-resolution}

このエラーを回避するために、別のプランを選択するよう求められます。


### プロジェクト作成中にコード取得に失敗する
{: #code}

{{site.data.keyword.dev_cli_short}} を使用してプロジェクトを作成する場合に、以下のエラーが発生することがあります。
	
```
FAILED
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### 原因
{: #code-cause}

このエラーは、内部タイムアウトが原因です。
	

#### 解決策
{: #code-resolution}

コードは、以下のいずれかの方法で取得できます。

* CLI で次のコマンドを実行します。

	```
	bx dev code <your-project-name>
	```
	{: codeblock}
	
	`<your-project-name>` は、プロジェクト作成中に使用したプロジェクト名に置き換えてください。

* {{site.data.keyword.dev_console}} を使用します。

	1. {{site.data.keyword.dev_console}} で[プロジェクト ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/developer/projects) を選択して、**「コードの取得 (Get the Code)」**をクリックします。

	2. **「コードの生成 (Generate Code)」**をクリックします。

	3. コードが生成されたら、**「コードのダウンロード」**をクリックします。


### Node.js プロジェクトで `bx dev run` を実行中にエラーが発生する
{: #node}

Node.js Web または BFF プロジェクトについて {{site.data.keyword.dev_cli_short}} で `bx dev run` を実行中に、次のエラーが発生することがあります。

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### 原因
{: #node-cause}
   
このエラーは、`appmetrics` モジュールが別のアーキテクチャーでインストールされていることが原因です。1 つのアーキテクチャーでインストールされたネイティブ npm モジュールは、別のアーキテクチャーで動作しません。組み込まれた Docker イメージは、Linux カーネルをベースとしています。


#### 解決策
{: #node-resolution}

`node_modules` フォルダーを削除して、`bx dev run` をもう一度実行してください。


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## ヘルプおよびサポートの利用
{: #gettinghelp}

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} または {{site.data.keyword.dev_cli_notm}} の使用時に問題または質問がある場合、情報を検索するか、フォーラムを通して質問することによって、ヘルプを利用できます。また、サポート・チケットをオープンすることも可能です。

フォーラムを使用して質問するときは、{{site.data.keyword.Bluemix_notm}} 開発チームの目に止まるように、質問にタグを付けてください。

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

{{site.data.keyword.dev_console}} または {{site.data.keyword.dev_cli_notm}} でのアプリの開発またはデプロイについて技術的な質問がある場合は、以下を行ってください。

* [スタック・オーバーフロー ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) で質問を投稿し、`bluemix-dev-services` と `ibm-bluemix` のタグを付けます。
* [Slack ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://ibm-cloud-tech.slack.com/) の `bluemix-dev-services` チャネルで質問を投稿します。今すぐ[ご登録ください![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://ibm.biz/IBMCloudNativeSlack)。


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

フォーラムの使用について詳しくは、[ヘルプの利用 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/support/index.html#getting-help) を参照してください。

{{site.data.keyword.IBM}} サポート・チケットのオープン、またはサポート・レベルとチケットの重大度については、[サポートへのお問い合わせ ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/support/index.html#contacting-support) を参照してください。

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

