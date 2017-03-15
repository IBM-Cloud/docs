---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} でのゲートウェイの開発
{: #gw_dev_index}

デバイスを直接インターネットに接続できない場合、{{site.data.keyword.iot_full}} 組織でデータをアプリケーションに取得したり送信したりするためのゲートウェイ・デバイスを作成できます。
ゲートウェイ・デバイスを {{site.data.keyword.iot_short_notm}} の組織とアプリケーションに接続するのに役立つように、クライアント・ライブラリー、サンプルや情報が用意されています。
{:shortdesc}

## 接続プロトコル
ゲートウェイは、MQTT メッセージ・プロトコルを使用して {{site.data.keyword.iot_short_notm}} に接続します。HTTP メッセージを使用してゲートウェイを {{site.data.keyword.iot_short_notm}} に接続することはサポートされていません。HTTP メッセージを使用して接続できるのはデバイスだけです。

## クライアント・ライブラリー
{{site.data.keyword.iot_short_notm}} に接続できるゲートウェイを開発するためのクライアント・ライブラリーが以下の言語で用意されています。

|クライアント・ライブラリー |ライブラリーや詳細情報のリンク
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp](https://github.com/ibm-watson-iot/iot-cpp)
|C#|[https://github.com/ibm-watson-iot/iot-csharp](https://github.com/ibm-watson-iot/iot-csharp)
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc](https://github.com/ibm-watson-iot/iot-embeddedc)
|Java™|[https://github.com/ibm-watson-iot/iot-java](https://github.com/ibm-watson-iot/iot-java)
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs)
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered](https://github.com/ibm-watson-iot/iot-nodered)
|Python|[https://github.com/ibm-watson-iot/iot-python

](https://github.com/ibm-watson-iot/iot-python)

用意されているクライアント・ライブラリーの詳細情報やリンクについては、[{{site.data.keyword.iot_short_notm}} 開発用のクライアント・ライブラリー](../iot_platform_client_lib.html)も参照してください。

## エッジ分析
{: #eaa_community}

{{site.data.keyword.iot_short_notm}} エッジ分析機能を使用すると、ゲートウェイ・デバイス上で {{site.data.keyword.iot_short_notm}} 分析を実行できます。エッジ分析を使用して分析能力を持ってくることで、ネットワークのエッジで収集されたデータを分析し、対応することが可能になります。デバイス・データを {{site.data.keyword.iot_short_notm}} に送信して追加の分析処理を行ったり、ダッシュボードで視覚化したり、他の分析への入力として使用したりできます。また、クラウド・ベースのヒストリアン・リポジトリーに保管することもできます。

[IBM エッジ分析のコミュニティー・ページ](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true)からエッジ分析 SDK をダウンロードできます。この SDK には、SDK JAR ファイル、javadoc、サンプル・コード、レシピのリンク、README ファイルが含まれています。このコミュニティーで、ビデオを視聴してエッジ分析を開始したり、コミュニティー・フォーラムを使用して質問したりすることもできます。
