---

copyright:
  years: 2016
lastupdated: "2016-10-26"

---



{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# API によるサービスの拡張
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}} には、{{site.data.keyword.iotinsurance_short}} ソリューションをカスタマイズしたり拡張したりするための API が用意されています。
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} には、Wink 水漏れセンサー用の組み込みサポートが付属しています。提供されている API を使用することにより、新しいデバイス・タイプやベンダーをサポートするように、{{site.data.keyword.iotinsurance_short}} ソリューションをカスタマイズすることができます。{{site.data.keyword.iotinsurance_short}} は、デバイスからセンサー・データを取得する上で、クラウド間通信に依存しています。{{site.data.keyword.iotinsurance_short}} をカスタマイズすることによって、新しいデバイスからセンサー・データを読み、{{site.data.keyword.iot_short_notm}} サービスによってそれをシステムの残りの部分に渡した後、該当するアクションを実行することができます。このカスタマイズは、新しい変換マイクロ・サービスを作成して行います。

サンプル・コード・セット全体を確認する場合は、[API サンプル GitHub リポジトリー](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples)を参照してください。

API の包括的な情報については、[API ドキュメンテーション](https://iot4i-api-docs.mybluemix.net/)を参照してください。


# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}
* [GitHub のサンプル・モバイル・アプリ・コード](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API リファレンス
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API サンプル](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## 関連リンク
{: #general}
* [{{site.data.keyword.iot_full}} 資料](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [開発者サポート・フォーラム](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow サポート・フォーラム](http://stackoverflow.com/questions/tagged/ibm-bluemix)
