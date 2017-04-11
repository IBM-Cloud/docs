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

#Adaptateurs compatibles
{: #c_compatible_adapters}


Un kit d'outils est un ensemble d'artefacts, qui sont organisés dans un package. Les kits d'outils permettent de réutiliser sur différents plateformes les fonctions ou opérateurs primitifs ou composites.
{:shortdesc}

##Internet Toolkit

Le kit d'outils Internet Toolkit (com.ibm.streamsx.inet) fournit une prise en charge pour les protocoles Internet courants. Cet kit d'outils est intégré à {{site.data.keyword.streamsshort}} et est disponible dans votre environnement de développement {{site.data.keyword.streamsshort}}.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils Internet Toolkit.


| ***Opérateurs compatibles*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*Tableau 1. Opérateurs compatibles avec le kit d'outils Internet Toolkit*

**Remarque** : Les opérateurs marqués d'un astérisque (*) fonctionnent dans l'environnement de cloud quand ils sont utilisés avec un client qui s'exécute aussi dans {{site.data.keyword.Bluemix_short}}.

Pour plus d'informations sur les opérateurs compatibles avec le kit d'outils Internet Toolkit, voir [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} dans [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Vous pouvez télécharger des versions plus récentes du kit d'outils qui comportent des améliorations et des opérateurs supplémentaires, depuis [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. Une fois que vous avez téléchargé le kit d'outils, compilez-le (si nécessaire) et installez-le dans votre environnement de développement {{site.data.keyword.streamsshort}}.

##IoT Integration Toolkit

Le kit d'outils IoT Integration Toolkit (com.ibm.streamsx.iot) fournit une connectivité avec {{site.data.keyword.iot_full}}. Les applications {{site.data.keyword.streamsshort}} peuvent utiliser ce kit d'outils pour fournir une application en temps réel face à tous les événements pouvant provenir de milliers de périphériques, incluant l'envoi de commandes vers des périphériques spécifiques au sujet de cette analyse.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils IoT Integration Toolkit.


| ***Opérateurs compatibles*** | 							               |
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

*Tableau 2. Opérateurs compatibles avec le kit d'outils IoT Integration Toolkit*

Pour plus d'informations sur les opérateurs compatibles avec le kit d'outils IoT Integration, voir [Operators: com.ibm.streamsx.iot](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

##Messaging Toolkit

Le projet Messaging Toolkit (com.ibm.streamsx.messaging) est un projet de kit d'outils {{site.data.keyword.streamsshort}} open source. Il se concentre sur le développement d'opérateurs et de fonctions qui vous aident à utiliser {{site.data.keyword.streamsshort}} pour interagir avec des systèmes de messagerie tels que Kafka, JMS, XMS et MQTT. 

Cet kit d'outils est intégré à {{site.data.keyword.streamsshort}} et est disponible dans votre environnement de développement {{site.data.keyword.streamsshort}}.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils Messaging Toolkit.


| ***Opérateurs compatibles*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `JMSSink avec Apache ActiveMQ`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*Tableau 3. Opérateurs compatibles avec le kit d'outils Messaging Toolkit*

Pour plus d'informations sur les opérateurs compatibles avec le kit d'outils Messaging Toolkit, voir [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window} dans [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}.

Vous pouvez télécharger des versions plus récentes du kit d'outils qui comportent des améliorations et des opérateurs supplémentaires, depuis [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}. Une fois que vous avez téléchargé le kit d'outils, compilez-le (si nécessaire) et installez-le dans votre environnement de développement {{site.data.keyword.streamsshort}}.

Pour plus d'informations sur les restrictions de kit d'outils, voir [Restrictions concernant les kits d'outils spécialisés d'{{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

**Remarque** : Pour utiliser JMSSource, JMSSink, XMSSource, XMSSink avec WebSphere MQ, effectuez la procédure ci-dessous dans votre environnement de développement : 

1. Accédez à [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window} et téléchargez le kit d'outils Messaging Toolkit (com.ibm.streamsx.messaging) version 3.0.0 ou ultérieure dans votre environnement de développement.
2. Utilisez la version 5.1.0 du kit d'outils ou une version ultérieure pour générer votre application.
3. Placez le fichier .bindings requis dans le répertoire `/etc` de votre application pour l'inclure dans le bundle d'applications {{site.data.keyword.streamsshort}}.
