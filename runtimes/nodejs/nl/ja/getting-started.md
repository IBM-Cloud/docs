---

copyright:
  years: 2017
lastupdated: "2017-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Bluemix での Node.js 入門

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

このガイドに従うことによって、開発環境をセットアップし、ローカルおよび {{site.data.keyword.Bluemix}} でアプリケーションをデプロイし、{{site.data.keyword.Bluemix}} データベース・サービスをアプリケーションに統合します。

## 前提条件
{: #prereqs}

以下のアカウントおよびツールが必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Node ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://nodejs.org/en/){: new_window}


## 1. サンプル・アプリケーションを複製する
{: #clone}

最初に、Node.js *hello world* サンプル・アプリケーション GitHub リポジトリーを複製します。
  ```
git clone https://github.com/IBM-Bluemix/get-started-node
  ```
  {: pre}

## 2. アプリケーションをローカルで実行する
{: #run_locally}

npm パッケージ・マネージャーを使用して依存関係をインストールし、アプリケーションを実行します。

1. コマンド・ラインで、サンプル・アプリケーションがあるディレクトリーに移動します。
  ```
cd get-started-node
```
  {: pre}

1. アプリケーションをローカルに実行するため、[package.json ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.npmjs.com/files/package.json) ファイルにリストされている依存関係をインストールします。  
  ```
npm install
```
  {: pre}

1. アプリケーションを実行します。
  ```
npm start  
  ```
  {: pre}

http://localhost:3000 でアプリケーションを表示できます。

ファイル変更時にアプリケーションを自動再始動するには [nodemon](https://nodemon.io/) を使用します。
{: tip}


## 3. デプロイメントのためにアプリケーションを準備する
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。サンプル manifest.yml ファイルが `get-started-node` ディレクトリー内に用意されています。

manifest.yml ファイルを開き、`name` の `GetStartedNode` を、ご使用のアプリケーション名 (<var class="keyword varname" data-hd-keyref="app_name">app_name</var>) に変更します。
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

この manifest.yml ファイル内の **random-route: true** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。任意のホスト名を指定して、**random-route: true** を **host: myChosenHostName** に置き換えることも選択できます。[詳細はこちら...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. アプリケーションをデプロイする
{: #deploy}

Cloud Foundry CLI を使用して、アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイできます。

以下のコマンドを実行して API エンドポイントを設定します (*API-endpoint* 値は該当地域の API エンドポイントに置き換えてください)。
   ```
cf api <API-endpoint>
   ```
   {: pre}

|API エンドポイント                            |地域          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | 米国南部       |
| https://api.eu-gb.bluemix.net  | 英国 |
| https://api.au-syd.bluemix.net | シドニー         |

{{site.data.keyword.Bluemix_notm}} アカウントにログインします。

  ```
cf login
```
  {: pre}

*get-started-node* ディレクトリー内からアプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
  ```
cf push
```
  {: pre}

アプリケーションのデプロイには数分かかることがあります。デプロイメントが完了すると、アプリケーションが実行中であるというメッセージが表示されます。push コマンドの出力にリストされる URL でアプリケーションを表示するか、または、以下のコマンドを実行して、アプリケーションのデプロイメント状況と URL の両方を表示してください。
  ```
cf apps
  ```
  {: pre}

`cf logs <Your-App-Name> --recent` コマンドを使用して、デプロイメント処理でのエラーについてのトラブルシューティングを行うことができます。
{: tip}

## 5. データベースを追加する
{: #add_database}

次に、NoSQL データベースをこのアプリケーションに追加して、ローカルおよび {{site.data.keyword.Bluemix_notm}} 上で実行できるようにアプリケーションをセットアップします。

1. ブラウザーで {{site.data.keyword.Bluemix_notm}} にログインし、ダッシュボードに移動します。**「名前」**列でアプリケーションの名前をクリックして選択します。
2. **「接続」**をクリックし、**「新規に接続」**をクリックします。
2. **「データおよび分析」**セクションで`「Cloudant NoSQL DB」`を選択し、その後、サービスを作成します。
3. プロンプトが出されたら**「再ステージ」**を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。アプリケーションに対してこの環境変数が使用可能なのは、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合のみです。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. データベースを使用する
{: #use_database}
次に、このデータベースを指すようにローカル・コードを更新します。アプリケーションが使用するサービスの資格情報を保管する JSON ファイルを作成します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は `VCAP_SERVICES` 環境変数から読み取られます。

1. `get-started-node` ディレクトリーに、以下の内容の `vcap-local.json` という名前のファイルを作成します。
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. ブラウザーで、{{site.data.keyword.Bluemix_notm}} に移動し、**「アプリ」 > 「_your app_」 > 「接続」 > 「Cloudant」 > 「資格情報の表示」**を選択します。

3. 資格情報から `url` のみをコピーして、`vcap-local.json` ファイルの `url` フィールドに貼り付けて、**CLOUDANT_DATABASE_URL** を置き換えます。

4. アプリケーションをローカルで実行します。
  ```
npm start  
  ```
  {: pre}

  http://localhost:3000 でローカル・アプリケーションを表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションはデータベースを共有します。ブラウザーを最新表示すると、どちらかのアプリケーションから追加した名前が両方に表示されます。

予期しない課金が発生しないように、アプリケーションを {{site.data.keyword.Bluemix_notm}} で稼働中にしておく必要がない場合、アプリケーションを停止することを忘れないでください。
{: tip}
