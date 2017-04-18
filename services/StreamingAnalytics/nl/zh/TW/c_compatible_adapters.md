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

# 相容的配接器
{: #c_compatible_adapters}


工具箱是一組組織成套件的構件。工具箱可讓函數和基本或複合運算子能夠在不同應用程式中重複使用。
{:shortdesc}

## Internet Toolkit

Internet Toolkit (com.ibm.streamsx.inet) 支援一般網際網路通訊協定。此工具箱內嵌在 {{site.data.keyword.streamsshort}} 中，也提供於 {{site.data.keyword.streamsshort}} 開發環境中。

下表列出 Internet Toolkit 所提供的運算子。


| ***相容的運算子*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*表 1. 與 Internet Toolkit 相容的運算子*

**附註**：標上星號 (*) 函數的運算子與同時在 {{site.data.keyword.Bluemix_short}} 中執行的用戶端搭配使用時，可在雲端環境中運作。

如需 Internet Toolkit 相容運算子的相關資訊，請參閱 [GitHub 上的 IBMStreams](https://github.com/IBMStreams){:new_window} 中的 [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window}。

您可以從 [GitHub 上的 IBM Streams](https://github.com/IBMStreams){:new_window} 下載工具箱的新版本（含加強功能和其他運算子）。下載工具箱之後，請建置它（必要的話），並在 {{site.data.keyword.streamsshort}} 開發環境上安裝它。

## IoT Integration Toolkit

IoT Integration Toolkit (com.ibm.streamsx.iot) 提供與 {{site.data.keyword.iot_full}} 的連線功能。{{site.data.keyword.streamsshort}} 應用程式可以使用此工具箱，針對可能來自數千個裝置的所有事件（包括根據分析將指令傳送至特定裝置）提供即時分析。

下表列出 IoT Integration Toolkit 所提供的運算子。


| ***相容的運算子*** | 							               |
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

*表 2. 與 IoT Integration Toolkit 相容的運算子*

如需 IoT Integration Toolkit 相容運算子的相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window}。

## Messaging Toolkit

Messaging Toolkit (com.ibm.streamsx.messaging) 專案是開放程式碼 {{site.data.keyword.streamsshort}} 工具箱專案。著重在開發運算子和函數，以協助您使用 {{site.data.keyword.streamsshort}} 與傳訊系統（例如 Kafka、JMS、XMS 和 MQTT）互動。 

此工具箱內嵌在 {{site.data.keyword.streamsshort}} 中，也提供於 {{site.data.keyword.streamsshort}} 開發環境中。

下表列出 Messaging Toolkit 所提供的運算子。


| ***相容的運算子*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink（含 Apache ActiveMQ）`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*表 3. 與 Messaging Toolkit 相容的運算子*

如需 Messaging Toolkit 相容運算子的相關資訊，請參閱 [GitHub 上的 IBMStreams](https://github.com/IBMStreams){:new_window} 中的 [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window}。

您可以從 [GitHub 上的 IBM Streams](https://github.com/IBMStreams){:new_window} 下載工具箱的新版本（含加強功能和其他運算子）。下載工具箱之後，請建置它（必要的話），並在 {{site.data.keyword.streamsshort}} 開發環境上安裝它。

如需工具箱限制的相關資訊，請參閱 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

**附註**：若要搭配使用 JMSSource、JMSSink、XMSSource、XMSSink 與 WebSphere MQ，請在開發環境中完成下列必要步驟： 

1. 移至 [GitHub 上的 IBMStreams](https://github.com/IBMStreams){:new_window}，並在開發環境中下載 Messaging Toolkit (com.ibm.streamsx.messaging) 3.0.0 版或更新版本。
2. 使用 5.1.0 版或更新版本的工具箱來建置您的應用程式。
3. 將必要的 .bindings 檔案放在您應用程式的 `/etc` 目錄中，以將它包括在 {{site.data.keyword.streamsshort}} 應用程式軟體組中。
