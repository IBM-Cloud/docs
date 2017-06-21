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

#Adaptadores compatíveis
{: #c_compatible_adapters}


Um kit de ferramentas é um conjunto de artefatos organizados em um pacote. Os kits de ferramentas tornam
as funções e os operadores primitivos ou composto reutilizáveis em diferentes aplicativos.
{:shortdesc}

##Kit de ferramentas de Internet
{: #internet notoc}

O Internet Toolkit (com.ibm.streamsx.inet) fornece suporte para protocolos da Internet comuns. Esse kit de ferramentas está integrado ao {{site.data.keyword.streamsshort}} e está disponível em seu ambiente
de desenvolvimento do {{site.data.keyword.streamsshort}}.

A tabela a seguir lista os operadores fornecidos pelo Internet Toolkit.


| ***Operadores compatíveis*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*Tabela 1. Operadores que são compatíveis com o Internet Toolkit*

**Nota**: os operadores marcados com um asterisco (*) funcionam no ambiente de nuvem quando usados com um cliente que também está em
execução no {{site.data.keyword.Bluemix_short}}.

Para obter mais informações sobre operadores compatíveis do Internet Toolkit, veja
[Operadores: IBMStreams com.ibm.streamsx.inet
Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} em [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

É possível fazer download das versões mais recentes do kit de ferramentas, com aprimoramentos e
operadores adicionais, por meio do [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. Após você fazer download do kit de
ferramentas, compile-o (se necessário) e instale-o em seu ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}.

##IoT Integration Toolkit
{: #iot notoc}

O IoT Integration Toolkit (com.ibm.streamsx.iot) fornece conectividade com o {{site.data.keyword.iot_full}}. Os
aplicativos {{site.data.keyword.streamsshort}} podem usar esse kit de ferramentas para fornecer analítica em tempo real com relação a todos os eventos de
potencialmente milhares de dispositivos, incluindo o envio de comandos para dispositivos específicos com base na analítica.

A tabela a seguir lista os operadores fornecidos pelo IoT Integration Toolkit.


| ***Operadores compatíveis*** | 							               |
| ---------------------------| --------------------------- |
| `AllDevices` 	   			     |	`IotPlatformBluemix`  		 | 	 	 	
| `CommandPublish`		 	     |	`PublishDeviceCommands`		 |
| `CommandTupleToPayload`	   | 	`PublishDeviceEvents`	 	   |
| `CommandsSubscribe`	 	     | 	`PublishDeviceStatuses`		 |
| `DeviceCommands`	 	 	     |  `Iniciação rápida`				       |
| `DeviceEventExtractData`	 |  `QuickstartDeviceEvents`	 |
| `DeviceEvents`			       |  `SendCommandToDevice`		   |
| `DeviceStatuses`		 	     |  `StatusesSubscribe`			   |
| `EventsSubscribe`			     |  `SubscribeDeviceCommands`	 |
| `IotPlatform`				       |  `ViewAllDevices`			     |

*Tabela 2. Operadores que são compatíveis com o IoT Integration Toolkit*

Para obter mais informações sobre os operadores compatíveis do Kit de ferramentas de integração IoT, consulte
[Operadores: kit de ferramentas
com.ibm.streamsx.iot](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

##Kit de Ferramentas de Sistema de Mensagens
{: #messaging notoc}

O projeto do Messaging Toolkit (com.ibm.streamsx.messaging) é um projeto de kit de ferramentas do {{site.data.keyword.streamsshort}} de software livre. Ele
está focado no desenvolvimento de operadores e funções que o ajudam a usar o {{site.data.keyword.streamsshort}} para interagir com sistemas de mensagens, como
Kafka, JMS, XMS e MQTT.

Esse kit de ferramentas está integrado ao {{site.data.keyword.streamsshort}} e está disponível em seu ambiente
de desenvolvimento do {{site.data.keyword.streamsshort}}.

A tabela a seguir lista os operadores fornecidos pelo Messaging Toolkit.


| ***Operadores compatíveis*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink com Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*Tabela 3. Operadores que são compatíveis com o Messaging Toolkit*

Para obter mais informações sobre operadores compatíveis do Messaging Toolkit, veja
[Operadores: IBMStreams
com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} em [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

É possível fazer download das versões mais recentes do kit de ferramentas, com aprimoramentos e
operadores adicionais, por meio do [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. Após você fazer download do kit de
ferramentas, compile-o (se necessário) e instale-o em seu ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}.

Para obter informações sobre restrições do kit de ferramentas, veja
[Restrições
para os kits de ferramentas especializados do {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

**Nota**: para usar JMSSource, JMSSink, XMSSource, XMSSink com o WebSphere MQ, conclua estas etapas necessárias em seu ambiente de
desenvolvimento:

1. Acesse o [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} e faça download do Messaging Toolkit
(com.ibm.streamsx.messaging) versão 3.0.0 ou mais recente em seu ambiente de desenvolvimento.
2. Use a versão 5.1.0 ou mais recente do kit de ferramentas para construir o seu aplicativo.
3. Coloque o arquivo .bindings necessário no diretório `/etc` de seu aplicativo para incluí-lo no pacote configurável do aplicativo
{{site.data.keyword.streamsshort}}.
