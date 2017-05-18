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

#互換性のある分析およびユーティリティー
{: #c_analytics_utilities}



以下の分析ツールキットおよびユーティリティーは、{{site.data.keyword.streaminganalyticsshort}} と互換性があります。
{:shortdesc}

##SPSS Analytics Toolkit
{: #spss notoc}

SPSS Analytics Toolkit には、SPSS Modeler 製品および SPSS Collaboration and Deployment Services 製品と統合して {{site.data.keyword.streamsshort}} アプリケーションに SPSS Modeler 予測分析のさまざまな側面を実装する、{{site.data.keyword.streamsshort}} 演算子が含まれています。

SPL アプリケーションで SPSS ツールキットからの演算子を使用するには、[Support for SPSS Analytics Toolkit in {{site.data.keyword.streaminganalyticsshort}}
Service](https://developer.ibm.com/streamsdev/docs/spss-in-bluemix-streaming-analytics-service/){:new_window} に説明されているように、SPSS Solution Publisher を {{site.data.keyword.streamsshort}} 開発環境にインストールする必要があります。

以下の表では、SPSS Analytics Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** |
| ---------------------------|
| `SPSSScoring` 	   		     |
| `SPSSPublish`	     	 	     |
| `SPSSRepository`			     |

*表 1. SPSS Analytics Toolkit との互換性のあるオペレーター*


##Complex Event Processing Toolkit
{: #cep notoc}

Complex Event Processing Toolkit (com.ibm.streams.cep) は、複合イベント処理を実行する MatchRegex オペレーターを提供します。

詳細については、
{{site.data.keyword.streamsshort}} 製品資料の [Operator MatchRegex](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.cep/op$com.ibm.streams.cep$MatchRegex.html?lang=en){:new_window} を参照してください。

Complex Event Processing (CEP) では、パターンを使用して、ストリーム・タプル内の複合イベントを検出します。例えば、CEP を使用して、株価のパターン、運輸アプリケーションのルーティング・パターン、あるいは Web Commerce 設定でのユーザー行動パターンを検出できます。

##TimeSeries Toolkit
{: #timeseries notoc}

TimeSeries Toolkit (com.ibm.streams.timeseries) のオペレーターおよび関数は、時系列データの条件付け、分析、およびモデル化を行います。

時系列とは、時間の経過にともなう単一または
複数のオブジェクトの値を表す、一連の数値データを指します。例えば、時系列を計測できるものとして、スマート・メーターから収集される毎月の電気使用量、毎日の株価と出来高、心電図 (ECG) の記録、地震計、ネットワーク・パフォーマンス・レコードなどがあります。時系列には時間的順序があり、この時間的順序がすべての時系列分析アルゴリズムの基盤になります。

このツールキットでは、テストおよび検証の目的で時系列を生成するために使用できる、一連の関数も提供されます。

以下の表では、TimeSeries Toolkit で提供されるオペレーターをリストします。

| ***互換性のあるオペレーター*** |              								 |
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

*表 2. TimeSeries Toolkit との互換性のあるオペレーター*

TimeSeries Toolkit 互換のオペレーターの詳細なリストについては、{{site.data.keyword.streamsshort}} 製品資料の『[Operators: com.ibm.streams.timeseries](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.timeseries/ix$Operator.html?lang=en){:new_window}』を参照してください。

ツールキットの制約事項については、
[Restrictions
for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window} を参照してください。

##Geospatial Toolkit
{: #geospatial notoc}

Geospatial Toolkit (com.ibm.streams.geospatial) には、位置データの処理および索引付けを効率的に行えるようにするオペレーターと関数が含まれています。例えば、全地球測位システム (GPS) の位置データを使用して、対象の地域内または周辺の存在物の動きを追跡したり、地球上のさまざまな地物の空間的な関係を計算したりできます。


以下の表では、Geospatial Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** | 						              		 |
| ---------------------------| ------------------------------|
| `GeoFence` 	   			       |	`OSMXMLGeometrySource`	 	   | 	 		
| `Hangout`				 	         |	`PointMapMatcher`		      	 |
| `OSMCorrelator`    	 	     | 	`SpatialGridIndex`		 	     |
| `OSMPointMatcher`		 	     | 	`SpatialRouter`		 	 	       |

*表 3. Geospatial Toolkit との互換性のあるオペレーター*

詳細については、
{{site.data.keyword.streamsshort}} 製品資料の[
Operators: com.ibm.streams.geospatial](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.geospatial/ix$Operator.html?lang=en){:new_window} を参照してください。

##HDFS for {{site.data.keyword.Bluemix_short}} Toolkit
{: #hdfs notoc}

HDFS for {{site.data.keyword.Bluemix_short}} Toolkit (com.ibm.streamsx.hdfs.bluemix) は、IBM BigInsights for Apache Hadoop for {{site.data.keyword.Bluemix_short}} に接続するためのサポートを追加する、HDFS Toolkit の特別バージョンです。

以下の表では、HDFS Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** |
| ---------------------------|
| `HDFS2FileSource` 	     	 |
| `HDFS2FileSink`     	   	 |
| `HDFS2DirectoryScan`	  	 |

*表 4. HDFS Toolkit との互換性のあるオペレーター*

このツールキットの使用法について詳しくは、 [Get started with {{site.data.keyword.streaminganalyticsshort}} and BigInsights on {{site.data.keyword.Bluemix_short}} using
HDFS](https://developer.ibm.com/bluemix/2016/02/26/streaming-analytics-and-biginsights-using-hdfs/){:new_window} を参照してください。

##JSON Toolkit
{: #json notoc}

JSON Toolkit (com.ibm.streamsx.json) は、SPL に対する JSON サポート、および SPL 値と JSON オブジェクト間の標準変換を提供します。

以下の表では、JSON Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** |
| ---------------------------|
| `JSONToTuple` 	   		     |
| `TupleToJSON`      		     |

*表 5. JSON Toolkit との互換性のあるオペレーター*


詳細については、
{{site.data.keyword.streamsshort}} 製品資料の [com.ibm.streamsx.json](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.json/tk$com.ibm.streamsx.json.html){:new_window} を参照してください。

##JDBC Toolkit
{: #jdbc notoc}

JDBC Toolkit (com.ibm.streams.jdbc) により、{{site.data.keyword.streaminganalyticsshort}} は、追加の {{site.data.keyword.Bluemix_short}} データベース・サービス (SQL Database、dashDB など) と通信できるようになります。

ツールキットは、JDBCRun 演算子を組み込みます。詳しくは、『[Using {{site.data.keyword.streaminganalyticsshort}} with JDBC-enabled {{site.data.keyword.Bluemix_short}}](https://developer.ibm.com/bluemix/2016/01/26/streaming-analytics-with-jdbc-enabled-databases/){:new_window}』および{{site.data.keyword.streamsshort}} 製品資料内の『[com.ibm.streamsx.jdbc](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.jdbc/tk$com.ibm.streamsx.jdbc.html){:new_window}』を参照してください。

##R-project Toolkit
{: #rproject notoc}

R-project Toolkit (com.ibm.streams.rproject) には RScript オペレーターが含まれています。これを使用して R コマンドを実行し、複雑なデータ・マイニング・アルゴリズムを適用して、データ・ストリーム内の対象パターンを検出できます。

詳細については、
{{site.data.keyword.streamsshort}} 製品資料の [
Operator RScript](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rproject/op$com.ibm.streams.rproject$RScript.html?lang=en){:new_window}
を参照してください。


##Rules コンパイラー
{: #rulescompiler notoc}

Rules コンパイラー (com.ibm.streams.rulescompiler) ツールキットでは、ODM で作成されたビジネス・ルールの SPL への変換がサポートされます。SPL は、{{site.data.keyword.streamsshort}} アプリケーションで使用できます。

詳細については、 {{site.data.keyword.streamsshort}} 製品資料の
[Operators: com.ibm.streams.rulescompiler](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.rulescompiler/ix$Operator.html){:new_window} を参照してください。

##Text Toolkit
{: #text notoc}

Text Toolkit (com.ibm.streams.text) には、テキスト・データから情報を抽出する `TextExtract` および `SentimentExtractoroperator` が含まれています。

詳細については、{{site.data.keyword.streamsshort}} 製品資料の
[TextExtract](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.text/ix$Operator.html){:new_window} を参照してください。

ツールキットの制約事項については、
[Restrictions
for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window} を参照してください。

##Mining Toolkit
{: #mining notoc}

Mining Toolkit (com.ibm.streams.mining) には、モデルを適用してデータ・ストリームのマイニングを行うために使用できるオペレーターが含まれています。データ・ストリームのマイニングによって関連情報 (インテリジェンス) を取り出すことは、ほとんどのストリーム処理アプリケーションにとって非常に重要な作業です。この作業には、不正検出から、顧客のセグメンテーション、チャーンや侵入の防止に至るまで様々なものがあります。

以下の表では、Mining Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** |
| ---------------------------|
| `Associations` 		      	 |
| `Classification`       	 	 |
| `Clustering`			       	 |
| `Regression`			       	 |

*表 6. Mining Toolkit との互換性のあるオペレーター*

詳細については、
{{site.data.keyword.streamsshort}} 製品資料の
[
Operators: com.ibm.streams.mining](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.mining/ix$Operator.html?lang=en){:new_window} を参照してください。

ツールキットの制約事項については、
[Restrictions
for the {{site.data.keyword.streamsshort}} specialized toolkits](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-toolkit-restrictions.html){:new_window} を参照してください。

##Telecommunications Event Data Analytics (TEDA) Toolkit
{: #teda notoc}

Telecommunications Event Data Analytics (TEDA) Toolkit (com.ibm.streams.teda) は、遠隔通信アプリケーションに使用される一連の汎用オペレーターを提供します。また、新しいファイル間 (file-to-file) アプリケーションをセットアップするための一連のアプリケーション・フレームワークも提供します。これらのアプリケーションはコード・テンプレートに基づいており、カスタマイズ、構成可能な並列処理、アプリケーションの安全なシャットダウン、および信頼性のあるファイル処理をサポートしています。

以下の表では、Telecommunications Event Data Analytics Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** | 						           |
| ---------------------------| --------------------- |
| `ASN1Encode` 	   		 	     |	`DirectoryWatch`	   | 	 	 	
| `ASN1Parse`				         |	`ExceptionCatcher` 	 |
| `BloomFilter`    	 	    	 | 	`ScheduledBeacon`		 |
| `CSVParse`				         | 	`StructureParse`	 	 |

*表 7. TEDA Toolkit との互換性のあるオペレーター*

**注**: `ASN1Encode`、`CSVParse`、`ASN1Parse`、および `StructureParse` の各オペレーターには、コンパイル時にのみ必要な構成ファイルがあります。

詳細については、 {{site.data.keyword.streamsshort}} 製品資料の
[
Operators: com.ibm.streams.teda](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streams.teda/ix$Operator.html?lang=en){:new_window} を参照してください。


##Topology Toolkit
{: #topology notoc}

このトポロジー・ツールキットは、以下のプログラミング言語で {{site.data.keyword.streamsshort}} アプリケーション
をビルドするためのサポートを提供します。

* Python: Python アプリケーション API は、Python で実装されたストリーミング・アプリケーションの定義および実行を可能にするモジュールです。アプリケーションは、Python コードを使用してタプル (Python オブジェクト) を処理しま
す。
* Java: Java アプリケーション API は、Java で実装されたストリーミング・アプリケーションの定義および実行を可能にするライブラリーです。
* Scala へのサポート: 提供される Java アプリケーション API は、Scala で作成されたアプリケーションをサポートします。
* SPL: Publish 演算子および Subscribe 演算子は、その層の実装言語とは関係なく、アプリケーション間でストリームを交換するメカニズムを提供します。SPL タイプを使用すると、他の言語で実装されたアプリケーションと交換できます。

以下の表では、Topology Toolkit で提供されるオペレーターをリストします。


| ***互換性のあるオペレーター*** |
| ---------------------------|
| `FilteredSubscribe`      	 |
| `Publish`     		      	 |
| `Subscribe`		        		 |

*表 8. Topology Toolkit との互換性のあるオペレーター*

詳細については、 {{site.data.keyword.streamsshort}} 製品資料の [ Operators: com.ibm.streams.topology](http://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.toolkits.doc/spldoc/dita/tk$com.ibm.streamsx.topology/tk$com.ibm.streamsx.topology.html){:new_window} を参照してください。
