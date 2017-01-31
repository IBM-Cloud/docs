---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} によるアプリケーションのモニター
{: #monitoringapps}

{{site.data.keyword.mobileanalytics_full}} には、モバイル・アプリケーションのモニタリングや分析を行う機能が備えられています。{{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用して、アプリケーション・ログを記録したりデータをモニターしたりできます。開発者は、このデータを {{site.data.keyword.mobileanalytics_short}} サービスに送信するタイミングを制御できます。データが {{site.data.keyword.mobileanalytics_short}} に送信されたら、{{site.data.keyword.mobileanalytics_short}} コンソールを使用して、モバイル・アプリケーション、デバイス、アプリケーション・ログに関する分析の洞察を得ることができます。
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

## アラートの設定
{: #alerts}

{{site.data.keyword.mobileanalytics_short}} コンソールでアラート定義にしきい値を設定すると、アクティビティーのモニターに役立ちます。

しきい値を構成して、そのしきい値を超過した場合にアラートをトリガーして {{site.data.keyword.mobileanalytics_short}} コンソール・モニターに通知するようにすることができます。トリガーされたアラートは、コンソールで視覚化したり、カスタム Webhook で処理したりできます。<!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.-->この機能は、アプリケーション・ログ・エラー、アプリケーションの異常終了、サーバー・ログ・エラーを検出するプロアクティブな手段になります。リアクティブのしきい値やアラートにより、データをふるいにかけたり、しきい値を細分して設定したりする必要がなくなります。

### アプリケーション・ログのアラート定義の作成
{: #alert-def-client-logs}

アプリケーション・ログに基づくアラート定義を作成できます。

この例では、アプリケーション・ログ・データを使用してアラート定義を作成します。アラートは、過去 5 分間に受け取ったすべてのアプリケーション・ログをモニターし、アラート定義が無効になるか削除されるまで、5 分ごとに検査し続けるとします。デバイスが同じアプリケーション名で同じバージョンのアプリケーション・エラー・ログを 3 つ以上送信するたびに、アラートがトリガーされます。

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「定義 (Definitions)」**をクリックして、「アラート定義 (Alert Definitions)」ページに進みます。
2. **「アラートの作成」**をクリックして、アラートを作成します。
3. 以下の値を入力します。
	* アラート名: アプリ・ログのアラート
	* メッセージ: エラー・メッセージのアラート
	* 照会の頻度: 5 分
	* イベント・タイプ: アプリ・ログ
		* プロパティー: ログ・レベル
			* 値: エラー
			* しきい値
				* しきい値のタイプ: アプリケーション・インスタンスの合計

					**注**: 「アプリケーションの平均」オプションを選択すると、アプリ・ログ数が、デバイス数で平均化された数になります。例えば、デバイスが 2 つあり、一方のデバイスがアプリ・ログを 6 つ送信し、もう一方のデバイスがアプリ・ログを 3 つ送信した場合、アプリ・ログの平均は 4.5 になります。
				* 演算子: 3 以上
	<!-- insert alert definition tab image? -->

4. **「次へ」**をクリックして、次の値を入力します。
	* 方法: 分析コンソールのみ

		**注**: カスタマイズした URL に JSON ペイロードとともに POST メッセージを追加で送信する場合は、「分析コンソールとネットワーク・ポスト (Analytics Console and Network Post)」オプションを選択します。このオプションを選択すると、以下のフィールドが使用可能になります。
		* ネットワーク・ポスト URL (Network Post URL)
        * ヘッダー (Headers)
        * 認証タイプ (Authentication Type)
5. **「保存」**をクリックします。

5 分間隔の最後にしきい値 (エラー・ログが 3 個以上) にアプリ・ログ数が達していればアラートをトリガーする、というアラート定義が作成されました。

### アプリケーション異常終了のアラート定義の作成
{: #alert-def-app-crash}

アプリケーション異常終了に基づくアラート定義を作成できます。

この例では、アプリケーション異常終了データを使用して、アラート定義を作成します。アラートは、過去 2 分間におけるすべてのアプリケーション異常終了をモニターし、アラート定義が無効になるか削除されるまで、2 分ごとに検査し続けるとします。5 回以上異常終了した各アプリケーションに対してアラートがトリガーされるようにします。アプリケーション異常終了について詳しくは、[アプリケーション異常終了](#app_crash)を参照してください。

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「定義 (Definitions)」**をクリックして、「アラート定義 (Alert Definitions)」ページを表示します。
2. **「アラートの作成 (Create Alert)」**をクリックします。
3. 以下の値を入力します。
	* アラート名: アプリケーション異常終了のアラート
	* メッセージ: アプリ異常終了のアラート
	* 照会の頻度: アプリケーションの異常終了
		* 照会の頻度: 2 分
	* イベント・タイプ: アプリケーションの異常終了
		* アプリケーション名: 任意のアプリケーション
		* アプリケーションのバージョン: 任意のバージョン
    * しきい値
      * しきい値のタイプ: 異常終了回数
      * 演算子: 5 以上
4. **「分布方法 (Distribution Method)」**タブをクリックし、次の値を入力します。
  * 方法: 分析コンソールのみ

    **注**: カスタマイズされた URL に JSON ペイロードとともに POST メッセージを追加で送信する場合、**「分析コンソールとネットワーク・ポスト (Analytics Console and Network Post)」**オプションを選択します。このオプションを選択すると、以下のフィールドが使用可能になります。
      * ネットワーク・ポスト URL (Network Post URL)(必須)
      * ヘッダー (Headers)(オプション)
      * 認証タイプ (Authentication Type)(必須)
5. **「保存」**をクリックします。

### アラート定義の管理
{: #managing-alert-definitions}

この例では、「アラート管理 (Alert Management)」ページからアラート定義を管理します。

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「ログ」**をクリックします。このアクションにより、「アラート・ログ」ページが開きます。
2. オプション:**「有効」**列の下のチェック・ボックスを切り替えて、特定のアラート定義を有効または無効にします。
3. オプション: アラート定義のコピーを作成し、いくつかの値を変更する場合は、**「複写」**アイコンをクリックします。
4. オプション: アラート定義を編集する場合は、**「鉛筆 (Pencil)」**アイコンをクリックします。
5. オプション: アラート定義を削除する場合は、**「ごみ箱」**アイコンをクリックします。

### アラート詳細の表示
{: #viewing-alert-details}

この例では、トリガーされたアラートの詳細を「アラート・ログ」ページから表示します。

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「ログ」**をクリックします。このアクションにより、「アラート・ログ」ページが開きます。
2. 任意のアラートの**「+」**アイコンをクリックします。このアクションにより、**「アラート定義 (Alert Definition)」**セクションと**「アラート・インスタンス (Alert Instances)」**セクションが表示されます。

    **注**: 対応するアラート定義が削除も変更もされていない場合、**「アラートの編集 (Edit Alert)」**をクリックしてアラート定義を編集できます。削除または変更されている場合、**「アラートの編集 (Edit Alert)」**ボタンを使用できず、以下のメッセージが表示されます。

    `このアラート定義は変更または削除されました。(This alert definition has since been modified or deleted.)`

3. オプション: アラートを削除するには、アラートを選択し**「ごみ箱」**アイコンをクリックします。

## アプリケーション異常終了のモニター
{: #monitor-app-crash}

{{site.data.keyword.mobileanalytics_short}} コンソールでアプリケーションの異常終了に関する情報を参照すると、アプリケーションのモニターやトラブルシューティングに役立ちます。

### アプリケーション異常終了のモニター
{: #app-crash}

**「異常終了」**ページの**「異常終了の概要」**表に、次のデータ列が表示されます。

* アプリケーション: アプリケーション名
* 異常終了: そのアプリの異常終了の総数
* 合計使用回数: ユーザーがアプリをオープンおよびクローズした回数の合計
* 異常終了率: 使用ごとの異常終了のパーセンテージ

**「異常終了」**表で、アプリケーションの異常終了に関する情報を即座に確認できます。<!--In the **Overview** page of the **Dashboard** section,-->**「異常終了 (Crashes)」**棒グラフにより、経時的な異常終了のヒストグラムが示されます。

クラッシュ・データの表示方法は 2 とおりあります。

1. 異常終了率の表示: 時間別の異常終了率
2. 合計異常終了回数の表示: 時間別の合計異常終了回数

### アプリ異常終了のトラブルシューティング
{: #app-crash-troubleshooting}

<!-- **Applications** section of the -->{{site.data.keyword.mobileanalytics_short}} コンソールの**「トラブルシューティング」**ページでは、**「異常終了の要約 (Crash Summary)」**表を使用して、アプリ異常終了の詳細が表示されます。

**「異常終了の要約 (Crash Summary)」**表はソート可能であり、次のデータ列が含まれています。

* 異常終了
* デバイス
* 最終異常終了日時
* アプリケーション
* OS
* メッセージ

項目の横の + アイコンをクリックして、**「異常終了の詳細」**表を表示します。この表には、次の列が含まれています。

* 異常終了時刻
* アプリケーション・バージョン
* OS バージョン
* デバイス・モデル
* デバイス ID
* ダウンロード: 異常終了につながるログをダウンロードするためのリンク

**「異常終了の詳細」**表内の任意の項目を展開して、スタック・トレースなどの詳細を表示します。

**注**: **「異常終了の要約 (Crash Summary)」**表のデータは、重大レベルのアプリ・ログの照会によって取り込まれます。アプリケーションで重大なアプリケーション・ログを収集していない場合、データはありません。

## ネットワーク要求のモニタリング
{: #monitor-network-requests}


{{site.data.keyword.mobileanalytics_short}} コンソールで、アプリケーションのネットワーク要求データを表示します。 

以下の測定値のデータを確認できます。
	
* 往復時間 - アプリがネットワーク要求をするのにかかる時間の長さを、ms 単位で定義します。
* 要求カウント - 1 つのアプリによるネットワーク要求の頻度を表示します。データは平均値としても表示されます。

## dashDB へのデータのエクスポート
{: #dashdb}

{{site.data.keyword.mobileanalytics_short}} コンソールに表示される評価指標は、モバイル・データから収集できる洞察のサンプルにすぎません。モバイル・データを {{site.data.keyword.IBM}} dashDB データウェアハウスに自動的にパイプ接続することができます。データウェアハウスで分析をカスタマイズし、データを他のパブリック・データ・ソースやプライベート・データ・ソースと集約し、最先端の分析を適用することで、ビジネスを理解、推進するための詳細で深い高度な洞察を引き出すことができます。

**「エクスポート」**ページにある**「DashDB」**をクリックして、{{site.data.keyword.mobileanalytics_short}} コンソールに dashDB をセットアップします。セットアップ完了後 1、2 時間以内に、{{site.data.keyword.mobileanalytics_short}} に送信される新しいデータは dashDB にも転送されるようになります。 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

