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

#Adaptadores compatibles
{: #c_compatible_adapters}


Un kit de herramientas es un conjunto de artefactos, organizados en un paquete. Los kits de herramientas permiten reutilizar funciones y operadores primitivos o compuestos en distintas aplicaciones.
{:shortdesc}

##Internet Toolkit

Internet Toolkit (com.ibm.streamsx.inet) proporciona soporte para protocolos de Internet comunes. Este kit de herramientas está incrustado en {{site.data.keyword.streamsshort}} y está disponible en el entorno de desarrollo de {{site.data.keyword.streamsshort}}.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de Internet.


| ***Operadores compatibles*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*Tabla 1. Operadores que son compatibles con el kit de herramientas de Internet*

**Nota**: Los operadores marcados con un asterisco (*) funcionan en el entorno en la nube cuando se utilizan con un cliente que también se ejecuta en {{site.data.keyword.Bluemix_short}}.

Para obtener más información sobre operadores compatibles de Internet Toolkit, consulte [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} en [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Puede descargar versiones más recientes del kit de herramientas, con mejoras y operadores adicionales desde [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. Una vez descargado el kit de herramientas, créelo (si es necesario) e instálelo en el entorno de desarrollo de {{site.data.keyword.streamsshort}}.

##IoT Integration Toolkit

IoT Integration Toolkit (com.ibm.streamsx.iot) ofrece conectividad con {{site.data.keyword.iot_full}}. Las aplicaciones {{site.data.keyword.streamsshort}} pueden utilizar este kit de herramientas para ofrecer analíticas en tiempo real sobre todos los sucesos procedentes de miles de dispositivos, incluido el envío de mandatos a dispositivos determinados en función de las analíticas.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de IoT Integration.


| ***Operadores compatibles*** | 							               |
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

*Tabla 2. Operadores que son compatibles con el kit de herramientas de IoT Integration*

Para obtener más información sobre los operadores compatibles con IoT Integration Toolkit, consulte el apartado [Operadores: com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

##Messaging Toolkit

El proyecto Messaging Toolkit (com.ibm.streamsx.messaging) es un proyecto de kit de herramientas de {{site.data.keyword.streamsshort}} de origen abierto. Se centra en el desarrollo de operadores y funciones que le ayudan a utilizar {{site.data.keyword.streamsshort}} para interactuar con sistemas de mensajería como Kafka, JMS, XMS y MQTT. 

Este kit de herramientas está incrustado en {{site.data.keyword.streamsshort}} y está disponible en el entorno de desarrollo de {{site.data.keyword.streamsshort}}.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de Messaging.


| ***Operadores compatibles*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink con Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*Tabla 3. Operadores que son compatibles con el kit de herramientas de Messaging*

Para obtener más información sobre operadores compatibles de Messaging Toolkit, consulte [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} en [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Puede descargar versiones más recientes del kit de herramientas, con mejoras y operadores adicionales desde [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. Una vez descargado el kit de herramientas, créelo (si es necesario) e instálelo en el entorno de desarrollo de {{site.data.keyword.streamsshort}}.

Para obtener información sobre las restricciones del kit de herramientas, consulte [Restricciones de los kits de herramientas especializados de {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

**Nota**: Para utilizar JMSSource, JMSSink, XMSSource, XMSSink con WebSphere MQ, complete estos pasos obligatorios en el entorno de desarrollo: 

1. Vaya a [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} y descargue Messaging Toolkit (com.ibm.streamsx.messaging) versión 3.0.0 o posterior en el entorno de desarrollo.
2. Utilice la versión 5.1.0 o una versión posterior del kit de herramientas para crear su aplicación.
3. Coloque el archivo .bindings necesario en el directorio `/etc` de la aplicación para incluirlo en el paquete de aplicación de {{site.data.keyword.streamsshort}}.
