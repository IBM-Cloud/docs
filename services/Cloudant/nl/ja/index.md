---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloudant の概要
{: #getting-started-with-cloudant}
最終更新日: 2016 年 8 月 12 日
{: .last-updated}

{{site.data.keyword.cloudant}} は、データを JSON で保管する、文書の Database as a service (DBaaS) です。
これは、拡張容易性、高可用性、および耐久性を念頭に構築されています。
map-reduce、Cloudant 照会、フルテキスト索引付け、地理情報索引付けなどの多様な索引オプションを備えています。
複製機能により、データベース・クラスター、デスクトップ PC、モバイル・デバイス間で簡単にデータを同期できます。
{:shortdesc}

{{site.data.keyword.cloudant}} コンソールは、Bluemix ダッシュボードのサービス起動ページから起動できます。

サービスを使用するには、以下の手順に従ってください。
<ol>
<li>Bluemix ダッシュボードまたは CloudFoundry コマンド・ライン・インターフェースを使用して、サービス・インスタンスを作成します。
<p>ダッシュボードを使用してインスタンスを作成するには、以下の手順に従います。
<ol>
<li>Bluemix にログオンします。</li>
<li>ダッシュボード上で、「データ &amp; 分析」パネルの「<code>データの処理</code>」リンクをクリックします。</li>
<li>「<code>新規サービス</code>」ボタンをクリックします。</li>
<li>サービスのリストで、「{{site.data.keyword.cloudant}}」ボタンをクリックします。</li>
<li>{{site.data.keyword.cloudant}} 情報ページで、「<code>{{site.data.keyword.cloudant}} の選択</code>」ボタンをクリックします。</li>
<li>{{site.data.keyword.cloudant}} カタログ・ページで、必要なサービスの詳細を入力します。
続行する準備ができたら「<code>作成</code>」ボタンをクリックします。</li>
<li>Cloudant インスタンスが作成されると、そのインスタンス用のダッシュボードが表示されます。
「<code>サービス資格情報</code>」リンクをクリックして、インスタンスにアクセスするために必要なすべての詳細を確認します。</li>
</ol>
</p>
<p>CloudFoundry コマンド・ライン・インターフェースを使用してインスタンスを作成するには、以下の手順に従います。
<ol>
<li>システムに CloudFoundry <code>cf</code> ツールをインストールします。
これを行う方法については、「<a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix の CLI と開発ツール・ガイド</a>」に記載されています。</li>
<li>次のコマンドを使用して、新規サービス・インスタンスを作成します。<br/>
<pre><code>cf create-service</code></pre></li>
<li>使用可能なサービスのリストが表示されます。
1 つを選択し、そのサービスに固有のインスタンス名とプランを入力します。
インスタンスにはランダム名が提示されますが、必要に応じて別の名前に変更できます。</li>
<li>サービスを作成した後、次のように入力すると、作成したすべてのサービスのリストを入手できます。<br/>
<pre><code>cf services</code></pre></li>
<li>アプリケーションの中でサービスを使用する前に、
サービスをアプリケーションにバインドする必要があります。
次のコマンドを使用して、これを行います。<br/>
<pre><code>cf bind-service</code></pre>
結果のリストから、アプリケーションとサービスを 1 つずつ選択します。
<code>cf</code> コマンドにより、バインディング・アクションが成功すると通知を受け取ります。</li>
</ol>
</p>
</li>
<li><p>サービス・インスタンスを作成すると、以下のような JSON データが表示されます。これは Bluemix ダッシュボードで参照することができます。<br/>
<pre><code>{
"cloudantNoSQLDB": {
"name": "Cloudant-3s",
"label": "cloudantNoSQLDB",
"plan": "shared",
"credentials": {
"username": "someusername",
"password": "secret",
"host": "myhost-bluemix.cloudant.com",
"port": 443,
"url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>このデータは、サービスがバインドされた Bluemix アプリケーションの <code>VCAP_SERVICES</code> 環境変数にも追加されます。</p>
<p>サービス資格情報は、以下のフィールドを含む JSON オブジェクトに保管されます。
<ul>
<li><code>key</code>: サービスの名前 (cloudantNoSQLDB)</li>
<li><code>name</code>: ユーザーが提供した、サービス・インスタンスの名前</li>
<li><code>host</code>: サーバーのホスト名</li>
<li><code>port</code>: サービスが稼働しているポート番号。通常、443</li>
<li><code>username</code>: 認証用ユーザー名</li>
<li><code>password</code>: 認証用パスワード</li>
<li><code>url</code>: サービス・インスタンスの URL</li>
</ul></li>
<li><p>Bluemix アプリケーションで、<code>VCAP_SERVICES</code> 環境変数から資格情報を読み取ります。</p>
<p>Bluemix の外部で実行されるアプリケーション、または Bluemix 内の別の地理的領域で実行されるアプリケーションでは、Bluemix ダッシュボードから資格情報を取得してアプリケーションの構成に追加することができます。</p>
</li>
<li>データベースにアクセスするための基本的なメカニズムは、認証用のユーザー名とパスワードを使用して、特定のホストおよびポートに HTTPS で要求を送信することです。
次のような、さまざまなアプリケーション言語およびプラットフォームを使用して、要求を送信できます。
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C および Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
... その他にも多数あります。
詳しくは、<a href="https://cloudant.com/for-developers/">Cloudant Developer ホーム・ページ</a>および <a href="http://docs.cloudant.com/libraries.html">Client Libraries</a> のリストを参照してください。
</li>
<li>アプリケーションの準備ができたら、検証のために Bluemix 環境にデプロイすることができます。
アプリケーションをデプロイするには、次のコマンドを使用します。<br/>
<pre><code>cf push</code></pre></li>
<li>アプリケーションからサービス・インスタンスをアンバインドするには、次のコマンドを使用します。<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>サービス・インスタンスを削除するには、次のコマンドを使用します。<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

データベースに対する認証や要求の実行に関する詳細は、[API リファレンス](https://docs.cloudant.com/api.html)にあります。

# 関連リンク
{: #rellinks}

## チュートリアルおよびサンプル
{: #samples}

* [Cloudant のクライアント・ライブラリー](https://docs.cloudant.com/libraries.html)
* [Bluemix での Liberty と Cloudant の使用](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Cloudant のガイド](https://docs.cloudant.com/guides.html)

## API リファレンス
{: #api}

* [Cloudant の API リファレンス](https://docs.cloudant.com/api.html)

## 関連リンク
{: #general}

* [Cloudant の Web サイトおよびダッシュボード](https://cloudant.com/)
* [Cloudant のブログ](https://cloudant.com/blog)
