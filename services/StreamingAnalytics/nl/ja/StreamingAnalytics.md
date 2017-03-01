---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 概要
{: #about}

{{site.data.keyword.streaminganalyticsfull}} を使用して、Data in Motion (流れているデータ) に関するリアルタイム分析を、 {{site.data.keyword.Bluemix_short}} アプリケーションの一部として実行することができます。
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}} では {{site.data.keyword.streamsshort}} を採用しています。これは、タイプが異なるデータ・ソースから到着する情報をリアルタイムで取り込み、分析し、相互に関連付けるために使用できる、高機能の分析プラットフォームです。{{site.data.keyword.streaminganalyticsshort}} サービスのインスタンスを作成すると、{{site.data.keyword.Bluemix_short}} クラウド内で稼働する {{site.data.keyword.streamsshort}} のユーザー独自のインスタンスが得られ、{{site.data.keyword.streamsshort}} アプリケーションを実行する準備が整います。

{{site.data.keyword.streaminganalyticsshort}} を初めて使用する場合は、
 [このサービスの簡単な概要](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}を参照してください。ユーザー独自のアプリケーションをさらに開発したい場合は、{{site.data.keyword.streamsshort}} 開発環境が必要であり、SPL をクラウド対応にする必要があります。

{{site.data.keyword.streaminganalyticsshort}} サービスは、クラウドでデータのデプロイ、分析、およびモニターを可能にする以下の機能を提供します。

**サービスの対話式での使用およびプログラマチックな使用:**

このサービスは、[{{site.data.keyword.streaminganalyticsshort}} コンソール](/docs/services/StreamingAnalytics/c_streams_console.html)によって対話式に使用することも、[{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window} によってプログラマチックに使用することもできます。

**SPL および Java アプリケーションのデプロイメントおよびモニター:**

{{site.data.keyword.streamsfull}} Processing Language (SPL) は、ストリーム処理アプリケーションの作成に使用されるプログラミング言語です。{{site.data.keyword.streamsshort}} アプリケーションは、SPL または Java で作成することができます。[これらのアプリケーションのデプロイおよびモニター](/docs/services/StreamingAnalytics/t_deploytocloud.html)は、{{site.data.keyword.streaminganalyticsshort}} を使用して行います。 

**{{site.data.keyword.streamsshort}} 演算子との互換性:**

[{{site.data.keyword.streamsshort}} Processing Language (SPL) 標準ツールキットに含まれる {{site.data.keyword.streamsshort}} 演算子は、すべて {{site.data.keyword.streaminganalyticsshort}} と互換性があります](/docs/services/StreamingAnalytics/c_beta_adapters.html)。

## {{site.data.keyword.streaminganalyticsfull}} の責任

### お客様の責任

以下は、お客様の責任となります。

* {{site.data.keyword.streamsshort}} の IBM の初期構成の後での、インスタンスで実行される
{{site.data.keyword.streamsshort}} ジョブのモニタリング、構成、および管理。
お客様は、インスタンスの開始および停止、インスタンスでの jobskeywordnning の開始および停止を柔軟に行うことができます。
* データを分析し、そこから洞察を得るために必要な場合または必須である場合の、サービスのプログラムおよびアプリケーションの開発。お客様は、かかる開発されたプログラムや開発されたアプリケーションの品質およびパフォーマンスについ
ても責任を負うものとします。プログラムは、{{site.data.keyword.streamsshort}} トポロジー・フィーチャーを使用して、SPL、Java、または他のサ
ポート対象言語で開発することができます。プログラムは、{{site.data.keyword.streaminganalyticsshort}} で使用されるのと同じオペレーティング・システムで、{{site.data.keyword.streamsshort}} Developer Edition または {{site.data.keyword.streamsshort}} Quick Start Edition のいずれかを使用してコンパイルする必要があります。 
* 予定されている非中断型または中断型のダウン時間について情報を得るための以下のリンクの定期的な確認 - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* 継続性を確保するための、すべてのデータ、メタデータ、構成ファイルおよび環境パラメーターのビジネス要件に従ったバックアップ。
* これに限らないもののデータセンターや POD の障害、サーバー障害またはハード・ディスク障害もしくはソフトウェア障害を含むあらゆるタイプの障害が発生した場合
の、データ、メタデータ、構成ファイルおよび環境パラメーターのバックアップからの復元による継続性の確保。

### IBM の責任

{{site.data.keyword.streaminganalyticsfull}} の一部として、IBM は以下を行います。

* お客様のインスタンスのサーバー、ストレージおよびネットワーキング・インフラストラクチャーの提供および管理。 
* 選択したノードの数の {{site.data.keyword.streamsshort}} の初期構成の提供。
* 保護および分離のための、インターネットに面している、内部ファイアウォールのインフラストラクチャーの提供および管理。 
* {{site.data.keyword.streaminganalyticsfull}} 上の以下のコンポーネントのモニターおよび管理。
	* ネットワーク・コンポーネント
	* サーバーおよびそれぞれのローカル・ストレージ
	* インフラストラクチャー・オペレーティング・システム
	* {{site.data.keyword.streamsshort}} の管理サービス
	* {{site.data.keyword.streamsshort}} インスタンス 
* インフラストラクチャー・オペレーティング・システムおよび {{site.data.keyword.streamsshort}} 用の適切なセキュリティー
・パッチを含む、保守パッチの提供。
* システム・ダウン時間を必要としない定期保守 (「非中断型」保守) および多少のシステム・ダウン時間やリスタートが必要になる可能性のある保守 (「中断型」保守)の、[https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} で公開されている予定時刻の実行。 
* 定期保守時間に変更がある場合の、適宜通知のポスト。 
