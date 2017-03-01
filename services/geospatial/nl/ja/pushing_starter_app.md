---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#スターター・アプリケーションを {{site.data.keyword.Bluemix_short}} にプッシュする
{: #pushing_starter_app}


 
スターター・アプリケーションをデプロイし、{{site.data.keyword.geospatialshort_Geospatial}} サービスの使用方法を素早く習得します。
{:shortdesc}

1. まだインストールしていなければ、[cf コマンド・ライン・ツールをインストール](docs/starters/install_cli.html)します。
2. {{site.data.keyword.geospatialshort_Geospatial}} スターター・アプリケーションの[コードを取得](https://hub.jazz.net/project/streamscloud/geo-starter/overview)します。 
3. アプリケーション・ファイルが入っているディレクトリーを名前変更して、{{site.data.keyword.Bluemix_short}} でアプリケーションに付けた名前に一致するようにします。例えば、アプリケーションに myapp という名前を付けた場合、ディレクトリーを myapp に名前変更します。
4. コマンド・ラインで、名前変更したディレクトリーに移動します。
<pre><code>cd myapp</code></pre>
5. {{site.data.keyword.Bluemix_short}} に接続します。
<pre><code>cf api https://api.DomainName</code></pre>
6. {{site.data.keyword.Bluemix_short}} にログインし、プロンプトが出されたらターゲット組織を設定してアプリケーションをデプ
ロイします。
<pre><code>
cf login
cf push myapp
</code></pre>

##次に行うこと

* アプリケーションが正常に開始したことを検証するため、{{site.data.keyword.Bluemix_short}} ダッシュボードからアクセス可能なアプリケーション概要ページに移動します。
* アプリケーションを起動してブラウザーに表示します。アプリケーションの URL (または「経路」) は、アプリケーション概要ページにあります。サンプル・アプリケーションの Web ページには、
アプリケーション・コード中の REST API 呼び出しの状況についての情報、および {{site.data.keyword.geospatialshort_Geospatial}} が検出するイベントについての情報が表示されます。
