---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.iot4auto_short}} (Beta) について
{: #iotautomotive_overview}

最終更新日: 2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.iot4auto_full}} は、自動車から取得したビッグデータの表示と分析のために使用できる、{{site.data.keyword.Bluemix_notm}} のサービスです。

{{site.data.keyword.iot4auto_short}} サービスを使用すると、自動車から大量のデータを収集して処理することができます。{{site.data.keyword.iot4auto_short}} のアナリティクスは、ドライバーの動作、車両の位置、その他の自動車関連アクティビティーとイベントについての、すぐに利用できる強力な洞察を提供します。
{:shortdesc}

## アーキテクチャー
{: #architecture}
{{site.data.keyword.iot4auto_short}} は、自動車用アプリケーションおよび接続された自動車用デバイス向けの、基盤となるリアルタイム・インフラストラクチャー・プラットフォームです。さらにこのサービスは、台頭しつつある将来の自動運転機能をサポートできるようにも設計されています。

![{{site.data.keyword.iot4auto_full}} アーキテクチャー](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}} アーキテクチャー")

{{site.data.keyword.iot4auto_short}} サービスには、以下の {{site.data.keyword.Bluemix_notm}} サービスが含まれます。それらは別々に {{site.data.keyword.Bluemix_notm}} カタログにも用意されています。

|サービス|説明 |
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| このサービスは、ドライバーの動作を分析し、接続された車両から取得した自動車プローブ・データとコンテキスト・データから、走行の軌跡パターンを識別します。
|[Context Mapping](../IotMapInsights/index.html)| このサービスは、マップ・マッチングや道路ネットワークでの最短経路検索など、地理情報機能を提供します。
*表 1. {{site.data.keyword.iot4auto_short}} のサービス*

## フィーチャー
{: #features}

{{site.data.keyword.iot4auto_short}} は、接続された自動車用デバイスから取得した自動車プローブ・データを提供するソリューション向けに、以下のフィーチャーおよび機能をサポートしています。

### {{site.data.keyword.iot4auto_short}} デバイスからのデータの取得

- 以下のプロトコルとデータ・モデルをサポートします
   - TPEG
   - ITS
   - ISO 自動車規格
- 他の非自動車用デバイスおよびセンサーをサポートします

### データの正規化と保管

- 異常データを識別してフィルター処理します
- データを、分析用の標準データ・モデルにマップ、変換、フォーマット設定します
- データをボリューム、待ち時間、アプリケーションやサービスの用途に従って、以下のいずれかのデータ・ストアに入れます
   -  ビッグデータ分析用の Hadoop データ・ストア
   -  リアルタイム分析用のエージェント・データ・ストア

### 地理情報マップ・ベースのサービス

- リアルタイム・マップ・マッチング
- イベント・サービス
- 自動車および外部ソースからの動的イベント注入
- リンクまたはノード・ベース・トポロジー認識検索
- 気象データが組み込まれたコンテキスト・マップ・サポート

### 拡張が容易で低遅延のリアルタイム分析プラットフォーム

- エージェント・ベースのテクノロジー
- パーソナライズされた分析
- 柔軟なルール・ベースの分析

### 移動オブジェクト・マップ分析 (MOMA)

- 車両からのデータを使用したバッチ (ビッグデータ) 分析
- ドライバー動作分析
- ドライバー・プロファイル
- 軌跡パターン分析

### データ・プロバイダー・サービス

- サード・パーティーのアプリケーションおよびサービス用の API

### 資産管理との統合

- 車両資産管理システム

## REST API
{: #api}

[{{site.data.keyword.iot4auto_short}} API](http://ibm.biz/IoT4Automotive_APIdoc) は、特定の要件に合わせて {{site.data.keyword.iot4auto_short}} をさらに発展させるためのコマンドを提供します。

用意されている REST API コマンドを使用して、{{site.data.keyword.iot4auto_short}} サービス・インスタンスを以下のようにカスタマイズできます。

- 特定のイベントをシステムに注入します
- 車両から取得して正規化した自動車プローブ・データを、希望する分析データ・ストアに保管します
- 関心の対象のイベントを、車両の地理的位置と共にリアルタイムで取得します。

### REST API コマンド

|目的 |API コマンド |説明  |
|:---|:---|:---|
|イベントの注入|`sendEvent`|トラフィックまたは他のイベントをプラットフォームに送信します。|
|自動車プローブ・データの送信|`sendCarProbe`|車両からの位置ベース・センサー・データを送信し、リアルタイム分析の結果により、車両に影響があったイベントを取得します。|
|車両データの作成|`createVehicle`|車両のレコードを資産として作成します。この情報は、認証、目録、その他の用途に使用します。|
|マップ API|該当なし|詳細については、[Contextual Map サービス API](http://ibm.biz/IoTContextMapping_APIdoc) を参照してください。|
|分析 API|該当なし|詳細については、[Driver Behavior サービス API]( http://ibm.biz/IoTDriverBehavior_APIdoc) を参照してください。|
|自動車プローブ・データの取得|`getCarProbe`|`sendCarProbe` API コマンドによって送信された、車両の最新の自動車プローブ・データを取得します。|
|マップ・イベントの取得|`getEvent` |`sendEvent` API コマンドによって送信された、マップ上のイベントを取得します。|
|車両資産データの取得|`getVehicle`| `createVehicle` API コマンドによる、資産としての車両データを取得します。|
*表 2. {{site.data.keyword.iot4auto_short}} REST API コマンド*
