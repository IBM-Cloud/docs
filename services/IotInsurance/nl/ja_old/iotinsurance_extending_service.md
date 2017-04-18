---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# API によるサービスの拡張
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}} には、{{site.data.keyword.iotinsurance_short}} ソリューションをカスタマイズしたり拡張したりするための API が用意されています。
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} には、Wink 水漏れセンサー用の組み込みサポートが付属しています。提供されている API を使用することにより、新しいデバイス・タイプやベンダーをサポートするように、{{site.data.keyword.iotinsurance_short}} ソリューションをカスタマイズすることができます。{{site.data.keyword.iotinsurance_short}} は、デバイスからセンサー・データを取得する上で、クラウド間通信に依存しています。{{site.data.keyword.iotinsurance_short}} をカスタマイズすることによって、新しいデバイスからセンサー・データを読み、{{site.data.keyword.iot_short_notm}} サービスによってそれをシステムの残りの部分に渡した後、該当するアクションを実行することができます。このカスタマイズは、新しい変換マイクロ・サービスを作成して行います。

サンプル・コード一式を確認するには、[GitHub の API サンプル・リポジトリー ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window} を参照してください。

API の詳細については、[API ドキュメンテーション ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window} を参照してください。
