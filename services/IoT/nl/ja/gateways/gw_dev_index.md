---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

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
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|Embedded C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

用意されているクライアント・ライブラリーの詳細情報やリンクについては、[{{site.data.keyword.iot_short_notm}} 開発用のクライアント・ライブラリー](../iot_platform_client_lib.html)も参照してください。
