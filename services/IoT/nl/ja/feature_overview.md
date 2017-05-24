---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 機能の概要
{: #feature_overview}

{{site.data.keyword.iot_full}} は、以下の重要な分野に構築されます。

  1. 接続 - デバイスを接続し、アプリケーションを開発します。
  2. 情報管理 - デバイス・データを保管/検討し、{{site.data.keyword.iot_short_notm}} を他のサービスに統合します。
  3. 分析 - {{site.data.keyword.iot_short_notm}} ダッシュボードを使用して、リアルタイム・デバイス・データを視覚化します。
  4. リスク管理 - ユーザーとアプリケーションに対するアクセス制御により、セキュアな接続とアーキテクチャーを構成します。

## 接続
{: #connect}

{{site.data.keyword.iot_short_notm}} の「接続」は、あらゆる {{site.data.keyword.iot_short_notm}} サービスの開始点になります。デバイスの接続、アプリケーションの作成、デバイスの制御、サード・パーティー・サービスとの対話はすべて、{{site.data.keyword.iot_short_notm}} の接続を利用して行います。

### ゲートウェイ・デバイス

ゲートウェイを使用することで、それ以外の方法ではインターネットに接続できないデバイスを {{site.data.keyword.iot_short_notm}} に接続することができます。ゲートウェイとは、デバイスの機能をすべて備えたうえで、そのゲートウェイに接続しているデバイスの代わりにパブリッシュやサブスクライブを実行できるものです。インターネットに接続できない一群のセンサーも、ゲートウェイ・デバイスを使用してセンサーのデータをゲートウェイに送信することで、{{site.data.keyword.iot_short_notm}} に接続することができます。詳細については、[ゲートウェイ用の開発の資料](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html)を参照してください。

### デバイス管理

デバイス管理機能は、デバイス管理 API とデバイスにインストールするデバイス管理エージェントによって実装されます。デバイス管理エージェントをインストールしたデバイスは、デバイス管理操作を実行できます。デバイス管理操作は、メインの {{site.data.keyword.iot_short_notm}} ダッシュボードまたはデバイス管理 API からトリガーできます。デバイス管理操作には、リブート、ファームウェア更新のダウンロードとインストール、工場出荷時設定へのリセットなどがあります。デバイス管理を拡張して、カスタムのデバイス管理操作を組み込むこともできます。詳細については、[デバイス管理の資料](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html)を参照してください。

### 拡張とサービス統合

拡張とサービス統合によって、外部サービスと、コア・サービスのユーザー定義拡張との両方を {{site.data.keyword.iot_short_notm}} のインスタンスに追加できます。{{site.data.keyword.iot_short_notm}} に統合できる外部サービスとしては、デバイスの場所の現在の気象情報を確認できる The Weather Company の気象と位置のサービスがあります。また、Jasper SIM データや、{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}} もあります。 サード・パーティーのサービスの統合や拡張の詳細については、[外部サービスの統合](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html)を参照してください。

---

## 情報管理
{: #information_management}

{{site.data.keyword.iot_short_notm}} の「情報管理」は、{{site.data.keyword.iot_short_notm}} サービスに届いた後、デバイスによって送信されるデータを制御します。情報管理には、データの保管と変換が含まれます。

### デバイスの最新イベント・キャッシュ

{{site.data.keyword.iot_short_notm}} Last Event Cache API を使用して、デバイスによって送信された最新のイベントを取得することができます。これは、デバイスがオンラインかオフラインかに関わらず機能するので、デバイスの物理的位置や使用状況に関係なくデバイスの状況を取得できます。過去 365 日以内に発生したものであれば、特定のイベントに関するデバイスの最新イベント・データを取得できます。

### デバイスのイベント・データの保管

{{site.data.keyword.iot_short_notm}} サービスからのデバイス・イベント・データは、後で使用するために保管することができます。データ保管は、そのデータからの洞察を得るための洞察力に富んだ分析を行ううえで重要な最初のステップです。例えば、長期間に渡って変更を追跡し、強力な分析ツールで使用するため (Watson API やコグニティブ・コンピューティングでの使用を含む) にデータのセットを保管することができます。詳細については、[{{site.data.keyword.cloudant_short_notm}} 履歴サービスの接続](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html)や [{{site.data.keyword.messagehub}} 履歴サービスの接続](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html)を参照してください。

---

## 分析
{: #analytics}

### リアルタイム・デバイス・データの視覚化

ダッシュボード・カードを使用して、リアルタイム・デバイス・データを視覚化/表示することができます。ダッシュボード・カードは、デバイス・データをリアルタイムでモニター/表示します。これにより、重要なデバイスまたはデバイス・データを追跡することができます。リアルタイム・デバイス・データのコンテキストと状況に素早くアクセスできるよう、これらの視覚化はメインの {{site.data.keyword.iot_short_notm}} ダッシュボードに表示されます。詳細については、[リアルタイム・データの視覚化の資料](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)を参照してください。

### エッジ分析とクラウド分析

{{site.data.keyword.iot_short_notm}} クラウド分析を使用することによって、リアルタイムのデバイス・データに基づいて、条件を満たした場合にアラートやオプションのアクションを起動するルール条件を指定できます。例えば、1 つのルールを作成し、その中で、デバイスが除去された場合やデバイスの温度が急上昇した場合に、アラートをユーザーのデバイス上のダッシュボードに送信し、E メールを管理者に送信するように指定することもできます。詳細については、[クラウド分析の資料](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html)を参照してください。

エッジ分析を使用して、ルール・トリガー・プロセスをクラウドからエッジ分析対応のゲートウェイに移動します。こうしてデバイスの近くで分析処理を行うことで、クラウドへのデバイス・データ・トラフィックの量が大幅に削減される可能性があります。
詳細については、[エッジ分析の資料](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html)を参照してください。

---

## リスク管理
{: #risk_management}

### セキュアな接続とアーキテクチャー

{{site.data.keyword.iot_short_notm}} のアーキテクチャーは、デバイスが他のデバイスになりすますことがないように設計されています。これにより、デバイス・データの保全性が維持されます。デバイスは、クライアント ID と認証トークンの組み合わせ (自分しか知らない) を使用して {{site.data.keyword.iot_short_notm}} に接続します。デバイスの登録後または API キーの生成後に、認証トークンが生成され、そのハッシュが生成されて、資格情報のセキュリティーを維持します。

リスク管理とセキュリティー管理のアドオンを利用すれば、{{site.data.keyword.iot_short_notm}} のセキュリティーを強化し、サーバーとデバイスの間のすべての接続ポイントを信頼できる資格情報によって認証できるようになります。このアドオンを使用すると、{{site.data.keyword.iot_short_notm}} のユーザー ID とトークンに加えて、証明書とトランスポート層セキュリティー (TLS) による認証が使用されます。サーバーとの通信時に、サーバーにアクセスするための有効な証明書を持っていないデバイスは、有効なユーザー ID とパスワードを使用しても、リスク管理とセキュリティー管理のアドオンの構成に基づいてアクセスを拒否されます。

---
