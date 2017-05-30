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

# 環境内のリソースの管理
{: #managing}

{{site.data.keyword.bplong}} を使用すると、環境の管理が簡単になります。デプロイしたリソースを変更したり、オンデマンドで変更を繰り返し再デプロイしたりできます。

{:shortdesc}

環境に対する変更は、軽量プロセスを使用してデプロイできます。割り振られているリソースを変更する場合は、構成に対する変更を宣言構文でコーディングします。つまり、必要な結果のみを記述します。{{site.data.keyword.bpshort}} では、デプロイメントの前に変更内容をプレビューできます。


## GUI を使用したリソースの更新
{: #gui}

グラフィカル・ビューを使用して環境内のリソースを管理したい場合は、{{site.data.keyword.bpshort}} ダッシュボードを使用できます。
{:shortdesc}

構成に対するコード変更を GitHub で公開した後や、GUI で変数を変更した後で、以下の手順を実行して、更新内容を環境にデプロイします。

1. **{{site.data.keyword.bpshort}}** ダッシュボードで、「**環境**」を選択します。

2. 更新する特定の環境の行を選択します。

3. **「プラン」**をクリックし、プランのログにエラーがないか確認します。自分または {{site.data.keyword.Bluemix_notm}} アカウント内の他のコラボレーターがプランを適用するか取り消すまで、環境はロックされます。 

4. **「適用」**をクリックして、更新をデプロイします。 


## CLI を使用したリソースの更新
{: #cli}

{{site.data.keyword.bpshort}} CLI を使用したプログラムによって、環境内のリソースを更新することができます。
{:shortdesc}

構成に対するコード変更を GitHub に公開した後で、以下の手順を実行して、更新内容を環境にデプロイします。

1. `plan` コマンドを実行します。{{site.data.keyword.bpshort}} CLI は、更新された環境構成を GitHub からプルし、リソースと現在のデプロイメントの差分を示すプレビューを出力します。

  ```
  bx schematics action plan --id ENVIRONMENT_ID
```
  {: codeblock}

2. アクティビティー・ログで plan の出力を確認します。

  ```
  bx schematics activity log --id ACTIVITY_ID
```
  {: codeblock}

3. `apply` コマンドを実行して、プランをデプロイします。 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
```
  {: codeblock}


## API を使用したリソースの更新
{: #api}

{{site.data.keyword.bpshort}} API を使用したプログラムによって、環境内のリソースを管理することができます。
{:shortdesc}

構成に対するコード変更を GitHub に公開した後で、以下の手順を実行して、更新内容を環境にデプロイします。

1. `POST v1/environments/<environment_ID>/plan` 呼び出しを実行します。{{site.data.keyword.bpshort}} API は、更新された環境構成を GitHub からプルし、Terraform 状態ファイルと比較して、リソースと現在のデプロイメントの差分を示します。

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  応答の例:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. アクティビティー・ログで plan の出力を確認します。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. `PUT /v1/environments/<environment_ID>/apply` 呼び出しを実行して、プランをデプロイします。 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## 環境に対する変更の監査
{: #auditing}

ソース・コントロール・リポジトリーのバージョン履歴で構成を監査することができます。環境へのデプロイメントをモニターしたり、過去のデプロイメントのログを参照したりするために、{{site.data.keyword.bpshort}} では以下の方法で監査ログを表示することができます。

### {{site.data.keyword.bpshort}} ダッシュボードから
{: #auditing-gui}

1. 該当する環境の行を選択して、環境の詳細ページにアクセスします。

2. **「最近のアクティビティー」**セクションをモニターします。過去のプランとデプロイメントの履歴ログを表示することもできます。

### {{site.data.keyword.bpshort}} CLI を使用
{: #auditing-cli}

1. 環境 ID を取得します。

  ```
  bx schematics environment list
```
  {: codeblock}

2. 環境のアクティビティー ID を取得します。アクティビティー ID は、プラン、適用、破棄、削除の各操作に割り当てられます。次のコマンドによって、環境に対して実行されたすべてのアクティビティーがリストされます。

  ```
  bx schematics activity list --id ENVIRONMENT_ID
```
  {: codeblock}

3. いつ、だれが環境に変更を加えたかといった、特定のアクティビティーに関するデータを取得します。

  ```
  bx schematics activity show --id ACTIVITY_ID
```
  {: codeblock}

4. オプション: プランや適用の出力などの詳細なログを表示するには、`log` コマンドを実行します。 

  ```
  bx schematics activity log --id ACTIVITY_ID
```
  {: codeblock}

### {{site.data.keyword.bpshort}} API を使用
{: #auditing-api}

1. 環境 ID を取得します。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  応答本文には、{{site.data.keyword.Bluemix_notm}} アカウント内のすべての環境が含まれます。監査する特定の環境の `id` 値を見つけます。

2. 環境に対して実行されたアクションのアクティビティー ID を取得します。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. 環境に対する特定のアクティビティーを取得します。 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Terraform 出力の詳細なログを調べます。

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
