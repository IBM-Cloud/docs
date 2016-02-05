{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンの作成{: #deploy-button} 

*最終更新日: 2016 年 1 月 19 日* 

「{{site.data.keyword.Bluemix}} にデプロイ」ボタンを使用すると Git から入手したパブリック・アプリを効率的に共有することができ、それによって、他のユーザーがそのコードを試し、IBM {{site.data.keyword.Bluemix_notm}} にデプロイできるようになります。このボタンは最小限の構成で済み、マークアップをサポートする場所ならどこにでも挿入できます。誰かがこのボタンをクリックすると、オリジナルのアプリには影響しないように、新しい Git リポジトリー内にコードの複製コピーが作成されます。
{: shortdesc} 

**ヒント:** 企業ブランディングが重要な場合、ボタンを挿入する代わりに、[「{{site.data.keyword.Bluemix_notm}} にデプロイ」iFrame フローを埋め込む](../develop/deploy_button_embed.html)ことができます。Git から入手したパブリック・アプリの複製コピーを作成したユーザーは、bluemix.net Web サイトにリダイレクトされる代わりに、コンテンツにとどまります。 

誰かがボタンをクリックすると、以下のアクションが起こります。 

1. クリックしたユーザーがアクティブな {{site.data.keyword.Bluemix}} アカウントを持っていない場合、トライアル・アカウントが作成される必要があります。 

2. ユーザーは、地域、組織、スペース、およびアプリ名を選択できます。推奨アプリ名は、前のアプリ名、ユーザーのユーザー名、および時刻で構成されます。 

3. オリジナルのパブリック Git リポジトリーのマスター・ブランチが、新しい Git リポジトリーを使用した新しいプライベートの {{site.data.keyword.jazzhub_title}} プロジェクトに複製されます。 

4. アプリにビルド・ファイルが必要な場合、そのビルド・ファイルは自動的に検出されて、アプリがビルドされます。 

5. アプリにコンテナーが必要な場合、**IBM Container Service** を定義する `pipeline.yml` およびイメージを定義する Dockerfile が、{{site.data.keyword.Bluemix_notm}} コンテナー内にアプリをデプロイするために使用されます。 

6. アプリがユーザーの {{site.data.keyword.Bluemix_notm}} 組織にデプロイされます。 

##このボタンの例{: #button-examples} 

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

##ボタンの作成{: #create-button}

「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンを作成するには、以下のようにします。 

<ol>
<li> 以下のスニペット・テンプレートのいずれかをコピーして変更し、パブリック Git リポジトリーを含めます。
<p></p>
<p>
<strong>ヒント</strong>: DevOps サービス・プロジェクト用のビルド入力を指定する場合は、Git URL にブランチ・パラメーターを追加します。ブランチ・パラメーターを追加すると、元のパブリック Git リポジトリーが、そのすべてのブランチを含め、新しい Git リポジトリーを使用する新しいプライベート DevOps サービス・プロジェクトに複製されます。指定された Git ブランチは、ビルド・ジョブの入力として設定されます。ブランチを指定しないと、ビルド・ジョブの入力はデフォルトでマスター・ブランチに設定されます。
</p>
<ul>
<li>HTML:
<p>
デフォルト・マスター・ブランチ:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
指定された Git ブランチ:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown:
<p>
デフォルト・マスター・ブランチ:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&#41;
</pre>
<p>指定された Git ブランチ:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&#41;
</pre>
</li>
</ul>
</li>
<li>このスニペットを、ブログ、記事、wiki、README ファイルをはじめ、アプリをプロモートしたい場所ならどこにでも挿入します。
</li>
</ol>

##このボタンのスニペットの考慮事項{: #button-snippet}

「Bluemix にデプロイ」ボタンのスニペットをカスタマイズする際は、以下の考慮事項を検討してください。 

* テンプレートは両方とも、外部にある PNG フォーマットのボタン・イメージへのデフォルト・パスを使用し、言語は英語になっています。 

    * ボタンのイメージに PNG ではなく SVG イメージを使用したい場合は、SVG バージョンを使用できます。スニペット内で使用する外部ボタン・イメージへのパスを `https://bluemix.net/deploy/button.svg` に変更できます。
	
	* より大きいボタンのイメージを使用したい場合は、元のイメージの 2 倍のサイズの PNG イメージを使用できます。スニペット内で使用する外部ボタン・イメージへのパスを `https://bluemix.net/deploy/button_x2.png` に変更できます。 
	
	* イメージをローカルに保管したい場合は、イメージをダウンロードし、ご使用の Git リポジトリーに保管できます。イメージの相対ロケーションを使用するようにパスを調整してください。 
	
	* 翻訳版のボタンを使用したい場合は、そのボタンをリモートで参照するか、[ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button) からダウンロードすることができます。 
	
##このボタンのリポジトリーの考慮事項{: #button-repo} 

「Bluemix にデプロイ」ボタンで使用するプロジェクト・リポジトリーについての以下の考慮事項を検討してください。 

<ul>
<li><code>manifest.yml</code> がリポジトリー内に存在する必要はありません。ただし、アプリが他のサービスの実行を必要とする場合は、それらのサービスを宣言しているマニフェスト・ファイルを用意する必要があります。  

マニフェスト・ファイルによって、以下を指定できます。 
    <ul>
    <li>固有のアプリ名</li>  
    <li>宣言されたサービス: アプリのデプロイ前にセットアップされていることが求められる必須サービスまたはオプション・サービス (データ・キャッシュ・サービスなど) を作成または検索するマニフェスト拡張。適格な {{site.data.keyword.Bluemix_notm}} サービス、ラベル、およびプランのリストは、<a href="https://github.com/cloudfoundry/cli/releases">CF コマンド・ライン・インターフェース</a>を使用して <code>cf marketplace</code> コマンドを実行するか、<a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store">{{site.data.keyword.Bluemix_notm}} カタログ</a>を参照すれば、見つけることができます。
    
    <strong>注:</strong> 宣言されたサービスは、標準 Cloud Foundry マニフェスト・フォーマットに対する IBM 拡張です。この拡張は、フィーチャーの発展と改善に伴い、今後のリリースで改訂される可能性があります。
	
	<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank"><code>manifest.yml</code> ファイルを作成する方法を学習してください。</a>  
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
	<li> アプリがデプロイされる前にリポジトリーが作成されている必要がある場合、デプロイメントの前にリポジトリー内でコードの自動ビルドがトリガーされます。自動ビルドは、リポジトリーのルート・ディレクトリー内でビルド・スクリプト・ファイルが検出された場合に起こります。
	
	サポートされるビルダー: 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant:</a> /<code>build.xml</code> (<code>./output/</code> フォルダーへの出力をビルドする)</li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle:</a> <code>/build.gradle</code> (<code>. </code> フォルダーへの出力をビルドする)</li>
		<li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt:</a> <code>/Gruntfile.js</code> (<code>. </code> フォルダーへの出力をビルドする)</li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven:</a> <code>/pom.xml</code> (<code>./target/</code> フォルダーへの出力をビルドする)</li>
	   </ul>
	</li>	
	<li><stong>IBM Container Service</strong> を使用してアプリをコンテナーにデプロイする場合、リポジトリーのルート・ディレクトリーに Dockerfile を含め、<code>.bluemix</code> ディレクトリーに <code>pipeline.yml</code> ファイルを含める必要があります。
	<ul>
	    <li> Dockerfile の作成について詳しくは、Docker 資料を参照してください。</li>
	    <li><code>pipeline.yml</code> ファイルは手動で作成するか、既存の DevOps Services プロジェクトから生成することができます。<code>pipeline.yml</code> を手動で作成するには、<a href="https://github.com/Puquios/" target="_blank">GitHub にある例を参照してください</a>。pipeline.yml ファイルを {{site.data.keyword.jazzhub_short}} プロジェクトから作成して、それをリポジトリーに追加するには、以下の手順を実行してください。
<ol>
<li>ブラウザーで DevOps Services プロジェクトを開き、「<b>ビルドとデプロイ</b>」をクリックします。</li>
<li>「<b>IBM Container Service</b>」のビルドとデプロイメントのジョブを使用してパイプラインを構成します。</li>
<li>ブラウザーで、<code>/yaml</code> をプロジェクト・パイプライン URL に追加し、Enter キーを押します。
<br>例: <code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>作成された <code>pipeline.yml</code> ファイルを保存します。</li>
<li>プロジェクトのルート・ディレクトリー内に <code>.bluemix</code> ディレクトリーを作成します。</li>
<li>この <code>pipeline.yml</code> ファイルを <code>.bluemix</code> リポジトリーにアップロードします。</li>
</ol> </li>
        </ul>

 </li>
 </ul>
</ul>

トラブルシューティングのヘルプについては、[「Bluemix にデプロイ」ボタンでアプリがデプロイされない](../troubleshoot/managingapps.html#deploytobluemixbuttondoesntdeployanapp){: new_window}を参照してください。	

