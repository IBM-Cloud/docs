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

#호환 가능 어댑터
{: #c_compatible_adapters}


툴킷은 패키지로 구성되는 아티팩트 세트입니다. 툴킷은 다양한 애플리케이션에서 함수 및 기본 또는 복합 연산자를 다시 사용할 수 있게 합니다.
{:shortdesc}

##인터넷 툴킷

인터넷 툴킷(com.ibm.streamsx.inet)은 일반 인터넷 프로토콜에 대한 지원을 제공합니다. 이 툴킷은 {{site.data.keyword.streamsshort}}에 임베드되고 {{site.data.keyword.streamsshort}} 개발 환경에서 사용 가능합니다.

다음 표에는 인터넷 툴킷에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** | 							           |
| ---------------------------| ----------------------- |
| `FTPCommand` 	   		 	     |	`HTTPJSONInjection`*   | 	 	 	
|  `FTPPutFile`				       |	`HTTPTupleInjection`*	 |
| `FTPReader`    	 		       | 	`HTTPTupleView`*		   |
| `HTTPGetStream`			       | 	`HTTPXMLInjection`*		 |
| `HTTPGetJSONContent`	 	   |  `HTTPXMLView`*			 	 |
| `HTTPPost`				         |  `WebContext`*				   |
| `InetSource`				       |  `WebSocketInject`			 |
| `HTTPGetXMLContent`		     |  `WebSocketSend`			 	 |

*표 1. 인터넷 툴킷과 호환 가능한 연산자*

**참고**: {{site.data.keyword.Bluemix_short}}에서도 실행 중인 클라이언트와 함께 사용될 때 클라우드 환경에서 별표(*) 함수로 표시된 연산자입니다.

인터넷 툴킷 호환 가능 연산자에 대한 자세한 정보는 [Operators: IBMStreams com.ibm.streamsx.inet Toolkit](http://ibmstreams.github.io/streamsx.inet/com.ibm.streamsx.inet/doc/spldoc/html/toolkits/ix$Operator.html){:new_window}을 참조하십시오([IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}).

개선사항과 추가 연산자를 포함하는 툴킷의 신규 버전은 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}에서 다운로드할 수 있습니다. 툴킷을 다운로드한 후 (필요하면) 빌드하고 {{site.data.keyword.streamsshort}} 개발 환경에 설치하십시오. 

##IoT Integration Toolkit

IoT Integration Toolkit(com.ibm.streamsx.iot)은 {{site.data.keyword.iot_full}}과의 연결성을 제공합니다. {{site.data.keyword.streamsshort}} 애플리케이션은 이 툴킷을 사용하여 잠재적으로 수천 개의 디바이스에서 오는 모든 이벤트에 대해 실시간 분석을 제공할 수 있으며, 분석을 기초로 특정 디바이스에 명령을 전송할 수 있습니다. 

다음 표에는 IoT Integration Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** | 							               |
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

*표 2. IoT Integration Toolkit과 호환 가능한 연산자*

IoT Integration Toolkit 호환 가능 연산자에 대한 자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operators: com.ibm.streamsx.iot Toolkit](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.iot/ix$Operator.html?lang=en){:new_window}을 참조하십시오. 

##메시징 툴킷

메시징 툴킷(com.ibm.streamsx.messaging) 프로젝트는 오픈 소스 {{site.data.keyword.streamsshort}} 툴킷 프로젝트입니다. 이는 Kafka, JMS, XMS 및 MQTT와 같은 메시징 시스템과 상호작용하도록 {{site.data.keyword.streamsshort}}를 사용하게 도와주는 연산자 및 함수의 개발에 중점을 둡니다.  

이 툴킷은 {{site.data.keyword.streamsshort}}에 임베드되고 {{site.data.keyword.streamsshort}} 개발 환경에서 사용 가능합니다.

다음 표에는 메시징 툴킷에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** 		    | 						       |
| ---------------------------------	| ------------------ |
| `Apache ActiveMQ가 있는 JMSSink`   	|	`MQTTSource`  	   | 	 	 	
| `JMSSource`		 	 			            |	`RabbitMQSink`		 |
| `KafkaConsumer`	 				          | `RabbitMQSource`	 |
| `KafkaProducer`	 	 			          | `XMSSource`	       |
| `MQTTSink`	 	 	 			            |  `XMSSink`				 |

*표 3. 메시징 툴킷과 호환 가능한 연산자*

메시징 툴킷 호환 가능 연산자에 대한 자세한 정보는 [Operators: IBMStreams com.ibm.streamsx.messaging Toolkit](http://ibmstreams.github.io/streamsx.messaging/com.ibm.streamsx.messaging/doc/spldoc/html/toolkits/ix$Operator.html){:new_window}을 참조하십시오([IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}).

개선사항과 추가 연산자를 포함하는 툴킷의 신규 버전은 [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}에서 다운로드할 수 있습니다. 툴킷을 다운로드한 후 (필요하면) 빌드하고 {{site.data.keyword.streamsshort}} 개발 환경에 설치하십시오. 

툴킷 제한사항에 대한 정보는 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}를 참조하십시오.

**참고**: WebSphere MQ와 함께 JMSSource, JMSSink, XMSSource, XMSSink를 사용하려면 사용자의 개발 환경에 필요한 해당 단계를 완료하십시오. 

1. [IBMStreams on GitHub](https://github.com/IBMStreams){:new_window}로 이동하여 개발 환경에 메시징 툴킷(com.ibm.streamsx.messaging) 버전 3.0.0 이상을 다운로드하십시오.
2. 애플리케이션을 빌드하려면 5.1.0 버전 이상의 툴킷을 사용하십시오. 
3. {{site.data.keyword.streamsshort}} 애플리케이션 번들에 포함하도록 필수 .bindings 파일을 애플리케이션의 `/etc` 디렉토리에 넣으십시오.
