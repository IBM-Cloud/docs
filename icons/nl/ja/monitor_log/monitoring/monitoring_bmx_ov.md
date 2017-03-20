---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Bluemix でのモニター
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}} は、デフォルトで、CPU 使用量、メモリー使用率、およびネットワーク I/O のパフォーマンス・メトリックを収集し、表示します。これらのメトリックは、個々のクラウド・リソースのパフォーマンスについての情報を提供します。ご使用のクラウド環境におけるこれらのリソースのパフォーマンスを {{site.data.keyword.Bluemix_notm}} UI を介してモニターできます。ほぼリアルタイムのデータおよび履歴データを表示することができます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} のモニター機能を使用して、ご使用の環境およびアプリケーションから主要メトリックを自動的に収集および測定することができます。メトリックの収集には、特別な計測装置は必要ありません。例えば、パフォーマンス・メトリックによって提供される情報を使用して、サービスがクラウドでどのように稼働しているのかをモニターしたり、リソースのボトルネックを検出したり、SLA (Service Level Agreement) を監視したりできます。サービスのパフォーマンス・データを分析すると、リソースのボトルネックにつながる可能性があって、結果的にクライアントへのサービス SLA に影響するかもしれない状況を検出できます。早期に処置することで、業務にネガティブな影響を与える可能性のある状況を防止できます。  

さらに多くのパフォーマンス・メトリックを構成してモニターすることができます。これらのメトリックの視覚化と分析を {{site.data.keyword.Bluemix_notm}} の外側で行うことができます。例えば、{{site.data.keyword.containershort}} 内でアプリを実行している場合、Grafana を使用して、さらに多くのメトリックをモニターすることができます。パフォーマンス・データの視覚化と分析を行うコンテナー・インスタンスまたはスペースごとに、ダッシュボードをカスタマイズできます。

![{{site.data.keyword.Bluemix_notm}} で実行しているコンテナーの Grafana モニター・ビュー](images/monitoring_default_container_grafana_view.jpg)

{{site.data.keyword.Bluemix_notm}} プラットフォームのモニターを使用して、以下を行うことができます。

* アプリケーションの操作に関する洞察を得る (例えば、潜在的ボトルネックやアップグレードの必要性を検出する)。
* クラウド・プラットフォームでの将来のアプリ要件を計画するために使用できるトレンドを定義する。

Cloud Foundry で実行しているアプリのモニターについて詳しくは、『[Cloud Foundry で実行されているアプリのモニター](monitoring_cf_apps.html#monitoring_bluemix_apps)』を参照してください。

{{site.data.keyword.containershort}} でのモニターについて詳しくは、『[{{site.data.keyword.containershort}} でのモニター](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)』を参照してください。   

