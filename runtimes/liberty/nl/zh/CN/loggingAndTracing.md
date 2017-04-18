---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 日志记录和跟踪
{: #logging_tracing}

## 日志文件
{: #log_files}

标准 Liberty 日志（例如 messages.log 或 ffdc directory）位于 IBM Bluemix 中每个应用程序实例的 logs 目录下。这些日志可以从 IBM Bluemix 控制台进行访问，也可以使用 cf logs 和 cf files 命令进行访问。例如，要查看 messages.log 文件，请运行以下命令：
```
$ cf files <yourappname> logs/messages.log
```
{: codeblock}

日志级别及其他跟踪选项可以通过 Liberty 配置文件进行设置。有关更多信息，请参阅 [Liberty 概要文件：跟踪和日志记录](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0)。还可以使用 IBM Bluemix 控制台调整对运行中应用程序实例的跟踪。

## 使用跟踪和转储功能
{: #using_trace_and_dump}

在 IBM Bluemix 用户界面中有跟踪和转储功能。
* 使用跟踪可查看和更新有关运行中应用程序实例的 Liberty 日志记录 traceSpecification。
* 使用转储可创建在运行中应用程序实例上的线程和堆转储。

要执行此操作，请在用户界面中选择 Liberty 应用程序。在导航中的“运行时”类别下，可以打开实例详细信息。选择一个或多个实例。在“操作”菜单中，可以选择 TRACE 或 DUMP。

## 下载转储文件
{: #download_dumps}

<strong>先决条件：</strong>
* [安装 CF CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [安装 Diego-Enabler 插件](https://github.com/cloudfoundry-incubator/Diego-Enabler)（如果应用程序在 Diego 中运行的话）

<strong>如果应用程序在 DEA 中运行，请使用以下步骤：</strong>
  
1. 获取 app_guid
```
$ cf app <app_name> --guid
```

2. 下载转储文件
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>如果应用程序在 Diego 中运行，请使用以下步骤：</strong>
  
1. 获取 app_guid
```
$ cf app <app_name> --guid
```

2. 获取 app_ssh_endpoint(host and port) 和 app_ssh_host_key_fingerprint
```
$ cf curl /v2/info
```

3. 为 scp 命令获取 ssh-code
```
$ cf ssh-code
```

4. scp 远程转储文件到本地，提示输入密码时使用 ssh-code
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

有关更多详细信息，请参阅[使用SSH 访问应用程序](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)


# 相关链接
{: #rellinks}
## 常规
{: #general}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

