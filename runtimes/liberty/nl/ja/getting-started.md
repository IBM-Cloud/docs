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

# Bluemix での Liberty 入門

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

このガイドに従うことによって、開発環境をセットアップし、ローカルおよび {{site.data.keyword.Bluemix}} でアプリケーションをデプロイし、{{site.data.keyword.Bluemix}} データベース・サービスをアプリケーションに統合します。

## 前提条件
{: #prereqs}

以下のアカウントおよびツールが必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://maven.apache.org/download.cgi){: new_window}

{{site.data.keyword.eclipsetoolsfull}} を使用して Eclipse で開発を行うには、[ツールのダウンロード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window} も必要です。

## 1. サンプル・アプリケーションを複製する
{: #clone}

最初に、サンプル・アプリケーション GitHub リポジトリーを複製します。
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. コマンド・ラインを使用してアプリケーションをローカルで実行する
{: #run_locally}

Maven を使用して、ソース・コードをビルドし、結果のアプリケーションを実行します。

1. コマンド・ラインで、サンプル・アプリケーションがあるディレクトリーに移動します。

  ```
cd get-started-java
  ```
  {: pre}

1. Maven を使用して、依存関係をインストールし、.war ファイルをビルドします。

  ```
mvn clean install
  ```
  {: pre}

1. Liberty 上でアプリケーションをローカルに実行します。
  ```
mvn install liberty:run-server
  ```
  {: pre}

*The server defaultServer is ready to run a smarter planet.* というメッセージが表示されたら、http://localhost:9080/GetStartedJava でアプリケーションを表示します。

アプリケーションを停止するには、アプリケーションを開始したコマンド・ライン・ウィンドウで *Ctrl-C* を押します。

## 3. デプロイメントのためにアプリケーションを準備する
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。サンプル manifest.yml ファイルが `get-started-java` ディレクトリー内に用意されています。

manifest.yml ファイルを開き、`name` の `GetStartedJava` を、ご使用のアプリケーション名 (<var class="keyword varname" data-hd-keyref="app_name">app_name</var>) に変更します。
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

この manifest.yml ファイル内の **random-route: true** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。任意のホスト名を指定して、**random-route: true** を **host: myChosenHostName** に置き換えることも選択できます。[詳細はこちら...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. {{site.data.keyword.Bluemix_notm}} にデプロイする
{: #deploy}

以下のいずれかの Bluemix 地域にアプリケーションをデプロイします。待ち時間をできるだけ短くするため、ユーザーに最も近い地域を選択してください。

|地域          |API エンドポイント                             |
|:---------------|:-------------------------------|
| 米国南部       |https://api.ng.bluemix.net     |
| 英国 | https://api.eu-gb.bluemix.net  |
| シドニー         | https://api.au-syd.bluemix.net |

1. `<API-endpoint>` を該当する地域のエンドポイントに置き換えて、API エンドポイントを設定します。
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. {{site.data.keyword.Bluemix_notm}} アカウントにログインします。
  ```
cf login
```
  {: pre}

1. `get-started-java` ディレクトリー内からアプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
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

## 5. Eclipse を使用して開発する
{: #eclipse}

{{site.data.keyword.eclipsetoolsfull}} では、ご使用の統合開発環境 (IDE) と {{site.data.keyword.Bluemix_notm}} とを統合する上で役立つプラグインが用意されています。このプラグインは、既存の Eclipse 環境にインストールできます。

1. [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix) があることを確認します。

2. **「ファイル」 > 「インポート」 > 「Maven」 > 「既存 Maven プロジェクト」**と進んで、`get-started-java` サンプルを Eclipse にインポートします。

3. Liberty サーバー定義を作成します。以下のステップで、新規 Liberty サーバーがダウンロードされます。
  - 「サーバー」ビュー (**「ウィンドウ」 > 「ビューの表示」 > 「サーバー」**) で右クリックし、**「新規」 > 「サーバー」**と選択します。
  - **「IBM」 > 「WebSphere Application Server Liberty」**を選択します。
  - **「アーカイブまたはリポジトリーからインストール」**を選択します。
  - プロンプトが出されたら、Liberty をインストールする新規フォルダーへの宛先パス (/Users/username/liberty) を入力します。
  - **「ibm.com から新規ランタイム環境をダウンロードしてインストール」**を選択します。
  - **「WAS Liberty with Java EE 7 Web Profile」**を選択します。
  - デフォルト・オプションでウィザードを続行して、終了します。

4. Liberty でアプリケーションをローカルに実行します。
  - **「ウィンドウ」 > 「Web ブラウザー」 > 「デフォルトのシステム Web ブラウザー」**と進んで、Web ブラウザーをシステム・デフォルトに変更します。
  - `GetStartedJava` サンプルを右クリックし、**「実行」 > 「サーバーで実行」**を選択します。
  - localhost Liberty サーバーを見つけて選択し、**「完了」**をクリックします。

  数秒内に、アプリケーションは http://localhost:9080/GetStartedJava で実行中になります。

5. コードを更新します。
  - `src/main/webapp/index.html` を開き、ヘッディングを `<h1>Welcome.</h1>` から `<h1>Welcome Jane.</h1>` に更新します。
  - 変更を保存します。Liberty によって変更が自動的に選出されます。
  - ブラウザー (http://localhost:9080/GetStartedJava) を最新表示して変更を確認します。

6. 変更を {{site.data.keyword.Bluemix_notm}} にプッシュします。
  - コマンド・ラインの `get-started-java` ディレクトリーから、.war ファイルを再ビルドします。
    ```
mvn clean install
    ```
    {: pre}
  - アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
    ```
cf push
```
    {: pre}

これで、ローカルとクラウドの両方でコードを実行できました。

## 6. データベースを追加する
{: #add_database}

次に、NoSQL データベースをこのアプリケーションに追加して、ローカルおよび {{site.data.keyword.Bluemix_notm}} 上で実行できるようにアプリケーションをセットアップします。

1. ブラウザーで {{site.data.keyword.Bluemix_notm}} にログインし、ダッシュボードに移動します。**「名前」**列でアプリケーションの名前をクリックして選択します。
2. **「接続」**をクリックし、次に**「新規に接続」**をクリックします。
3. **「データおよび分析」**セクションで**「Cloudant NoSQL DB」**を選択し、その後、サービスを作成します。
4. プロンプトが出されたら**「再ステージ」**を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。アプリケーションに対してこの環境変数が使用可能なのは、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合のみです。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. データベースを使用する
{: #use_database}
次に、このデータベースを指すようにローカル・コードを更新します。サービス用の資格情報をプロパティー・ファイルに保管します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は `VCAP_SERVICES` 環境変数から読み取られます。

1. Eclipse で、src/main/resources/cloudant.properties ファイルを開きます。
  ```
  cloudant_url=
  ```
  {: pre}

2. ブラウザーで、{{site.data.keyword.Bluemix_notm}} に移動し、**「アプリ」 > 「_your app_」 > 「接続」 > 「Cloudant」 > 「資格情報の表示」**を選択します。

3. 資格情報から `url` のみをコピーして、`cloudant.properties` ファイルの `url` フィールドに貼り付け、変更を保存します。
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. Eclipse で`「サーバー」`ビューから Liberty サーバーを再始動します。

  http://localhost:9080/GetStartedJava/ でブラウザーの表示を最新表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションはデータベースを共有します。ブラウザーを最新表示すると、どちらかのアプリケーションから追加した名前が両方に表示されます。


予期しない課金が発生しないように、アプリケーションを {{site.data.keyword.Bluemix_notm}} で稼働中にしておく必要がない場合、アプリケーションを停止することを忘れないでください。
{: tip}  
