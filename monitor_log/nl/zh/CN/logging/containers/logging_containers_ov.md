---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 对 IBM Bluemix Container Service 进行日志记录
{: #logging_containers_ov}

在 {{site.data.keyword.Bluemix}} 中，可以通过 {{site.data.keyword.Bluemix_notm}}“仪表板”、Kibana 以及命令行界面来查看、过滤和分析容器日志。
{:shortdesc}

容器日志使用搜寻器从容器外部进行监视和转发。搜寻器会将数据发送到 {{site.data.keyword.Bluemix_notm}} 中的多租户 Elasticsearch。

**注：**可以在 {{site.data.keyword.Bluemix_notm}} 中分析部署在 {{site.data.keyword.IBM}} 管理的云基础架构中的 Docker 容器的容器日志。

下图显示了 {{site.data.keyword.containershort}} 的日志记录的高级别视图：

![容器的高级别组件概览图](images/logging_containers_ov.jpg "容器的高级别组件概览图")

在 {{site.data.keyword.Bluemix_notm}} 中部署容器时，会自动启用对相应容器的日志记录。


## 用于分析容器日志的方法
{: #logging_containers_ov_methods}
 
可以选择以下任一方法来分析容器的日志：

* 在 {{site.data.keyword.Bluemix_notm}} 中分析日志以查看容器的最新活动。
    
    可以通过可用于每个容器的**监视和日志**选项卡来查看、过滤和分析日志。有关更多信息，请参阅[通过 Bluemix 仪表板分析日志](../logging_view_dashboard.html#analyzing_logs_bmx_ui)。
    
* 在 Kibana 中分析日志以执行高级分析任务。
    
    可以使用 Kibana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来对数据进行监视、搜索、分析和可视化。有关更多信息，请参阅[在 Kibana 中分析日志](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)。

* 通过 CLI 分析日志可使用命令以编程方式管理日志。
    
    可以通过命令行界面使用 **cf ic logs** 命令来查看、过滤和分析日志。有关更多信息，请参阅[通过命令行界面分析日志](../logging_view_cli.html#analyzing_logs_cli)。

## 为容器收集的日志
{: #logging_containers_ov_logs_collected}

缺省情况下，将收集以下日志：

<table>
  <caption>表 1. 日志</caption>
  <tbody>
    <tr>
      <th align="center">日志</th>
      <th align="center">描述</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> 缺省情况下，Docker 消息会存储在容器的 /var/log/messages 文件夹中。此日志包含系统消息。</td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">此日志是 Docker 日志。<br> Docker 日志文件并不存储为容器内部的文件，但无论如何都会进行收集。缺省情况下会收集此日志文件，因为这是用于公开容器的 stdout（标准输出）和 stderr（标准错误）信息的标准 Docker 约定。如果任何容器进程输出到 stdout 或 stderr，那么会收集该信息。</td>
     </tr>
  </tbody>
</table>

要收集其他日志，请在创建容器时添加带有日志文件路径的 **LOG_LOCATIONS** 环境变量。可以添加多个日志文件，各文件之间用逗号分隔。有关更多信息，请参阅[从容器收集非缺省日志数据](logging_containers_other_logs.html#logging_containers_collect_data)。



## 日志保留时间
{: #logging_containers_ov_log_retention}

请考虑有关日志保留时间的以下信息：

* 每天每个空间最多存储 1 GB 的数据。超过该 1 GB 上限的任何日志都会被废弃。每天中午 12:30 UTC 会重置分配的上限。 

    可以通过联系支持人员来提高上限。在支持凭单中，包含用于提高上限的请求的空间标识、新的上限大小以及请求的原因。

* 可搜索最长 7 天最多 7 GB 的数据。达到 7 GB 数据或超过 7 天后，日志数据会进行滚动式覆盖（先进先出）。

