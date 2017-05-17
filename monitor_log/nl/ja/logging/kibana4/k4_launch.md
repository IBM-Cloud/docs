---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana ダッシュボードへのナビゲート
{: #k4_launch}

Kibana は、{{site.data.keyword.Bluemix}} UI から、または Web ブラウザーから直接、起動できます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} から Kibana を起動して、Kibana を起動したリソースに応じてデータを表示し、分析します。例えば、Kibana で特定の CF アプリのログをその特定のアプリに応じて起動することも、Kibana で特定の Docker コンテナーのログをその特定のコンテナーに応じて起動することもできます。 
    
提供される {{site.data.keyword.Bluemix_notm}} スペース内でサービスから集計されたログ・データを表示する場合は、直接ブラウザー・リンクから Kibana を起動します。ダッシュボードに表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix_notm}} 組織内のスペースのログ項目が取り出されます。Kibana に表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix_notm}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。 

Kibana について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。
    

##  Bluemix ダッシュボードから Kibana ダッシュボードへのナビゲート
{: #launch_Kibana_from_bluemix}

Kibana で表示されるデータをフィルタリングするために使用される照会によって、Kibana を起動した {{site.data.keyword.Bluemix_notm}} CF アプリまたはコンテナーのログ項目を取得します。 

Cloud Foundry アプリケーションまたは Docker コンテナーのログを Kibana で表示するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインし、{{site.data.keyword.Bluemix_notm}} ダッシュボードでアプリ名またはコンテナーをクリックします。 
    
2. {{site.data.keyword.Bluemix_notm}} UI でログ・タブを開きます。

    * CF アプリの場合、ナビゲーション・バーの**「ログ」**をクリックします。 
    * コンテナーの場合、ナビゲーション・バーの**「モニターおよびログ (Monitoring and logs)」**を選択してから、**「ロギング (Logging)」**タブをクリックします。 
    
    「ログ」タブが開きます。 
    
3. **「拡張ビュー」**をクリックします。**「Kibana 4」**ダッシュボードが開きます。

    デフォルトでは、**「Discover」**ページは、デフォルトの索引パターンが選択され、時間フィルターが過去 30 秒に設定された状態でロードされます。検索照会は、CF アプリまたは Docker コンテナーのすべての項目に突き合わせるように設定されます。

    「Discover」ページでログ項目が表示されない場合は、時間ピッカーを調整します。詳しくは、『[時間フィルターの設定](logging_kibana_set_time_filter.html#set_time_filter)』を参照してください。


##  Web ブラウザーから Kibana ダッシュボードへのナビゲート
{: #launch_Kibana_from_browser}

Kibana に表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix_notm}} 組織内のスペースのログ項目が取り出されます。Kibana に表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix_notm}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。

以下のステップを実行して、ブラウザーから Kibana を起動します。

1. Kibana ユーザー・インターフェースにログインするため、[https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) を開きます。

2. ログの分析に使用する Kibana のバージョンを選択します。
    * Kibana 4 で作業する場合は、**「Kibana 4」**タブを選択します。「Discovery」ページが開きます。詳しくは、[logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively) を参照してください。
    * Kibana 3 を使用して作業する場合は**「Kibana 3」**タブを選択します。 デフォルト Kibana ダッシュボードが開きます。Kibana 3 を使用したログの分析については、[Kibana 3 でのログの分析 (非推奨)](../logging_view_kibana3.html#analyzing_logs_Kibana3) に関する個所を参照してください。Kibana 3 ダッシュボードのカスタマイズについて詳しくは、[このブログ投稿![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)を参照してください。
     
        **注:** Kibana 3 は非推奨です。

    「Discover」ページでログ項目が表示されない場合は、時間ピッカーを調整します。詳しくは、『[時間フィルターの設定](logging_kibana_set_time_filter.html#set_time_filter)』を参照してください。


