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

#兼容的分析和实用程序
{: #c_analytics_utilities}



以下分析工具箱和实用程序与 {{site.data.keyword.streaminganalyticsshort}} 兼容。
{:shortdesc}

##SPSS Analytics Toolkit

SPSS Analytics Toolkit 包含与 SPSS Modeler 和 SPSS Collaboration and Deployment Services 产品集成的 {{site.data.keyword.streamsshort}} 操作程序，可在您的 {{site.data.keyword.streamsshort}} 应用程序中，实现 SPSS Modeler 预测性分析的各个方面。

要在 SPL 应用程序中，通过 SPSS 工具箱使用操作程序，您必须在 {{site.data.keyword.streamsshort}} 开发环境中安装 SPSS Solution Publisher，如 [{{site.data.keyword.streaminganalyticsshort}} Service 中 SPSS Analytics Toolkit 的支持](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}所述。

下表列出 SPSS Analytics Toolkit 提供的操作程序。


| ***兼容的操作程序*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*表 1. 与 SPSS Analytics Toolkit 兼容的操作程序*


##Complex Event Processing Toolkit

Complex Event Processing Toolkit (com.ibm.streams.cep) 提供 MatchRegex 操作程序，以执行复杂事件处理。

有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的 [MatchRegex 操作程序](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window}。

复杂事件处理 (CEP) 使用模式在元组流中检测组合事件。
例如，CEP 可用于检测股价模式、运输应用程序中的路线模式或 Web 商业设置中的用户行为模式。
 

##TimeSeries Toolkit

TimeSeries Toolkit (com.ibm.streams.timeseries) 中的操作程序和功能可决定、分析时间序列数据，并对该数据进行建模。 

时间序列是数值数据的序列，代表一段时间内一个或多个对象的值。
例如，您的时间序列可以包含：从智能计量表收集的每月用电量；每日股价和交易量；ECG 记录；地震记录；或网络性能记录。
时间序列具有时间顺序，此时间顺序是所有时间序列分析算法的基础。


该工具箱还提供一组功能，您可以查看这些功能，以生成用于测试和验证的时间序列。
 

下表列出 TimeSeries Toolkit 提供的操作程序。

| ***兼容的操作程序*** |              								 |
| ---------------------------| ----------------------------  |
| `ARIMA2` 	  	 			       |	`Generator`       		 		 	 | 	
| `AnomalyDetector`		 	     |	`HoltWinters2`			 	       |
| `AutoForecaster2`   		   | 	`IncrementalInterpolate` 	   |
| `CrossCorrelate2`			     | 	`KMeansClustering`    		 	 |
| `CrossCorrelateMulti`	 	   |	`Kalman`		 			           |
| `DSPFilter2`				       |	`LPC`           						 |
| `DWT2`     	 			         | 	`Normalize`		 		 	         |
| `Distribution`      			 |	`PSAX`		 				           |
| `FFT` 	   	 			         |	`RLSFilter`		 		        	 | 	
| `FMPFilter`    	 		       |	`ReSample`		         			 | 
| `GAMLearner`		 	 	       |	`STD2`			           			 |
| `GAMScorer` 	   			     |	`TSWindowing`	        	 		 |
| `GMM`     	 			         | 	`VAR2`			 	          		 |

*表 2. 与 TimeSeries Toolkit 兼容的操作程序*

有关 TimeSeries Toolkit 兼容的操作程序的详细列表，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window}。

有关工具箱限制的更多信息，请参阅 [{{site.data.keyword.streamsshort}} 专业工具箱的限制](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

##Geospatial Toolkit

Geospatial Toolkit (com.ibm.streams.geospatial) 包括可促进有效处理位置数据并建立索引的操作程序和功能。例如，使用全球定位系统 (GPS) 位置数据，您可以跟踪感兴趣区域中或周围实体的移动，或者计算地球上不同特征之间的空间关系。



下表列出 Geospatial Toolkit 提供的操作程序。

  
| ***兼容的操作程序*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*表 3. 与 Geospatial Toolkit 兼容的操作程序*

有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window}。

##HDFS for {{site.data.keyword.Bluemix_short}} Toolkit

HDFS for {{site.data.keyword.Bluemix_short}} Toolkit (com.ibm.streamsx.hdfs.bluemix) 是 HDFS Toolkit 的特殊版本，可添加连接到 IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}} 的支持。

下表列出 HDFS Toolkit 提供的操作程序。


| ***兼容的操作程序*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*表 4. 与 HDFS Toolkit 兼容的操作程序*

有关如何使用此工具箱的更多信息，请参阅[在 {{site.data.keyword.Bluemix_short}} 上利用 HDFS 开始使用 {{site.data.keyword.streaminganalyticsshort}} 和 BigInsights](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}。

##JSON Toolkit

JSON Toolkit (com.ibm.streamsx.json) 提供 SPL 的 JSON 支持，以及 SPL 值与 JSON 对象之间的标准转换。 

下表列出 JSON Toolkit 提供的操作程序。


| ***兼容的操作程序*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*表 5. 与 JSON Toolkit 兼容的操作程序*


有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的 [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window}。

##JDBC Toolkit

通过 JDBC Toolkit (com.ibm.streams.jdbc) 可使 {{site.data.keyword.streaminganalyticsshort}} 与更多 {{site.data.keyword.Bluemix_short}} 数据库服务（如 SQL Database、dashDB 等）进行通信。

该工具箱包括 JDBCRun 操作程序。有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[使用 {{site.data.keyword.streaminganalyticsshort}} 与启用 JDBC 的 {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} 和 [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window}。

##R-project Toolkit

R-project Toolkit (com.ibm.streams.rproject) 包括 RScript 操作程序，您可以使用该操作程序来运行 R 命令，并应用复杂的数据挖掘算法，以检测对数据流感兴趣的模式。


有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的 [RScript 操作程序](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window}。


##Rules Compiler

Rules Compiler (com.ibm.streams.rulescompiler) 支持将以 ODM 撰写的业务规则转换为可在 {{site.data.keyword.streamsshort}} 应用程序中使用的 SPL。

有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streams.rulescompile](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window}。

##Text Toolkit

Text Toolkit (com.ibm.streams.text) 包括 `TextExtract` 和 `SentimentExtractor` 操作程序，其可从文本数据抽取信息。

有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的 [TextExtract 操作程序](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window}。

有关工具箱限制的更多信息，请参阅 [{{site.data.keyword.streamsshort}} 专业工具箱的限制](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

##Mining Toolkit

Mining Toolkit (com.ibm.streams.mining) 包括您可用于通过应用模型进行数据流挖掘的操作程序。对数据流进行挖掘以抽取相关信息或情报对大部分流处理应用程序来说至关重要，其中包括从欺诈检测到客户细分乃至流失或侵入防护等应用程序。


下表列出 Mining Toolkit 提供的操作程序。


| ***兼容的操作程序*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 | 
| `Clustering`			       	 |
| `Regression`			       	 |

*表 6. 与 Mining Toolkit 兼容的操作程序*

有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window}。

有关工具箱限制的更多信息，请参阅 [{{site.data.keyword.streamsshort}} 专业工具箱的限制](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

##Telecommunications Event Data Analytics (TEDA) Toolkit

Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) 提供一组在电信应用程序中使用的通用操作程序，它还提供一种应用程序框架，可设置新的文件到文件应用程序。
这些应用程序基于代码模板，并支持定制、可配置的并行处理、正常应用程序关闭和可靠的文件处理。


下表列出 Telecommunications Event Data Analytics Toolkit 提供的操作程序。


| ***兼容的操作程序*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*表 7. 与 TEDA Toolkit 兼容的操作程序*

**注**：`ASN1Encode`、`CSVParse`、`ASN1Parse` 和 `StructureParse` 操作程序具有仅在编译时需要的配置文件。


有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window}。


##Topology Toolkit

Topology Toolkit 提供以下列编程语言构建 {{site.data.keyword.streamsshort}} 应用程序的支持：

* Python：Python 应用程序 API 是一个模块，允许定义和执行在 Python 中实现的流式应用程序。应用程序使用 Python 代码处理元组（Python 对象）。

* Java：Java 应用程序 API 是一个库，允许定义和执行在 Java 中实现的流式应用程序。 
* Scala 支持：所提供的 Java 应用程序 API 支持以 Scala 编写的应用程序。
* SPL：Publish 和 Subscribe 操作程序提供在应用程序之间交换数据流的机制，而不管层实现语言。
SPL 类型允许与使用其他语言实现的应用程序进行交换。


下表列出 Topology Toolkit 提供的操作程序。


| ***兼容的操作程序*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*表 8. 与 Topology Toolkit 兼容的操作程序*

有关更多信息，请参阅 {{site.data.keyword.streamsshort}} 产品文档中的[操作程序：com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window}。
