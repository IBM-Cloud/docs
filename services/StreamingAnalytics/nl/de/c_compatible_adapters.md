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

#Kompatible Adapter
{: #c_compatible_adapters}


Ein Toolkit besteht aus einer Reihe von Artefakten,
die in einem Paket zusammengefasst sind. Toolkits ermöglichen es, dass Funktionen
sowie einfache oder zusammengesetzte Operatoren anwendungsübergreifend wiederverwendet
werden können.
{:shortdesc}

##Internet Toolkit

Das Internet Toolkit (com.ibm.streamsx.inet) unterstützt die gängigen Internetprotokolle. Dieses Toolkit ist in {{site.data.keyword.streamsshort}} integriert und es steht in Ihrer {{site.data.keyword.streamsshort}}-Entwicklungsumgebung zur Verfügung.

Die folgende Tabelle listet Operatoren auf, die vom Internet Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*Tabelle 1. Operatoren, die mit dem Internet Toolkit kompatibel sind*

**Hinweis**: Operatoren, die mit einem Stern (*) gekennzeichnet sind, können in einer Cloudumgebung ausgeführt werden, wenn Sie mit einem Client verwendet werden, der auch in {{site.data.keyword.Bluemix_short}} ausgeführt wird.

Weitere Informationen zu den mit dem Internet Toolkit kompatiblen Operatoren finden Sie unter [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} in [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Sie können neuere Versionen des Toolkits mit Erweiterungen und zusätzlichen Operatoren
von [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} herunterladen. Wenn Sie das Toolkit heruntergeladen haben, erstellen Sie einen Build (falls erforderlich)
und installieren Sie das Toolkit in Ihrer {{site.data.keyword.streamsshort}}-Entwicklungsumgebung.

##IoT Integration Toolkit

Das IoT Integration Toolkit (com.ibm.streamsx.iot) stellt Konnektivität mit {{site.data.keyword.iot_full}} bereit. {{site.data.keyword.streamsshort}}-Anwendungen
können dieses Toolkit nutzen, um Echtzeitanalysen für alle Ereignisse aus
potenziell tausenden von Geräten bereitzustellen; dazu gehört auch das Senden von Befehlen an
bestimmte Geräte auf Basis der Analyse.

Die folgende Tabelle listet Operatoren auf, die vom IoT Integration Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** | 							               |
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

*Tabelle 2. Operatoren, die mit dem IoT Integration Toolkit kompatibel sind*

Weitere Informationen zu den mit
IoT Integration Toolkit kompatiblen Operatoren finden Sie
unter [Operators: com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

##Messaging Toolkit

Das Messaging Toolkit-Projekt (com.ibm.streamsx.messaging) ist ein quelloffenes {{site.data.keyword.streamsshort}}-Toolkit-Projekt. Es dient in erster Linie der Entwicklung von Operatoren und Funktionen, mit denen Sie {{site.data.keyword.streamsshort}}
verwenden können, um mit Messaging-Systemen wie Kafka, JMS, XMS und MQTT zu interagieren. 

Dieses Toolkit ist in {{site.data.keyword.streamsshort}} integriert und es steht in Ihrer {{site.data.keyword.streamsshort}}-Entwicklungsumgebung zur Verfügung.

Die folgende Tabelle listet Operatoren auf, die vom Messaging Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink mit Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*Tabelle 3. Operatoren, die mit dem Messaging Toolkit kompatibel sind*

Weitere Informationen zu den mit dem Messaging Toolkit kompatiblen Operatoren finden Sie unter [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} in [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Sie können neuere Versionen des Toolkits mit Erweiterungen und zusätzlichen Operatoren
von [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} herunterladen. Wenn Sie das Toolkit heruntergeladen haben, erstellen Sie einen Build (falls erforderlich)
und installieren Sie das Toolkit in Ihrer {{site.data.keyword.streamsshort}}-Entwicklungsumgebung.

Weitere Informationen zu den Toolkiteinschränkungen finden Sie unter [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

**Hinweis**: Um JMSSource, JMSSink, XMSSource oder XMSSink mit WebSphere MQ verwenden zu können, führen Sie die folgenden erforderlichen Schritte in Ihrer Entwicklungsumgebung aus: 

1. Navigieren Sie zu [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} und laden Sie das Messaging Toolkit (com.ibm.streamsx.messaging) Version 3.0.0 oder höher in Ihre Entwicklungsumgebung herunter.
2. Verwenden Sie das Toolkit in Version 5.1.0 oder höher, um einen Build Ihrer Anwendung zu erstellen.
3. Stellen Sie die erforderliche Datei mit der Erweiterung .bindings in das Verzeichnis `/etc` Ihrer Anwendung, um sie in das {{site.data.keyword.streamsshort}}-Anwendungsbundle aufzunehmen.
