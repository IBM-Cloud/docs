---

copyright:
  years: 2015, 2016

---
# {{site.data.keyword.mobileanalytics_short}} によるアプリのモニター
{: #monitoringapps}
*最終更新日時: 2016 年 5 月 6 日*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} には、モバイル・アプリケーションのモニタリングや分析を行う機能が備えられています。{{site.data.keyword.mobileanalytics_short}} クライアント SDK を使用して、クライアント・ログを記録したりデータをモニターしたりできます。開発者は、このデータを {{site.data.keyword.mobileanalytics_short}} サービスに送信するタイミングを制御できます。データが {{site.data.keyword.mobileanalytics_short}} に送信されると、{{site.data.keyword.mobileanalytics_short}} ダッシュボードを使用して、モバイル・アプリケーションや、デバイス、クライアント・ログに関する分析の洞察を得ることができます。
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for client logs
{: #custom-charts-client-logs}

You can create a custom chart for client logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use client log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

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
  * Event Type: Client Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your app name
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

{{site.data.keyword.mobileanalytics_short}} コンソールでのアラート定義のしきい値の設定により、アクティビティーのモニターを改善できます。

しきい値を構成して、しきい値を超過するとアラートをトリガーして {{site.data.keyword.mobileanalytics_short}} コンソール・モニターに通知するようにできます。トリガーされたアラートをコンソールで視覚化するか、アラートをカスタム Webhook で処理できます。この機能により、クライアント・ログ・エラー、サーバー・ログ・エラー、ネットワーク待ち時間の長期化、認証の失敗を検出する事前対応手段が提供されます。リアクティブのしきい値やアラートにより、データをふるいにかけたり、しきい値を細分して設定したりする必要がなくなります。

### クライアント・ログのアラート定義の作成
{: #alert-def-client-logs}

クライアント・ログに基づくアラート定義を作成できます。

この例では、クライアント・ログ・データを使用して、アラート定義を作成します。アラートは、直近の 5 分以内に受信したすべてのクライアント・ログをモニターし、アラート定義が無効になるか削除されるまで、5 分おきに継続的にチェックします。アラートは、同じアプリ名とバージョンのクライアント・エラー・ログを 3 つ以上送信した各デバイスでトリガーされます。

1. {{site.data.keyword.mobileanalytics_short}} コンソールでベル・アイコンをクリックし、**「アラート・ログ」**ページに移動します。
2. **「アラート管理 (Alert Management)」**ページに移動し、**「アラートの作成 (Create Alert)」**をクリックします。
3. 以下の値を入力します。
	* アラート名: クライアント・ログのアラート
	* メッセージ: エラー・メッセージのアラート
	* 照会の頻度: 5 分
	* イベント・タイプ: クライアント・ログ
		* プロパティー: ログ・レベル
			* 値: エラー
			* しきい値
				* しきい値のタイプ: アプリケーション・インスタンスの合計

					**注**:「アプリケーションの平均 (Average for Application)」オプションを選択する場合、クライアント・ログは、デバイス数によって平均化されます。例えば、デバイスが 2 つあり、一方のデバイスが 6 つのクライアント・ログを送信し、もう一方のデバイスが 3 つのクライアント・ログを送信する場合、クライアント・ログの平均は 4.5 になります。
				* 演算子: 3 以上
<!-- insert alert definition tab image? -->

4. **「次へ」**または**「分布方法 (Distribution Method)」**タブをクリックし、次の値を入力します。
	* 方法: 分析コンソールのみ

		注: カスタマイズされた URL に JSON ペイロードとともに POST メッセージを追加で送信する場合、「分析コンソールとネットワーク・ポスト (Analytics Console and Network Post)」オプションを選択します。このオプションを選択すると、以下のフィールドが使用可能になります。
		* ネットワーク・ポスト URL (Network Post URL)
        * ヘッダー (Headers)
        * 認証タイプ (Authentication Type)
5. **「保存」**をクリックします。

クライアント・ログの数がしきい値の 3 個以上のエラー・ログになった場合に 5 分の各間隔の最後にアラートをトリガーするアラート定義が作成されました。

### アプリ異常終了のアラート定義の作成
{: #alert-def-app-crash}

アプリ異常終了に基づいてアラート定義を作成できます。

この例では、アプリ異常終了データを使用して、アラート定義を作成します。アラートは、直近の 2 分以内のすべてのアプリ異常終了をモニターし、アラート定義が無効になるか削除されるまで、2 分おきに継続的にチェックします。アラートは、各アプリの異常終了回数が 5 回以上になるとトリガーされます。アプリ異常終了について詳しくは、[アプリ異常終了](app_crash/c_op_analytics_crashes.html)を参照してください。

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「アラート」**アイコンをクリックします。このアクションにより、「アラート・ログ」ページが開きます。
2. **「アラート管理 (Alert Management)」**タブをクリックし、**「アラートの作成 (Create Alert)」**をクリックします。
3. 以下の値を入力します。
	* アラート名: アプリ異常終了のアラート
	* メッセージ: アプリ異常終了のアラート
	* 照会の頻度: アプリケーションの異常終了
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

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「アラート」**アイコンをクリックします。このアクションにより、「アラート・ログ」ページが開きます。
2. **「アラート管理 (Alerts Management)」**タブをクリックします。
3. オプション:**「有効」**列の下のチェック・ボックスを切り替えて、特定のアラート定義を有効または無効にします。
4. オプション: アラート定義のコピーを作成し、いくつかの値を変更する場合は、**「複写」**アイコンをクリックします。
5. オプション: アラート定義を編集する場合は、**「鉛筆 (Pencil)」**アイコンをクリックします。
6. オプション: アラート定義を削除する場合は、**「ごみ箱」**アイコンをクリックします。

### アラート詳細の表示
{: #viewing-alert-details}

この例では、トリガーされたアラートの詳細を「アラート・ログ」ページから表示します。

1. {{site.data.keyword.mobileanalytics_short}} コンソールで、**「アラート」**アイコンをクリックします。このアクションにより、「アラート・ログ」ページが開きます。
2. 任意のアラートの**「+」**アイコンをクリックします。このアクションにより、**「アラート定義 (Alert Definition)」**セクションと**「アラート・インスタンス (Alert Instances)」**セクションが表示されます。

    **注**: 対応するアラート定義が削除も変更もされていない場合、**「アラートの編集 (Edit Alert)」**をクリックしてアラート定義を編集できます。削除または変更されている場合、**「アラートの編集 (Edit Alert)」**ボタンを使用できず、以下のメッセージが表示されます。

    `このアラート定義は変更または削除されました。(This alert definition has since been modified or deleted.)`

3. オプション: アラートを削除するには、アラートを選択し**「ごみ箱」**アイコンをクリックします。

## アプリの異常終了
{: #monitor-app-crash}

{{site.data.keyword.mobileanalytics_short}} コンソールでアプリの異常終了に関する情報を表示し、アプリのモニターやトラブルシューティングを向上させることができます。

### アプリ異常終了のモニター
{: #app-crash}

{{site.data.keyword.mobileanalytics_short}} コンソールの**「ダッシュボード」**セクションにアプリの異常終了に関する情報が即座に表示されます。

**「ダッシュボード」**セクションの**「概要」**ページの**「異常終了」**棒グラフに、時間別の異常終了ヒストグラムが表示されます。

データの表示方法は 2 とおりあります。

1. 異常終了率の表示: 時間別の異常終了率
2. 合計異常終了回数の表示: 時間別の合計異常終了回数


### アプリ異常終了のトラブルシューティング
{: #app-crash-troubleshooting}

{{site.data.keyword.mobileanalytics_short}} コンソールの**「アプリケーション」**セクションの**「異常終了」**ページを表示して、アプリの管理を向上させることができます。

**「異常終了の概要 (Crash Overview)」**表に、次のデータ列が表示されます。

* アプリ: アプリ名
* 異常終了: そのアプリの異常終了の総数
* 合計使用回数: ユーザーがアプリをオープンおよびクローズした回数の合計
* 異常終了率: 使用ごとの異常終了のパーセンテージ

**「異常終了の要約 (Crash Summary)」**表はソート可能であり、次のデータ列が含まれています。

* 異常終了
* デバイス
* 最終異常終了日時
* アプリ
* OS
* メッセージ

項目の横の + アイコンをクリックして、**「異常終了の詳細 (Crash Details)」**表を表示できます。この表には、次の列が含まれています。

* 異常終了時刻
* アプリのバージョン
* OS バージョン
* デバイス・モデル
* デバイス ID
* ダウンロード: 異常終了につながるログをダウンロードするためのリンク

**「異常終了の詳細 (Crash Details)」**表の項目を展開して、スタック・トレースなどの詳細を取得できます。

**注**: 重大レベルのクライアント・ログを照会することにより、**「異常終了の要約 (Crash Summary)」**表にデータが取り込まれます。アプリが重大なクライアント・ログを収集しない場合、データを使用できません。


