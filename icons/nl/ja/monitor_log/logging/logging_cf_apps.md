---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix での Cloud Foundry アプリのロギング
{: #logging_bluemix_cf_apps}

{{site.data.keyword.Bluemix}} では、ログの表示、フィルター操作、および分析を、{{site.data.keyword.Bluemix}} ダッシュボード、Kibana、およびコマンド・ライン・インターフェースを介して行うことができます。それに加えて、ログ・レコードを外部ログ管理ツールにストリーミングすることもできます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 上の Cloud Foundry など、クラウド Platform as a Service (PaaS) でアプリを実行する場合、ログにアクセスするためにアプリの実行場所であるインフラストラクチャーに入る際に SSH または FTP を使用できません。プラットフォームはクラウド・プロバイダーによって制御されています。{{site.data.keyword.Bluemix_notm}} で実行している Cloud Foundry アプリは、Loggerator コンポーネントを使用して、Cloud Foundry インフラストラクチャー内部からログ・レコードを転送します。Loggregator は、STDOUT データと STDERR データを自動的に選出します。{{site.data.keyword.Bluemix}} ダッシュボード、Kibana、およびコマンド・ライン・インターフェースを介して、これらのログの視覚化および分析を行うことができます。

以下の図は、{{site.data.keyword.Bluemix_notm}} での Cloud Foundry アプリの概要図を示します。

![CF アプリ用のコンポーネント概要図](images/logging_cf_apps_ov.jpg)
 
Cloud Foundry アプリのロギングは、Cloud Foundry インフラストラクチャーを使用して {{site.data.keyword.Bluemix_notm}} 上でアプリを実行すると自動的に有効になります。Cloud Foundry ランタイム・ログを表示するには、ログを STDOUT および STDERR に書き込む必要があります。詳しくは、『[CF アプリを介したランタイム・アプリケーションのロギング](cfapps/logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app)』を参照してください。

Cloud Foundry アプリケーションのログを分析するための方法には以下のものがあり、任意の方法を選択できます。

* {{site.data.keyword.Bluemix_notm}} でログを分析して、アプリケーションの最新アクティビティーを表示します。
    
    {{site.data.keyword.Bluemix}} では、Cloud Foundry アプリケーションごとにある**「ログ」**タブを使用して、ログの表示、フィルター操作、および分析を行うことができます。詳しくは、『[Bluemix ダッシュボードからの CF アプリ・ログの分析](logging_view_dashboard.html#analyzing_logs_bmx_ui)』を参照してください。
    
* Kibana でログを分析して、高機能な分析タスクを実行します。
    
    {{site.data.keyword.Bluemix}} では、分析および視覚化のためのオープン・ソース・プラットフォームである Kibana を使用して、さまざまなグラフ (図表や表など) でデータのモニター、検索、分析、および視覚化を行うことができます。詳しくは、『[Kibana でのログの分析](logging_view_kibana3.html#analyzing_logs_Kibana)』を参照してください。

* CLI を介してログを分析して、コマンドを使用してログをプログラマチックに管理します。
    
    {{site.data.keyword.Bluemix}} では、**cf logs** コマンドを使用することによって、ログの表示、フィルター操作、および分析をコマンド・ライン・インターフェースを介して行うことができます。詳しくは、『[コマンド・ライン・インターフェースからの Cloud Foundry アプリ・ログの分析](logging_view_cli.html#analyzing_logs_cli)』を参照してください。

{{site.data.keyword.Bluemix_notm}} は、限られた量のログ情報を保持します。情報がログに記録されると、古い情報が新しい情報に置き換えられます。組織または業界の方針に準拠する必要があり、その方針では監査またはその他の目的のためにすべてのログ情報または一部のログ情報を保持しなければならない場合、外部ログ・ホスト (例えば、サード・パーティーのログ管理サービスまたはその他のホスト) にログをストリーミングできます。詳しくは、『[外部ログ・ホストの構成](logging_view_external.html#viewing_logs_external)』を参照してください。



