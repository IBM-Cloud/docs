---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# カスタム・ツールチェーンのセットアップ (試験)
{: #toolchains-custom}
最終更新日時: 2016 年 4 月 27 日
{: .last-updated}

カスタム・ツールチェーンを作成すると、DevOps のワークフローを向上できます。既存のツールチェーンのテンプレートの 1 つを使用して素早く開始するか、テンプレートの 1 つをカスタマイズして、細かく調整したツールチェーンを作成して開始することができます。
{:shortdesc}

[ツールチェーンの作成とデプロイ](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}には、多数の方法があります。このガイドでは、[「{{site.data.keyword.Bluemix_notm}} にデプロイ」](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window}ボタンを使用してデプロイできるカスタム・ツールチェーンを作成する手順を説明します。いくらかの構成を行った後、{{site.data.keyword.Bluemix_notm}} でデプロイ可能なツールチェーンを使用して、GitHub プロジェクトを簡単に共有できます。


## 概説
{: #toolchains_custom_gettingstarted}

カスタム・ツールチェーンを作成するには、まずツールチェーン・テンプレートのクローン作成から開始します。既存のテンプレートのクローンを作成し、それを開始点としてカスタマイズを始めることができます。

1. 選択した Git クライアントを使用して、次のコマンドを入力し、GitHub の[シンプルなツールチェーン](https://github.com/open-toolchain/simple-toolchain){: new_window}のテンプレートのクローンを作成します。

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 このテンプレートは、基本的な Hello World アプリケーションを単一の GitHub リポジトリーからデプロイします。このテンプレートには、継続的デリバリー、ソース管理、問題のトラッキング、オンライン編集のための構成があらかじめ行われたシンプルなツールチェーンが含まれています。

2. **(オプション)**: さらに複雑なツールチェーン・テンプレートから開始する場合は、 [マイクロサービス用のクラウド・ネイティブのツールチェーン](https://github.com/open-toolchain/toolchain-demo){: new_window}のクローンを作成することから始めることができます。

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 このテンプレートは、3 つのマイクロサービス (それぞれ独自の GitHub リポジトリーに含まれる) で構成されるオンライン・ストアをデプロイします。また、継続的デリバリー、ソース管理、blue-green デプロイメント、機能テスト、問題のトラッキング、オンライン編集、メッセージングのための構成があらかじめ行われた複雑なツールチェーンも含まれています。

どのテンプレートを選択するとしても、このガイドで概説するカスタム・ツールチェーンの作成の基本は似ています。

テンプレートのクローンを作成すると、*Readme* ファイルと、ツールチェーンの動作に必要な構成ファイルがすべて含まれる `.bluemix` ディレクトリーを含んだ基本的な GitHub リポジトリーが作成されます。 `.bluemix` ディレクトリーには、少なくとも以下が含まれている必要があります。

* toolchain.yml
* deploy.json
* pipeline.yml

これらの各ファイルについては、次のセクションで説明します。ツールチェーンの展開に合わせて追加しなければならなくなる可能性のあるいくつかの追加構成についても説明します。

## 構成ファイルについて
{: #toolchains_custom_config_files}

ツールチェーン・テンプレートの構成ファイルは、主に YAML 形式のファイルで構成されます。各ファイルには、ツールチェーンの様々な側面を記述するメタデータが含まれます。これには、ツールチェーンに関する一般的な記述情報、含まれる GitHub リポジトリー、コードを作成する方法とデプロイする場所に関する詳細、ツールチェーンに含まれる様々なツールの構成の詳細が含まれます。ツールチェーンが複雑になると、構成ファイルも同様に複雑になります。エラーが発生するリスクを軽減するために、ファイルを正しい形式に保つことが重要です。

YAML ファイルを操作する際に注意すべきガイドラインは次のとおりです。

* タブは許可されません。スペースだけを使用してください。
* すべてのプロパティーとリストは、1 つ以上のスペースでインデントする必要があります。
* すべてのキーとプロパティーは大/小文字が区別されます。

作業を確認するために、[YAML パーサー](http://wiki.ess3.net/yaml/){: new_window}などのシンプルな YAML バリデーターを使用すると、そのようなエラーを回避できます。

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

`toolchain.yml` ファイルは、ツールチェーンの中核です。プルするリポジトリー、含めるサービス、ビルドの詳細などのツールチェーンの仕様が、すべてこのファイルに記述されます。内容を分かりやすくするために、いくつかのセクションに分割することができます。

1\. **ツールチェーンの情報の概要**

 このセクションでは、ツールチェーンの作成ページでユーザーに表示されるツールチェーンの詳細情報について簡潔に説明します。ツールチェーンの名前とともに、ツールチェーンの目的やデプロイしたときの動作についての説明を含める必要があります。ロゴやツールチェーンを視覚的に表した画像を含めることもできます。

 ツールチェーンの概要のコンテンツのほかに、このセクションには、ツールチェーンの作成ページで作成時に構成できるツール統合を定義する `required` というキーも含まれています。作成時にツールが構成できるようにすると、簡単に再利用したり、別の目的で利用したりできるツールチェーンを作成できます。ツールチェーンの作成ページで構成できるツールごとに、`toolchain.yml` ファイル内で定義されたそのツールの親キーを `required` キーのプロパティーとして追加します。

 次のスニペットは、このセクションの例を示しています。

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

 **注意:** 画像はまず[AskApache](http://www.askapache.com/online-tools/base64-image-converter/)などのツールを使用して、Base 64 の表記に変換する必要があります。

2\. **GitHub リポジトリーの定義**

 ツールチェーンは、任意の数の GitHub リポジトリーに対して継続的デリバリーを提供できます。`toolchain.yml` ファイルのこのセクションで、各リポジトリーを定義する必要があります。

 まず、ツールチェーンに追加 GitHub リポジトリーごとに、次のプロパティーを使用して、GitHub リポジトリーの名前を表す親キーを追加します。

| アイテム | キー/プロパティー | 値  | 説明 |
|------|--------------|-------|-------------|
| repo-name | キー |  | リポジトリーの名前 |
| service_id | プロパティー | <`githubpublic`、 `githubprivate`> | GitHub リポジトリーのタイプ |
| パラメーター: | キー |  |  |
| repo_name | プロパティー |  | **COMMENT:  定義方法** |
| repo_url | プロパティー |  | GitHub リポジトリーの URL |
| タイプ | プロパティー | <`new`、`fork`、`clone`、`link`> | リポジトリーの作成方法 |
| has_issues | プロパティー | <`true`、`false`> | GitHub Issues の使用 |

 **注意:** 複数のリポジトリーを定義して `has_issues: true` として構成すると、`true` に設定されたすべてのリポジトリーの問題をトラッキングする、GitHub Issue トラッカーの単一のインスタンスがツールチェーンに追加されます。

 次のスニペットは、このセクションの例を示しています。

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

3\. **パイプラインの情報:**

 継続的デリバリーは、パイプラインによって可能となります。このセクションでは、各 GitHub リポジトリーでコードをビルドしてデプロイするのに使用される構成の詳細を定義します。

 まず、ツールチェーンで定義された GitHub の各リポジトリーに対して、そのパイプラインの名前を表す親キーを追加します。このキーは GitHub リポジトリーの名前に基づいたものにすることをお勧めします。次のプロパティーを追加します。

| アイテム | キー/プロパティー | 値  | 説明 |
|------|--------------|-------|-------------|
| pipeline-name | キー |  | パイプラインの名前
 |
| service_id | プロパティー | <`pipeline`> | 使用するサービスの名前 |
| パラメーター
   | キー |  |  |
| 名前
 | プロパティー | <`repo_name`> | #Github リポジトリーのセクションで定義される名前と同じです |
| ui-pipeline | プロパティー | <`true`、`false`> |  |
| 構成
 | キー |  |  |
| コンテンツ | プロパティー | <`$file(pipeline.yml)`> | パイプラインを定義するファイル |
| env | キー |  |  |
| REPO_NAME | キー | <`repo-name-key`> | GitHub リポジトリーの親キーと同じ名前 |
| CF_APP_NAME |  プロパティー | <`"{{deploy.parameters.repo-name-key}}"`> | Cloud Foundry で使用する名前。GitHub リポジトリーの親キーの名前を含めてください |
| PROD_SPACE_NAME | プロパティー | <`"{{deploy.parameters.prod-space}}"`> | デプロイ先の {{site.data.keyword.Bluemix_notm}} スペースの名前 |
| PROD_ORG_NAME | プロパティー | <`"{{deploy.parameters.prod-organization}}"`> | デプロイ先の {{site.data.keyword.Bluemix_notm}} の組織の名前 |
| PROD_REGION_ID | プロパティー | <`"{{deploy.parameters.prod-region}}"`> | デプロイ先の {{site.data.keyword.Bluemix_notm}} の地域の名前 |
| execute | プロパティー | <`true`、`false`> | 作成後にパイプラインを開始します |
| services | プロパティー | <`repo-name-key`> |  GitHub リポジトリーの親キー |
| hidden | プロパティー | <`[form, description]`> |  |

 `pipeline.yml` ファイルの作成については、[後続のセクション](#toolchains_custom_pipeline_yml)を参照してください。

 次のスニペットは、このセクションの例を示しています。

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

4\. **デプロイメントの詳細:
**

 継続的デリバリー・プロセスの一部としてツールチェーンをセットアップし、ツールチェーンをデプロイするユーザーがアクセスできる {{site.data.keyword.Bluemix_notm}} の地域、組織、またはスペースにアプリケーションをデプロイすることができます。アプリケーションをデプロイする場所の具体的な詳細を、ツールチェーンの作成ページから選択できます。  

 ![Delivery Pipeline の構成設定](images/deploy_configuration.png)

 `toolchain.yml` ファイルのこのセクションでは、ツールチェーンの作成ページから構成できるパイプラインのステージを定義します。

 まず、親キー `deploy` を使用して、デプロイメントの構成プロパティーを特定します。このセクションを構成するその他のプロパティーは次のとおりです。

| アイテム | キー/プロパティー | 値  | 説明 |
|------|--------------|-------|-------------|
| deploy | キー |  | デプロイ・セクションの名前 |
| schema | プロパティー | <`deploy.json`> | デプロイメントの詳細を構成するための UI のレイアウトを定義するファイル |
| service-category | プロパティー | <`pipeline`> | デプロイメントの構成を使用するサービス |
| parameters | キー |  |  |
| prod-region | プロパティー | <`"{{region}}"`> | 実動ステージの {{site.data.keyword.Bluemix_notm}} の地域を定義します。 |
| prod-organization | プロパティー | <`"{{organization}}"`> | 実動ステージの {{site.data.keyword.Bluemix_notm}} の組織を定義します。 |
| prod-space | プロパティー | <`prod`> | 実動ステージの {{site.data.keyword.Bluemix_notm}} のスペースを定義します。 |
| github-repo-name | プロパティー | <`"{{repo-name-key.parameters.repo_name}}"`> | ツールチェーンの作成ページに GitHub リポジトリーの名前を渡す変数 |

 `deploy.json` ファイルの作成については、[後続のセクション](#toolchains_custom_deploy_json)を参照してください。

 次の例では、実稼働環境にデプロイする単一のステージを定義しています。

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

 このサンプル・コードは、ほとんどの部分をそのまま使用することができますが、わずかな点だけを変更する必要があります。このセクションをカスタマイズするには、リポジトリーの名前に合わせて `github-repo-name` を更新する必要があります。 [`deploy.json`](#toolchains_custom_deploy_json) ファイル内の詳細も更新する必要があります。

 開発、QA、実動ステージを含むより複雑なパイプラインを作成する場合は、`parameters` キーの次のプロパティーを置き換えます。

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

5\. **ツールの構成**

 ツールチェーンの中核となるコンポーネントを構成した後で、ツールチェーンに機能を追加して使いやすさを向上するその他のツールの統合を含めることができます。すべてのツールに対するエントリーを `toolchain.yml` ファイルに追加する必要があり、ツールによっては、別の YAML 構成ファイルを `.bluemix` ディレクトリー内に作成する必要もあります。

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

`pipeline.yml` ファイルには、パイプラインのステージの構成の詳細がすべて含まれます。`pipeline.yml` ファイルの作成方法は 2 つあります。

1. `pipeline.yml` ファイルを手動で作成します。`pipeline.yml` ファイルを作成するための詳細と構文は、DevOps Services のサンプル・プロジェクトの「[DevOps Services サンプル・プロジェクトにおけるテキスト・ベースのパイプラインの共有](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}」に記載されています。

2. `pipeline.yml` ファイルを既存の DevOps Servicesプロジェクトから生成します。そのためには、次のようにします。
	
	1. 新しい [DevOps サービス・プロジェクト](https://hub.jazz.net/create){: new_window}を作成します。
	
	2. プロジェクトを開いて **BUILD & DEPLOY** をクリックします。
	
	3. パイプラインに必要なすべてのステージを構成します。
	
	4. ブラウザーのアドレス・バーで、`/yaml` をプロジェクトの URL に追加して Enter を押します。
	
	5. 結果として生成された `pipeline.yml` ファイルを GitHub リポジトリーの `.bluemix` ディレクトリーに保存します。

ツールチェーンに複数のパイプラインが含まれている場合、`pipeline.yml` ファイルごとに固有の名前を指定します。

以下は `pipeline.yml` ファイルの例です。

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

ツールチェーンの作成ページで、「構成可能な統合 (Configurable Integrations)」セクションから「Delivery Pipeline」を選択すると、セクションが展開されてそのツールに関して構成できる次のアイテムが表示されます。

	* アプリケーション名
	* パイプラインのステージがデプロイする地域、組織、スペース。

![Delivery Pipeline の構成設定](images/deploy_configuration.png)

UI のこのセクションのレイアウトは、`deploy.json` スキーマによって定義されます。

スキーマ内で、アプリケーションの詳細と一致するように、次のプロパティーを更新する必要があります。

	* Title
	* Description
	* LongDescription
	* `hello-world-name` のすべてのインスタンスと関連情報を、アプリケーションに合わせて変更する必要があります。

以下は `deploy.json` ファイルの例です。

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
