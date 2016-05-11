---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
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

# コマンド・ライン・インターフェースを使用したアプリのデプロイ
*最終更新日: 2016 年 2 月 24 日*

コマンド・ライン・インターフェースを使用して、アプリケーションおよびサービス・インスタンスのデプロイと変更が可能です。
{:shortdesc}

最初に、{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェースと Cloud Foundry コマンド・ライン・インターフェースをインストールします。

<p>
<a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェースのダウンロード" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry コマンド・ライン・インターフェースのダウンロード" /> </a>
</p>

**制約事項:** コマンド・ライン・ツールは Cygwin でサポートされません。このツールは Cygwin コマンド・ライン・ウィンドウ以外のコマンド・ライン・ウィンドウで使用してください。{:prereq}

コマンド・ライン・インターフェースをインストールしたら、以下の手順を開始できます。

  1. {: download} スターター・コードをダウンロードします。 
      
    <a class="xref" href="http://bluemix.net" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/btn_starter-code.svg" alt="スターター・コードのダウンロード" /> </a>
  
  2. パッケージを新規ディレクトリーに解凍し、開発環境をセットアップします。
  3. 新規ディレクトリーに移動します。
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
   4.  適切なアプリ・コードを変更します。アプリを {{site.data.keyword.Bluemix}} にデプロイする前に、それがローカルで稼働するか確認することをお勧めします。<br><br>注意が必要なファイルは、`manifest.yml` ファイルです。{{site.data.keyword.Bluemix}} にアプリをデプロイする際、このファイルを使用してアプリケーションの URL、メモリー割り振り、インスタンス数、その他の重要なパラメーターを判別します。Cloud Foundry の資料で[マニフェスト・ファイルの詳細](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window}を参照してください。
  
  5. {{site.data.keyword.Bluemix}} に接続します。
  
  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  6. {{site.data.keyword.Bluemix_notm}} にログインします。
 
  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></pre>
  
  7. アプリを {{site.data.keyword.Bluemix_notm}} にデプロイします。cf push コマンドについて詳しくは、『[アプリケーションのアップロード](./upload_app.html)』を参照してください。
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  8. ご使用のブラウザーで以下の URL を入力して、アプリにアクセスします。
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
