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

#Analíticos e utilitários compatíveis
{: #c_analytics_utilities}



Esses kits de ferramentas analíticos e utilitários são compatíveis com o {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

##SPSS Analytics Toolkit

O SPSS Analytics Toolkit contém operadores do {{site.data.keyword.streamsshort}} que se integram aos produtos SPSS Modeler e SPSS Collaboration and
Deployment Services para implementar vários aspectos de análise preditiva do SPSS Modeler em seus aplicativos {{site.data.keyword.streamsshort}}.

Para usar os operadores do kit de ferramentas do SPSS em seu aplicativo SPL, deve-se instalar o SPSS Solution Publisher em seu ambiente de desenvolvimento do {{site.data.keyword.streamsshort}}, conforme descrito em [Suporte para o SPSS Analytics Toolkit no {{site.data.keyword.streaminganalyticsshort}} Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window}.

A tabela a seguir lista os operadores fornecidos pelo SPSS Analytics Toolkit.


| ***Operadores compatíveis*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     | 
| `SPSSRepository`			     |

*Tabela 1. Operadores que são compatíveis com o SPSS Analytics Toolkit*


##Kit de ferramentas de processamento de evento complexo

O Complex Event Processing Toolkit (com.ibm.streams.cep) fornece o operador MatchRegex para executar processamento de evento
complexo.

Para obter mais informações, veja
[Operador
MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

O Processamento de evento complexo (CEP) usa
padrões para detectar eventos compostos em fluxos de tuplas. Por exemplo, o CEP pode ser usado para detectar
padrões de preço de ações, padrões de roteamento em aplicativos de transporte ou padrões de comportamento do usuário em
configurações de comércio da web. 

##Kit de Ferramentas TimeSeries

Os operadores e as funções no TimeSeries Toolkit (com.ibm.streams.timeseries) condicionam, analisam e modelam dados de série temporal. 

Uma série temporal é uma sequência de dados numéricos que representam o valor de um objeto ou
de múltiplos objetos ao longo do tempo. Por exemplo, é possível ter série temporal que contém: o uso mensal
de eletricidade coletada de medidores inteligentes, preços de ações e volumes de negócios diários, registros
de ECG, sismógrafos ou registros de desempenho de rede. Série temporal tem uma ordem temporal que
é a base de todos os algoritmos de análise de série temporal.

O kit de ferramentas também
fornece um conjunto de funções que você pode ver para gerar série temporal para propósitos de teste e
validação. 

A tabela a seguir lista os operadores fornecidos pelo TimeSeries Toolkit.

| ***Operadores compatíveis*** |              								 |
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

*Tabela 2. Operadores que são compatíveis com o TimeSeries Toolkit*

Para obter uma lista detalhada dos operadores compatíveis do TimeSeries Toolkit, veja
[Operadores:
com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

Para obter informações sobre restrições do kit de ferramentas, veja
[Restrições
para os kits de ferramentas especializados do {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Kit de ferramentas geoespacial

O Geospatial Toolkit (com.ibm.streams.geospatial) inclui operadores e funções que facilitam o processamento e a indexação eficientes de dados da
localização. Por exemplo, com
dados da localização do Sistema de posicionamento global (GPS), é possível rastrear o movimento de entidades em uma área
de interesse ou ao redor dela ou calcular relacionamentos espaciais entre diferentes recursos na terra.


A tabela a seguir lista os operadores fornecidos pelo Geospatial Toolkit.

  
| ***Operadores compatíveis*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*Tabela 3. Operadores que são compatíveis com o Geospatial Toolkit*

Para obter mais informações, consulte
[Operadores:
com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

##Kit de ferramentas do HDFS for {{site.data.keyword.Bluemix_short}}

O kit de ferramentas do HDFS for {{site.data.keyword.Bluemix_short}} (com.ibm.streamsx.hdfs.bluemix) é uma versão especial do kit de ferramentas
do HDFS que inclui suporte para conexão com o IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}}.

A tabela a seguir lista os operadores fornecidos pelo HDFS Toolkit.


| ***Operadores compatíveis*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 | 
| `HDFS2DirectoryScan`	  	 |

*Tabela 4. Operadores que são compatíveis com o HDFS Toolkit*

Para obter mais informações sobre como usar esse kit de ferramentas, veja [Introdução ao {{site.data.keyword.streaminganalyticsshort}} e ao BigInsights no {{site.data.keyword.Bluemix_short}} usando HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window}.

##Kit de ferramentas do JSON

O kit de ferramentas do JSON (com.ibm.streamsx.json) fornece suporte de JSON para SPL e conversões padrão entre valores do SPL e objetos
de JSON. 

A tabela a seguir lista os operadores fornecidos pelo JSON Toolkit.


| ***Operadores compatíveis*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     | 

*Tabela 5. Operadores que são compatíveis com o JSON Toolkit*


Para obter mais informações, consulte
[com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window}
na documentação do produto {{site.data.keyword.streamsshort}}.

##Kit de ferramentas do JDBC

O kit de ferramentas do JDBC (com.ibm.streams.jdbc) permite que o {{site.data.keyword.streaminganalyticsshort}} se comunique com mais serviços de banco
de dados do {{site.data.keyword.Bluemix_short}} como SQL Database, dashDB etc.

O kit de ferramentas inclui o operador JDBCRun. Para obter mais informações, veja [Usando o {{site.data.keyword.streaminganalyticsshort}} com {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window} ativado por JDBC e [com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

##Kit de ferramentas R-project

O kit de ferramentas do projeto do R (com.ibm.streams.rproject) inclui o operador RScript, que pode ser usado para executar comandos R e aplicar algoritmos de
mineração de dados complexos para detectar padrões de interesse em fluxos de dados.

Para obter mais informações, consulte
[Operador
RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.


##Compilador de regras

O kit de ferramentas do Compilador de regras (com.ibm.streams.rulescompiler) suporta a conversão de regras de negócios que são gravadas em ODM no SPL que podem
ser usadas em aplicativos {{site.data.keyword.streamsshort}}.

Para obter mais informações, veja
[Operadores:
com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

##Kit de ferramentas de texto

O Text Toolkit (com.ibm.streams.text) inclui o `TextExtract` e o `SentimentExtractoroperator`, que extraem informações dos
dados de texto.

Para obter mais informações, veja
[Operador
TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

Para obter informações sobre restrições do kit de ferramentas, veja
[Restrições
para os kits de ferramentas especializados do {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Kit de Ferramentas de Mineração

O Mining Toolkit (com.ibm.streams.mining) inclui operadores que podem ser usados para extrair fluxos de dados aplicando modelos. A mineração de fluxos de dados para extrair informações
relevantes ou de inteligência é crítica para a maioria dos aplicativos de processamento de fluxo, que varia
de detecção de fraude até segmentação de cliente e prevenção de perda de clientes ou de intrusão.

A tabela a seguir lista os operadores fornecidos pelo Mining Toolkit.


| ***Operadores compatíveis*** |
| ---------------------------|
| `Associações
` 		      	 |
| `Classificação
`       	 	 | 
| `Armazenamento em cluster`			       	 |
| `Regressão`			       	 |

*Tabela 6. Operadores que são compatíveis com o Mining Toolkit*

Para obter mais informações, veja
[Operadores:
com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.

Para obter informações sobre restrições do kit de ferramentas, veja
[Restrições
para os kits de ferramentas especializados do {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window}.

##Kit de ferramentas Telecommunications
Event Data Analytics (TEDA)

O Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) fornece um conjunto de operadores genéricos que são usados em aplicativos de
telecomunicações e também fornece uma estrutura de aplicativo para configurar novos aplicativos de arquivo para arquivo. Esses aplicativos
se baseiam em modelos de código e suportam customização, processamento paralelo configurável, encerramento
normal do aplicativo e processamento de arquivo confiável.

A tabela a seguir lista os operadores fornecidos pelo Telecommunications Event Data Analytics Toolkit.


| ***Operadores compatíveis*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*Tabela 7. Operadores que são compatíveis com o TEDA Toolkit*

**Nota**: os operadores `ASN1Encode`, `CSVParse`, `ASN1Parse` e
`StructureParse` têm arquivos de configuração que são necessários somente durante o tempo de compilação.

Para obter mais informações, consulte
[Operadores:
com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.


##Kit de ferramentas Topology

O kit de ferramentas Topology fornece suporte para construir aplicativos {{site.data.keyword.streamsshort}}
nas linguagens de programação a seguir:

* Python: a API do aplicativo Python é um módulo que permite a definição e a execução de
aplicativos de fluxo implementados em Python. Os aplicativos usam código do Python para processar tuplas (objetos
do Python).
* Java: a API do aplicativo Java é uma biblioteca que permite a definição e a execução de
aplicativos de fluxo implementados em Java. 
* Suporte do Scala: a API do aplicativo Java fornecida suporta aplicativos gravados no Scala.
* SPL: publicar e assinar operadores fornecem o mecanismo para trocar fluxos entre aplicativos, independentemente da linguagem de implementação de camada. Tipos
do SPL permitem troca com aplicativos implementados em outras linguagens.

A tabela a seguir lista os operadores fornecidos pelo Topology Toolkit.


| ***Operadores compatíveis*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 | 
| `Subscribe`		        		 |

*Tabela 8. Operadores que são compatíveis com o Topology Toolkit*

Para obter mais informações, veja
[Operadores:
com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} na documentação do produto {{site.data.keyword.streamsshort}}.
