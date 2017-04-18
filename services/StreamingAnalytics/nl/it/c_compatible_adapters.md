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

# Adattatori compatibili
{: #c_compatible_adapters}


Un toolkit è una serie di risorse utente organizzate in un pacchetto. I toolkit rendono
le funzioni e gli operatori compositi o primitivi riutilizzabili per diverse applicazioni.
{:shortdesc}

## Internet Toolkit

Internet Toolkit (com.ibm.streamsx.inet) fornisce supporto per i protocolli Internet comuni. Questo toolkit è integrato in {{site.data.keyword.streamsshort}} ed è disponibile nel tuo ambiente di sviluppo {{site.data.keyword.streamsshort}}.

La seguente tabella elenca gli operatori forniti da Internet Toolkit.


| ***Operatori compatibili*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*Tabella 1. Operatori compatibili con Internet Toolkit*

**Nota**: gli operatori contrassegnati con un asterisco (*) funzionano nell'ambiente cloud quando utilizzati con un client in esecuzione a sua volta in {{site.data.keyword.Bluemix_short}}.

Per ulteriori informazioni sugli operatori compatibili di Internet Toolkit, vedi [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} in [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Puoi scaricare le nuove versioni del toolkit, con miglioramenti e ulteriori operatori,
da [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. In seguito scarica il toolkit, integralo (se necessario) e installalo
sul tuo ambiente di sviluppo {{site.data.keyword.streamsshort}}.

## IoT Integration Toolkit

IoT Integration Toolkit (com.ibm.streamsx.iot) fornisce connettività con {{site.data.keyword.iot_full}}. Le applicazioni {{site.data.keyword.streamsshort}} possono utilizzare questo toolkit per
fornire l'analisi in tempo reale su tutti gli eventi da centinaia di dispositivi, incluso
l'invio di comandi a specifici dispositivi sulla base dell'analisi.

La seguente tabella elenca gli operatori forniti da IoT Integration Toolkit.


| ***Operatori compatibili*** | 							               |
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

*Tabella 2. Operatori compatibili con IoT Integration Toolkit*

Per ulteriori informazioni sugli operatori compatibili di IoT Integration Toolkit, vedi [Operators: com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

## Messaging Toolkit

Il progetto Messaging Toolkit (com.ibm.streamsx.messaging) è un progetto toolkit  {{site.data.keyword.streamsshort}} open source. È incentrato sullo sviluppo degli operatori e delle funzioni che ti aiutano nell'utilizzo di {{site.data.keyword.streamsshort}} per interagire con i sistemi di messaggistica come
Kafka, JMS, XMS e MQTT. 

Questo toolkit è integrato in {{site.data.keyword.streamsshort}} ed è disponibile nel tuo ambiente di sviluppo {{site.data.keyword.streamsshort}}.

La seguente tabella elenca gli operatori forniti da Messaging Toolkit.


| ***Operatori compatibili*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink with Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*Tabella 3. Operatori compatibili con Messaging Toolkit*

Per ulteriori informazioni sugli operatori compatibili di Messaging Toolkit, vedi [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} in [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Puoi scaricare le nuove versioni del toolkit, con miglioramenti e ulteriori operatori,
da [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. In seguito scarica il toolkit, integralo (se necessario) e installalo
sul tuo ambiente di sviluppo {{site.data.keyword.streamsshort}}.

Per informazioni sulle limitazioni del toolkit, vedi [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

**Nota**: per utilizzare JMSSource, JMSSink, XMSSource, XMSSink con WebSphere MQ, completa la seguente procedura nel tuo ambiente di sviluppo: 

1. Vai a [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} e scarica Messaging Toolkit (com.ibm.streamsx.messaging) versione 3.0.0 o successiva nel tuo ambiente di sviluppo.
2. Utilizza la versione 5.1.0 o successiva del toolkit per creare la tua applicazione.
3. Inserisci il file .bindings necessario nella directory `/etc` della tua applicazione per includerlo nel bundle dell'applicazione {{site.data.keyword.streamsshort}}.
