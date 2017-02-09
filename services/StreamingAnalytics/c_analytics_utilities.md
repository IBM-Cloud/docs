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

#Compatible analytics and utilities
{: #c_analytics_utilities}



These analytics toolkits and utilities are compatible with {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

##SPSS Analytics Toolkit

The SPSS Analytics Toolkit contains {{site.data.keyword.streamsshort}} operators that integrate with SPSS Modeler and SPSS Collaboration and Deployment Services products to implement various aspects of SPSS Modeler predictive analytics in your {{site.data.keyword.streamsshort}} applications.

To use the operators from the SPSS toolkit in your SPL application, you must install SPSS Solution Publisher on your {{site.data.keyword.streamsshort}} development environment as described in [Support for SPSS Analytics Toolkit in  {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}.

The following table lists operators provided by the SPSS Analytics Toolkit.


| ***Compatible operators*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*Table 1. Operators that are compatible with the SPSS Analytics Toolkit*


##Complex Event Processing Toolkit

The Complex Event Processing Toolkit (com.ibm.streams.cep) provides the MatchRegex operator to perform complex event processing.

For more information, see [Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

Complex Event Processing (CEP) uses patterns to detect composite events in streams of tuples. For example, CEP can be used to detect stock price patterns, routing patterns in transportation applications, or user behavior patterns in web commerce settings. 

##TimeSeries Toolkit

The operators and functions in the TimeSeries Toolkit (com.ibm.streams.timeseries) condition, analyze, and model time series data. 

A time series is a sequence of numerical data that represent the value of an object or multiple objects over time. For example, you can have time series that contain: the monthly electricity usage that is collected from smart meters; daily stock prices and trading volumes; ECG recordings; seismographs; or network performance records. Time series have a temporal order and this temporal order is the foundation of all time series analysis algorithms.

The toolkit also provides a set of functions that you can see to generate time series for test and validation purposes. 

The following table lists operators provided by the TimeSeries Toolkit.

| ***Compatible operators*** |              								 |
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
| `GAMLearner `		 	 	       |	`STD2`			           			 |
| `GAMScorer` 	   			     |	`TSWindowing`	        	 		 |
| `GMM`     	 			         | 	`VAR2`			 	          		 |

*Table 2. Operators that are compatible with the TimeSeries Toolkit*

For a detailed list and of the TimeSeries Toolkit compatible operators, see [Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

For information about toolkit restrictions, see [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Geospatial Toolkit

The Geospatial Toolkit (com.ibm.streams.geospatial) includes operators and functions that facilitate efficient processing and indexing of location data. For example, with Global Positioning System (GPS) location data, you can track the movement of entities in or around an area of interest, or calculate spatial relationships between different features on the Earth.


The following table lists operators provided by the Geospatial Toolkit.

  
| ***Compatible operators*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*Table 3. Operators that are compatible with the Geospatial Toolkit*

For more information, see [Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

##HDFS for {{site.data.keyword.Bluemix_short}} toolkit

The HDFS for {{site.data.keyword.Bluemix_short}} toolkit (com.ibm.streamsx.hdfs.bluemix) is a special version of the HDFS toolkit that adds support for connecting to IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}.

The following table lists operators provided by the HDFS Toolkit.


| ***Compatible operators*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*Table 4. Operators that are compatible with the HDFS Toolkit*

For more information on how to use this toolkit see [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}.

##JSON toolkit

The JSON toolkit (com.ibm.streamsx.json) provides JSON support for SPL, and standard transforms between SPL values and JSON objects. 

The following table lists operators provided by the JSON Toolkit.


| ***Compatible operators*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*Table 5. Operators that are compatible with the JSON Toolkit*


For more information, see [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

##JDBC toolkit

The JDBC toolkit (com.ibm.streams.jdbc) enables {{site.data.keyword.streaminganalyticsshort}} to communicate with more {{site.data.keyword.Bluemix_short}} database services such as SQL Database, dashDB, etc.

The toolkit includes the JDBCRun operator. For more information, see [Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} and [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

##R-project Toolkit

The R-project Toolkit (com.ibm.streams.rproject) includes the RScript operator, which you can use to run R commands and apply complex data mining algorithms to detect patterns of interest in data streams.

For more information, see [Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.


##Rules compiler

The Rules compiler (com.ibm.streams.rulescompiler) toolkit supports the conversion of business rules that are written in ODM into SPL that can be used in {{site.data.keyword.streamsshort}} applications.

For more information, see [Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

##Text Toolkit

The Text Toolkit (com.ibm.streams.text) includes the `TextExtract` and `SentimentExtractoroperator`, which extracts information from text data.

For more information, see [Operator TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

For information about toolkit restrictions, see [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Mining Toolkit

The Mining Toolkit (com.ibm.streams.mining) includes operators that you can use to mine data streams by applying models. Mining data streams to extract relevant information or intelligence is critical for most stream processing applications that range from fraud detection, to customer segmentation, to churn or intrusion prevention.

The following table lists operators provided by the Mining Toolkit.


| ***Compatible operators*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 | 
| `Clustering`			       	 |
| `Regression`			       	 |

*Table 6. Operators that are compatible with the Mining Toolkit*

For more information, see [Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.

For information about toolkit restrictions, see [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Telecommunications Event Data Analytics (TEDA) Toolkit

The Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) provides a set of generic operators that are used in telecommunications applications, and it also provides an application framework to set up new file-to-file applications. These applications are based on code templates and support customization, configurable parallel processing, graceful application shutdown, and reliable file processing.

The following table lists operators provided by the Telecommunications Event Data Analytics Toolkit.


| ***Compatible operators*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*Table 7. Operators that are compatible with the TEDA Toolkit*

**Note**: The `ASN1Encode`, `CSVParse`, `ASN1Parse`, and `StructureParse` operators have configuration files that are needed during compile-time only.

For more information, see [Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.


##Topology toolkit

The Topology toolkit provides support to build {{site.data.keyword.streamsshort}} applications in the following programming languages:

* Python: The Python Application API is a module that allows the definition and execution of streaming applications implemented in Python. Applications use Python code to process tuples (Python objects).
* Java: The Java Application API is a library that allows the definition and execution of streaming applications implemented in Java. 
* Scala Support: The provided Java Application API supports applications written in Scala.
* SPL: Publish and Subscribe operators provide the mechanism to exchange streams between applications regardless of the tier implementation language. SPL types allow interchange with applications implemented in other languages.

The following table lists operators provided by the Topology Toolkit.


| ***Compatible operators*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*Table 8. Operators that are compatible with the Topology Toolkit*

For more information, see [Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} in the {{site.data.keyword.streamsshort}} product documentation.
