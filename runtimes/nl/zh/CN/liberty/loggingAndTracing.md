---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 日志记录和跟踪
{: #logging_tracing}

*上次更新时间：2016 年 3 月 23 日*

## 日志文件
{: #log_files}

标准 Liberty 日志（例如 messages.log 或 ffdc directory）位于 IBM Bluemix 中每个应用程序实例的 logs 目录下。这些日志可以从 IBM Bluemix 控制台进行访问，也可以使用 cf logs 和 cf files 命令进行访问。例如，要查看 messages.log 文件，请运行以下命令：```
    $ cf files <yourappname> logs/messages.log```
{: codeblock}

日志级别及其他跟踪选项可以通过 Liberty 配置文件进行设置。有关更多信息，请参阅 [Liberty 概要文件：跟踪和日志记录](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0)。还可以使用 IBM Bluemix 控制台调整对运行中应用程序实例的跟踪。

## 使用跟踪和转储功能
{: #using_trace_and_dump}

在 IBM Bluemix 用户界面中有跟踪和转储功能。
* 使用跟踪可查看和更新有关运行中应用程序实例的 Liberty 日志记录 traceSpecification。
* 使用转储可创建和处理在运行中应用程序实例上的线程和堆转储。

要执行此操作，请在用户界面中选择 Liberty 应用程序。在左侧导航中的“运行时”下，可以打开实例详细信息。选择一个或多个实例。在“操作”菜单下，可以选择 TRACE 或 DUMP。

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
