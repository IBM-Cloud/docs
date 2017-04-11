---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#サービス要件
{: #requirements}


##MQTT デバイス・メッセージ要件

* MQTT メッセージ・ブローカーは、1 つ以上の MQTT トピックで、JSON フォーマットのデバイス・メッセージを提供する必要があります。
* デバイス・メッセージは、任意の数の属性を含むことができますが、以下の 3 つの属性は常に必須です。
	* デバイスを一意的に識別する属性。
	* デバイスの現在位置の緯度を指定する属性。
	* デバイスの現在位置の経度を指定する属性。
* 次の 2 つのメッセージ・モードがサポートされます。
	* 1 つの MQTT メッセージに、1 つのデバイスに関する情報が入った 1つの JSON オブジェクトを含めることができます。
	* 1 つの MQTT メッセージに、デバイスの集合に関する情報が入った複数オブジェクトからなる JSON 配列を含めることができます。

##MQTT イベントとサービスの構成

アプリケーションは MQTT メッセージをサブスクライブし、{{site.data.keyword.geospatialshort_Geospatial}} をその [REST API](https://console.ng.bluemix.net/apidocs/246) によって制御します。REST API 呼び出しにより使用可能なアクションは次のとおりです。

* サービスの構成と開始。
* モニターする地域の追加と削除。
* サービス状況に関する情報と、現在定義されている地域のセットに関する情報の取得。
* サービスの停止。
* 既に構成済みのサービスの再始動。

