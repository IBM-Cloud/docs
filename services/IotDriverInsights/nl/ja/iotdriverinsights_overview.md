---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotdriverinsights_short}} について
{: #iotdriverinsights_overview}

{{site.data.keyword.iotdriverinsights_full}} を使用すると、自動車プローブ・データとコンテキスト・データに基づいてドライバーの行動を分析できます。
{:shortdesc}

## ドライバーの行動分析
{: #driver_behavior_analysis}
急な加速やブレーキ、頻繁なブレーキ、速度違反、鋭角な転回などのドライバーの行動を、自動車プローブ・データとコンテキスト・データから分析できます。

次のアクティビティーとコンテキストが含まれます。
 - 運転動作 
    - 速度関連
       - 急な加速
       - 急なブレーキ
       - 速度違反
       - 頻繁な停止
       - 頻繁な加速
       - 頻繁なブレーキ
    - 転回関連
       - 鋭角な転回 (高速転回)
       - 転回前の加速
       - 転回中の過度のブレーキ
    - その他
       - 過労運転
 - 運転コンテキスト
    - 時刻範囲
       - 朝のピーク時
       - 夕方のピーク時
       - 日中
       - 夜間
    - 道路タイプ
       - 高速道路
       - 都市高速道路
       - 都市幹線道路
       - 都市道路
       - 他の道路
    - 道路タイプに基づく速度パターン
       - 自由流れ
       - 定常流れ
       - 渋滞
       - 重度の渋滞
       - 混合状態

## ビッグデータ分析のインフラストラクチャー
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} は、バックエンド・インフラストラクチャーとして Hadoop を使用します。Hadoop を使用すると、{{site.data.keyword.iotdriverinsights_short}} は自動車プローブ・データとコンテキスト・データに基づくビッグデータの分析に関する高度なスケーラビリティーを実現できます。

## REST API
{: #rest_api}
開発者は REST API によって分析結果を取得し、その結果を {{site.data.keyword.Bluemix_notm}} アプリケーションで使用できます。
 1. 車両データ
   - `sendCarProbeData` は、分析対象の自動車プローブ・データを送信します。
   - `getCarProbeDataListAsDate` は、日付に基づいて自動車プローブ・データのリストを返します。
   - `deleteCarProbeDataListByDate` は、自動車プローブ・データを削除します。
 2. 分析ジョブ
   - `sendJobRequest` は、運転の行動分析ジョブ要求を送信します。
   - `getJobInfo` は、指定のジョブの情報を返します。
   - `getJobInfoList` は、ジョブ情報のリストを返します。
 3. 分析結果 
   - `getAnalyzedTripSummaryList` は、分析済みの経路要約情報のリストを返します。
   - `getAnalyzedTripInfo` は、指定された分析済み経路情報を返します。
   - `deleteJobResult` は、ジョブに関連する分析済み結果すべてを削除します。

## 構成可能性
{: #configurability}
分析しきい値パラメーターの一部 (道路タイプの速度範囲、転回角度範囲など) はユーザー・インターフェース (UI) から構成できます。
