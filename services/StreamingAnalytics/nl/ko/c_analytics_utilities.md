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

#호환 가능 분석 및 유틸리티
{: #c_analytics_utilities}



해당 분석 툴킷과 유틸리티는 {{site.data.keyword.streaminganalyticsshort}}와 호환 가능합니다.
{:shortdesc}

##SPSS Analytics Toolkit
{: #spss notoc}

SPSS Analytics Toolkit은 {{site.data.keyword.streamsshort}} 애플리케이션에서 SPSS Modeler 예측 분석의 다양한 측면을 구현하려고 SPSS Modeler 및 SPSS Collaboration and Deployment Services 제품과 통합되는 {{site.data.keyword.streamsshort}} 연산자를 포함합니다. 

SPL 애플리케이션에서 SPSS 툴킷의 연산자를 사용하려면 [Support for SPSS Analytics Toolkit in {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}에 설명된 대로 {{site.data.keyword.streamsshort}} 개발 환경에 SPSS Solution Publisher를 설치해야 합니다.

다음 표에는 SPSS Analytics Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     |
| `SPSSRepository`			     |

*표 1. SPSS Analytics Toolkit과 호환 가능한 연산자*


##Complex Event Processing Toolkit
{: #cep notoc}

Complex Event Processing Toolkit(com.ibm.streams.cep)은 복합 이벤트 처리를 수행하기 위해 MatchRegex 연산자를 제공합니다.

자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window}를 참조하십시오.

복합 이벤트 처리(CEP)에서는 튜플 스트림에서 복합 이벤트를 발견하기 위해 패턴을 사용합니다. 예를 들어, CEP는 재고 가격 패턴, 전송 애플리케이션에서 라우팅 패턴, 웹 커머스 설정에서 사용자 동작 패턴을 발견하는 데 사용될 수 있습니다. 

##TimeSeries Toolkit
{: #timeseries notoc}

TimeSeries Toolkit(com.ibm.streams.timeseries) 조건, 분석, 모델 시계열 데이터의 연산자 및 함수입니다.

시계열은 시간 경과에 따라 하나의 오브젝트 또는 다중 오브젝트의 값을 나타내는 일련의 숫자 데이터입니다. 예를 들어 스마트 계량기에서 수집한 월별 전기 사용량, 일일 재고 가격 및 거래 볼륨, ECG 레코딩, 지진계, 또는 네트워크 성능 레코드를 포함하는 시계열을 가질 수 있습니다. 시계열은 시간적 순서이며 이 시간적 순서는 모든 시계열 분석 알고리즘의 기반입니다. 

툴킷은 또한 테스트 및 유효성 검증 목적으로 시계열을 생성하기 위해 볼 수 있는 기능 세트를 제공합니다. 

다음 표에는 TimeSeries Toolkit에서 제공하는 연산자가 나열되어 있습니다.

| ***호환 가능 연산자*** |              								 |
| ---------------------------| ----------------------------  |
| `ARIMA2` 	  	 			       |	`Generator`       		 		 	 | 	
| `AnomalyDetector`		 	     |	`HoltWinters2`			 	       |
| `AutoForecaster2`   		   | 	`IncrementalInterpolate` 	   |
| ` CrossCorrelate2`			     | 	`KMeansClustering`    		 	 |
| `CrossCorrelateMulti`	 	   |	`Kalman`		 			           |
| `DSPFilter2`				       |	`LPC`           						 |
| `DWT2`     	 			         | 	`Normalize`		 		 	         |
| `Distribution`      			 |	`PSAX`		 				           |
| `FFT` 	   	 			         |	`RLSFilter`		 		        	 | 	
| `FMPFilter`    	 		       |	`ReSample`		         			 |
| `GAMLearner`		 	 	       |	`STD2`			           			 |
| `GAMScorer` 	   			     |	`TSWindowing`	        	 		 |
| `GMM`     	 			         | 	`VAR2`			 	          		 |

*표 2. TimeSeries Toolkit과 호환 가능한 연산자*

TimeSeries Toolkit 호환 가능 연산자의 상세 목록은 {{site.data.keyword.streamsshort}} 제품 문서에서 [Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window}를 참조하십시오.

툴킷 제한사항에 대한 정보는 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}를 참조하십시오.

##Geospatial Toolkit
{: #geospatial notoc}

Geospatial Toolkit(com.ibm.streams.geospatial)에는 위치 데이터의 효율적 처리와 색인 작성을 용이하게 하는 연산자와 함수가 포함되어 있습니다. 예를 들어 GPS(Global Positioning System) 위치 데이터를 사용하면 관심 있는 지역 내 또는 주변에서 엔티티의 움직임을 추적하거나 지구의 다양한 특징 사이에서 공간 관계를 계산할 수 있습니다. 


다음 표에는 Geospatial Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*표 3. Geospatial Toolkit과 호환 가능한 연산자*

자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window}을 참조하십시오.

##HDFS for {{site.data.keyword.Bluemix_short}} 툴킷
{: #hdfs notoc}

HDFS for {{site.data.keyword.Bluemix_short}} 툴킷(com.ibm.streamsx.hdfs.bluemix)은 IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}에 연결하기 위한 지원을 추가한 HDFS Toolkit의 특별 버전입니다.

다음 표에는 HDFS Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 |
| `HDFS2DirectoryScan`	  	 |

*표 4. HDFS Toolkit과 호환 가능한 연산자*

이 툴킷을 사용하는 방법에 대한 자세한 정보는 [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}를 참조하십시오.

##JSON Toolkit
{: #json notoc}

JSON Toolkit(com.ibm.streamsx.json)은 SPL에 대한 JSON 지원 및 SPL 값과 JSON 오브젝트 간의 표준 변환을 제공합니다.

다음 표에는 JSON Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     |

*표 5. JSON Toolkit과 호환 가능한 연산자*


자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window}을 참조하십시오.

##JDBC 툴킷
{: #jdbc notoc}

JDBC 툴킷(com.ibm.streams.jdbc)을 사용하면 {{site.data.keyword.streaminganalyticsshort}}가 더 많은 {{site.data.keyword.Bluemix_short}} 데이터베이스 서비스(예: SQL 데이터베이스, dashDB 등)와 통신할 수 있습니다.

툴킷에는 JDBCRun 연산자가 포함됩니다. 자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} 및 [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window}를 참조하십시오.

##R-project Toolkit
{: #rproject notoc}

R-project Toolkit은 RScript 연산자를 포함하며 이를 사용하여 사용자는 R 명령을 실행하고 데이터 스트림에서 관심 있는 패턴을 발견하기 위해 복합 데이터 마이닝 알고리즘을 적용할 수 있습니다.

자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window}를 참조하십시오. 


##규칙 컴파일러
{: #rulescompiler notoc}

규칙 컴파일러(com.ibm.streams.rulescompiler) 툴킷은 ODM으로 작성된 비즈니스 규칙을 {{site.data.keyword.streamsshort}} 애플리케이션에 사용할 수 있는 SPL로 변환하는 것을 지원합니다.

자세한 정보는 {{site.data.keyword.streamsshort}} 제품문서의 [Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window}를 참조하십시오.

##Text Toolkit
{: #text notoc}

Text Toolkit(com.ibm.streams.text)에는 `TextExtract` 및 `SentimentExtractoroperator`가 포함되며 이 연산자는 텍스트 데이터에서 정보를 추출합니다.

자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operator TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window}를 참조하십시오.

툴킷 제한사항에 대한 정보는 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}를 참조하십시오.

##Mining Toolkit
{: #mining notoc}

Mining Toolkit(com.ibm.streams.mining)에는 모델을 적용하여 데이터 스트림을 마이닝하는 데 사용할 수 있는 연산자가 포함됩니다. 관련 정보 또는 인텔리전스를 추출하기 위한 데이터 스트림 마이닝은 사기 감지에서 고객 세분화, 이탈 또는 침입 방지에 이르는 대부분 스트림 처리 애플리케이션에 매우 중요합니다. 

다음 표에는 Mining Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 |
| `Clustering`			       	 |
| `Regression`			       	 |

*표 6. Mining Toolkit과 호환 가능한 연산자*

자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window}을 참조하십시오.

툴킷 제한사항에 대한 정보는 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}를 참조하십시오.

##Telecommunications Event Data Analytics(TEDA) Toolkit
{: #teda notoc}

Telecommunications Event Data Analytics(TEDA) Toolkit(com.ibm.streams.teda)은 전기통신 애플리케이션에 사용되는 일반 연산자 세트를 제공하고 새로운 파일 간(File-to-File) 애플리케이션을 설정하기 위한 애플리케이션 프레임워크를 제공합니다. 이러한 애플리케이션은 코드 템플리트 및 지원 사용자 정의, 구성 가능 병렬 처리, 애플리케이션 정상(graceful) 종료, 안정적 파일 처리를 기반으로 합니다. 

다음 표에는 Telecommunications Event Data Analytics Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*표 7. TEDA Toolkit과 호환 가능한 연산자*

**참고**: `ASN1Encode`, `CSVParse`, `ASN1Parse`, `StructureParse` 연산자는 컴파일 시간에만 필요한 구성 파일을 갖습니다.

자세한 정보는 {{site.data.keyword.streamsshort}} 제품문서의 [Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window}를 참조하십시오. 


##Topology Toolkit
{: #topology notoc}

Topology Toolkit은 다음 프로그래밍 언어로 {{site.data.keyword.streamsshort}} 애플리케이션을 빌드하기 위한 지원을 제공합니다. 

* Python: Python 애플리케이션 API는 Python으로 구현된 스트리밍 애플리케이션의 정의와 실행을 허용하는 모듈입니다. 애플리케이션은 Python 코드를 사용하여 튜플(Python 오브젝트)을 처리합니다. 
* Java: Java 애플리케이션 API는 Java로 구현된 스트리밍 애플리케이션의 정의와 실행을 허용하는 라이브러리입니다. 
* Scala 지원: 제공된 Java 애플리케이션 API는 Scala로 작성된 애플리케이션을 지원합니다.
* SPL: Publish및 Subscribe 연산자는 계층의 구현 언어에 관계없이 애플리케이션 사이에서 스트림을 교환하는 메커니즘을 제공합니다. SPL 유형은 기타 언어로 구현된 애플리케이션과의 상호 교환을 허용합니다.

다음 표에는 Topology Toolkit에서 제공하는 연산자가 나열되어 있습니다.


| ***호환 가능 연산자*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 |
| `Subscribe`		        		 |

*표 8. Topology Toolkit과 호환 가능한 연산자*

자세한 정보는 {{site.data.keyword.streamsshort}} 제품 문서의 [Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window}를 참조하십시오.
