---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 CF 应用程序进行运行时应用程序日志记录
{: #logging_writing_to_log_from_cf_app}

在 {{site.data.keyword.Bluemix}} 中，要持久存储 Cloud Foundry 应用程序及其运行时的日志数据，必须将日志写入 STDOUT 和 STDERR。
{:shortdesc}

在 {{site.data.keyword.Bluemix_notm}} 中，会自动收集 STDOUT 和 STDERR 日志记录：

* STDOUT（标准输出）提供常规信息。  
* STDERR（标准错误）提供包含错误消息和其他诊断警告在内的信息。 

Loggregator 会自动选取标准输出和标准错误数据。Loggregator 是用于从 Cloud Foundry 内部转发日志的组件。 

例如： 

对于 **Liberty Cloud Foundry 应用程序**，Loggregator 会自动选取 Liberty 服务器的缺省 console.log。 

* console.log 包含从 JVM 进程重定向的 STDOUT 和 STDERR。如果使用缺省 consoleLogLevel 配置，控制台输出将包含重大事件和错误。如果使用缺省 copySystemStreams 配置，那么控制台输出还会包含写入 system.out 和 system.err 流的所有消息。控制台输出始终包含由 JVM 进程直接写入的消息，例如 -verbose:gc 输出。可以通过 server.xml 调整 Liberty 的日志记录级别。
* consoleLogLevel 会设置 console.log 处理程序的过滤级别。将 consoleLogLevel 设置为 INFO 时，即表示将所有 INFO、AUDIT、WARNING 和 ERROR 消息都配置为写入 console.log 文件。**注：**FINE、FINER 和 FINEST 日志条目只会写入 trace.log 文件。

有关 Liberty for Java™ 应用程序的更多信息，请参阅 [Liberty Profile: Logging and Trace ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}。

对于 **Node.js Cloud Foundry 应用程序**，可以使用内置控制台日志记录模块来配置对 {{site.data.keyword.Bluemix}} 中的运行时的日志记录。可以将消息同时放入 stdout 和 stderr：

* console.log('message') 会将消息发送到 STDOUT 流
* console.error('error_message') 会将错误发送到 STDERR 流

有关 Node.js 应用程序的更多信息，请参阅 [How to log in node.js ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}。


有关 **Ruby on Rails 应用程序**的更多信息，请参阅 [The Logger ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}。

下表列出了某些应用程序运行时日志与 Loggregator 自动选取的日志之间的映射：

| **运行时** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log 和 console.info | console.error 和 console.warn |
| Ruby | stdout| stderr |
{: caption="表 1. 某些应用程序运行时日志与 Loggregator 自动选取的日志之间的映射" caption-side="top"}

