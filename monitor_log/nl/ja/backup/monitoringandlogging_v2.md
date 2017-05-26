---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# モニターとロギング
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} は、アプリやサービスを作成、実行、管理するための {{site.data.keyword.IBM_notm}} のクラウド・コンピューティング・プラットフォームです。{{site.data.keyword.Bluemix_notm}} は、Platform as a Service (PaaS) と Infrastructure as a Service (IaaS) を組み合わせています。また、{{site.data.keyword.Bluemix_notm}} は、ビジネス・アプリケーションを迅速に作成するために PaaS および IaaS と簡単に統合できる、クラウド・サービスの豊富なカタログを備えています。
{{site.data.keyword.Bluemix_notm}} には、プラットフォーム全体にわたるロギング・サービスとモニタリング・サービスが統合されて組み込まれています。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} は、異なる複数の計算サービス (Cloud Foundry および {{site.data.keyword.containershort}} など) にわたってロギング・サービスおよびモニター・サービスを提供します。通常はアプリの開発と立ち上げに結び付いている、インフラストラクチャーの複雑な構築と保守を必要とせずに、任意の計算ランタイムでアプリケーションを開発、実行、および管理できます。
 

**注:** モニタリングとロギングの機能は、米国南部地域および英国地域のみで使用可能です。

{{site.data.keyword.Bluemix_notm}} のモニター機能を使用して、ご使用の環境およびアプリケーションから主要メトリックを自動的に収集および測定することができます。メトリックの収集には、特別な計測装置は必要ありません。例えば、パフォーマンス・メトリックによって提供される情報を使用して、サービスがクラウドでどのように稼働しているのかをモニターしたり、リソースのボトルネックを検出したり、SLA (Service Level Agreement) を監視したりできます。例えば、サービスのパフォーマンス・データを分析すると、リソースのボトルネックにつながる可能性があり、結果的にクライアントへのサービス SLA に影響する可能性のある状況を検出できます。早期に処置することで、業務にネガティブな影響を与える可能性のある状況を防止できます。  

{{site.data.keyword.Bluemix_notm}} のロギング機能を使用して、クラウド・プラットフォームと、そこで稼働しているリソースの動作を理解することができます。標準出力と標準エラーのログを収集するために特別な計測装置は必要ありません。例えば、ログを使用することによって、アプリケーションの監査証跡の提供、ご使用のサービスにおける問題の検出、脆弱性の識別、アプリケーション・デプロイメントおよびランタイム動作の障害追及、アプリを実行しているインフラストラクチャーの問題の検出、クラウド・プラットフォームの複数のコンポーネントにわたるアプリのトレース、および、サービス SLA に影響する可能性のあるアクションを回避するために使用できるパターンの検出を行うことができます。

## コンピュート・インフラストラクチャー・リソースのモニタリング
{: #monitoring_sl_ov}

すべての {{site.data.keyword.Bluemix_notm}} サーバーには、常に使用できるモニタリングと読みやすいレポートが組み込まれています。詳しくは、[インフラストラクチャーのモニタリングとレポーティング ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window} を参照してください。


## 計算サービスのための {{site.data.keyword.Bluemix}} でのモニタリング
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}} は、デフォルトで、CPU 使用量、メモリー使用率、およびネットワーク I/O のパフォーマンス・メトリックを収集し、表示します。これらのメトリックは、個々のクラウド・リソースのパフォーマンスについての情報を提供します。ご使用のクラウド環境におけるこれらのリソースのパフォーマンスを {{site.data.keyword.Bluemix_notm}} UI を介してモニターできます。ほぼリアルタイムのデータおよび履歴データを表示することができます。
 

さらに多くのパフォーマンス・メトリックを構成してモニターすることができます。これらのメトリックの視覚化と分析を {{site.data.keyword.Bluemix_notm}} の外側で行うことができます。例えば、{{site.data.keyword.containershort}} 内でアプリを実行している場合、Grafana を使用して、さらに多くのメトリックをモニターすることができます。パフォーマンス・データの視覚化と分析を行うコンテナー・インスタンスまたはスペースごとに、ダッシュボードをカスタマイズできます。

![{{site.data.keyword.Bluemix_notm}} で実行しているコンテナーの Grafana モニター・ビュー](images/monitoring_default_container_grafana_view.jpg)

{{site.data.keyword.Bluemix_notm}} プラットフォームのモニターを使用して、以下を行うことができます。

* アプリケーションの操作に関する洞察を得る (例えば、潜在的ボトルネックやアップグレードの必要性を検出する)。
* クラウド・プラットフォームでの将来のアプリ要件を計画するために使用できるトレンドを定義する。

Cloud Foundry で実行しているアプリのモニターについて詳しくは、『[Cloud Foundry で実行されているアプリのモニター](monitoring_cf_apps.html#monitoring_bluemix_apps)』を参照してください。

{{site.data.keyword.containershort}} でのモニターについて詳しくは、『[{{site.data.keyword.containershort}} でのモニター](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)』を参照してください。   

## {{site.data.keyword.Bluemix}} でのロギング
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} ロギング機能はプラットフォームに統合されており、クラウド・リソースに関するデータ収集は自動的に有効になります。{{site.data.keyword.Bluemix_notm}} は、デフォルトで、アプリ、アプリ・ランタイム、およびそれらのアプリの実行場所である計算ランタイムについて、ログの収集と表示を行います。 

アプリをクラウドで実行する場合、ログにアクセスするためにアプリが実行されているインフラストラクチャーに入る際に SSH または
FTP を使用できないことがあります (例えば、アプリケーションが Cloud Foundry で実行している場合など)。一方、{{site.data.keyword.Bluemix_notm}} で使用可能な別の計算ランタイムである {{site.data.keyword.containershort}} でアプリを実行することができ、そこでは SSH を使用し、ログにアクセスすることができます。計算ランタイムに関係なく、ログへのアクセスは重要であり、{{site.data.keyword.Bluemix_notm}} は、ご使用のクラウド・プラットフォームでのログの視覚化と分析のための一般的なエクスペリエンスを提供します。

{{site.data.keyword.Bluemix_notm}} は、Cloud Foundry プラットフォームによって生成されるログ・データ、および Cloud Foundry アプリケーションによって生成されるログ・データを記録します。ログでは、アプリに対して生成されたエラー、警告、および情報の各メッセージを表示できます。Cloud Foundry でのロギングについて詳しくは、『[{{site.data.keyword.Bluemix}} での Cloud Foundry アプリのロギング](logging_cf_apps.html#logging_bluemix_cf_apps)』を参照してください。

{{site.data.keyword.Bluemix_notm}} は、{{site.data.keyword.containershort}} によって生成されるログ・データを記録します。{{site.data.keyword.containershort}} でのロギングについて詳しくは、『[{{site.data.keyword.containershort}} でのロギング](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs)』を参照してください。   


{{site.data.keyword.Bluemix_notm}} が提供するロギング機能を使用することによって、以下を行うことができます。

* クラウド・リソースおよびそれらの実行状況を把握する。
* 処置が必要なシナリオを特定するのに役立つ傾向を定義する。
* 例えば監査に使用できる、アプリのデータの証跡を定義する。
* アプリの問題を見つけて修復するのに必要な時間と労力を削減する。 
* クラウド・プラットフォームでのアプリのデプロイメントをモニターする。
* サービスまたはアプリがダウンまたはクラッシュしたときに検出する。
* アプリケーション実行およびデータのフローをたどる。
* アプリの脆弱性を特定する。
* インフラストラクチャーの問題を検出する。
* アプリ・ランタイムの問題を検出する。


