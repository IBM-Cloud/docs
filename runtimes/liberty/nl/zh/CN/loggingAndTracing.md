---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 日志记录和跟踪
{: #logging_tracing}

## 日志文件
{: #log_files}

标准 Liberty 日志（例如 `messages.log` 或 `ffdc` directory）位于 IBM Bluemix 中每个应用程序实例的 `logs` 目录下。这些日志可以从 IBM Bluemix 控制台进行访问，也可以通过 CF CLI 进行访问。例如：

* 要访问应用程序最近的日志，请运行以下命令：

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* 要查看在 DEA 节点上运行的应用程序的 `messages.log` 文件，请运行以下命令：

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* 要查看在 Diego 单元上运行的应用程序的 `messages.log` 文件，请运行以下命令：

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

日志级别及其他跟踪选项可以通过 Liberty 配置文件进行设置。有关更多信息，请参阅 [Liberty 概要文件：跟踪和日志记录](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)。还可以使用 IBM Bluemix 控制台调整对运行中应用程序实例的跟踪。

## 使用跟踪和转储功能
{: #using_trace_and_dump}

可以直接从 Bluemix 控制台针对正在运行的应用程序调整 Liberty 跟踪配置。控制台还提供了请求并下载线程和堆转储的功能。为了调整跟踪配置或请求转储，请在 Bluemix 控制台中选择 Liberty 应用程序，然后在导航中选择`运行时`菜单。在`运行时`视图中，选择实例，然后按*跟踪*或*转储*按钮。如果要调整跟踪级别，请参阅 [Liberty 概要文件：跟踪和日志记录](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)，以获取有关跟踪规范语法的详细信息。

### Diego：通过 SSH 触发转储

对于在 Diego 单元中运行的应用程序，还可以通过 CF CLI 使用 SSH 功能来触发线程和堆转储。例如：

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

有关下载生成的转储文件的详细信息，请参阅下面的文档。

## 下载转储文件
{: #download_dumps}

缺省情况下，各种转储文件会放入应用程序容器的 `dumps` 目录中。

### DEA 应用程序

对于在 DEA 节点中运行的应用程序，请使用“cf files”功能来查看和下载转储文件。

* 要查看生成的转储，请运行以下命令：

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* 要下载转储文件，请运行以下命令：

    1. 获取应用程序 GUID

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. 下载转储文件

      ```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```
      {: codeblock}

### Diego 应用程序

对于在 Diego 单元中运行的应用程序，请使用“cf ssh”功能来查看和下载转储文件。

* 要查看生成的转储，请运行以下命令：

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* 要下载转储文件，请运行以下命令：

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

还可以使用 `scp` 和其他类似工具来查看并下载转储文件。有关更多信息，请参阅 [Accessing Apps with SSH ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
