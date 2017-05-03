---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Bluemix での Tomcat 入門
{: #getting_started}

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

このガイドに従うことによって、開発環境をセットアップし、ローカルおよび {{site.data.keyword.Bluemix}} でアプリケーションをデプロイし、{{site.data.keyword.Bluemix}} データベース・サービスをアプリケーションに統合します。

## 前提条件
{: #prereqs}

以下が必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat バージョン 8.0.41 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## 1. サンプル・アプリケーションの複製
{: #clone}

サンプルの Tomcat アプリケーションの操作を開始する準備ができました。リポジトリーを複製して、サンプル・アプリケーションがあるディレクトリーに変更します。
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

*get-started-tomcat* ディレクトリー内のファイルを詳細に調べて、内容をよく理解します。

## 2. アプリケーションのローカルでの実行
{: #run_locally}

アプリケーションをインストールするには、pom.xml ファイルで定義されているように依存関係をインストールして、.war ファイルをビルドする必要があります。

依存関係をインストールします。

```
mvn clean install
```
{: pre}


GetStartedTomcat.war を `target` ディレクトリーから `tomcat-install-dir` `webapps` ディレクトリーにコピーします。

アプリケーションを実行します。  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: screen}

http://localhost:8080/GetStartedTomcat/ でアプリケーションを表示します。

`shutdown.bat|.sh` を使用してアプリケーションを停止します。コマンドの実行許可の付与が必要になる可能性があることに注意してください。
{: tip}

## 3. {{site.data.keyword.Bluemix_notm}} のデプロイメントのためのアプリケーションの準備
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。`get-started-tomcat` ディレクトリーにサンプルの manifest.yml ファイルが用意されています。

manifest.yml ファイルを開き、`name` を `GetStartedTomcat` からご使用のアプリケーション名 <var class="keyword varname" data-hd-keyref="app_name">app_name</var> に変更します。
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/TomcatHelloWorldApp.war
    buildpack: java_buildpack
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
{:pre}

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

*get-started-tomcat* ディレクトリー内から、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
```
cf push
```
{: pre}

これには約 2 分かかることがあります。デプロイメント・プロセスでエラーが発生した場合、`cf logs <Your-App-Name> --recent` コマンドを使用してトラブルシューティングできます。

デプロイメントが完了すると、アプリケーションが実行中であることを示すメッセージが表示されます。push コマンドの出力にリストされている URL でアプリケーションを表示します。また、
  ```
cf apps
  ```
  {: pre}
  コマンドを発行して、アプリケーションの状況と URL を確認することもできます。

## 6. Eclipse での開発
{: #developing_in_eclipse}

IBM® Eclipse Tools for {{site.data.keyword.Bluemix}} には、開発者の統合開発環境 (IDE) を {{site.data.keyword.Bluemix_notm}} と統合するのを支援するために、既存の Eclipse 環境にインストールできるプラグインが用意されています。

[IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix) をダウンロードしてインストールします。

`「ファイル」`->`「インポート」`->`「Maven」`->`「既存の Maven プロジェクト」`オプションを使用して、このサンプルを Eclipse にインポートします。

Tomcat サーバー定義を作成します。
  - `「サーバー (Servers)」`ビューで、右クリック ->`「新規 (New)」`->`「サーバー (Server)」`と選択します。
  - `「Apache」`->`「Tomcat v8.0 サーバー」`を選択します。
  - `tomcat-install-dir` を選択します。
  - デフォルト・オプションでウィザードを続行して、終了します。

アプリケーションを Apache サーバーでローカルで実行します。
  - `GetStartedTomcat` サンプルを右クリックして、`「実行 (Run As)」`->`「サーバーで実行 (Run on Server)」`オプションを選択します。
  - ローカル・ホスト Tomcat サーバーを見つけて選択し、「完了」を押します。
  - 数秒後に、http://localhost:8080/TomcatHelloWorldApp/ でアプリケーションが実行されます。

{{site.data.keyword.Bluemix_notm}} サーバー定義を作成します。
  - `「サーバー (Servers)」`ビューで、右クリック ->`「新規 (New)」`->`「サーバー (Server)」`を選択します。
  - `「IBM」`->`「IBM Bluemix」`を選択して、ウィザードの手順に従います。
  - 資格情報を入力して、`「次へ」`をクリックします。
  - `「組織」`と`「スペース」`を選択して、`「完了」`をクリックします。

{{site.data.keyword.Bluemix_notm}} でアプリケーションを実行します。
  - `GetStartedTomcat` サンプルを右クリックして、`「実行 (Run As)」`->`「サーバーで実行 (Run on Server)」`オプションを選択します。
  - `IBM Bluemix` を見つけて選択し、「完了」を押します。
  - ウィザードでデプロイメント・オプションが示されます。アプリケーションには必ず固有の`「名前」`を選択してください。
  - 数分後に、選択した URL でアプリケーションが実行されます。

これで、コードをローカルおよびクラウド上で実行しました。

## 7. データベースの追加
{: #add_database}

次に、NoSQL データベースをこのアプリケーションに追加して、ローカルおよび Bluemix 上で実行できるようにアプリケーションをセットアップします。

1. ご使用のブラウザーで {{site.data.keyword.Bluemix_notm}} にログインします。`「ダッシュボード」`を参照します。`「名前」`列でアプリケーション名をクリックして、そのアプリケーションを選択します。
2. `「接続」`、`「新規に接続」`の順にクリックします。
2. `「データおよび分析」`セクションで、`「Cloudant NoSQL DB」`を選択して、サービスを`作成`します。
3. プロンプトが出されたら、`「再ステージ」`を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。この環境変数は、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合にのみアプリケーションで使用できます。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 8. データベースの使用
{: #use_database}
次に、このデータベースを指すようにローカル・コードを更新します。サービス用の資格情報をプロパティー・ファイルに保管します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は VCAP_SERVICES 環境変数から読み取られます。

1. Eclipse を開いて、ファイル src/main/resources/cloudant.properties を開きます。
  ```
  cloudant_url=
  ```
  {: pre}

2. ご使用のブラウザーで {{site.data.keyword.Bluemix_notm}} UI を開いて、「アプリ」->「接続」->「Cloudant」->「資格情報の表示」を選択します。

3. 資格情報から `url` のみをコピーして、`cloudant.properties` ファイルの `url` フィールドに貼り付け、変更を保存します。結果は次のようになります。
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. `「サーバー (Servers)」`ビューから、Eclipse で Tomcat サーバーを再始動します。

  http://localhost:8080/GetStartedTomcat/ でブラウザー・ビューを最新表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションはデータベースを共有しています。上の push コマンドの出力にリストされている URL で {{site.data.keyword.Bluemix_notm}} アプリケーションを表示します。いずれかのアプリケーションから追加した名前は、ブラウザーを最新表示すると両方に表示されます。

{{site.data.keyword.Bluemix_notm}} でアプリケーションが稼働中である必要がない場合、予期しない料金が発生しないように、忘れずに停止してください。
{: tip}  
