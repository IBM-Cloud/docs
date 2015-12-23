{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Cloud Foundry コマンド・ライン・インターフェースを使用したアプリのデプロイ
*最終更新日: 2015 年 11 月 11 日*

Cloud Foundry コマンド・ライン・インターフェースを使用して、アプリケーションおよびサービス・インスタンスのデプロイと変更が可能です。
{:shortdesc}

最初に、CF コマンド・ライン・インターフェースをインストールします。

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(新規タブまたはウィンドウで開きます)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry コマンド・ライン・インターフェースのダウンロード" /> </a>
</p>

**制限:** Cloud Foundry コマンド・ライン・インターフェースは、Cygwin ではサポートされていません。Cloud Foundry コマンド・ライン・インターフェースは Cygwin コマンド・ライン・ウィンドウ以外のコマンド・ライン・ウィンドウで使用してください。

cf コマンド・ライン・インターフェースのインストール後に始めることができます。

  1. スターター・コードをダウンロードします。
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(新規タブまたはウィンドウで開きます)"><img class="image" src="images/btn_starter-code.svg" alt="スターター・コードのダウンロード" /> </a>
  </p>
  
  {:download}
  2. パッケージを新規ディレクトリーに解凍し、開発環境をセットアップします。
  3. 新規ディレクトリーに移動します。
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
  4. {{site.data.keyword.Bluemix}} に接続します。
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  5. {{site.data.keyword.Bluemix_notm}} にログインします。
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  6. アプリを {{site.data.keyword.Bluemix_notm}} にデプロイします。cf push コマンドについて詳しくは、『[アプリケーションのアップロード](upload_app.html#upload_app__push)』を参照してください。
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  7. ご使用のブラウザーで以下の URL を入力して、アプリにアクセスします。
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
