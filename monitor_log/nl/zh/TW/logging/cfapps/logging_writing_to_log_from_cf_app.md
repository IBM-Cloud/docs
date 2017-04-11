---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 透過 CF 應用程式的運行環境應用程式記載
{: #logging_writing_to_log_from_cf_app}

在 {{site.data.keyword.Bluemix}} 中，若要持續保存 Cloud Foundry 應用程式及其運行環境的日誌資料，您必須將日誌寫入 STDOUT 和 STDERR。
{:shortdesc}

在 {{site.data.keyword.Bluemix}} 中，會自動收集 STDOUT 和 STDERR 日誌記錄：

* STDOUT（標準輸出）提供一般資訊。  
* STDERR（標準錯誤）提供包括錯誤訊息和其他診斷警告的資訊。 

日誌聚集器會自動挑選標準輸出和標準錯誤資料。日誌聚集器是一種元件，可轉遞 Cloud Foundry 中的日誌。 

例如， 

對於 **Liberty Cloud Foundry 應用程式**，日誌聚集器會自動挑選 Liberty 伺服器的預設 console.log。 

* console.log 包含來自 JVM 程序的重新導向 STDOUT 和 STDERR。如果您使用預設的 consoleLogLevel 配置，主控台輸出會包含主要事件和錯誤。如果您使用預設的 copySystemStreams 配置，主控台輸出也會包含寫入 system.out 和 system.err 串流的任何訊息。主控台輸出一律包含 JVM 程序直接寫入的訊息，例如 -verbose:gc 輸出。您可以透過 server.xml 來調整 Liberty 的記載層次。
* consoleLogLevel 可設定 console.log 處理程式的過濾層次。當您將 consoleLogLevel 設為 INFO 時，就是將所有 INFO、AUDIT、WARNING 和 ERROR 訊息配置為寫入 console.log 檔案。**附註：** FINE、FINER、FINEST 日誌項目只會寫入 trace.log 檔案。

如需 Liberty for Java™ 應用程式的相關資訊，請參閱 [Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html)。

對於 **Node.js Cloud Foundry 應用程式**，您可以使用內建的主控台記錄模組來為 {{site.data.keyword.Bluemix}} 中的運行環境配置記載功能。您可以將訊息同時放在 stdout 和 stderr 上：

* console.log('message') 會將訊息傳送至 STDOUT 串流
* console.error('error_message') 會將錯誤傳送至 STDERR 串流

如需 Node.js 應用程式的相關資訊，請參閱 [How to log in node.js ](http://docs.nodejitsu.com/articles/intermediate/how-to-log)。


如需 **Ruby on Rails 應用程式** 的相關資訊，請參閱 [The Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger)。

下表列出部分應用程式運行環境日誌與日誌聚集器自動挑選之日誌的對映：

| **運行環境** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log、console.info | console.error、console.warn |
| Ruby | stdout| stderr |
{: caption="表 1. 部分應用程式運行環境日誌及日誌聚集器自動挑選的日誌之間的對映" caption-side="top"}

