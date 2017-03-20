---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# アプリケーションのアップロード

{{site.data.keyword.Bluemix}} にログインすると、cf push コマンドを使用してアプリケーションをアップロードすることができます。
{:shortdesc}

開始前に、以下のことを行ってください。
  1. {{site.data.keyword.Bluemix}} と Cloud Foundry コマンド・ライン・インターフェースをインストールします。 

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェースのダウンロード" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry コマンド・ライン・インターフェースのダウンロード" /> </a>

  2. {{site.data.keyword.Bluemix}} に接続します。

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>

  3. {{site.data.keyword.Bluemix_notm}} にログインします。

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>

**cf push** コマンドが実行されると、**cf** コマンド・ライン・インターフェースは、ビルドパックを使用してアプリケーションのビルドと実行を行う {{site.data.keyword.Bluemix_notm}} 環境に対して作業ディレクトリーを提供します。

  1. アプリケーション・ディレクトリーから、**cf push** コマンドをアプリケーション名と共に入力します。アプリ名は、{{site.data.keyword.Bluemix_notm}} 環境内で固有でなければなりません。

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</pre>

  {{site.data.keyword.Bluemix_notm}} には、組み込みのビルドパックが含まれています。場合によっては、組み込みビルドパックの場合でも、アプリケーションの始動に使用するコマンドを指定する際に、-c オプションも使用する必要があります。例えば、Node.js アプリケーションをプッシュするには -c オプションを使用する必要があります。

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</pre>

  さらに、Node.js アプリケーションには、有効な package.json ファイルが含まれていなければなりません。

  その他のすべての外部ビルドパックは、-b オプションを使用してプッシュする必要があります。例えば次のようにします。

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</pre>

  **ヒント:** **cf push** コマンドを使用すると、**cf** コマンド・ライン・インターフェースはすべてのファイルおよびディレクトリーを現行ディレクトリーから Bluemix にコピーします。アプリケーション・ディレクトリーには必要なファイルだけを保管しておくようにしてください。

  cf push コマンドにより、アプリケーションは {{site.data.keyword.Bluemix_notm}} にアップロードされ、デプロイされます。cf push について詳しくは、『[cf コマンド](/docs/cli/reference/cfcommands/index.html)』を参照してください。ビルドパックについては、『[コミュニティー・ビルドパックの使用](/docs/cfapps/byob.html)』を参照してください。

  2. アプリケーションを変更した場合、cf push コマンドを再度入力することで、それらの変更をアップロードすることができます。cf コマンド・ライン・インターフェースは、アプリケーションの実行中のインスタンスを新規コードで更新するようプロンプトを出されたときに、ユーザーの過去のオプションとユーザーの応答を使用します。

**ヒント:** また、DevOps Services からもアプリケーションのアップロードとデプロイを行うことができます。[Developing a {{site.data.keyword.Bluemix_notm}} application in Node.js with the Web IDE ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://hub.jazz.net/tutorials/devopsweb/){: new_window} を参照してください。
