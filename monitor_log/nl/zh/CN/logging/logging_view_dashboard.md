---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 Bluemix 仪表板分析 CF 应用程序日志
{: #analyzing_logs_bmx_ui}

在 {{site.data.keyword.Bluemix}} 中，可以通过可用于每个 Cloud Foundry 应用程序的**日志**选项卡来查看、过滤和分析日志。使用 {{site.data.keyword.Bluemix}} 仪表板可查看应用程序的最新活动。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public 提供了集成的“日志记录”服务。在 Cloud Foundry 中运行应用程序时，“日志记录”服务将在您使用 stdout 和 stderr 时，从与应用程序交互的系统组件中捕获日志数据，捕获有关应用程序的日志数据，甚至捕获应用程序内的日志数据。

{{site.data.keyword.Bluemix_notm}} 应用程序的日志以固定格式显示，类似于以下模式：

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>     <var class="keyword varname">message</var>     <var class="keyword varname">timestamp</var></code>
   
有关日志格式的更多信息，请参阅 [Cloud Foundry 应用程序日志的日志格式](logging_view_dashboard.html#log_format_cf)。

**注：**在 {{site.data.keyword.Bluemix_notm}} Public 中，缺省情况下日志数据会存储 7 天。每天最多可以搜索 1 GB 的数据。



##  访问 Bluemix“日志”选项卡
{: #launch_logs_tab_bmx_ui}

要查看 Cloud Foundry 应用程序的部署或运行时日志，请完成以下步骤：

1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后单击 {{site.data.keyword.Bluemix_notm}} **应用程序**仪表板上的应用程序名称。 

    这将显示应用程序详细信息页面。
    
2. 在导航栏中，单击**日志**。

    这将打开“日志”选项卡。 
    
    在**日志**选项卡中，可以查看应用程序的最近日志或实时跟踪日志。此外，可以按组件（日志类型）、按应用程序实例标识以及按错误来过滤日志。



## Cloud Foundry 应用程序日志的日志格式
{: #log_format_cf}

每个日志条目都包含以下字段：

<dl>
<dt><strong>时间戳记</strong></dt>
<dd>
<p>日志语句的时间。时间戳记定义为精确到毫秒。</p>
</dd>

<dt><strong>组件</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>用于生成日志的组件。</p>
<p>每个组件类型后跟一个斜杠和一个数字，数字指示应用程序实例。0 表示分配给第一个实例的数字，1 表示分配给第二个实例的数字，依此类推。请注意，您可以进行过滤，以在仪表板中仅显示一个应用程序实例。</p>
<p>以下列表概述了不同类型的组件：</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator：LGR 组件提供有关 Cloud Foundry Loggregator 的信息，Loggregator 用于从 Cloud Foundry 内部转发日志。</dd>

<dt><strong>RTR</strong></dt>
<dd>路由器：RTR 组件提供有关向应用程序发出的 HTTP 请求的信息。</dd>

<dt><strong>STG</strong></dt>
<dd>编译打包：STG 组件提供有关应用程序如何编译打包或重新编译打包的信息。</dd>

<dt><strong>APP</strong></dt>
<dd>应用程序：APP 组件提供应用程序中的日志。这是代码中的 stderr 和 stdout 将出现的位置。
</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API：API 组件提供有关因用户请求更改应用程序状态而导致的内部操作的信息。</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent：DEA 组件提供有关应用程序启动、停止或崩溃的信息。
<p>仅当应用程序部署在基于 DEA 的 Cloud Foundry 体系结构中时，此组件才可用。</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego 单元：CELL 组件提供有关应用程序启动、停止或崩溃的信息。
<p>仅当应用程序部署在基于 Diego 的 Cloud Foundry 体系结构中时，此组件才可用。</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH：每当用户使用 **cf ssh** 命令访问应用程序时，SSH 组件都会提供相关信息。
<p>仅当应用程序部署在基于 Diego 的 Cloud Foundry 体系结构中时，此组件才可用。</p></dd>

</dl>
</dd>

<dt><strong>消息</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>组件发出的消息。消息根据上下文而变化。</p>
</dd>
</dl>

下图显示了基于 Droplet Execution Agent (DEA) 的 Cloud Foundry 体系结构中的不同组件（日志类型）：![DEA 体系结构中的日志类型。](images/logging_F1.png "基于 Droplet Execution Agent 的 Cloud Foundry 体系结构中的组件。")



