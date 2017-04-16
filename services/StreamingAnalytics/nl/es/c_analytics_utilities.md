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

# Análisis y programas de utilidad compatibles
{: #c_analytics_utilities}



Los siguientes kits de herramientas y programas de utilidad de análisis son compatibles con {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

## SPSS Analytics Toolkit

El kit SPSS Analytics Toolkit contiene operadores de {{site.data.keyword.streamsshort}} que se integran con los productos SPSS
Modeler y SPSS Collaboration and Deployment Services para implementar varios aspectos del análisis predictivo de SPSS
Modeler en las aplicaciones de {{site.data.keyword.streamsshort}}.

Para utilizar los operadores del kit de herramientas SPSS en su aplicación SPL, instale SPSS Solution Publisher en el entorno de desarrollo de {{site.data.keyword.streamsshort}} tal como se describe en [Soporte para SPSS Analytics Toolkit en {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de SPSS Analytics.


| ***Operadores compatibles*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*Tabla 1. Operadores que son compatibles con el kit de herramientas de SPSS Analytics*


## Complex Event Processing Toolkit

Complex Event Processing Toolkit (com.ibm.streams.cep) proporciona el operador MatchRegex para llevar a cabo procesos de sucesos complejos.

Para obtener más información, consulte [Operador MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

Complex Event Processing (CEP) utiliza patrones para detectar sucesos compuestos en secuencias de tuplas. Por ejemplo, se puede utilizar CEP para detectar patrones en los precios de la bolsa, patrones de rutas en aplicaciones de transporte o patrones de comportamiento de los usuarios en parámetros de comercio web. 

## TimeSeries Toolkit

Los operadores y funciones de TimeSeries Toolkit (com.ibm.streams.timeseries) condicionan, analizan y modelan datos de series de tiempo. 

Una serie de datos es una secuencia de datos numéricos que representa el valor de un objeto o varios objetos a lo largo del tiempo. Por ejemplo, puede tener series de tiempo que contengan: el uso de electricidad mensual recopilado de medidores inteligentes, precios de la bolsa diarios y volúmenes de operaciones, registros ECG, sismógrafos o registros de rendimiento de red. Las series de tiempo tienen un orden temporal, que es la base de todos los algoritmos de análisis de series temporales.

El kit de herramientas también proporciona un conjunto de funciones que se pueden ver para generar series de tiempo con finalidades de pruebas y validación. 

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de TimeSeries.

| ***Operadores compatibles*** |              								 |
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

*Tabla 2. Operadores que son compatibles con el kit de herramientas de TimeSeries*

Para obtener una lista detallada de operadores de TimeSeries Toolkit compatibles, consulte [Operadores: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

Para obtener información sobre las restricciones del kit de herramientas, consulte [Restricciones de los kits de herramientas especializados de {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

## Geospatial Toolkit

Geospatial Toolkit (com.ibm.streams.geospatial) incluye operadores y funciones que facilitan el procesamiento y la indexación eficientes de datos de ubicación. Por ejemplo, con datos de ubicación GPS, puede rastrear el movimiento de entidades relacionadas con un área de interés o calcular relaciones espaciales entre distintas funciones globales.


La tabla siguiente contiene los operadores que proporciona el kit de herramientas de Geospatial.

  
| ***Operadores compatibles*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*Tabla 3. Operadores que son compatibles con el kit de herramientas de Geospatial*

Para obtener más información, consulte [Operadores: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

## Kit de herramientas de HDFS for {{site.data.keyword.Bluemix_short}}

El kit de herramientas HDFS for {{site.data.keyword.Bluemix_short}} (com.ibm.streamsx.hdfs.bluemix) es una versión especial del kit de herramientas HDFS que añade soporte para conectarse a IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de HDFS.


| ***Operadores compatibles*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*Tabla 4. Operadores que son compatibles con el kit de herramientas de HDFS*

Para obtener más información sobre cómo usar este kit de herramientas, consulte [Iniciación a {{site.data.keyword.streaminganalyticsshort}} y BigInsights en {{site.data.keyword.Bluemix_short}} utilizando HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}.

## Kit de herramientas de JSON

El kit de herramientas de JSON (com.ibm.streamsx.json) proporciona soporte de JSON para SPL y transformaciones estándares entre valores de SPL u objetos JSON. 

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de JSON.


| ***Operadores compatibles*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*Tabla 5. Operadores que son compatibles con el kit de herramientas de JSON*


Para obtener más información, consulte [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

## Kit de herramientas de JDBC

El kit de herramientas de JDBC (com.ibm.streams.jdbc) permite a {{site.data.keyword.streaminganalyticsshort}} comunicarse con más servicios de base de datos de {{site.data.keyword.Bluemix_short}} como SQL Database, dashDB, etc.

El kit de herramientas incluye el operador JDBCRun. Para obtener más información, consulte [Uso de {{site.data.keyword.streaminganalyticsshort}} con {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} con JDBC habilitado y [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

## R-project Toolkit

R-project Toolkit (com.ibm.streams.rproject) incluye el operador RScript, que se puede utilizar para ejecutar mandatos R y aplicar algoritmos de minería de datos complejos para detectar patrones de interés en secuencias de datos.

Para obtener más información, consulte [Operador RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.


## Rules compiler

El kit de herramientas del Rules compiler (com.ibm.streams.rulescompiler) da soporte a la conversión de reglas empresariales escritas en ODM en SPL que se pueden utilizar en aplicaciones {{site.data.keyword.streamsshort}}.

Para obtener más información, consulte [Operadores: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

## Text Toolkit

Text Toolkit (com.ibm.streams.text) incluye `TextExtract` y `SentimentExtractoroperator`, que extrae información de datos de texto.

Para obtener más información, consulte [Operador TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

Para obtener información sobre las restricciones del kit de herramientas, consulte [Restricciones de los kits de herramientas especializados de {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

## Mining Toolkit

Mining Toolkit (com.ibm.streams.mining) incluye operadores que se pueden utilizar para extraer secuencias de datos mediante la aplicación de modelos. La extracción de secuencias de datos para extraer información o inteligencia relevante es fundamental para la mayoría de aplicaciones de procesamiento de secuencias que van desde la detección de fraudes hasta la segmentación de clientes, pasando por la renovación o prevención de intrusión.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de Mining.


| ***Operadores compatibles*** |
| ---------------------------|
| `Asociaciones` 		      	 |
| `Clasificación`       	 	 | 
| `Agrupación en clúster`			       	 |
| `Regresión`			       	 |

*Tabla 6. Operadores que son compatibles con el kit de herramientas de Mining*

Para obtener más información, consulte [Operadores: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.

Para obtener información sobre las restricciones del kit de herramientas, consulte [Restricciones de los kits de herramientas especializados de {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

## Telecommunications Event Data Analytics (TEDA) Toolkit

Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) proporciona un conjunto de operadores genéricos que se utilizan en aplicaciones de telecomunicaciones y que también proporcionan una infraestructura de aplicación para configurar nuevas aplicaciones de archivo a archivo. Estas aplicaciones se basan en plantillas de código y soportan la personalización, el procesamiento paralelo configurable, el cierre estable de aplicaciones y el procesamiento fiable de archivos.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de Telecommunications Event Data Analytics.


| ***Operadores compatibles*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*Tabla 7. Operadores que son compatibles con el kit de herramientas de TEDA*

**Nota**: Los operadores `ASN1Encode`, `CSVParse`, `ASN1Parse` y `StructureParse` tienen archivos de configuración que solo son necesarios durante la fase de compilación.

Para obtener más información, consulte [Operadores: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.


## Kit de herramientas Topology

El kit de herramientas Topology ofrece soporte para crear aplicaciones {{site.data.keyword.streamsshort}} en los siguientes lenguajes de programación:

* Python: la API de aplicaciones Python es un módulo que permite definir y ejecutar aplicaciones en modalidad continua implementadas en
Python. Las aplicaciones utilizan código Python para procesar tuplas (objetos Python).
* Java: la API de aplicaciones Java es una biblioteca que permite definir y ejecutar aplicaciones en modalidad continua implementadas en
Java. 
* Soporte de Scala: la API de aplicación Java proporcionada da soporte a las aplicaciones escritas en Scala.
* SPL: los operadores Publish y Subscribe ofrecen el mecanismo para intercambiar corrientes entre aplicaciones, independientemente del lenguaje de implementación del nivel. Los tipos SPL permiten el intercambio con aplicaciones implementadas en otros lenguajes.

La tabla siguiente contiene los operadores que proporciona el kit de herramientas de Topology.


| ***Operadores compatibles*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*Tabla 8. Operadores que son compatibles con el kit de herramientas de Topology*

Para obtener más información, consulte [Operadores: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} en la documentación del producto {{site.data.keyword.streamsshort}}.
