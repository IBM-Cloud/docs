---

copyright:
  years: 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Bluemix での Python 入門
{: #getting_started}

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

このガイドに従うことによって、開発環境をセットアップし、ローカルおよび {{site.data.keyword.Bluemix}} でアプリケーションをデプロイし、{{site.data.keyword.Bluemix}} データベース・サービスをアプリケーションに統合します。

## 前提条件
{: #prereqs}

以下が必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Python ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.python.org/downloads/){: new_window}

## 1. サンプル・アプリケーションの複製
{: #clone}

アプリケーションの操作を開始する準備ができました。リポジトリーを複製して、サンプル・アプリケーションがあるディレクトリーに変更します。
  ```
git clone https://github.com/IBM-Bluemix/get-started-python
  ```
  {: pre}
  ```
cd get-started-python
  ```
  {: pre}

  *get-started-python* ディレクトリー内のファイルを詳細に調べて、内容をよく理解します。

## 2. アプリケーションのローカルでの実行
{: #run_locally}

ご使用のシステムでの Python のセットアップに関するヘルプについては、[『The Hitchhiker’s Guide to Python!』![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://docs.python-guide.org/en/latest/)を参照してください。
{: tip}

ローカルでアプリケーションを実行できるようにするには、[requirements.txt ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://pip.readthedocs.io/en/stable/user_guide/#requirements-files) ファイルにリストされている依存関係をインストールします。

オプションで[仮想環境![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://packaging.python.org/installing/#creating-and-using-virtual-environments)を使用して、これらの依存関係が他の Python プロジェクトやご使用のオペレーティング・システムの依存関係と衝突するのを避けることができます。
{: tip}

  ```
pip install -r requirements.txt
  ```
  {: pre}

または、Python3 を使用して以下を発行できます。

  ```
python3 -m pip install -r requirements.txt
  ```
  {: pre}

アプリケーションを実行します。
  ```
python hello.py
  ```
  {: pre}

 http://localhost:8000 でアプリケーションを表示します。


## 3. デプロイメントのためのアプリケーションの準備
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。`get-started-python` ディレクトリーにサンプルの manifest.yml ファイルが用意されています。

manifest.yml ファイルを開き、`name` を `GetStartedPython` からご使用のアプリケーション名 <var class="keyword varname" data-hd-keyref="app_name">app_name</var> に変更します。
{: download}

  ```
  applications:
  - name: GetStartedPython
    random-route: true
    memory: 128M
  ```
  {: codeblock}

この manifest.yml ファイル内の **random-route: true** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。任意のホスト名を指定して、**random-route: true** を **host: myChosenHostName** に置き換えることも選択できます。[詳細はこちら...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. アプリケーションのデプロイ
{: #deploy}

Cloud Foundry CLI を使用してアプリケーションをデプロイできます。

API エンドポイントを選択します。
   ```
cf api <API-endpoint>
   ```
   {: pre}

コマンド内の *API-endpoint* は以下のリストにある API エンドポイントのいずれかで置き換えてください。

|URL                             |地域          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | 米国南部       |
| https://api.eu-gb.bluemix.net  | 英国 |
| https://api.au-syd.bluemix.net | シドニー         |

{{site.data.keyword.Bluemix_notm}} アカウントにログインします。

  ```
cf login
```
  {: pre}

*get-started-python* ディレクトリー内から、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
  ```
cf push
```
  {: pre}

これには時間がかかることがあります。デプロイメント・プロセスでエラーが発生した場合、`cf logs <Your-App-Name> --recent` コマンドを使用してトラブルシューティングできます。

デプロイメントが完了すると、アプリケーションが実行中であることを示すメッセージが表示されます。push コマンドの出力にリストされている URL でアプリケーションを表示します。また、
  ```
cf apps
  ```
  {: pre}
  コマンドを発行して、アプリケーションの状況と URL を確認することもできます。

## 5. データベースの追加
{: #add_database}

次に、NoSQL データベースをこのアプリケーションに追加して、ローカルおよび {{site.data.keyword.Bluemix_notm}} 上で実行できるようにアプリケーションをセットアップします。

1. ご使用のブラウザーで {{site.data.keyword.Bluemix_notm}} にログインします。`「ダッシュボード」`を参照します。`「名前」`列でアプリケーション名をクリックして、そのアプリケーションを選択します。
2. `「接続」`、`「新規に接続」`の順にクリックします。
2. `「データおよび分析」`セクションで、`「Cloudant NoSQL DB」`を選択して、サービスを`作成`します。
3. プロンプトが出されたら、`「再ステージ」`を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。この環境変数は、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合にのみアプリケーションで使用できます。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. データベースの使用
{: #use_database}
次に、このデータベースを指すようにローカル・コードを更新します。アプリケーションが使用するサービスの資格情報を保管する json ファイルを作成します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は VCAP_SERVICES 環境変数から読み取られます。

1. `get-started-python` ディレクトリーに、次の内容の `vcap-local.json` というファイルを作成します。
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "username":"CLOUDANT_DATABASE_USERNAME",
            "password":"CLOUDANT_DATABASE_PASSWORD",
            "host":"CLOUDANT_DATABASE_HOST"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: pre}

2. {{site.data.keyword.Bluemix_notm}} UI に戻って、「アプリ」->「接続」->「Cloudant」->「資格情報の表示」を選択します。

3. 資格情報から `username`、`password`、および `host` をコピーして、`vcap-local.json` ファイルの同じフィールドに貼り付けて、**CLOUDANT_DATABASE_USERNAME**、**CLOUDANT_DATABASE_PASSWORD**、および **CLOUDANT_DATABASE_URL** を置き換えます。

4. アプリケーションをローカルで実行します。
  ```
python hello.py
  ```
  {: pre}

  http://localhost:8000 でアプリケーションを表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションはデータベースを共有しています。上の push コマンドの出力にリストされている URL で {{site.data.keyword.Bluemix_notm}} アプリケーションを表示します。いずれかのアプリケーションから追加した名前は、ブラウザーを最新表示すると両方に表示されます。

予期しない課金が発生しないように、アプリケーションを稼働中にしておく必要がない場合は停止することを忘れないでください。
{: tip}
