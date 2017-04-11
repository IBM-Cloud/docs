---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"
---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#互換性のあるアダプター
{: #c_compatible_adapters}


ツールキットは、1 つのパッケージに編成された、成果物の集合です。ツールキットは、関数および原始演算子または合成演算子を、複数の異なるアプリケーション間で再使用可能にします。
{:shortdesc}

##Internet Toolkit

Internet Toolkit (com.ibm.streamsx.inet) は、一般的なインターネット・プロトコルをサポートします。このツールキットは {{site.data.keyword.streamsshort}} に組み込まれており、{{site.data.keyword.streamsshort}} 開発環境で使用できるようになっています。

以下の表には、Internet Toolkit で提供される演算子がリストされています。


| ***互換性のある演算子*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*表 1. Internet Toolkit と互換性のある演算子*

**注**: アスタリスク (*) のマークが付いている演算子は、{{site.data.keyword.Bluemix_short}} 内でも稼働しているクライアントとともに使用される場合、クラウド環境で機能します。

Internet Toolkit と互換性のある演算子について詳しくは、[GitHub 上の IBMStreams](https://github.com/IBMStreams){:new_window} にある [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} を参照してください。

機能拡張と追加の演算子を含む新しいバージョンのツールキットを、
[GitHub 上の IBMStreams](https://github.com/IBMStreams){:new_window} からダウンロードできます。ツールキットをダウンロードした後、(必要に応じて) それをビルドし、{{site.data.keyword.streamsshort}} 開発環境にインストールします。

##IoT 統合ツールキット

IoT 統合ツールキット (com.ibm.streamsx.iot) は、{{site.data.keyword.iot_full}} との接続を提供します。{{site.data.keyword.streamsshort}} アプリケーションは、このツ
ールキットを使用して、数千台に及ぶ可能性もあるデバイスのすべてのイベントに対するリアルタイムの分析を提供することができます。この分析に基づいて特定のデバイスへコマンドを送信することもできます。

以下の表には、IoT 統合ツールキットで提供される演算子がリストされています。


| ***互換性のある演算子*** | 							               |
| ---------------------------| --------------------------- |
| `AllDevices` 	   			     |	`IotPlatformBluemix`  		 | 	 	 	
| `CommandPublish`		 	     |	`PublishDeviceCommands`		 |
| `CommandTupleToPayload`	   | 	`PublishDeviceEvents`	 	   |
| `CommandsSubscribe`	 	     | 	`PublishDeviceStatuses`		 |
| `DeviceCommands`	 	 	     |  `Quickstart`				       |
| `DeviceEventExtractData`	 |  `QuickstartDeviceEvents`	 |
| `DeviceEvents`			       |  `SendCommandToDevice`		   |
| `DeviceStatuses`		 	     |  `StatusesSubscribe`			   |
| `EventsSubscribe`			     |  `SubscribeDeviceCommands`	 |
| `IotPlatform`				       |  `ViewAllDevices`			     |

*表 2. IoT 統合ツールキットと互換性のある演算子*

IoT 統合ツールキットの互換性のある演算子について詳しくは、
{{site.data.keyword.streamsshort}} 製品資料の
[Operators:
com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} を参照してください。

##Messaging Toolkit

Messaging Toolkit (com.ibm.streamsx.messaging) プロジェクトは、オープン・ソースの {{site.data.keyword.streamsshort}} ツールキット・プロジェクトです。このプロジェクトは、{{site.data.keyword.streamsshort}} を使用して Kafka、JMS、XMS、および MQTT などのメッセージング・システムと相互作用するのに役立つ、演算子および関数の開発に重点を置いています。 

このツールキットは {{site.data.keyword.streamsshort}} に組み込まれており、{{site.data.keyword.streamsshort}} 開発環境で使用できるようになっています。

以下の表には、Messaging Toolkit で提供される演算子がリストされています。


| ***互換性のある演算子*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink with Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*表 3. Messaging Toolkit と互換性のある演算子*

Messaging Toolkit と互換性のある演算子について詳しくは、[GitHub 上の IBMStreams](https://github.com/IBMStreams){:new_window} にある [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} を参照してください。

機能拡張と追加の演算子を含む新しいバージョンのツールキットを、
[GitHub 上の IBMStreams](https://github.com/IBMStreams){:new_window} からダウンロードできます。ツールキットをダウンロードした後、(必要に応じて) それをビルドし、{{site.data.keyword.streamsshort}} 開発環境にインストールします。

ツールキットの制約事項については、[Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window} を参照してください。

**注**: WebSphere MQ で JMSSource、JMSSink、XMSSource、XMSSink を使用するには、開発環境で以下の必要な手順を実行します。 

1. [GitHub 上の IBMStreams](https://github.com/IBMStreams){:new_window}にアクセスし、開発環境に Messaging Toolkit (com.ibm.streamsx.messaging) バージョン 3.0.0 以降をダウンロードします。
2. バージョン 5.1.0 以降のツールキットを使用して、アプリケーションをビルドします。
3. アプリケーションの `/etc` ディレクトリーに、必要な .bindings ファイルを置き、それを {{site.data.keyword.streamsshort}} アプリケーション・バンドルに組み込みます。
