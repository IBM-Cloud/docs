---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix でのロギング
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} ロギング機能はプラットフォームに統合されており、クラウド・リソースに関するデータ収集は自動的に有効になります。{{site.data.keyword.Bluemix_notm}} は、デフォルトで、アプリ、アプリ・ランタイム、およびそれらのアプリの実行場所である計算ランタイムについて、ログの収集と表示を行います。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} のロギング機能を使用して、クラウド・プラットフォームと、そこで稼働しているリソースの動作を理解することができます。標準出力と標準エラーのログを収集するために特別な計測装置は必要ありません。例えば、ログを使用することによって、アプリケーションの監査証跡の提供、ご使用のサービスにおける問題の検出、脆弱性の識別、アプリケーション・デプロイメントおよびランタイム動作の障害追及、アプリを実行しているインフラストラクチャーの問題の検出、クラウド・プラットフォームの複数のコンポーネントにわたるアプリのトレース、および、サービス SLA に影響する可能性のあるアクションを回避するために使用できるパターンの検出を行うことができます。

アプリをクラウドで実行する場合、ログにアクセスするためにアプリが実行されているインフラストラクチャーに入る際に SSH または
FTP を使用できないことがあります (例えば、アプリケーションが Cloud Foundry で実行している場合など)。一方、{{site.data.keyword.Bluemix_notm}} で使用可能な別の計算ランタイムである {{site.data.keyword.containershort}} でアプリを実行することができ、そこでは SSH を使用し、ログにアクセスすることができます。計算ランタイムに関係なく、ログへのアクセスは重要であり、{{site.data.keyword.Bluemix_notm}} は、ご使用のクラウド・プラットフォームでのログの視覚化と分析のための一般的なエクスペリエンスを提供します。

{{site.data.keyword.Bluemix_notm}} は、Cloud Foundry プラットフォームによって生成されるログ・データ、および Cloud Foundry アプリケーションによって生成されるログ・データを記録します。ログでは、アプリに対して生成されたエラー、警告、および情報の各メッセージを表示できます。Cloud Foundry でのロギングについて詳しくは、『[Bluemix での Cloud Foundry アプリのロギング](logging_cf_apps.html#logging_bluemix_cf_apps)』を参照してください。

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
