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

#Funzionalità e analisi compatibili
{: #c_analytics_utilities}



Queste funzionalità e toolkit di analisi sono compatibili con {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

##Toolkit di analisi SPSS

Il toolkit di analisi SPSS contiene operatori {{site.data.keyword.streamsshort}} che si integrano con i prodotti
SPSS Modeler e SPSS Collaboration and Deployment per implementare più aspetti delle analisi predittive SPSS
Modeler nelle tue applicazioni {{site.data.keyword.streamsshort}}.

Per utilizzare gli operatori dal toolkit SPSS nella tua applicazione SPL, devi installare SPSS Solution Publisher nel tuo ambiente di sviluppo {{site.data.keyword.streamsshort}} come descritto in [Support for SPSS Analytics Toolkit in  {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}.

La seguente tabella elenca gli operatori forniti dal Toolkit di analisi SPSS.


| ***Operatori compatibili*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*Tabella 1. Operatori compatibili con il Toolkit di analisi SPSS*


##Complex Event Processing Toolkit

Il toolkit Complex Event Processing (com.ibm.streams.cep) fornisce l'operatore MatchRegex per eseguire l'elaborazione di eventi complessi.

Per ulteriori informazioni, vedi [Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

CEP (Complex Event Processing) utilizza
dei pattern per individuare gli eventi compositi nei flussi di tupla. Ad esempio, CEP può essere utilizzata per individuare
i pattern di quotazione titolo, instradando i pattern alle applicazioni di trasporto o i pattern dei comportamenti utenti nelle impostazioni
di commercio web. 

##TimeSeries Toolkit

Le funzioni e gli operatori in TimeSeries Toolkit (com.ibm.streams.timeseries) condizionano, analizzano e modellano i dati delle serie temporali. 

Una serie temporale è una sequenza di dati numerici che rappresenta il valore di uno o più oggetti
nel tempo. Ad esempio, puoi avere serie temporali che contengono: utilizzo dell'elettricità mensile
raccolta dagli strumenti di misura smart; volumi di vendita e quotazioni titolo giornaliere; registrazioni ECG;
sismografi; o record delle prestazioni di rete. Le serie temporali hanno un ordine temporale che corrisponde alla
base di tutti gli algoritmi di analisi delle serie temporali.

Il toolkit fornisce inoltre
una serie di funzioni che puoi visualizzare per generare le serie temporali per scopi di test e convalida. 

La seguente tabella elenca gli operatori forniti da TimeSeries Toolkit.

| ***Operatori compatibili*** |              								 |
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

*Tabella 2. Operatori compatibili con TimeSeries Toolkit*

Per un elenco dettagliato degli operatori compatibili con TimeSeries Toolkit, vedi [Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

Per informazioni sulle limitazioni del toolkit, vedi [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Geospatial Toolkit

Geospatial Toolkit (com.ibm.streams.geospatial) include operatori e funzioni che facilitano l'indicizzazione e l'elaborazione efficiente dei dati locali. Ad esempio, con i dati di posizione
GPS (Global Positioning System), puoi tracciare i movimenti di entità in un'area di interesse o calcolare
le relazioni spaziali tra diverse funzioni sulla Terra.


La seguente tabella elenca gli operatori forniti da Geospatial Toolkit.

  
| ***Operatori compatibili*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*Tabella 3. Operatori compatibili con Geospatial Toolkit*

Per ulteriori informazioni, vedi [Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

##Toolkit HDFS for {{site.data.keyword.Bluemix_short}}

Il toolkit HDFS for {{site.data.keyword.Bluemix_short}} (com.ibm.streamsx.hdfs.bluemix) è una versione speciale del toolkit HDFS che aggiunge supporto per la connessione a IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}.

La seguente tabella elenca gli operatori forniti da HDFS Toolkit.


| ***Operatori compatibili*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*Tabella 4. Operatori compatibili con HDFS Toolkit*

Per ulteriori informazioni su come utilizzare questo toolkit, vedi [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}.

##Toolkit JSON

Il toolkit JSON (com.ibm.streamsx.json) fornisce il supporto JSON per SPL e le trasformazioni standard tra i valori SPL e gli oggetti JSON. 

La seguente tabella elenca gli operatori forniti dal toolkit JSON.


| ***Operatori compatibili*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*Tabella 5. Operatori compatibili con il toolkit JSON*


Per ulteriori informazioni, vedi [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

##Toolkit JDBC

Il toolkit JDBC (com.ibm.streams.jdbc) permette a {{site.data.keyword.streaminganalyticsshort}} di comunicare con più servizi di database {{site.data.keyword.Bluemix_short}} come SQL Database, dashDB, ecc.

Il toolkit include l'operatore JDBCRun. Per ulteriori informazioni, vedi [Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} e [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

##R-project Toolkit

R-project Toolkit (com.ibm.streams.rproject) include l'operatore RScript,  che puoi utilizzare per eseguire i comandi R e applicare algoritmi di data mining complessi per individuare pattern di interesse nei flussi di dati.

Per ulteriori informazioni, vedi [Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.


##Rules compiler

Il toolkit Rules compiler (com.ibm.streams.rulescompiler) supporta la conversione delle regole di business scritte in ODM nell'SPL che può essere utilizzato nelle applicazioni {{site.data.keyword.streamsshort}}.

Per
ulteriori informazioni, vedi [Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.

##Text Toolkit

Text Toolkit (com.ibm.streams.text) include `TextExtract` e `SentimentExtractoroperator`, che estrae le informazioni dai dati di testo.

Per ulteriori informazioni, vedi [Operator TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} nella documentazione del prodotto
{{site.data.keyword.streamsshort}}.

Per informazioni sulle limitazioni del toolkit, vedi [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Mining Toolkit

Mining Toolkit (com.ibm.streams.mining) include operatori che puoi utilizzare per esaminare i flussi di dati applicando dei modelli. L'esame dei flussi di dati per estrarre le informazioni rilevanti o
di intelligence è fondamentale per la maggior parte delle applicazioni di elaborazione del flusso che vanno
dall'individuazione delle frodi, alla segmentazione cliente, per indicare o prevenire le intrusioni.

La seguente tabella elenca gli operatori forniti da Mining Toolkit.


| ***Operatori compatibili*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 | 
| `Clustering`			       	 |
| `Regression`			       	 |

*Tabella 6. Operatori compatibili con Mining Toolkit*

Per ulteriori informazioni, vedi [Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} nella documentazione del prodotto
{{site.data.keyword.streamsshort}}.

Per informazioni sulle limitazioni del toolkit, vedi [Restrictions for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Telecommunications Event Data Analytics (TEDA) Toolkit

Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) fornisce una serie di operatori generici utilizzati nelle applicazioni di telecomunicazioni e fornisce inoltre un framework dell'applicazione per configurare nuove applicazioni file-to-file. Queste applicazioni si basano
su template di codice e supportano la personalizzazione, l'elaborazione parallela configurabile,
l'arresto normale dell'applicazione e l'elaborazione del file affidabile.

La seguente tabella elenca gli operatori forniti da Telecommunications Event Data Analytics Toolkit.


| ***Operatori compatibili*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*Tabella 7. Operatori compatibili con TEDA Toolkit*

**Nota**: gli operatori `ASN1Encode`, `CSVParse`, `ASN1Parse` e `StructureParse` dispongono di file di configurazione necessari solo durante la fase di compilazione.

Per ulteriori informazioni, vedi [Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.


##Toolkit Topology

Il toolkit Topology fornisce supporto per creare applicazioni {{site.data.keyword.streamsshort}} nei seguenti linguaggi di programmazione:

* Python: l'API di applicazione Python è un modulo che consente la definizione e l'esecuzione di
applicazioni di gestione flussi implementate in Python. Le applicazioni utilizzano il codice Python per elaborare le tuple (oggetti
Python).
* Java: l'API di applicazione Java è una libreria che consente la definizione e l'esecuzione di
applicazioni di gestione flussi implementate in Java. 
* Supporto Scala: l'API di applicazione Java fornita supporta le applicazioni scritte in Scala.
* SPL: gli operatori Publish e Subscribe forniscono il meccanismo per scambiare i flussi tra le applicazioni indipendentemente dal linguaggio di implementazione dei livelli. I tipi SPL consentono l'interscambio con le applicazioni implementate in altri linguaggi.

La seguente tabella elenca gli operatori forniti dal toolkit Topology.


| ***Operatori compatibili*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*Tabella 8. Operatori compatibili con il toolkit Topology*

Per ulteriori informazioni, vedi [Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} nella documentazione del prodotto {{site.data.keyword.streamsshort}}.
