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

#Kits d'outils d'analyse et utilitaires compatibles
{: #c_analytics_utilities}



Ces kits d'outils d'analyse et utilitaires sont compatibles avec {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

##Kit d'outils d'analyse SPSS

Le kit d'outils d'analyse SPSS contient des opérateurs {{site.data.keyword.streamsshort}} qui s'intègrent avec les services SPSS
Modeler et SPSS Collaboration and Deployment Services pour implémenter différents aspects de l'analyse prédictive SPSS
Modeler dans vos applications {{site.data.keyword.streamsshort}}.

Pour utiliser les opérateurs depuis le kit d'outils SPSS de votre application SPL, vous devez installer SPSS Solution Publisher dans votre environnement de développement {{site.data.keyword.streamsshort}}, comme décrit dans [Support for SPSS Analytics Toolkit in  {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils SPSS Analytics Toolkit.


| ***Opérateurs compatibles*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*Tableau 1. Opérateurs compatibles avec le kit d'outils SPSS Analytics Toolkit*


##Complex Event Processing Toolkit

Le kit d'outils Complex Event Processing Toolkit (com.ibm.streams.cep) fournit l'opérateur MatchRegex pour traiter les événements complexes.

Pour plus d'informations, voir [Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

Le kit CEP (Complex Event Processing) utilise des schémas pour détecter les événements composites dans des flux de tuples. Ainsi, CEP peut être utilisé pour détecter des structures de cours d'actions, des schémas de routage dans des applications de transport ou des schémas de comportement utilisateur dans des paramètres d'e-commerce. 

##TimeSeries Toolkit

Les opérateurs et fonctions du kit d'outils TimeSeries Toolkit (com.ibm.streams.timeseries) conditionnent, analysent et modélisent les données de séries temporelles. 

Une série temporelle est une séquence de données numériques qui représentent la valeur d'un ou de plusieurs objets dans le temps. Ainsi, vous pouvez avoir les séries temporelles suivantes : consommation électrique mensuelle relevée par des compteurs intelligents, cours des actions du jour et volume des transactions, enregistrements ECG, sismographes ou enregistrements de performance réseau. Les séries temporelles disposent d'un ordonnancement temporel qui est la base de tous les algorithmes d'analyse de séries temporelles.

Le kit d'outils fournit aussi un ensemble de fonctions que vous pouvez utiliser pour générer des séries temporelles en vue d'effectuer des opérations de test et de validation. 

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils TimeSeries Toolkit.

| ***Opérateurs compatibles*** |              								 |
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

*Tableau 2. Opérateurs compatibles avec le kit d'outils TimeSeries Toolkit*

Pour une liste détaillée des opérateurs compatibles TimeSeries Toolkit, voir [Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window} dans la documentation du produit {{site.data.keyword.streamsshort}}.

Pour plus d'informations sur les restrictions de kit d'outils, voir [Restrictions concernant les kits d'outils spécialisés d'{{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Geospatial Toolkit

Le kit d'outils Geospatial Toolkit (com.ibm.streams.geospatial) inclut des opérateurs et des fonctions facilitant un traitement et une indexation des données de localisation. Ainsi, avec des données de localisation GPS (Global Positioning System), vous pouvez suivre le mouvement d'entités à l'intérieur ou autour d'une zone d'intéret ou calculer les relations spatiales entre différentes fonctions sur la terre.


Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils Geospatial Toolkit.

  
| ***Opérateurs compatibles*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*Tableau 3. Opérateurs compatibles avec le kit d'outils Geospatial Toolkit*

Pour plus d'informations, voir [Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

##Kit d'outils HDFS for {{site.data.keyword.Bluemix_short}}

Le kit d'outils HDFS for {{site.data.keyword.Bluemix_short}} (com.ibm.streamsx.hdfs.bluemix) est une version spéciale du kit HDFS qui ajoute une prise en charge pour la connexion à IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils HDFS.


| ***Opérateurs compatibles*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*Tableau 4. Opérateurs compatibles avec le kit d'outils HDFS*

Pour plus d'informations sur l'utilisation de ce kit d'outils, voir [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}.

##Kit d'outils JSON

Le kit d'outils JSON (com.ibm.streamsx.json) fournit une prise en charge JSON pour SPL et des transformations standard entre des valeurs SPL et des objets JSON. 

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils JSON.


| ***Opérateurs compatibles*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*Tableau 5. Opérateurs compatibles avec le kit d'outils JSON*


Pour plus d'informations, voir [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

##Kit d'outils JDBC

Le kit d'outils JDBC (com.ibm.streams.jdbc) permet à {{site.data.keyword.streaminganalyticsshort}} de communiquer avec davantage de services de base de données {{site.data.keyword.Bluemix_short}} tels que SQL Database, dashDB, etc.

Le kit d'outils inclut l'opérateur JDBCRun. Pour plus d'informations, voir [Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} et [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window} dans la documentation du produit {{site.data.keyword.streamsshort}}.

##R-project Toolkit

Le kit d'outils R-project Toolkit (com.ibm.streams.rproject) inclut l'opérateur RScript, que vous pouvez utiliser pour exécuter des commandes R et appliquer des algorithmes d'exploration de données complexes pour détecter des zones d'intérêt dans les flux de données.

Pour plus d'informations, voir [Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.


##Rules compiler

Le kit d'outils Rules compiler (com.ibm.streams.rulescompiler) prend en charge la conversion en langage SPL de règles métier écrites en ODM, et qui peuvent être utilisées dans des applications {{site.data.keyword.streamsshort}}.

Pour plus d'informations, voir [Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

##Text Toolkit

Le kit d'outils Text Toolkit (com.ibm.streams.text) inclut les opérateurs `TextExtract` et `SentimentExtractoroperator`, qui extraient des informations à partir de données texte.

Pour plus d'informations, voir [Operators: com.ibm.streams.text](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

Pour plus d'informations sur les restrictions de kit d'outils, voir [Restrictions concernant les kits d'outils spécialisés d'{{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Mining Toolkit

Le kit d'outils Mining Toolkit (com.ibm.streams.mining) inclut des opérateurs que vous pouvez utiliser pour explorer des flux de données en appliquant des modèles. L'exploration des flux de données pour extraire des informations pertinentes est primordiale pour la plupart des applications de traitement de flux chargées d'opérations allant de la détection de fraude, à la segmentation client jusqu'à la prévention d'une perte de clientèle ou d'une intrusion.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils Mining Toolkit.


| ***Opérateurs compatibles*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 | 
| `Clustering`			       	 |
| `Régression`			       	 |

*Tableau 6. Opérateurs compatibles avec le kit d'outils Mining Toolkit*

Pour plus d'informations, voir [Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.

Pour plus d'informations sur les restrictions de kit d'outils, voir [Restrictions concernant les kits d'outils spécialisés d'{{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Telecommunications Event Data Analytics (TEDA) Toolkit

Le kit d'outils Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) fournit un ensemble d'opérateurs génériques qui sont utilisés dans les applications de télécommunications et propose aussi une structure d'application pour définir de nouvelles applications de fichier à fichier. Ces applications, qui reposent sur des modèles de code, prennent en charge la personnalisation, le traitement parallèle configurable, la fermeture d'application sans perte de données et un traitement de fichiers fiable.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils Telecommunications Event Data Analytics Toolkit.


| ***Opérateurs compatibles*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*Tableau 7. Opérateurs compatibles avec le kit d'outils TEDA Toolkit*

**Remarque** : Les opérateurs `ASN1Encode`, `CSVParse`, `ASN1Parse` et `StructureParse` possèdent des fichiers de configuration qui sont nécessaires uniquement pendant la période de compilation.

Pour plus d'informations, voir [Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.


##Kit d'outils Topology

Le kit d'outils Topology fournit une prise en charge pour générer des applications {{site.data.keyword.streamsshort}} dans les langages de programmation suivants :

* Python : l'API d'application Python est un module qui permet de définir et d'exécuter des applications de diffusion en flux continu implémentées en Python. Les applications utilisent un code Python pour traiter les tuples (objets Python).
* Java : l'API d'application Java est une bibliothèque qui permet de définir et d'exécuter des applications de diffusion en flux continu implémentées en Java. 
* Prise en charge Scala : l'API d'application Java prend en charge des applications écrites en Scala.
* SPL : les opérateurs Publish et Subscribe fournissent un mécanisme d'échange de flux entre des applications quel que soit le langage d'implémentation utilisé par le groupe de serveurs d'applications. L'option relative aux types SPL autorise un échange avec des applications implémentées dans d'autres langues.

Le tableau ci-après répertorie les opérateurs fournis par le kit d'outils Topology.


| ***Opérateurs compatibles*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*Tableau 8. Opérateurs compatibles avec le kit d'outils Topology*

Pour plus d'informations, voir [Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} dans la documentation produit {{site.data.keyword.streamsshort}}.
