---

copyright:

  years: 2017

lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}} CLI 用 {{site.data.keyword.bpshort}} CLI プラグイン
{: #cli}

{{site.data.keyword.Bluemix_notm}} 内で環境を管理したり他の操作を実行したりする際は、{{site.data.keyword.Bluemix}} CLI 用 {{site.data.keyword.bpshort}} コマンドを参照してください。
{: shortdesc}

CLI コマンドを使用する前に:

* `bx login [--sso]` を使用して {{site.data.keyword.Bluemix_notm}} にログインし、セッションの認証を受けます。
フェデレーテッド ID を使用するユーザーは、`--sso` フラグを使用してワンタイム・パスコードを生成する必要があります。

コマンドのリストを表示するには、`bx schematics help` を実行します。

<table id="manage_environments" summary="bx schematics environment コマンドを使用して環境を管理する。">
<caption>表 1. 環境を管理するために使用できるコマンド。これらのコマンドは先頭が <code>bx schematics environment</code> 構文です。
</caption>
 <thead>
 <th colspan="5">環境の管理</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="環境によってプロビジョンされたリソースを bx schematics action コマンドを使用して更新する。">
 <caption>表 2. 環境内のリソースを更新するために使用できるコマンド。これらのコマンドは先頭が <code>bx schematics action</code> 構文です。
</caption>
  <thead>
  <th colspan="5">リソースの更新</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="環境に対して実行されたアクティビティーを bx schematics activity コマンドを使用して監査する。">
  <caption>表 3. 環境に対して実行されたアクティビティーを監査するために使用できるコマンド。これらのコマンドは先頭が <code>bx schematics activity</code> 構文です。
</caption>
   <thead>
   <th colspan="5">環境の監査</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

構成から {{site.data.keyword.Bluemix_notm}} 内に環境を作成します。

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### パラメーター

<dl>
<dt>--file FILE_NAME</dt>
<dd>環境についての詳細を渡すために使用する JSON ファイル。
<p>
<p>使用可能な値をすべて指定した JSON の例:
<pre>{
    "description": "(オプション) 環境の説明",
    "frozen": false,
    "name": "環境の名前",
    "sourceurl": "Terraform 構成を指す GitHub URL",
    "tags": ["(オプション) metadata_tag_1", "(オプション) metadata_tag_2"],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(オプション) variable_1",
        "secure": false,
        "value": "可視値"
    },
    {
        "name": "(オプション) variable_2_secret",
        "secure": true,
        "value": "保護された値"
    }]
}</pre></dd>
<dt>--json</dt>
<dd>JSON フォーマットで出力を表示します。</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

{{site.data.keyword.Bluemix_notm}} から環境構成を削除します。このコマンドは、実行中のリソースが存在しない環境に対してのみ使用することをお勧めします。実行中のリソースが存在する環境を削除する場合は、個々のサービス・ダッシュボードで各リソースを管理する必要があります。

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### パラメーター

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--force</dt>
<dd>yes/no の確認を行わずに強制的にコマンドを進めます。</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

{{site.data.keyword.Bluemix_notm}} アカウント内のすべての既存環境のリストを取得します。

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### パラメーター
<dl>
<dt>--count VALUE</dt>
<dd>返される環境の数を制限します。</dd>
<dt>--offset VALUE</dt>
<dd>環境のリストでのオフセット。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで出力を表示します。</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

既存の環境についての詳細を取得します。

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで出力を表示します。</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

環境名や GitHub URL など、既存の環境に関する詳細を更新します。環境内に割り振られているリソースの数を更新するには、[bx schematics action plan](#action-plan) を参照してください。

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--file FILE_NAME</dt>
<dd>環境についての詳細を渡すために使用する JSON ファイル。
使用できる値を指定した JSON スニペットの例を、[bx schematics environment create](#environment-create) で確認してください。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで出力を表示します。</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

環境構成をデプロイします。`apply` コマンドは、GitHub リポジトリーに保管されている構成をスキャンして実行します。

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--force</dt>
<dd>yes/no の確認を行わずに強制的にコマンドを進めます。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで apply の出力を表示します。</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

環境とリソースを破棄します。`destroy` コマンドは、実行中のリソースも含めて環境を破棄します。一般に、この操作は一時的な環境にのみ使用します。例えば、限られた期間だけ環境を提供するために作成された QA 環境などに使用します。実稼働環境を破棄することはお勧めできません。`destroy` 操作は取り消せないため、注意して使用する必要があります。

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--force</dt>
<dd>yes/no の確認を行わずに強制的にコマンドを進めます。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで destroy 出力を表示します。</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

環境構成とデプロイされている構成を比較します。`plan` コマンドは GitHub リポジトリー内の構成をスキャンし、デプロイされた環境に関連付けられている状態ファイルとの差分の取得を実行します。plan の出力には、`apply` コマンドを使用して環境構成をデプロイした場合に追加または削除されるリソースが示されます。 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--file FILE_NAME</dt>
<dd>plan アクションのパラメーターを渡すために使用するオプションの JSON ファイル。パラメーター <code>sourcesha</code> を渡して、環境の Terraform 構成用の特定の Git ブランチを指定することができます。Git ブランチは、<code>refs/heads/BRANCH_NAME</code> などの head 参照として指定する必要があります。パラメーターを指定しない場合、デフォルト値は master ブランチの head (<code>refs/heads/master</code>) です。
<p>
<p>値を指定した JSON スニペットの例:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>JSON フォーマットで plan の出力を表示します。</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

環境に対して実行された Terraform アクティビティーからのデータをリストします。

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>環境の固有 ID。この値は <code>bx schematics environment list</code> を実行して取得できます。</dd>
<dt>--count VALUE</dt>
<dd>返されるアクティビティーの数。</dd>
<dt>--offset VALUE</dt>
<dd>リストでのオフセット。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで plan の出力を表示します。</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

環境に対して実行されたアクションの詳細なアクティビティー・ログを表示します。

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>特定のアクティビティーについての詳細を返すためのフラグ。<code>bx schematics activity list --id ENVIRONMENT_ID</code> コマンドを使用して、環境ごとのアクティビティー ID のリストを取得できます。</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

環境のプラン・ファイルを表示します。

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>特定のアクティビティーについての詳細を返すためのフラグ。<code>bx schematics activity list --id ENVIRONMENT_ID</code> コマンドを使用して、環境ごとのアクティビティー ID のリストを取得できます。</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

環境に対して実行された特定のアクティビティーについての詳細を取得します。

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### パラメーター
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>特定のアクティビティーについての詳細を返すためのフラグ。<code>bx schematics activity list --id ENVIRONMENT_ID</code> コマンドを使用して、環境ごとのアクティビティー ID のリストを取得できます。</dd>
<dt>--json</dt>
<dd>JSON フォーマットで plan の出力を表示します。</dd>
</dl>
