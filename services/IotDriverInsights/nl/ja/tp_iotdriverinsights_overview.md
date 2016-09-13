---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Trajectory Pattern Analysis について
{: #tp_iotdriverinsights_overview}
最終更新: 2016 年 6 月 16 日
{: .last-updated}

Trajectory Pattern Analysis API は、{{site.data.keyword.iotdriverinsights_full}} によって提供されるサービスの 1 つであり、カー・プローブ・データからトリップの起点/終点 (O/D) およびルート・パターンを分析するために使用できます。


{:shortdesc}

## ルート経路パターン分析
{: #tpa}

複数のトリップ・データから O/D パターンおよびルート・パターンを識別し、分析することができます。
複数のトリップ・データから取られた、ある自動車 (vehicle-1) の O/D パターンおよびルート・パターンのシンプルな例を、以下の図に示します。
この例では、Trajectory Pattern Analysis により 2 つの O/D パターンが識別されます。

- 2 つのルート・パターンがある、(起点1) から勤務先 (終点1) への O/D パターン
- ルート・パターンが 1 つである、自宅 (起点1) から店 (終点2) への O/D パターン

![od ルートの例](images/tp_odroute_example.png "O/D およびルート・パターンの例")

また、以下の表に示されているようにして、Trajectory Pattern Analysis により各自動車についていくつかのドライブ多様性メトリックが計算されます。
それらのメトリックを使用することにより、ドライバーのドライブの特性を判定することができます。


|メトリック名|説明|
|:---|:---|
|希少 O/D 率|総入力トリップ回数に対する、O/D パターンでカバーされないトリップの回数の比率。|
|希少走行距離比率|総入力トリップ走行距離に対する、ルート・パターンでカバーされない走行距離の比率。|
|希少トリップ率|総入力トリップ回数に対する、ルート・パターンでカバーされないトリップ回数の比率。|


## REST API
{: #rest_api}

Trajectory Pattern Analysis REST API は、{{site.data.keyword.Bluemix_notm}} アプリケーションをカスタマイズおよびビルドするために使用できるさまざまな要求を提供します。


 1. 自動車データ・コマンド:
   - `sendCarProbeData` は、分析するためにカー・プローブ・データを送信します
   - `getCarProbeDataListAsDate` は、日付ごとのカー・プローブ・データのリストを返します
   - `deleteCarProbeDataListByDate` は、カー・プローブ・データを削除します
 2. 分析ジョブのコマンド:
   - `sendJobRequest` は、経路パターン分析ジョブ要求を送信します
   - `getJobInfo` は、指定されたジョブの情報を返します
   - `getJobInfoList` は、ジョブ情報のリストを返します
 3. 分析結果のコマンド:
   - `getResultSummary` は、経路パターン分析の分析結果要約情報を返します
   - `getAnalyzedODDetail` は、指定された分析済み O/D パターンの詳細情報を返します
   - `getRouteGPSList` は、指定された分析済みルート・パターンの GPS 情報のリストを返します
   - `getODList` は、指定された引数の O/D パターン情報のリストを返します
   - `deleteJobResult` は、ジョブに関連するすべての分析結果を削除します

詳しくは、[{{site.data.keyword.iotdriverinsights_short}} API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} の資料を参照してください。

