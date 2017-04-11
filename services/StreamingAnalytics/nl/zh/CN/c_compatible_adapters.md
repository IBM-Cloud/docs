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

#兼容的适配器
{: #c_compatible_adapters}


工具箱是组织成包的一组工件。工具箱使得功能和原始或组合操作程序可跨不同的应用程序重复使用。
{:shortdesc}

##Internet Toolkit

Internet Toolkit (com.ibm.streamsx.inet) 提供常用因特网协议的支持。此工具箱嵌入 {{site.data.keyword.streamsshort}}，在 {{site.data.keyword.streamsshort}} 开发环境中提供。


下表列出 Internet Toolkit 提供的操作程序。


| ***兼容的操作程序*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*表 1. 与 Internet Toolkit 兼容的操作程序*

**注**：以星号 (*) 标记的操作程序在与同时在 {{site.data.keyword.Bluemix_short}} 中运行的客户机一起使用时，可在云环境中运作。

有关 Internet Toolkit 兼容的操作程序的更多信息，请参阅 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} 中的[操作程序：IBMStreams com.ibm.streamsx.inet 工具箱](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window}。

您可以从 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} 下载具有增强功能和其他操作程序的较新版本的工具箱。下载工具箱之后，请在 {{site.data.keyword.streamsshort}} 开发环境中对其进行构建（必要的话）并安装。


##IoT Integration Toolkit

IoT Integration Toolkit (com.ibm.streamsx.iot) 提供与 {{site.data.keyword.iot_full}} 的连接。{{site.data.keyword.streamsshort}} 应用程序使用此工具箱，针对来自可能成百上千个设备的所有事件（包括基于分析，发送命令到特定设备），来提供实时分析。


下表列出 IoT Integration Toolkit 提供的操作程序。


| ***兼容的操作程序*** | 							               |
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

*表 2. 与 IoT Integration Toolkit 兼容的操作程序*

有关 IoT Integration Toolkit 兼容操作程序的更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streamsx.iot 工具箱](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window}。

##Messaging Toolkit

Messaging Toolkit (com.ibm.streamsx.messaging) 项目是开放式源代码 {{site.data.keyword.streamsshort}} 工具箱项目。它重点在于开发操作程序和功能，帮助您使用 {{site.data.keyword.streamsshort}}，与消息传递系统（如 Kafka、JMS、XMS 和 MQTT）交互。 

此工具箱嵌入 {{site.data.keyword.streamsshort}}，在 {{site.data.keyword.streamsshort}} 开发环境中提供。


下表列出 Messaging Toolkit 提供的操作程序。


| ***兼容的操作程序*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `具有 Apache ActiveMQ 的 JMSSink`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*表 3. 与 Messaging Toolkit 兼容的操作程序*

有关 Messaging Toolkit 兼容的操作程序的更多信息，请参阅 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} 中的[操作程序：IBMStreams com.ibm.streamsx.messaging 工具箱](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window}。

您可以从 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} 下载具有增强功能和其他操作程序的较新版本的工具箱。下载工具箱之后，请在 {{site.data.keyword.streamsshort}} 开发环境中对其进行构建（必要的话）并安装。


有关工具箱限制的更多信息，请参阅 [{{site.data.keyword.streamsshort}} 专业工具箱的限制](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

**注**：要使用 JMSSource、JMSSink、XMSSource、XMSSink 与 WebSphere MQ，请在您的开发环境中完成以下所需步骤：
 

1. 转至 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} 并在您的开发环境中下载 Messaging Toolkit (com.ibm.streamsx.messaging) V3.0.0 或更高版本。
2. 使用 V5.1.0 或更高版本的工具箱来构建应用程序。
3. 在应用程序的 `/etc` 目录中放置必要的 .bindings 文件，以将其包含在 {{site.data.keyword.streamsshort}} 应用程序捆绑软件中。
