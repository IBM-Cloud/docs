---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイス・データの視覚化
{: #visualizingdata_data}

このサンプルは、{{site.data.keyword.iot_full}} 組織に登録されているデバイスから取得したリアルタイム・データと履歴データを視覚化するのに役立ちます。
{:shortdesc}

## 始めに
{: #byb}

データを視覚化するには、その前に以下の操作を行う必要があります。

- デバイスを {{site.data.keyword.iot_short_notm}} 組織に登録する。
- デバイスがイベントを {{site.data.keyword.iot_short_notm}} に送信していることを確認する。
- GitHub リポジトリーから[視覚化サンプルをダウンロード](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip)し、.zip ファイルを解凍します。
- {{site.data.keyword.Bluemix_notm}} から [cf コマンド・ライン・ツールをインストール](../../starters/install_cli.html)します。

## {{site.data.keyword.Bluemix_notm}} でのサンプルの実行
{: #running_sample}

1. Node.js SDK を使用して、{{site.data.keyword.Bluemix_notm}} 内にアプリケーションを作成します。アプリケーション名とアプリケーションのホスト名をメモします。この情報は、アプリケーションを {{site.data.keyword.Bluemix_notm}} にアップロードするために必要です。
2. 以下のステップを行って、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の {{site.data.keyword.iot_short_notm}} インスタンスに node.JS アプリケーションをバインドします。

  a. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、作成した Node.JS アプリケーションをクリックします。

  b. **「サービスまたは API のバインド」**をクリックしてから {{site.data.keyword.iot_short_notm}} サービスを選択し、**「追加」**をクリックします。
3. cf コマンド・ライン・ツールを使用して、解凍した視覚化サンプル・パッケージにディレクトリーを変更し、次のコマンドを実行して {{site.data.keyword.Bluemix_notm}} に接続します。
```
cf api https://api.ng.bluemix.net
```
4. 次に、次のコマンドを使用して {{site.data.keyword.Bluemix_notm}} にログインします。
```
cf login -u <your_bluemix_login_id>
```
デフォルトの組織とスペースを使用していない場合は、次のコマンドを使用できます。
```
cf target-o <your_bluemix_org> -s dev
```

5. `manifest.yml` ファイルを編集して、ホスト名とアプリケーション名を以下の形式を使用して更新します。
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. 次のコマンドを使用して視覚化サンプルをデプロイします。
```
cf push <your_application_name>
```
7. ブラウザーで次の URL を入力します。
```
http://<your_application_name>.mybluemix.net
```

組織内のすべてのデバイスがデバイス・ドロップダウン・メニューにリストされます。ここでデバイスを選択すると、そのデバイスが {{site.data.keyword.iot_short_notm}} サービスに送信中のデータのリアルタイム視覚化が表示されるはずです。履歴データを表示するには、**「履歴データ (Historic Data)」**ボタンをクリックします。

## サンプルのカスタマイズ
{: #customize_sample}

このサンプル・アプリケーションは、node.js フレームワークで作成されたスタンドアロン Web アプリケーションです。このサンプルを実行すると、{{site.data.keyword.iot_short_notm}} に登録されたデバイスによって送信されるイベントが視覚化されます。このサンプルでは、以下のツールを使用します。

- Express: Node.js Web アプリケーション・フレームワーク
- JQuery: UI および Ajax 呼び出し
- Rickshaw : グラフィカル視覚化ツール
- Paho: MQTT クライアント

このサンプル・アプリケーションは以下のディレクトリーで構造化されています。

- Public
- CSS: スタイル・シート
- Images
- JS: 主な JavaScript 論理ファイル
- Historian: ヒストリアン視覚化のコード
- Realtime: リアルタイム視覚化のコード
- Uicontroller.js: ユーザー・インターフェースの制御コード
- Routes: ルーティング・ロジックと Web アプリケーション
- Utils: HTTP 呼び出しに使用するユーティリティー関数
- Views: Jade で作成されたユーザー・インターフェース・ファイル
- リアルタイム・データと履歴データの両方のグラフをプロットするために、Rickshaw チャート作成ライブラリーが使用されます。

## リアルタイム・データ表示のカスタマイズ
{: #customize_real_time_display}

リアルタイム・データのグラフィカル視覚化コードがあるディレクトリーは `public/ja/realtime` です。グラフ作成ロジックは、`public/js/historian/realtimeGraph.js` を編集してカスタマイズできます。

Paho MQTT ライブラリーを参照してデバイス・トピックへのサブスクライブと {{site.data.keyword.iot_short_notm}} からのデバイス・イベントの受信を行うファイルは、`public/js/historian/realtime.js` にあります。

デバイス・イベントは `realtimeGraph.js` ファイルに渡されて、グラフがプロットされます。

## 履歴データ表示のカスタマイズ
{: #customize_historical_display}

履歴デバイス・データのグラフィック視覚化コードがあるディレクトリーは `public/js/historian` です。グラフ作成ロジックは、`public/js/historian/historianGraph.js` を編集してカスタマイズできます。

履歴デバイス・データを収集する REST API 呼び出しを制御するファイルは `public/js/historian/historian.js` です。

履歴データは `historianGraph.js` ファイルに渡されて、グラフがプロットされます。

より詳細な開発者向けガイドを Github iot-visualization wiki から入手できます。
