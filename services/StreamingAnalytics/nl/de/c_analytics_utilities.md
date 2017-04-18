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

# Kompatible Toolkits und Dienstprogramme für die Analyse
{: #c_analytics_utilities}



Diese Toolkits und Dienstprogramme für die Analyse sind mit {{site.data.keyword.streaminganalyticsshort}} kompatibel.
{:shortdesc}

## SPSS Analytics Toolkit

SPSS Analytics Toolkit enthält {{site.data.keyword.streamsshort}}-Operatoren, die mit den Produkten SPSS
Modeler und SPSS Collaboration and Deployment Services integriert werden können, um verschiedene Aspekte
der SPSS Modeler-Vorhersageanalyse in Ihren {{site.data.keyword.streamsshort}}-Anwendungen zu implementieren.

Um die Operatoren aus dem SPSS-Toolkit in Ihrer SPL-Anwendung verwenden zu können, müssen Sie SPSS Solution Publisher in Ihrer {{site.data.keyword.streamsshort}}-Entwicklungsumgebung installieren, wie dies in [Support for SPSS Analytics Toolkit in {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window} beschrieben ist.

Die folgende Tabelle listet Operatoren auf, die vom SPSS Analytics Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*Tabelle 1. Operatoren, die mit dem SPSS Analytics Toolkit kompatibel sind*


## Complex Event Processing Toolkit

Das Complex Event Processing Toolkit (com.ibm.streams.cep) stellt den Operator 'MatchRegex' zur Verfügung, der das Complex Event Processing ermöglicht.

Weitere Informationen finden Sie unter
[Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

Complex Event Processing (CEP) verwendet Muster zur Erkennung zusammengesetzter Ereignisse
in Streams von Tupeln. Beispielsweise kann CEP verwendet werden, um Muster bei Aktienkursen,
Routenmuster in Verkehrsanwendungen oder Verhaltensmuster bei Kunden in Web-Commerce-Einstellungen
zu erkennen. 

## TimeSeries Toolkit

Mit den Operatoren und Funktionen im TimeSeries Toolkit (com.ibm.streams.timeseries) können Zeitreihendaten aufbereitet, analysiert und modelliert werden. 

Eine Zeitreihe ist eine Folge numerischer Daten, die den Wert eines Objekts oder
mehrerer Objekte im Zeitverlauf darstellen. Beispielsweise können Zeitreihen
folgende Daten enthalten: den monatlichen Stromverbrauch, der durch intelligente Messgeräte
erfasst wird, tägliche Aktienkurse und Handelsvolumen, Elektrokardiogramme, seismografische Aufzeichnungen
oder Daten zur Netzleistung. Zeitreihen beinhalten eine bestimmte zeitliche Abfolge. Darauf beruhen
alle Algorithmen der Zeitreihenanalyse.

Das Toolkit stellt auch verschiedene Funktionen zur Verfügung,
die Sie zur Erstellung von Zeitreihen für Test- und Prüfzwecke verwenden können. 

Die folgende Tabelle listet Operatoren auf, die vom TimeSeries Toolkit zur Verfügung gestellt werden.

| **Kompatible Operatoren*** |              								 |
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

*Tabelle 2. Operatoren, die mit dem TimeSeries Toolkit kompatibel sind*

Eine detaillierte Aufstellung und die mit dem TimeSeries Toolkit kompatiblen Operatoren finden Sie unter [Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window} in der Produktdokumentation zu {{site.data.keyword.streamsshort}}.

Weitere Informationen zu den Toolkiteinschränkungen finden Sie unter [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

## Geospatial Toolkit

Das Geospatial Toolkit (com.ibm.streams.geospatial) enthält Operatoren und Funktionen, die die effiziente Verarbeitung und Indexierung von Positionsdaten vereinfachen. Beispielsweise können Sie mit GPS-Positionsdaten
(GPS = Global Positioning System) den jeweiligen Aufenthaltsort von Entitäten in einem bestimmten
Bereich oder in dessen Umgebung verfolgen oder Sie können räumliche Beziehungen zwischen
verschiedenen geografischen Features berechnen.


Die folgende Tabelle listet Operatoren auf, die vom Geospatial Toolkit zur Verfügung gestellt werden.

  
| **Kompatible Operatoren*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*Tabelle 3. Operatoren, die mit dem Geospatial Toolkit kompatibel sind*

Weitere Informationen finden Sie unter
[Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

## HDFS for {{site.data.keyword.Bluemix_short}} Toolkit

Das HDFS for {{site.data.keyword.Bluemix_short}} Toolkit (com.ibm.streamsx.hdfs.bluemix) ist eine spezielle Version des HDFS Toolkit. Diese Version bietet zusätzlich die Möglichkeit zur Anbindung an IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}.

Die folgende Tabelle listet Operatoren auf, die vom HDFS Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*Tabelle 4. Operatoren, die mit dem HDFS Toolkit kompatibel sind*

Weitere Informationen zur Verwendung dieses Toolkits finden Sie unter [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}.

## JSON Toolkit

Das JSON Toolkit (com.ibm.streamsx.json) bietet JSON-Unterstützung für SPL und Standardumsetzungen zwischen SPL-Werten und JSON-Objekten.  

Die folgende Tabelle listet Operatoren auf, die vom JSON Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*Tabelle 5. Operatoren, die mit dem JSON Toolkit kompatibel sind*


Weitere Informationen finden Sie unter
[com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

## JDBC Toolkit

Das JDBC Toolkit (com.ibm.streams.jdbc) gibt {{site.data.keyword.streaminganalyticsshort}} die Möglichkeit, mit mehr {{site.data.keyword.Bluemix_short}}-Datenbankservices zu kommunizieren, wie z. B. SQL Database, dashDB usw.

Das Toolkit enthält den Operator 'JDBCRun'. Weitere Informationen finden Sie unter [Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} and [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window} in der Produktdokumentation zu {{site.data.keyword.streamsshort}}.

## R-project Toolkit

Das R-project Toolkit enthält den Operator 'RScript', den Sie verwenden können, um R-Befehle auszuführen und um komplexe Data-Mining-Algorithmen zur Erkennung relevanter Muster in Datenstreams anzuwenden.

Weitere Informationen finden Sie unter
[Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.


## Rules Compiler

Das Rules Compiler Toolkit (com.ibm.streams.rulescompiler) unterstützt die Konvertierung von in ODM geschriebenen Geschäftsregeln in SPL, die dann in {{site.data.keyword.streamsshort}}-Anwendungen verwendet werden können.

Weitere Informationen finden Sie unter
[Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

## Text Toolkit

Das Text Toolkit (com.ibm.streams.text) enthält die Operatoren `TextExtract` und `SentimentExtractoroperator`, die Informationen aus Textdaten extrahieren.

Weitere Informationen finden Sie unter
[Operator TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

Weitere Informationen zu den Toolkiteinschränkungen finden Sie unter [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

## Mining Toolkit

Das Mining Toolkit (com.ibm.streams.mining) enthält Operatoren, mit denen Sie ein Mining für Datenstreams durch Anwendung von Modellen durchführen können. Das Mining von Datenstreams zur Extraktion relevanter Informationen oder zur Gewinnung bestimmter Erkenntnisse
ist von größter Bedeutung für die meisten Anwendungsfälle bei der Verarbeitung von Streams -
wie z. B. Betrugserkennung, Definition von Kundensegmenten, das Verhindern von Kundenverlust
oder Abwehren unbefugter Zugriffe.

Die folgende Tabelle listet Operatoren auf, die vom Mining Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 | 
| `Clustering`			       	 |
| `Regression`			       	 |

*Tabelle 6. Operatoren, die mit dem Mining Toolkit kompatibel sind*

Weitere Informationen finden Sie unter
[Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.

Weitere Informationen zu den Toolkiteinschränkungen finden Sie unter [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

## Telecommunications Event Data Analytics (TEDA) Toolkit

Das Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) bietet eine Reihe von generischen Operatoren, die in Telekommunikationsanwendungen genutzt werden, und es stellt ein Anwendungsframework zur Verfügung, um neue File-to-File-Anwendungen einzurichten. Diese Anwendungen basieren auf Codevorlagen
und unterstützen die individuelle Anpassung, konfigurierbare Parallelverarbeitung, eine ordnungsgemäße Beendigung
und zuverlässige Dateiverarbeitung.

Die folgende Tabelle listet Operatoren auf, die vom Telecommunications Event Data Analytics Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*Tabelle 7. Operatoren, die mit dem TEDA Toolkit kompatibel sind*

**Hinweis**: Die Operatoren `ASN1Encode`, `CSVParse`, `ASN1Parse` und `StructureParse` haben Konfigurationsdateien, die nur zum Zeitpunkt der Kompilierung benötigt werden.

Weitere Informationen finden Sie unter
[Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} in der
Produktdokumentation zu {{site.data.keyword.streamsshort}}.


## Topology Toolkit

Das Topology Toolkit bietet Unterstützung für die Erstellung von {{site.data.keyword.streamsshort}}-Anwendungen in den folgenden Programmiersprachen:

* Python: Die Python-Anwendungs-API ist ein Modul, mit dem die Definition und Ausführung von
in Python implementierten Streaming-Anwendungen möglich ist. Anwendungen nutzen Python-Code zur Verarbeitung von Tupeln (Python-Objekte).
* Java: Die Java-Anwendungs-API ist eine Bibliothek, mit der die Definition und Ausführung von
in Java implementierten Streaming-Anwendungen möglich ist. 
* Scala-Unterstützung: Die bereitgestellte Java-Anwendungs-API unterstützt in Scala geschrieben Anwendungen.
* SPL: Die Operatoren 'Publish' und 'Subscribe' stellen den Mechanismus zum Austausch von Streams zwischen Anwendungen bereit, und zwar unabhängig von der Schichtimplementierungssprache. SPL-Typen ermöglichen den Austausch mit in anderen Sprachen implementierten Anwendungen.

Die folgende Tabelle listet Operatoren auf, die vom Topology Toolkit zur Verfügung gestellt werden.


| **Kompatible Operatoren*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*Tabelle 8. Operatoren, die mit dem Topology Toolkit kompatibel sind*

Weitere Informationen finden Sie unter [Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} in der Produktdokumentation zu {{site.data.keyword.streamsshort}}.
