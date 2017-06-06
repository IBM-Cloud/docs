---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# アプリケーションのアップロード

{{site.data.keyword.Bluemix}} にログインすると、`bluemix app push` コマンドを使用してアプリケーションをアップロードすることができます。
{:shortdesc}

開始前に、以下のことを行ってください。
  1. {{site.data.keyword.Bluemix}} コマンド・ライン・インターフェースをインストールします。

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(新規タブまたはウィンドウで開きます)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェースのダウンロード" /> </a>

  2. {{site.data.keyword.Bluemix}} に接続します。

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. {{site.data.keyword.Bluemix_notm}} にログインします。

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

**bluemix app push** コマンドを実行すると、コマンド・ライン・インターフェースは、ビルドパックを使用してアプリケーションをビルドおよび実行する {{site.data.keyword.Bluemix_notm}} 環境に対して作業ディレクトリーを提供します。

  1. アプリケーション・ディレクトリーから、**bluemix app push** コマンドをアプリケーション名とともに入力します。アプリ名は、{{site.data.keyword.Bluemix_notm}} 環境内で固有でなければなりません。

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} には、組み込みのビルドパックが含まれています。場合によっては、組み込みビルドパックの場合でも、アプリケーションの始動に使用するコマンドを指定する際に、-c オプションも使用する必要があります。例えば、Node.js アプリケーションをプッシュするには -c オプションを使用する必要があります。

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  さらに、Node.js アプリケーションには、有効な package.json ファイルが含まれていなければなりません。

  その他のすべての外部ビルドパックは、-b オプションを使用してプッシュする必要があります。例えば次のようにします。

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **ヒント:** **bluemix app push** コマンドを使用すると、このコマンドは、すべてのファイルとディレクトリーを現行ディレクトリーから Bluemix にコピーします。アプリケーション・ディレクトリーには必要なファイルだけを保管しておくようにしてください。


  2. アプリケーションを変更した場合、`bluemix app push` コマンドを再度入力することで、それらの変更をアップロードすることができます。このコマンドでは、ユーザーの前回のオプションとプロンプトに対する応答を使用して、アプリケーションの実行中のインスタンスを新規コードで更新します。

{{site.data.keyword.Bluemix}} CLI では、cf cli はインストール済み環境にバンドルされていました。`bluemix app push` コマンドは実際には、`cf push` を呼び出して、アプリケーションを {{site.data.keyword.Bluemix_notm}} にアップロードしてデプロイします。cf push について詳しくは、『[cf コマンド](/docs/cli/reference/cfcommands/index.html)』を参照してください。ビルドパックについては、『[コミュニティー・ビルドパックの使用](/docs/cfapps/byob.html)』を参照してください。
