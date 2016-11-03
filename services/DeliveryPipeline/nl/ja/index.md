---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}} の概要 {: #delivery-pipeline}  

最終更新日: 2016 年 9 月 15 日
{: .last-updated}

ビルドおよび {{site.data.keyword.Bluemix}} へのデプロイメントを自動化する
には、IBM Continuous {{site.data.keyword.deliverypipeline}} for
{{site.data.keyword.Bluemix_notm}} を使用します。
{: shortdesc}

この情報は、{{site.data.keyword.deliverypipeline}} および
{{site.data.keyword.deliverypipeline}} Next の両方に適用されます。

{{site.data.keyword.deliverypipeline}} サ
ービスでは、複数のビルド・タイプから選択することができます。ビルド・スクリプトを指定すると、{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} がそれを実行するため、ビルド・システムをセットアップする必要はありません。その後、1 回のクリックで、1 つ以上の {{site.data.keyword.Bluemix_notm}} スペース、パブリックの Cloud Foundry サーバー、または IBM Containers for {{site.data.keyword.Bluemix_notm}} 上の Docker コンテナーに、アプリを自動的にデプロイできます。  

ビルド・ジョブは、Git のリポジトリーまたは Jazz ソース・コントロール管理 (SCM) のリポジトリーから取得したアプリのソース・コードをコンパイルしてパッケージ化します。このビルド・ジョブによって、WAR ファイルや IBM Containers 用の Docker コンテナーなど、デプロイ可能な成果物が生成されます。さらに、ビルド内で単体テストを自動的に実行できます。ソース・コードが変更されるたびに、ビルドがトリガーされます。

デプロイメント・ジョブは、ビルド・ジョブの出力を取り込み、それを IBM Containers または {{site.data.keyword.Bluemix_notm}} などの Cloud Foundry サーバーにデプロイします。  

1 つ以上の地域およびサービスにデプロイできます。例えば、開発成果物が IBM Containers を使用し、1 つの地域でテストされ、複数の地域の実働環境にデプロイされるように {{site.data.keyword.deliverypipeline}} サービスをセットアップすることができます。詳細については、『[Regions](../../overview/index.html#ov_intro__reg)』を参照してください。

パイプラインの作成には、パイプラインを既存のアプリケーションに追
加する、既存のアプリケーションなしでパイプラインを作成する、など複数の方法があります。
組織に {{site.data.keyword.deliverypipeline}} サービスがない
場合は、カタログに移動し、{{site.data.keyword.deliverypipeline}} または
{{site.data.keyword.deliverypipeline}} Next をクリックして、「作成 (Create)」をクリックします。

次の手順を完了して、既存のアプリケーションに
{{site.data.keyword.deliverypipeline}} をセットアップします。    

1. {{site.data.keyword.Bluemix_notm}} アプリ・ダッシュ
ボードにある「概要」タブの**「継続的なデリバ
リー」**で、コンテキストに応じて
**「Git リポジトリーおよびパイプラインの追加 (Add Git
Repo And  Pipeline」** または **「Git の追加」**をクリックして、アプリ
用に Git でホストされたプロジェクトを作成します。
1. **「リポジトリーにスターター・アプリ・パッケージを取り込み、Build & Deploy パイプラインを使用可能にします」
**チェック・ボックスが選択されていることを確認して、
**「続行」**をクリックします。続行するには、E メール・アドレス
を確認する必要がある場合があります。  
1. Git リポジトリーが作成された後、**「閉じる」**をクリックします。
「Git の追加」ボタンは「コードの編集」ボタンと Git URL で置き換えられます。  
1. パイプラインを開くには、**「コードの編集」
**をクリックしてから**「ビルドとデプロイ (Build &
Deploy)」**をクリックします。最初にパイプラインを実行するには、Git リポジトリーに変更をプッシュします。

このサービスを追加した後、ビルド、テスト、およびデプロイメントの各ジョブが含まれているステージを構成して実行することで、{{site.data.keyword.Bluemix_notm}} スペース内にマルチステージ・デプロイメント・パイプラインを作成できます。{{site.data.keyword.deliverypipeline}} ダッシュボードで、{{site.data.keyword.jazzhub_short}} プロジェクトとそのプロジェクトの状態が確認できます。ビルド、デプロイ済みのアプリ、および最新のデプロイメントの状況を確認したり、最新のログやデプロイメントの詳細を表示したりできます。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">関連リンク</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">関連リンク</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(新しいタブまたはウィンドウで開きます)">{{site.data.keyword.Bluemix_notm}} 前提条件</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(新しいタブまたはウィンドウで開きます)">IBM Bluemix Garage Method: Delivery pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">チュートリアルおよびサンプル</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(新しいタブまたはウィンドウで開きます)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
