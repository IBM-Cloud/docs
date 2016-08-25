---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Trajectory Pattern Analysis 概説
{: #tp_index}
最終更新: 2016 年 6 月 16 日
{: .last-updated}

Trajectory Pattern Analysis API は、{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.iotdriverinsights_full}} サービス内に含まれるサービスの 1 つであり、カー・プローブ・データから運転トリップの起点/終点 (O/D) およびルート・パターンを分析するために使用できます。


{:shortdesc}

Trajectory Pattern Analysis での典型的な API 呼び出しシーケンスの概略を、以下の図に示します。


![標準的な分析シーケンス](images/tp_sequence_diagram.png "標準的な分析シーケンス")

{{site.data.keyword.iotdriverinsights_short}} をアンバウンド・サービス・インスタンスとして作成およびデプロイした後、以下の作業を実行して、アプリケーションに Trajectory Pattern Analysis API を組み込みます。


## 始めに
{: #tp_byb}
- [Trajectory Pattern Analysis について](tp_iotdriverinsights_overview.html)のトピックを参照して、分析可能な動作とコンテキストについて確認してください。

- 自動生成される*テナント ID*、*ユーザー名*、および*パスワード*の値を入手します。
{{site.data.keyword.iotdriverinsights_short}} API にアクセスするためには、それらが必要です。


  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.iotdriverinsights_short}} サービス・タイルをクリックします。

  2. サービス・インスタンスの**「管理」**ビューを選択します。

  3. テナント ID、ユーザー名、およびパスワードの値をメモします。


## タスク 1: 自動車データのアップロード
{: #tp_task1}
複数の運転トリップ・データのセットを {{site.data.keyword.iotdriverinsights_short}} テナントにアップロードして、ドライバー・データを Trajectory Pattern Analysis で使用できるようにします。


1. `sendCarProbeData` API で分析するため、カー・プローブ・データをストアに送信します。
カー・プローブ・データを {{site.data.keyword.iotdriverinsights_short}} にアップロードします。

   - 要求: カー・プローブ・データ

## タスク 2: 自動車データの処理
{: #tp_task2}

自動車データを処理して、O/D (起点/終点) パターンおよびルート・パターンを分析します


1. Trajectory Pattern Analysis API の `sendJobRequest` により、特定の期間についてカー・プローブ・データを分析するジョブの要求を送信します。

   - 要求: 開始/終了日付
   - 応答: ジョブ ID
2. Trajectory Pattern Analysis API の `getJobInfo` によりジョブ状況を確認します。
データ処理は、返されるジョブ状況が 'SUCCEEDED' となっていれば完了しています。
そうなった時点で、経路パターン分析結果データを要求できるようになります。

   - 要求: ジョブ ID
   - 応答: ジョブ状況

## タスク 3: トリップの分析
{: #tp_task3}
特定の日付範囲のトリップを分析して、分析しきい値パラメーターへの適合の程度を調べます。


1. 分析後の (起点/終点) パターン要約リストを入手するには、Trajectory Pattern Analysis API の `getResultSummary` を使用します。
O/D パターン要約リストには、入力パラメーターに応じて分析されたトリップ要約情報が含まれます。

   - 要求: ジョブ ID
   - 応答: 要約および O/D (起点/終点)、パターン ID のリスト
2. O/D パターンおよびルート・パターンの詳細分析情報を入手するには、Trajectory Pattern Analysis API コマンドの `getAnalyzedDetail` を使用します。
分析されたトリップについての詳細な経路パターン情報を入手します。

   - 要求: ジョブ ID /  O/D パターン ID
   - 応答: O/D の詳細 (ルート・パターン ID を含む)
3. 各ルート・パターンの GPS ポイントのリストを得るには、Trajectory Pattern Analysis API の `getRouteGPSList` を使用します。
最後に、特定のルート・パターンの GPS ポイントのリストを入手します。

   - 要求: ジョブ ID /  O/D パターン ID / ルート・パターン ID
   - 応答: ルート・パターンの経度/緯度のリスト

## 次のステップ
{: #tp_post}
これらのステップの実行が終了したら、一連の経路パターン分析データが組織内で生成されます。
アプリケーションまたはお気に入りの分析ソフトウェアを使用することにより、情報をさらに処理して、さらに意味のあるビジネス・データにします。


# 関連リンク
{: #rellinks}

## API リファレンス
{: #api}

* [API ドキュメント](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}

## その他の資料
{: #general}

* [{{site.data.keyword.iotmapinsights_short}} の使用を開始する](../IotMapInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} の使用を開始する](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [IBM developerWorks の dW Answers](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [スタック・オーバーフロー](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [Bluemix サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
