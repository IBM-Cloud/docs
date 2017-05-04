---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Grafana でのメトリックの分析
{:#analyzing_metrics_grafana}

{{site.data.keyword.Bluemix}} では、分析および視覚化のためのオープン・ソース・プラットフォームである Grafana を使用して、さまざまなグラフ (図表や表など) でメトリックのモニター、検索、分析、および視覚化を行うことができます。高機能な分析タスクを実行するには、Grafana を使用してください。
{:shortdesc}

Grafana は以下のどの方法でも起動できます。

* {{site.data.keyword.Bluemix_notm}} から

    Grafana では特定の Docker コンテナーのメトリックをその特定のコンテナーに応じて起動できます。 
    
    詳しくは、[{{site.data.keyword.Bluemix_notm}} ダッシュボードから
    Grafana ダッシュボードへの移動](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix)を参照してください。

* ブラウザーの直接リンクから

    Grafana を起動して、用意されている {{site.data.keyword.Bluemix_notm}} スペース内のサービスのログを、表示データで集約することができます。
    
    詳しくは、『[Web ブラウザーから Kibana ダッシュボードへの移動](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser)』を参照してください。
    


##  Bluemix ダッシュボードから Grafana ダッシュボードへの移動
{: #launch_grafana_from_bluemix}

Grafana に表示されるデータをフィルター操作するために使用される照会によって、Kibana を起動した場所から {{site.data.keyword.Bluemix_notm}} コンテナーのデータが取り出されます。 

Docker コンテナーのメトリックを Grafana で表示するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインし、{{site.data.keyword.Bluemix_notm}} ダッシュボードでコンテナーをクリックします。 
    
2. ナビゲーション・バーで、**「モニターおよびログ」**をクリックします。モニター・タブが開きます。 
    
3. **「拡張ビュー」**をクリックします。**「Grafana」**ダッシュボードが開きます。

Grafana について詳しくは、[Grafana のユーザー・ガイド ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://docs.grafana.org/){: new_window} を参照してください。


##  Web ブラウザーから Grafana ダッシュボードへの移動
{: #launch_grafana_from_browser}

Grafana に表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix_notm}} 組織内のスペースのデータが取り出されます。Grafana に表示されるメトリック情報には、ログインしている {{site.data.keyword.Bluemix_notm}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。

ブラウザーから Grafana を起動するには、以下の手順を実行します。

1. Grafana ユーザー・インターフェースにログインするため、[https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) を開きます。

2. **「Grafana」**を選択します。
     
Grafana について詳しくは、[Grafana のユーザー・ガイド ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://docs.grafana.org/){: new_window} を参照してください。
