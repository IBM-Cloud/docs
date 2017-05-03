---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Bluemix での Go 入門

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

このガイドに従うことによって、開発環境をセットアップし、ローカルおよび {{site.data.keyword.Bluemix}} でアプリケーションをデプロイし、{{site.data.keyword.Bluemix}} データベース・サービスをアプリケーションに統合します。

## 前提条件
{: #prereqs}

以下が必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Go ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://golang.org/dl/){: new_window}

## 1. ローカル環境をセットアップし、サンプル・アプリケーションを複製する
{: #clone}

最初に、すべての GO 環境変数が正しく設定されていることを確認して、ローカル環境をセットアップします。例えば、次のとおりです。
```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
```

パスを $GOPATH/src に変更します。
```
mkdir $GOPATH/src
cd $GOPATH/src
```

これで、単純な Go *hello world* アプリケーションを使用した作業を開始する準備ができました。リポジトリーを複製して、サンプル・アプリケーションがあるディレクトリーに移動します。
```
go get github.com/IBM-Bluemix/get-started-go
```
{: pre}
```
cd github.com/IBM-Bluemix/get-started-go
```
{: pre}

*get-started-go* ディレクトリー内のファイルをよく見て内容を把握してください。

## 2. アプリケーションをローカルで実行する
{: #run_locally}

  {: pre}

  アプリケーションをビルドし、実行します。
  ```
make
  ```
  {: pre}

  ```
go run main.go
  ```
  {: pre}

  http://localhost:8080 でアプリケーションを表示します。

アプリケーションを停止するには、アプリケーションを開始したのと同じウィンドウで *Ctrl-c* を使用します。
{: tip}

## 3. デプロイメントのためにアプリケーションを準備する
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。サンプル manifest.yml ファイルが `get-started-go` ディレクトリー内に用意されています。

manifest.yml ファイルを開き、`name` の `GetStartedGo` を、ご使用のアプリケーション名 (<var class="keyword varname" data-hd-keyref="app_name">app_name</var>) に変更します。
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

この manifest.yml ファイル内の **random-route: true** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。任意のホスト名を指定して、**random-route: true** を **host: myChosenHostName** に置き換えることも選択できます。[詳細はこちら...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. アプリケーションをデプロイする
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

*get-started-go* ディレクトリー内からアプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
  ```
cf push
```
  {: pre}

これには時間がかかることがあります。デプロイメント・プロセスでエラーが発生した場合、`cf logs <Your-App-Name> --recent` コマンドを使用してトラブルシューティングできます。

デプロイメントが完了すると、アプリケーションが実行中であることを示すメッセージが表示されます。push コマンドの出力にリストされている URL でアプリケーションを表示します。また、以下のコマンドを実行することもできます。

   ```
cf apps
    ```
  {: pre}
  このコマンドにより、アプリケーションの状況と URL が表示されます。

## 5. データベースを追加する
{: #add_database}

次に、NoSQL データベースをこのアプリケーションに追加して、ローカルおよび {{site.data.keyword.Bluemix_notm}} 上で実行できるようにアプリケーションをセットアップします。

1. ご使用のブラウザーで {{site.data.keyword.Bluemix_notm}} にログインします。`「ダッシュボード」`を参照します。`「名前」`列でアプリケーションの名前をクリックして選択します。
2. `「接続」`、`「新規に接続」`の順にクリックします。
3. `「データおよび分析」`セクションで、`「Cloudant NoSQL DB」`を選択して、サービスを`作成`します。
4. プロンプトが出されたら`「再ステージ」`を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。この環境変数は、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合にのみアプリケーションで使用できます。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. データベースを使用する
{: #use_database}
次に、このデータベースを指すようにローカル・コードを更新します。アプリケーションが使用するサービスの資格情報を保管する json ファイルを作成します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は VCAP_SERVICES 環境変数から読み取られます。

1. 次のような内容の `.env` という名前のファイルを `get-started-go` ディレクトリー内に作成します。
  ```
  CLOUDANT_URL=
  ```
  {: pre}

2. {{site.data.keyword.Bluemix_notm}} UI に戻って、「アプリ」->「接続」->「Cloudant」->「資格情報の表示」を選択します。

3. 資格情報から `url` のみをコピーして、`.env` ファイルの `CLOUDANT_URL` フィールドに貼り付け、変更を保存します。結果は次のようになります。
  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```

4. アプリケーションをローカルで実行します。
  ```
go run main.go
  ```
  {: pre}

  http://localhost:8080 でアプリケーションを表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションはデータベースを共有します。上の push コマンドの出力にリストされている URL で {{site.data.keyword.Bluemix_notm}} アプリケーションを表示します。いずれかのアプリケーションから追加した名前は、ブラウザーを最新表示すると両方に表示されます。


予期しない課金が発生しないように、アプリケーションを稼働中にしておく必要がない場合は停止することを忘れないでください。
{: tip}
