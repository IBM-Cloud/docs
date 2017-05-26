---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 概要
{: #about}

{{site.data.keyword.streaminganalyticsfull}} を使用して、Data in Motion (流れているデータ) に関するリアルタイム分析を、{{site.data.keyword.Bluemix_short}} アプリケーションの一部として実行することができます。
{:shortdesc}

{{site.data.keyword.streaminganalyticsshort}} を初めて使用する場合は、
 [このサービスの簡単な概要](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}を参照してください。

{{site.data.keyword.streaminganalyticsshort}} サービスは、クラウド内でデータをデプロイ、分析、およびモニターできるようにする以下の機能を提供します。

**サービスの対話式での使用およびプログラマチックな使用:**

このサービスは、[{{site.data.keyword.streaminganalyticsshort}} コンソール](/docs/services/StreamingAnalytics/c_streams_console.html)を使用して対話式に使用することも、[{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window} を使用してプログラマチックに使用することもできます。

**SPL、Java、Scala、および Python アプリケーションのデプロイおよびモニター**

{{site.data.keyword.streamsshort}} アプリケーションは、SPL、Java、Scala、および Python で作成できます。[これらのアプリケーションをデプロイおよびモニター](/docs/services/StreamingAnalytics/t_deploytocloud.html)するには、{{site.data.keyword.streaminganalyticsshort}} コンソールを使用します。

アプリケーションを SPL で作成する場合は、{{site.data.keyword.streamsfull}} Processing Language (SPL) がストリーム処理アプリケーションの作成に使用されるプログラミング言語であることを把握しておく必要があります。ユーザー独自の SPL アプリケーションでさらに活用する場合は、{{site.data.keyword.streamsshort}} 開発環境を取得でき、SPL アプリケーションをクラウド対応にする必要があります。

{{site.data.keyword.streamsshort}} 開発環境なしで Python アプリケーションを作成およびデプロイする場合は、IBM Data Science Experience(DSX) のノートブックまたは {{site.data.keyword.streamsshort}} Python API を使用します。詳しくは、『[{{site.data.keyword.streaminganalyticsshort}} 用の Python アプリケーションの開発](/docs/services/StreamingAnalytics/t_develop_apps_python.html)』を参照してください。

**{{site.data.keyword.streamsshort}} 演算子との互換性:**

[{{site.data.keyword.streamsshort}} Processing Language (SPL) 標準ツールキット](/docs/services/StreamingAnalytics/c_beta_adapters.html)に含まれる {{site.data.keyword.streamsshort}} オペレーターは、すべて {{site.data.keyword.streaminganalyticsshort}} と互換性があります。

## {{site.data.keyword.streaminganalyticsfull}} の責任
{: #responsibilities notoc}

### お客様の責任
{: #clientresponsibilities notoc}

以下は、お客様の責任となります。

* {{site.data.keyword.streamsshort}} の IBM の初期構成の後での、インスタンスで実行される
{{site.data.keyword.streamsshort}} ジョブのモニタリング、構成、および管理。
お客様は、インスタンスの開始および停止、ならびにインスタンスで実行されるジョブの開始および停止を柔軟に行うことができます。
* データを分析し、そこから洞察を得るために必要な場合または必須である場合の、サービスのプログラムおよびアプリケーションの開発。お客様は、かかる開発されたプログラムや開発されたアプリケーションの品質およびパフォーマンスについ
ても責任を負うものとします。プログラムは、{{site.data.keyword.streamsshort}} トポロジー・フィーチャーを使用して、SPL、Java、または他のサ
ポート対象言語で開発することができます。{{site.data.keyword.streaminganalyticsshort}} で使用されるのと同じオペレーティング・システムで、{{site.data.keyword.streamsshort}} Developer Edition または {{site.data.keyword.streamsshort}}Quick Start Edition のいずれかを使用してコンパイルする必要があります。
* 予定されている非中断型または中断型のダウンタイムについて情報を得るための以下のリンクの定期的な確認 - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* 継続性を確保するための、すべてのデータ、メタデータ、構成ファイルおよび環境パラメーターのビジネス要件に従ったバックアップ。
* これに限らないもののデータセンターや POD の障害、サーバー障害またはハード・ディスク障害もしくはソフトウェア障害を含むあらゆるタイプの障害が発生した場合
の、データ、メタデータ、構成ファイルおよび環境パラメーターのバックアップからの復元による継続性の確保。

### IBM の責任
{: #ibmresponsibilities notoc}

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
* システム・ダウンタイムを必要としない定期保守 (「非中断型」保守) および多少のシステム・ダウンタイムやリスタートが必要になる可能性のある保守 (「中断型」保守) の実行。[https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} で公開されている予定時刻に実行されます。
* 定期保守時間に変更がある場合の、適宜通知のポスト。
