---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 Kibana 中分析日志
{: #analyzing_logs_Kibana3}

在 {{site.data.keyword.Bluemix}} 中，可以使用 Kibana（一种开放式源代码分析和可视化平台）通过各种图形（例如，图表和表）来监视、搜索、分析和可视化数据。使用 Kibana 可执行高级分析任务。{:shortdesc}

您可以使用以下任何一种方法来启动 Kibana：

* 通过 Cloud Foundry 应用程序仪表板

    可以在 Kibana 中特定 CF 应用程序的上下文中启动到该特定应用程序的日志。
    
    用于过滤仪表板中所显示数据的查询会检索 Cloud Foundry 应用程序的日志条目。Kibana 仪表板缺省显示的日志信息全部与单个 Cloud Foundry 应用程序及其所有实例相关联。有关更多信息，请参阅[通过 {{site.data.keyword.Bluemix}} 仪表板访问 Kibana 仪表板](logging_view_kibana3.html#launch_Kibana_from_bluemix)。

* 通过直接浏览器链接

    您可能希望启动到用于从所提供 {{site.data.keyword.Bluemix}} 空间内的服务聚集数据的定制 Kibana 仪表板。
    
    用于过滤仪表板中所显示数据的查询会检索 {{site.data.keyword.Bluemix}} 组织中空间的日志条目。Kibana 仪表板显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix}} 组织空间内部署的所有资源的记录。有关更多信息，请参阅[通过 Web 浏览器访问 Kibana 仪表板](logging_view_kibana3.html#launch_Kibana_from_browser)。
    
    您还可以更改或除去初始查询以及添加更多查询。有关更多信息，请参阅[在 Kibana 中使用查询过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_query.html#logging_kibana_query)。


Kibana 是一种基于浏览器的界面，在其中可以定制仪表板，随后可用于分析日志数据并执行高级管理任务。 

在 {{site.data.keyword.Bluemix}} 中，可以使用为每个 Cloud Foundry 应用程序以及为组织的每个空间提供的缺省 Kibana 仪表板来分析数据。缺省情况下，这些仪表板会通过一个面板显示最近 24 小时可用的所有数据，该面板中包含一个直方图行和一个事件表行。 

要约束通过任何缺省仪表板显示的信息，可以向缺省仪表板添加查询和过滤器。然后，可以保存仪表板以供未来复用。 

Kibana 仪表板显示的数据由该查询进行控制。要修改仪表板中显示的信息，可以更改该查询，添加多个查询，然后保存仪表板。您可以同时定制、保存和共享多个仪表板。例如，这是 Kibana 显示空间中单个应用程序相关信息的方式。

您还可以通过日志字段（例如，message_type 和 instance_ID）来配置过滤器。有关更多信息，请参阅 [Kibana 日志格式](logging_view_kibana3.html#kibana_log_format_cf)。您可以动态启用或禁用此这些过滤器。仪表板将显示满足所启用的查询和过滤条件的日志条目。有关更多信息，请参阅[在 Kibana 仪表板中过滤数据](logging_view_kibana3.html#filter_data_kibana_dashboard)。

要可视化数据，可以配置面板。Kibana 包含可用于分析信息的不同面板，如表、趋势和直方图。可以在仪表板中添加、除去和重新排列面板。每个面板的用途各不相同。一些面板组织成行，用于提供一个或多个查询的结果。另一些面板则显示文档或定制信息。有关更多信息，请参阅[定制 Kibana 仪表板](logging_view_kibana3.html#customize_kibana_dashboard)。

定制仪表板后，可以从以下任何操作中进行选择：

* 可以保存仪表板以供未来复用。有关更多信息，请参阅[保存 Kibana 仪表板](logging_view_kibana3.html#save_Kibana_dashboard)。

* 可以导出 Kibana 仪表板或提供其直接链接以与其他用户共享。有关更多信息，请参阅[导出和共享 Kibana 仪表板](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash)。

* 可以在 Web 页面中嵌入仪表板。要使用户能够查看嵌入的仪表板，该用户必须具有访问 Kibana 的许可权。

有关更多信息，请参阅 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。

**注：**支持 Kibana 4 和 Kibana 3。但不推荐使用 Kibana 3。


##  通过 Bluemix 仪表板访问 Kibana 仪表板
{: #launch_Kibana_from_bluemix}

用于过滤仪表板中所显示数据的查询会检索 Cloud Foundry 应用程序的日志条目。Kibana 仪表板缺省显示的日志信息全部与单个 Cloud Foundry 应用程序及其所有实例相关联。

要在 Kibana 中查看 Cloud Foundry 应用程序的日志，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。这将打开应用程序详细信息页面。
    
2. 在导航栏中，单击**日志**。这将打开“日志”选项卡。 
    
3. 单击**高级视图**。这将打开 **Kibana 3** 仪表板。

如果未看到任何日志，请调整标题中的时间选取器。

有关定制 Kibana 仪表板的更多信息，请参阅[此博客帖子](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)或 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。

##  通过 Web 浏览器访问 Kibana 仪表板
{: #launch_Kibana_from_browser}

用于过滤仪表板中所显示数据的查询会检索 {{site.data.keyword.Bluemix}} 组织中空间的日志条目。Kibana 仪表板显示的日志信息包括在您登录到的 {{site.data.keyword.Bluemix}} 组织空间内部署的所有资源的记录。

要通过浏览器打开 Kibana 仪表板，请完成以下步骤：

1. 打开 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) 以登录到 Kibana 用户界面。

2. 选择 **Kibana 3** 选项卡以使用 Kibana 3。选择 **Kibana 4** 选项卡以使用 Kibana 4。这将打开缺省 Kibana 仪表板。 

如果未看到任何日志，请调整标题中的时间选取器。

有关定制 Kibana 仪表板的更多信息，请参阅[此博客帖子](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)或 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。



## 在 Kibana 仪表板中过滤数据
{: #filter_data_kibana_dashboard}

在 {{site.data.keyword.Bluemix}} 中，可以使用按每个资源或按 {{site.data.keyword.Bluemix}} 空间提供的缺省 Kibana 仪表板来分析数据。缺省情况下，这些仪表板会显示最近 24 小时可用的所有数据。但是，可以通过仪表板来约束显示的信息。您可以向缺省仪表板添加查询和过滤器，然后保存该仪表板以供未来复用。

在仪表板中，可以添加多个查询和过滤器。一个查询会定义一部分日志条目。过滤器通过包含或排除信息来优化数据选择内容。 

对于 Cloud Foundry 应用程序，以下列表概述了有关如何过滤数据的示例：
* 如果要在日志中查找包含关键项的信息，可以创建查询以按这些项进行过滤。通过 Kibana，可以在仪表板上直观地比较查询。有关更多信息，请参阅[在 Kibana 中使用查询过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_query.html#logging_kibana_query)。

* 如果要查找特定时间段内的信息，可以按时间范围过滤数据。有关更多信息，请参阅[在 Kibana 中按时间过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter)。

* 如果要查找特定实例标识的信息，可以按实例标识过滤数据。有关更多信息，请参阅[在 Kibana 中按实例标识过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id)和[在 Kibana 中按已知应用程序标识过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id)。

* 如果要查找特定组件的信息，可以按组件（日志类型）过滤数据。有关更多信息，请参阅[在 Kibana 中按日志类型过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter)。

* 如果要查找信息（例如错误消息），那么可以按消息类型过滤数据。有关更多信息，请参阅[在 Kibana 中按消息类型过滤 Cloud Foundry 应用程序日志](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter)。

## 定制 Kibana 仪表板
{: #customize_kibana_dashboard}

可定制不同类型的仪表板以可视化并分析数据，例如：
* 单 CF 应用程序仪表板：此仪表板用于显示单个 Cloud Foundry 应用程序的信息。  
* 多 CF 应用程序仪表板：此仪表板用于显示同一 {{site.data.keyword.Bluemix}} 空间内部署的所有 Cloud Foundry 应用程序的信息。 

定制仪表板后，可以配置查询和过滤器以选择要通过仪表板显示的日志数据子集。

要可视化数据，可以配置面板。Kibana 包含可用于分析信息的不同面板，如表、趋势和直方图。可以在仪表板中添加、除去和重新排列面板。每个面板的用途各不相同。一些面板组织成行，用于提供一个或多个查询的结果。另一些面板则显示文档或定制信息。例如，可以配置条形图、饼图或表来对数据进行可视化和分析。  


## 保存 Kibana 仪表板
{: #save_Kibana_dashboard}

要保存定制后的 Kibana 仪表板，请完成以下步骤：

1. 在工具栏中，单击**保存**图标。

2. 输入仪表板的名称。

    **注：**如果尝试使用包含空格的名称来保存仪表板，那么不会保存该仪表板。

3. 在“名称”字段旁边，单击**保存**图标。



## 通过 Kibana 仪表板分析日志
{: #analyze_kibana_logs}

定制 Kibana 仪表板后，可以通过其面板对数据进行可视化和分析。 

要搜索信息，可以将查询置顶或取消置顶。 

* 可以在仪表板中将查询置顶，这将自动激活搜索。
* 要从仪表板中除去内容，可以取消激活查询。

要过滤信息，可以启用或禁用过滤器。 

* 可以选中过滤器中的**切换**复选框 ![用于包含过滤器的切换框](images/logging_toggle_include_filter.jpg) 以启用该过滤器。   
* 可以取消选中过滤器中的**切换**复选框 ![用于包含过滤器的切换框](images/logging_toggle_exclude_filter.jpg) 以禁用该过滤器。 

仪表板中的图形和图表将显示数据。可以使用仪表板中的图形和图表来监视数据。 

例如，单 CF 仪表板中包含有关一个 Cloud Foundry 应用程序的信息。可以进行可视化和分析的数据仅限于该应用程序。您可以使用此仪表板来分析该应用程序的所有实例的数据。可以比较实例。也可以按实例标识来过滤信息。 

可以定义每个实例标识的查询并在仪表板中将其置顶。 

![带有已置顶查询的仪表板](images/logging_kibana_dash_activate_query.jpg)

然后，可以根据要在仪表板中查看的实例信息来激活或取消激活各个查询。 

下图显示一个查询已激活，另一个查询已取消激活：

![带有已置顶查询的仪表板](images/logging_kibana_dash_deactivate_query.jpg)

如果要在直方图中比较 2 个实例，可以在同一仪表板中定义 2 个查询，每个实例标识各一个查询。可以为其提供别名和唯一颜色，以便能轻松识别。Kibana 通过用逻辑 OR 连接多个查询来处理这些查询。 

下图显示的面板用于配置查询的别名和颜色、在仪表板中将查询置顶以及取消激活查询：

![用于配置查询的仪表板向导](images/logging_kibana_query_def.jpg)



## Cloud Foundry 应用程序的 Kibana 日志格式
{: #kibana_log_format_cf}

可以配置 Kibana 仪表板来显示每个日志条目的以下字段：

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>所记录事件的时间。时间戳记定义为精确到毫秒。</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 资源的标识。</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>日志文档的唯一标识。</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>日志条目的索引。</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>日志的类型；例如，<samp>syslog</samp>。</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 应用程序的名称。</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 应用程序的唯一标识。</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>生成日志数据的应用程序的名称。</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>生成日志数据的应用程序实例的实例标识。</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>所记录事件的严重性。</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>组件发出的消息。消息根据上下文而变化。</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>将日志消息写入其中的流。<samp class="ph codeph">OUT</samp> 是指 <samp class="ph codeph">stdout</samp> 流，<samp class="ph codeph">ERR</samp> 是指 <samp class="ph codeph">stderr</samp> 流。</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 组织的唯一标识。</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>在其中对应用程序编译打包的 {{site.data.keyword.Bluemix_notm}} 组织的名称。</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>生成日志的组件。以下列表描述了每个组件的日志：</p>

<dl>
<dt><strong>API</strong></dt>
<dd>记录的对请求更改应用程序状态的 API 调用的响应。</dd>

<dt><strong>APP</strong></dt>
<dd>记录的来自应用程序的响应。</dd>

<dt><strong>CELL</strong></dt>
<dd>记录的来自 Diego 单元的响应，用于指示应用程序启动、停止或崩溃情况。</dd>

<dt><strong>LGR</strong></dt>
<dd>记录的来自 Loggregator 的响应，用于指示日志记录进程发生的问题。</dd>

<dt><strong>RTR</strong></dt>
<dd>路由器将 HTTP 请求路由到应用程序时记录的来自路由器的响应。</dd>

<dt><strong>SSH</strong></dt>
<dd>用户使用 **cf ssh** 命令访问应用程序容器时记录的来自 Diego 单元的响应。</dd>

<dt><strong>STG</strong></dt>
<dd>对应用程序编译打包或重新编译打包时记录的来自 Diego 单元或 Droplet Execution Agent 的响应。</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>在其中对应用程序编译打包的 {{site.data.keyword.Bluemix_notm}} 空间的名称。</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>所记录事件的时间。时间戳记定义为精确到毫秒。</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>日志的类型；例如，<samp>syslog</samp>。</p>
</dd>
</dl>




