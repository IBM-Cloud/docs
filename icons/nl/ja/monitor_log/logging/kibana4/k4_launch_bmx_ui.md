---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix ダッシュボードから Kibana ダッシュボードへの移動
{: #launch_Kibana_from_bluemix}

{{site.data.keyword.Bluemix}} UI から Kibana を起動して、Cloud Foundry アプリケーションまたは Docker コンテナーの特定のログを表示します。
{:shortdesc}

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

Kibana について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。

