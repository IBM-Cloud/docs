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

#相容的分析和公用程式
{: #c_analytics_utilities}



這些分析工具箱和公用程式都與 {{site.data.keyword.streaminganalyticsshort}} 相容。
{:shortdesc}

##SPSS Analytics Toolkit
{: #spss notoc}

SPSS Analytics Toolkit 包含與 SPSS Modeler 和 SPSS Collaboration and Deployment Services 產品整合的 {{site.data.keyword.streamsshort}} 運算子，以實作 {{site.data.keyword.streamsshort}} 應用程式中 SPSS Modeler 預測分析的各種層面。

若要在 SPL 應用程式中使用 SPSS 工具箱的運算子，您必須在 {{site.data.keyword.streamsshort}} 開發環境上安裝 SPSS Solution Publisher（如 [{{site.data.keyword.streaminganalyticsshort}} 服務中的 SPSS Analytics Toolkit 支援](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}中所述）。

下表列出 SPSS Analytics Toolkit 所提供的運算子。


| ***相容的運算子*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     |
| `SPSSRepository`			     |

*表 1. 與 SPSS Analytics Toolkit 相容的運算子*


##Complex Event Processing Toolkit
{: #cep notoc}

Complex Event Processing Toolkit (com.ibm.streams.cep) 提供 MatchRegex 運算子來執行複式事件處理。

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window}。

Complex Event Processing (CEP) 使用型樣來偵測值組串流中的複合事件。例如，CEP 可以用來偵測股價型樣、交通工具應用程式中的路徑型樣，或 Web 商業設定中的使用者行為型樣。

##TimeSeries Toolkit
{: #timeseries notoc}

TimeSeries Toolkit (com.ibm.streams.timeseries) 中的運算子和函數可設定時間序列資料的條件、對其進行分析並建立其模型。

時間序列是一系列的數值資料，代表某個物件或多個物件一段時間的值。例如，您的時間序列可以包含：收集自智慧電表的每月用電量、每日股價和成交量、心電圖記錄、地震儀或網路效能記錄。時間序列具有時間順序，而且這個時間順序是所有時間序列分析演算法的基礎。

工具箱也提供一組函數，供您用來產生時間序列以進行測試和驗證。

下表列出 TimeSeries Toolkit 所提供的運算子。

| ***相容的運算子*** |              								 |
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

*表 2. 與 TimeSeries Toolkit 相容的運算子*

如需 TimeSeries Toolkit 相容運算子的詳細清單，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window}。

如需工具箱限制的相關資訊，請參閱 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

##Geospatial Toolkit
{: #geospatial notoc}

Geospatial Toolkit (com.ibm.streams.geospatial) 所包括的運算子和函數有助於位置資料的有效處理和編製索引作業。例如，使用「全球定位系統 (GPS)」位置資料，您可以追蹤感興趣區域中或周圍之實體的移動，或計算地球上不同特性之間的空間關係。


下表列出 Geospatial Toolkit 所提供的運算子。


| ***相容的運算子*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*表 3. 與 Geospatial Toolkit 相容的運算子*

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window}。

##HDFS for {{site.data.keyword.Bluemix_short}} Toolkit
{: #hdfs notoc}

HDFS for {{site.data.keyword.Bluemix_short}} Toolkit (com.ibm.streamsx.hdfs.bluemix) 是 HDFS 工具箱的特殊版本，支援連接至 IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}。

下表列出 HDFS Toolkit 所提供的運算子。


| ***相容的運算子*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 |
| `HDFS2DirectoryScan`	  	 |

*表 4. 與 HDFS Toolkit 相容的運算子*

如需如何使用此工具箱的相關資訊，請參閱 [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}。

##JSON Toolkit
{: #json notoc}

JSON Toolkit (com.ibm.streamsx.json) 提供 SPL 的 JSON 支援，以及 SPL 值與 JSON 物件之間的標準轉換。

下表列出 JSON Toolkit 所提供的運算子。


| ***相容的運算子*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     |

*表 5. 與 JSON Toolkit 相容的運算子*


如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window}。

##JDBC Toolkit
{: #jdbc notoc}

JDBC Toolkit (com.ibm.streams.jdbc) 可讓 {{site.data.keyword.streaminganalyticsshort}} 與其他 {{site.data.keyword.Bluemix_short}} 資料庫服務（例如 SQL Database、dashDB 等）進行通訊。

此工具箱包括 JDBCRun 運算子。如需相關資訊，請參閱 [Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} 和 {{site.data.keyword.streamsshort}} 產品文件中的 [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window}。

##R-project Toolkit
{: #rproject notoc}

R-project Toolkit (com.ibm.streams.rproject) 所包括的 RScript 運算子可用來執行 R 指令，並套用複式資料採礦演算法來偵測資料串流中感興趣的型樣。

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window}。


##Rules Compiler
{: #rulescompiler notoc}

Rules compiler (com.ibm.streams.rulescompiler) 工具箱支援將以 ODM 寫入的商業規則轉換成可在 {{site.data.keyword.streamsshort}} 應用程式中使用的 SPL。

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window}。

##Text Toolkit
{: #text notoc}

Text Toolkit (com.ibm.streams.text) 所包括的 `TextExtract` 及 `SentimentExtractoroperator` 運算子可從文字資料中擷取資訊。

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operator TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window}。

如需工具箱限制的相關資訊，請參閱 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

##Mining Toolkit
{: #mining notoc}

Mining Toolkit (com.ibm.streams.mining) 所包括的運算子可用來透過套用模型來發掘資料串流。對大部分串流處理應用程式（範圍從詐騙偵測到客戶區隔，再到流失或侵入防護）而言，發掘資料串流來擷取相關資訊或情報十分重要。

下表列出 Mining Toolkit 所提供的運算子。


| ***相容的運算子*** |
| ---------------------------|
| `關聯` 		      	 |
| `分類`       	 	 |
| `叢集作業`			       	 |
| `回歸`			       	 |

*表 6. 與 Mining Toolkit 相容的運算子*

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window}。

如需工具箱限制的相關資訊，請參閱 [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}。

##Telecommunications Event Data Analytics (TEDA) Toolkit
{: #teda notoc}

Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) 提供一組用於電信應用程式的通用運算子，同時提供一個設定新的檔案對檔案應用程式的應用程式架構。這些應用程式是根據程式碼範本，並且支援自訂、可配置的平行處理、循序應用程式關閉，以及可靠的檔案處理。

下表列出 Telecommunications Event Data Analytics Toolkit 所提供的運算子。


| ***相容的運算子*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*表 7. 與 TEDA Toolkit 相容的運算子*

**附註**：`ASN1Encode`、`CSVParse`、`ASN1Parse` 和 `StructureParse` 運算子僅包含編譯時期所需的配置檔。

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window}。


##Topology Toolkit
{: #topology notoc}

Topology Toolkit 支援使用下列程式設計語言來建置 {{site.data.keyword.streamsshort}} 應用程式：

* Python：Python Application API 是一種模組，可定義及執行使用 Python 所實作的串流應用程式。應用程式使用 Python 程式碼來處理值組（Python 物件）。
* Java：Java Application API 是一個程式庫，可定義及執行使用 Java 所實作的串流應用程式。
* Scala 支援：提供的 Java Application API 支援使用 Scala 所寫入的應用程式。
* SPL：Publish 及 Subscribe 運算子提供一種機制，在應用程式之間交換串流，而不論層級實作語言為何。SPL 類型容許與使用其他語言所實作的應用程式進行交換。

下表列出 Topology Toolkit 所提供的運算子。


| ***相容的運算子*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 |
| `Subscribe`		        		 |

*表 8. 與 Topology Toolkit 相容的運算子*

如需相關資訊，請參閱 {{site.data.keyword.streamsshort}} 產品文件中的 [Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window}。
