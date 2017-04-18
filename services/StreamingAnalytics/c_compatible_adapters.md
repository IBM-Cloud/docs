---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"
---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Compatible adapters
{: #c_compatible_adapters}


A toolkit is a set of artifacts, which are organized into a package. Toolkits make functions and primitive or composite operators reusable across different applications.
{:shortdesc}

##Internet Toolkit
{: #internet notoc}

The Internet Toolkit (com.ibm.streamsx.inet) provides support for common internet protocols. This toolkit is embedded in {{site.data.keyword.streamsshort}} and it is available in your {{site.data.keyword.streamsshort}} development environment.

The following table lists operators provided by the Internet Toolkit.


| ***Compatible operators*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*Table 1. Operators that are compatible with the Internet Toolkit*

**Note**: Operators marked with an asterisk (*) function in the cloud environment when used with a client that is also running in {{site.data.keyword.Bluemix_short}}.

For more information about the Internet Toolkit compatible operators, see [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} in [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

You can download newer versions of the toolkit, with enhancements and additional operators, from [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. After you download the toolkit, build it (if necessary) and install it on your {{site.data.keyword.streamsshort}} development environment.

##IoT Integration Toolkit
{: #iot notoc}

The IoT Integration Toolkit (com.ibm.streamsx.iot) provides connectivity with {{site.data.keyword.iot_full}}. {{site.data.keyword.streamsshort}} applications can use this toolkit to provide real-time analytics against all the events from potentially thousands of devices, including sending commands to specific devices based upon the analytics.

The following table lists operators provided by the IoT Integration Toolkit.


| ***Compatible operators*** | 							               |
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

*Table 2. Operators that are compatible with the IoT Integration Toolkit*

For more information about IoT Integration Toolkit compatible operators, see [Operators: com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} in {{site.data.keyword.streamsshort}} product documentation.

##Messaging Toolkit
{: #messaging notoc}

The Messaging Toolkit (com.ibm.streamsx.messaging) project is an open source {{site.data.keyword.streamsshort}} toolkit project. It is focused on the development of operators and functions that help you use {{site.data.keyword.streamsshort}} to interact with messaging systems such as Kafka, JMS, XMS, and MQTT.

This toolkit is embedded in {{site.data.keyword.streamsshort}} and it is available in your {{site.data.keyword.streamsshort}} development environment.

The following table lists operators provided by the Messaging Toolkit.


| ***Compatible operators*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink with Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*Table 3. Operators that are compatible with the Messaging Toolkit*

For more information about the Messaging Toolkit compatible operators, see [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} in [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

You can download newer versions of the toolkit, with enhancements and additional operators, from [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. After you download the toolkit, build it (if necessary) and install it on your {{site.data.keyword.streamsshort}} development environment.

For information about toolkit restrictions, see [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

**Note**: To use JMSSource, JMSSink, XMSSource, XMSSink with WebSphere MQ, complete these required steps in your development environment:

1. Go to [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} and download the Messaging Toolkit (com.ibm.streamsx.messaging) version 3.0.0 or later on your development environment.
2. Use version 5.1.0 or later version of the toolkit to build your application.
3. Put the required .bindings file in the `/etc` directory of your application to include it in the {{site.data.keyword.streamsshort}} application bundle.
