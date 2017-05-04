---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Web ブラウザーから Kibana ダッシュボードへの移動
{: #launch_Kibana_from_browser}

{{site.data.keyword.Bluemix}} スペース内のログ項目を分析する必要がある場合は、ブラウザーから Kibana を起動します。
{:shortdesc}

Kibana に表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix_notm}} 組織内のスペースのログ項目が取り出されます。Kibana に表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix_notm}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。

以下のステップを実行して、ブラウザーから Kibana を起動します。

1. Kibana ユーザー・インターフェースにログインするため、[https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) を開きます。

2. ログの分析に使用する Kibana のバージョンを選択します。
    * Kibana 4 で作業する場合は、**「Kibana 4」**タブを選択します。「Discovery」ページが開きます。詳しくは、[logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively) を参照してください。
    * Kibana 3 を使用して作業する場合は**「Kibana 3」**タブを選択します。 デフォルト Kibana ダッシュボードが開きます。Kibana 3 ダッシュボードのカスタマイズについて詳しくは、[このブログ投稿](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)を参照してください。
     
        **注:** Kibana 3 は非推奨です。

    「Discover」ページでログ項目が表示されない場合は、時間ピッカーを調整します。詳しくは、『[時間フィルターの設定](logging_kibana_set_time_filter.html#set_time_filter)』を参照してください。

Kibana について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。
