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

# 環境へのリソースのデプロイ
{: #deploying}

{{site.data.keyword.bplong}} を使用すると、ソース・コードから最新のコード変更を直接デプロイできます。環境をデプロイすると、構成ファイルで定義されたリソースがデプロイされます。その後、{{site.data.keyword.bpshort}} から、その環境のプロビジョニング、オーケストレーション、ライフサイクルを管理できます。
{:shortdesc}

## GUI による環境へのデプロイ
{: #gui}

グラフィカル・ビューを使用して環境をデプロイしたい場合は、{{site.data.keyword.bpshort}} ダッシュボードを使用できます。
{:shortdesc}


### 前提条件
{: #gui-prereq}

* ソース・コントロールに Terraform 構成を格納します。構成は、HashiCorp Configuration Language (HCL) または JSON 構文で記述できます。HCL 構文と構成の記述に関するガイドラインについては、<a href="https://www.terraform.io/docs/configuration/index.html">Terraform 構成の資料<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。使用できるリソースについては、<a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud プロバイダー<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。

構成を保管したら、次のようにします。

1. **{{site.data.keyword.bpshort}}** ダッシュボードで、「**環境**」を選択します。

2. 「**環境の作成 (Create Environment)**」をクリックして環境を追加するか、デプロイする既存の環境の行を選択します。

3. 「**プラン**」をクリックして、環境をデプロイした場合にプロビジョンされるリソースをプレビューします。プランを実行すると、{{site.data.keyword.bpshort}} がソース・コントロールから環境の詳細の変数と最新バージョンの構成を抽出します。プランの出力に、その構成と現在デプロイされているもの (Terraform 状態管理ファイルを基に認識されます) の比較が表示されます。プランが環境に適用されるかキャンセルされるまでは、変更を防止するために環境はロックされます。 

4. 「**最近のアクティビティー**」セクションのログを参照し、プランの出力を確認します。プランの出力には、エラーの有無、サービスによって作成、変更、または破棄されるリソースが示されます。

5. プランを起動する準備が整ったら、「**適用**」をクリックします。アクティビティー・ログをモニターして、最新の実行でプランが正常に適用されたことを確認できます。 


## CLI による環境へのデプロイ
{: #cli}

{{site.data.keyword.Bluemix_notm}} CLI 用の {{site.data.keyword.bpshort}} プラグインを使用して、環境に更新をデプロイできます。
{:shortdesc}

### 前提条件
{: #cli-prereq}

* ソース・コントロールに Terraform 構成を格納します。
* まだインストールしていない場合は、使用するオペレーティング・システムに合った {{site.data.keyword.Bluemix_notm}} CLI を [{{site.data.keyword.Bluemix_notm}} CLI リポジトリー](http://clis.ng.bluemix.net/ui/home.html)からインストールします。

{{site.data.keyword.Bluemix_notm}} CLI にログインしてから、次のようにします。

1. 以下のコマンドを実行して {{site.data.keyword.bpshort}} CLI プラグインをインストールします。
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  インストールが成功すると、{{site.data.keyword.bpshort}} プラグインが `bx plugin list` の下に表示されます。 

2. 構成から環境を作成します。環境を作成するときには、サービスにソース・コントロールを参照させ、サービスが最新のコードを抽出できるようにします。 
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="環境作成コマンドの説明。">
  <caption>表 1. 環境作成コマンドの説明。
  </caption>
  <thead>
  <th colspan="1">コマンド</th>
  <th colspan="1">説明</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>環境の詳細が格納されている JSON ファイル。
  <p>
  <p>JSON の例:
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
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  返された `ID` 値をメモしてください。`ID` は、環境に割り当てられた固有 ID であり、これ以降のコマンドで使用します。
  
3. `plan` コマンドを実行して、環境がどのように変更されるかをプレビューします。plan コマンドは、現在デプロイされているものと比較して、どのリソースがどれだけ変更されるのかを示しますが、`apply` コマンドを実行するまでそれらの変更は適用されません。
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="plan コマンドの説明。">
  <caption>表 2. plan コマンドの説明。
  </caption>
  <thead>
  <th colspan="1">コマンド</th>
  <th colspan="1">説明</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>実行プランを実行する特定の環境。環境 ID 値を取得する必要がある場合には、<code>bx schematics list</code> を実行できます。
  </td>
  </tbody></table>
  
  `activity_id` がプランに割り当てられ、アクティビティー・ログに記録されます。 

4. アクティビティー・ログを取得して、Terraform プランの出力を表示します。

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="log コマンドの説明。">
  <caption>表 3. log コマンドの説明。
  </caption>
  <thead>
  <th colspan="1">コマンド</th>
  <th colspan="1">説明</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>ログを表示する特定のアクティビティー。アクティビティー ID 値を取得する必要がある場合には、<code>bx schematics activity list --id ENVIRONMENT_ID</code> を実行できます。
  </td>
  </tbody></table>
  
5. `apply` コマンドを実行して、環境にリソースをデプロイします。
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="apply コマンドの説明。">
  <caption>表 4. apply コマンドの説明。
  </caption>
  <thead>
  <th colspan="1">コマンド</th>
  <th colspan="1">説明</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>更新をデプロイする特定の環境。環境 ID 値を取得する必要がある場合には、<code>bx schematics list</code> を実行できます。
  </td>
  </tbody></table>
  
6. apply の出力をモニターして、デプロイメントが正常に行われたことを確認します。 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  デプロイメントが成功すると、出力の最後のあたりに次の行が返されます。
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## API による環境へのデプロイ
{: #api}

{{site.data.keyword.bpshort}} API を使用したプログラムによって環境をデプロイすることができます。
{:shortdesc}

以下をベース・エンドポイントとする <a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}} API <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> ポイントを呼び出します。

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### 前提条件
{: #api-prereq}

* ソース・コントロールに Terraform 構成を格納します。

以下の手順を実行して、リソースを環境にデプロイします。

1. 認証ヘッダーで使用する IAM OAuth トークンを生成します。次のコマンドは、UAA トークンと IAM トークンを出力します。
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  出力例:
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  `Bearer eyJraWQ...` という出力は、IAM トークンの一部を例として切り出したものです。API 呼び出しのヘッダーにはトークン全体を含めてください。
  
2. `POST v1/environments` 呼び出しを実行して、環境を作成します。

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
  }'
  ```
  {: codeblock}
    
  成功した場合は、以下の出力が応答として返されます。
  ```
  {
    "id": "Environment ID",
    "name": "Environment name",
    "description": "Description of the environment",
    "account": "{{site.data.keyword.Bluemix_notm}} account GUID",
    "owner": "The IBMid of the user who created the environment",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "The GitHub URL that points to the configuration",
    "statefile": "The reference to the Terraform state file",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Visible value"
      }
    ]
  }
  ```
  {: screen}
    
  返された `id` 値をメモしてください。`id` は、環境に割り当てられた固有 ID であり、これ以降の呼び出しで使用します。
  
3. `POST v1/environments/<environment_ID>/plan` 呼び出しを実行し、構成を適用した場合に環境にデプロイされるリソースをプレビューします。plan によって、リポジトリーのマスター・ブランチにある環境構成が抽出されます。
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  成功した場合は、`activityid` が応答として返されます。plan や apply の出力などのログを表示するときに、このアクティビティー ID 値が必要になります。
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 呼び出しを実行して、plan の出力を表示します。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. `PUT v1/environments/<environment_ID>/apply/` 呼び出しを実行して、環境をデプロイします。
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` 呼び出しを実行して apply の出力を表示し、デプロイメントをモニターします。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  デプロイメントが成功すると、出力の最後のあたりに次の行が返されます。
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
