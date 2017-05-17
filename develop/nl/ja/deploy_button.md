---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンの作成 {: #deploy-button} 

「{{site.data.keyword.Bluemix}} にデプロイ」ボタンを使用すると Git から入手したパブリック・アプリを効率的に共有することができ、それによって、他のユーザーがそのコードを試し、IBM {{site.data.keyword.Bluemix_notm}} にデプロイできるようになります。このボタンは最小限の構成で済み、マークアップをサポートする場所ならどこにでも挿入できます。誰かがこのボタンをクリックすると、オリジナルのアプリには影響しないように、新しい Git リポジトリー内にコードの複製コピーが作成されます。
{: shortdesc} 

**ヒント:** 企業ブランディングが重要な場合、ボタンを挿入する代わりに、[「{{site.data.keyword.Bluemix_notm}} にデプロイ」iFrame フローを埋め込む](/docs/develop/deploy_button_embed.html)ことができます。Git から入手したパブリック・アプリの複製コピーを作成したユーザーは、bluemix.net Web サイトにリダイレクトされる代わりに、コンテンツにとどまります。 

**注**: ツールチェーン・フィーチャーが使用可能になりました。「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンをクリックすれば誰でも、バナーの該当リンクをクリックして、ツールチェーンを使用したアプリケーションのデプロイを試すことができます。

誰かがボタンをクリックすると、以下のアクションが起こります。 

1. クリックしたユーザーがアクティブな {{site.data.keyword.Bluemix_notm}} アカウントを持っていない場合、トライアル・アカウントが作成される必要があります。 

2. ユーザーは、地域、組織、スペース、およびアプリ名を選択できます。推奨アプリ名は、前のアプリ名、ユーザーのユーザー名、および時刻で構成されます。 

3. オリジナルのパブリック Git リポジトリーのマスター・ブランチが、新しい Git リポジトリーを使用した新しいプライベートの {{site.data.keyword.jazzhub_title}} プロジェクトに複製されます。 

4. アプリにビルド・ファイルが必要な場合、そのビルド・ファイルは自動的に検出されて、アプリがビルドされます。 

5. ビルドおよびデプロイメントのプロセス用にパイプラインが構成されている場合、アプリをデプロイするために `pipeline.yml` ファイルが使用されます。

6. アプリにコンテナーが必要な場合、**IBM Containers** サービスを定義する `pipeline.yml` およびイメージを定義する Dockerfile が、{{site.data.keyword.Bluemix_notm}} コンテナー内にアプリをデプロイするために使用されます。 

7. アプリがユーザーの {{site.data.keyword.Bluemix_notm}} 組織にデプロイされます。 

##このボタンの例 {: #button-examples} 

パブリック {{site.data.keyword.jazzhub_short}} リポジトリーのアプリ・ボタンの例を以下に示します。

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/deploy_buttonx2.png" alt="Bluemix にデプロイ" /></a>
</p> 

パブリック GitHub リポジトリーのアプリ・ボタンの例を以下に示します。 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/deploy_buttonx2.png" alt="Bluemix にデプロイ" /></a>
</p> 

{{site.data.keyword.Bluemix_notm}} コンテナーにデプロイされたアプリのボタンの例を以下に示します。 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/deploy_buttonx2.png" alt="Bluemix にデプロイ" /></a>
</p> 

##ボタンの作成 {: #create-button}

「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンを作成するには、以下のようにします。 

<ol>
<li> 以下のスニペット・テンプレートのいずれかをコピーして変更し、パブリック Git リポジトリーを含めます。
<p></p>
<p>
<strong>ヒント</strong>: Git URL にブランチ・パラメーターを追加することで、使用するブランチを指定できます。ブランチを指定しない場合、デフォルトでマスター・ブランチが使用されます。
</p>
<ul>
<li>HTML:
<p>
デフォルト・マスター・ブランチ:
</p>
<pre class="codeblock">
<code class="hljs">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</code>
</pre>
<p>
指定された Git ブランチ:
</p>
<pre class="codeblock">
<code class="hljs">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</code>
</pre>
</li>
<li>Markdown:
<p>
デフォルト・マスター・ブランチ:
</p>
<pre class="codeblock">
<code class="hljs">
[&excl;[Deploy to Bluemix]&lpar;https://bluemix.net/deploy/button.png&rpar;]&lpar;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&rpar;
</code>
</pre>
<p>指定された Git ブランチ:
</p>
<pre class="codeblock">
<code class="hljs"
[&excl;[Deploy to Bluemix]&lpar;https://bluemix.net/deploy/button.png&rpar;]&lpar;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&rpar;
</code>
</pre>
</li>
</ul>
</li>
<li>このスニペットを、ブログ、記事、wiki、README ファイルをはじめ、アプリをプロモートしたい場所ならどこにでも挿入します。
</li>
</ol>

##このボタンのスニペットの考慮事項 {: #button-snippet}

「Bluemix にデプロイ」ボタンのスニペットをカスタマイズする際は、以下の考慮事項を検討してください。 

* テンプレートは両方とも、外部にある PNG フォーマットのボタン・イメージへのデフォルト・パスを使用し、言語は英語になっています。 

    * ボタンのイメージに PNG ではなく SVG イメージを使用したい場合は、SVG バージョンを使用できます。スニペット内で使用する外部ボタン・イメージへのパスを `https://bluemix.net/deploy/button.svg` に変更できます。
	
	* より大きいボタンのイメージを使用したい場合は、元のイメージの 2 倍のサイズの PNG イメージを使用できます。スニペット内で使用する外部ボタン・イメージへのパスを `https://bluemix.net/deploy/button_x2.png` に変更できます。 
	
	* イメージをローカルに保管したい場合は、イメージをダウンロードし、ご使用の Git リポジトリーに保管できます。イメージの相対ロケーションを使用するようにパスを調整してください。 
	
	* 翻訳版のボタンを使用したい場合は、そのボタンをリモートで参照するか、[ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button){:new_window} からダウンロードすることができます。 
	
##このボタンのリポジトリーの考慮事項 {: #button-repo} 

「Bluemix にデプロイ」ボタンで使用するプロジェクト・リポジトリーについての以下の考慮事項を検討してください。 

<ul>
<li><code>manifest.yml</code> がリポジトリー内に存在する必要はありません。ただし、アプリが他のサービスの実行を必要とする場合は、それらのサービスを宣言しているマニフェスト・ファイルを用意する必要があります。  

マニフェスト・ファイルによって、以下を指定できます。 
    <ul>
    <li>固有のアプリ名</li>  
    <li>宣言されたサービス: アプリのデプロイ前にセットアップされていることが求められる必須サービスまたはオプション・サービス (データ・キャッシュ・サービスなど) を作成または検索するマニフェスト拡張。適格な {{site.data.keyword.Bluemix_notm}} サービス、ラベル、およびプランのリストは、<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(新しいタブまたはウィンドウで開きます)">CF コマンド・ライン・インターフェース<img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> を使用して <code>cf marketplace</code> コマンドを実行するか、<a class="xref" href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-_-dWdevcenter-_-devops-services-_-lp#/store" target="_blank" title="(新しいタブまたはウィンドウで開きます)"> {{site.data.keyword.Bluemix_notm}} カタログ<img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> を参照すれば、見つけることができます。
    
        
    <strong>注:</strong> 宣言されたサービスは、標準 Cloud Foundry マニフェスト・フォーマットに対する IBM 拡張です。
この拡張は、フィーチャーの発展と改善に伴い、今後のリリースで改訂
される可能性があります。
	
	<a class="xref" href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><code>manifest.yml</code> ファイルの作成方法を参照してください <img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> 。  
<pre class="codeblock">
	---
    #Template manifest.yml

  declared-services:
    &lt;`arbitrary_service_instance_name`&gt;:  # [required] 
      label: &lt;`actual_service_name`&gt; # [required] The actual service name from market place 
      plan: Shared # [optional] If provided, used to fetch the declared service. Otherwise, defaults to 'Free' or 'free'.
  applications:
  - services
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #Example manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB:
        label: cloudantNoSQLDB
        plan: Shared
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> アプリケーションのデプロイ前にビルドが必要な場合は、リポジトリーにビルド・ファイルを含めてください。リポジトリーのルート・ディレクトリーにビルド・スクリプト・ファイルが検出されると、デプロイメントの前にコードの自動ビルドが起動されます。
	
	サポートされるビルダー:<ul>
		<li> <a class="xref" href="http://ant.apache.org/manual/using.html" target="_blank" title="(新しいタブまたはウィンドウで開きます)">Ant:<img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> /<code>build.xml</code>。<code>./output/</code> フォルダーへの出力をビルドします。</li>
		<li> <a class="xref" href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank" title="(新しいタブまたはウィンドウで開きます)">Gradle:<img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> <code>/build.gradle</code>。<code>. </code> フォルダーへの出力をビルドします。</li>
		<li> <a class="xref" href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank" title="(新しいタブまたはウィンドウで開きます)">Grunt:<img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> <code>/Gruntfile.js</code>。<code>. </code> フォルダーへの出力をビルドします。</li>
		<li> <a class="xref" href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank" title="(新しいタブまたはウィンドウで開きます)">Maven:<img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a> <code>/pom.xml</code>。<code>./target/</code> フォルダーへの出力をビルドします。</li>
	   </ul>
	</li>	
	<li>プロジェクト用のパイプラインを構成するには、<code>.bluemix</code> ディレクトリーに <code>pipeline.yml</code> ファイルを含めます。<code>pipeline.yml</code> ファイルは手動で作成するか、既存の DevOps Services プロジェクトから生成することができます。pipeline.yml ファイルを {{site.data.keyword.jazzhub_short}} プロジェクトから作成して、それをリポジトリーに追加するには、以下の手順を実行してください。
<ol>
<li>ブラウザーで DevOps Services プロジェクトを開き、「<b>ビルドとデプロイ</b>」をクリックします。</li>
<li>ビルドとデプロイメントのジョブでパイプラインを構成します。</li>
<li>ブラウザーで、<code>/yaml</code> をプロジェクト・パイプライン URL に追加し、Enter キーを押します。
<br>例: <code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>作成された <code>pipeline.yml</code> ファイルを保存します。</li>
<li>プロジェクトのルート・ディレクトリー内に <code>.bluemix</code> ディレクトリーを作成します。</li>
<li>この <code>pipeline.yml</code> ファイルを <code>.bluemix</code> リポジトリーにアップロードします。</li>
</ol> </li>
	<li><strong>IBM Containers</strong> を使用してアプリをコンテナーにデプロイするには、リポジトリーのルート・ディレクトリーに Dockerfile を、<code>.bluemix</code> ディレクトリーに <code>pipeline.yml</code> ファイルを含める必要があります。
	<ul>
	    <li>Dockerfile は、アプリのビルド・スクリプトのようなものとして機能します。リポジトリーに Dockerfile が検出されると、アプリは、コンテナーにデプロイされる前に自動的にイメージにビルドされます。アプリがイメージにビルドされる前にアプリ自体をビルドする必要がある場合は、前述のとおり、Dockerfile とともにアプリのビルド・スクリプトを含めてください。</li>
	    <li> Dockerfile の作成について詳しくは、<a class="xref" href="https://docs.docker.com/reference/builder/" target="_blank" title="(新しいタブまたはウィンドウで開きます)">Docker 資料を参照してください <img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a>。</li>
	    <li><code>pipeline.yml</code> ファイルは手動で作成するか、既存の DevOps Services プロジェクトから生成することができます。コンテナーに固有の <code>pipeline.yml</code> を手動で作成するには、<a class="xref" href="https://github.com/Puquios/" target="_blank" title="(新しいタブまたはウィンドウで開きます)">GitHub にある例を参照してください <img class="image" src="../icons/launch-glyph.svg" alt="「外部リンク」アイコン"/></a>。</li>
        </ul>

 </li>
 </ul>
</ul>

トラブルシューティングのヘルプについては、[「Bluemix にデプロイ」ボタンでアプリがデプロイされない](/docs/troubleshoot/ts_apps.html#ts_deploybutton){:new_window}を参照してください。	
