---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 通过 Cloud Foundry 进行监视和日志记录
{: #monitoringandlogging}


通过监视应用程序和复查日志，您可以跟进应用程序的执行和数据流，从而更好地了解部署情况。此外，还可以减少问题定位及修复所需的时间和精力。{:shortdesc}

{{site.data.keyword.Bluemix}} 应用程序可以是广泛分布的多实例应用程序，并且应用程序的执行及其数据可以在许多服务中共享。在这种复杂的环境中，监视应用程序和复查日志对您管理应用程序非常重要。

## 对 Cloud Foundry 应用程序进行监视和日志记录
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} 具有内置日志记录机制，可在应用程序运行时为应用程序生成日志文件。在日志中，可以查看为应用程序生成的错误、警告和参考消息。此外，还可以配置应用程序，以便将日志消息写入日志文件中。有关日志格式和如何查看日志的更多信息，请参阅[为 Cloud Foundry 上运行的应用程序进行日志记录](#logging_for_bluemix_apps)。

通过监视应用程序，您可以查看和控制应用程序部署。通过监视，您可以完成以下任务：

* 收集和监视应用程序实例的性能信息，并检查这些实例是否运行正常。
* 深入了解应用程序运行情况，例如，检测潜在瓶颈或何时需要升级。
* 估算资源使用情况和费用。

为了使您的部署在 {{site.data.keyword.Bluemix_notm}} 平台上稳定运行，您希望及时检测到问题，并有效地确定原因。要实现此目标，请在设计应用程序时将故障诊断考虑在内，并在应用程序部署到 {{site.data.keyword.Bluemix_notm}} 后使用服务或工具进行监视和日志记录。

### 监视 Cloud Foundry 上运行的应用程序
{: #monitoring_bluemix_apps}

使用 Cloud Foundry 基础架构在 {{site.data.keyword.Bluemix_notm}} 上运行应用程序时，您会希望实时了解性能信息，例如运行状态、资源使用情况和流量度量值。通过这些性能信息，您可以相应地进行决策或执行操作。


要监视 {{site.data.keyword.Bluemix_notm}} 应用程序，请使用以下某种方法：

* {{site.data.keyword.Bluemix_notm}} 服务。Monitoring and Analytics 提供了可用于监视应用程序性能的服务。此外，此服务还提供了分析功能，例如日志分析。有关更多信息，请参阅 [Monitoring and
Analytics](/docs/services/monana/index.html#gettingstartedtemplate)。
* 第三方选项。例如，[New Relic ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://newrelic.com/){:new_window}。

### 为 Cloud Foundry 上运行的应用程序进行日志记录
{: #logging_for_bluemix_apps}

使用 Cloud Foundry 基础架构在 {{site.data.keyword.Bluemix_notm}} 上运行应用程序时，会自动创建日志文件。在从部署到运行时的任何阶段遇到错误时，都可以检查日志，以获取可能有助于解决问题的线索。


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### 日志格式和保留时间
{: #log_format}

在 {{site.data.keyword.Bluemix_notm}} Public Cloud Foundry 应用程序中，缺省情况下日志数据存储 7 天。每天最多可以搜索 1 GB 的数据。

{{site.data.keyword.Bluemix_notm}} 应用程序的日志以固定格式显示，类似于以下模式：

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

每个日志条目都包含四个字段。有关每个字段的简短描述，请参阅以下列表：

<dl>
<dt><strong>时间戳记</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>列：1 - 27</p>
<p>日志语句的时间。时间戳记定义为精确到毫秒。</p>
</dd>

<dt><strong>组件</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>列：29 - 40</p>
<p>生成日志的组件。</p>
<p>每个组件类型后跟一个斜杠和一个数字，数字指示应用程序实例。0 表示分配给第一个实例的数字，1 表示分配给第二个实例的数字，依此类推。</p>
<p>以下列表概述了不同类型的组件：</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator：LGR 组件提供有关日志记录服务的信息。</dd>

<dt><strong>RTR</strong></dt>
<dd>路由器：RTR 组件提供有关向应用程序发出的 HTTP 请求的信息。</dd>

<dt><strong>STG</strong></dt>
<dd>编译打包：STG 组件提供有关应用程序如何编译打包或重新编译打包的信息。</dd>

<dt><strong>APP</strong></dt>
<dd>应用程序：APP 组件提供有关应用程序的信息。</dd>

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

<dt><strong>流</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>列：42 - 44</p>
<p>将日志消息写入其中的流。<samp class="ph codeph">OUT</samp> 是指 <samp class="ph codeph">stdout</samp> 流，<samp class="ph codeph">ERR</samp> 是指 <samp class="ph codeph">stderr</samp> 流。</p>
</dd>

<dt><strong>消息</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>列：46 - 行末</p>
<p>组件发出的消息。消息根据上下文而变化。</p>
</dd>
</dl>

下图显示了基于 Droplet Execution Agent (DEA) 的 Cloud Foundry 体系结构中的不同组件（日志类型）：![DEA 体系结构中的日志类型。](images/logging_F1.png "基于 Droplet Execution Agent (DEA) 的 Cloud Foundry 体系结构中的组件（日志类型）。")


## 查看日志
{: #viewing_logs}

您可以在四个位置查看 Cloud Foundry 应用程序的日志：

  * {{site.data.keyword.Bluemix_notm}} 仪表板
  * Kibana 仪表板
  * 命令行界面
  * 外部日志主机

### 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中查看日志
{: #viewing_logs_UI}

要查看部署或运行时日志，请完成以下步骤：
1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后单击应用程序的磁贴。这将显示应用程序详细信息页面。
2. 在导航栏中，单击**日志**。

在**日志**控制台中，可以查看应用程序最近的日志或实时查看尾部日志。此外，可以按日志类型和通道来过滤日志。

**注**：在两次应用程序崩溃和部署之间，不会持久存储日志。


### 在 Kibana 仪表板中查看日志
{: #viewing_logs_Kibana}

创建定制仪表板以简单或有创意的方式显示在空间中运行的应用程序的日志。

1. 打开 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) 以登录到 Kibana 用户界面。
2. 选择 **Kibana 3** 选项卡。
3. 如果未看到任何日志，请调整标题中的时间选取器。
4. 将该仪表板另存为新仪表板。
  1. 在工具栏中，单击**保存**图标。
  2. 输入仪表板的名称。
  3. 在“名称”字段旁边，单击**保存**图标。

有关定制 Kibana 仪表板的更多信息，请参阅[此博客帖子](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)或 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。


### 通过命令行界面查看日志
{: #viewing_logs_cli}

要通过命令行界面查看日志，请从以下选项中进行选择：

<ul>
<li>部署应用程序时跟踪日志。
<p>将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，可使用 **cf logs** 命令来显示应用程序日志以及与应用程序进行交互的系统组件的日志。在 cf 命令行界面中，可以键入以下命令。有关 cf 日志的更多信息，请参阅 <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Log Types and Their Messages in Cloud Foundry <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a></p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>显示最近一段时间的日志。</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>显示自运行此命令以来生成的日志。</dd>
</dl>
<div class="note tip"><span class="tiptitle">提示：</span>在一个命令行窗口中运行 <span class="keyword cmdname">cf push</span> 或 <span class="keyword cmdname">cf start</span> 命令时，可以在另一个命令行窗口中输入 <samp class="ph codeph">cf logs appname --recent</samp> 来实时查看日志。</div>
</li>

<li>部署应用程序后查看日志。

<p>如果启用了应用程序日志记录，那么在运行时遇到应用程序问题时，可以查看以下应用程序日志。应用程序日志有助于确定错误的原因。</p>

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>此日志文件会记录细颗粒度的参考事件，用于调试目的。您可以使用此日志来对 buildpack 执行问题进行故障诊断。</p>
<p>要将数据生成到 <span class="ph filepath">buildpack.log</span> 文件中，必须使用以下命令来启用 buildpack 跟踪：
<pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre></p>
<p>要查看此日志，请输入以下命令：
<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>
<dt><strong>staging_task.log</strong></dt>
<dd><p>此日志文件会在编译打包任务的主要步骤之后记录消息。您可以使用此日志来对编译打包问题进行故障诊断。</p>
<p>要查看此日志，请输入以下命令：
<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**注：**有关如何启用应用程序日志记录的信息，请参阅[调试运行时错误](/docs/debug/index.html#debugging-runtime-errors)。

### 查看外部主机中的日志
{: #viewing_logs_external}


生成日志后，经过短暂延迟即可查看外部日志主机中的消息，这些消息类似于在 {{site.data.keyword.Bluemix_notm}} 用户界面中或通过 cf 命令行界面查看的消息。如果您有应用程序的多个实例，那么会聚集日志，这样就可以查看该应用程序的所有日志。此外，在两次应用程序崩溃和部署之间，不会持久存储日志。

**注：**您在命令行界面中查看的日志并不是 syslog 格式，并且可能与外部日志主机中显示的消息不完全一致。




## 通过命令行界面过滤日志
{: #filtering_logs}

要查看感兴趣的日志或排除不想查看的内容，可以在 cf 命令行界面中将 **cf logs** 命令与过滤选项（例如，**cut** 和 **grep**）一起使用。

* 要查看部分而不是完整的详细日志，请使用 **cut** 选项。例如，要显示组件和消息信息，请使用以下命令：
```
cf logs appname --recent | cut -c 29-40,46- 
```

有关 **grep** 选项的更多信息，请键入 cut --help。
* 要显示包含特定关键字的日志条目，请使用 **grep** 选项。例如，要显示包含关键字 `[APP` 的日志条目，可以使用以下命令：

```
cf logs appname --recent | grep '\[App'
```
有关 **grep** 选项的更多信息，请键入 `grep --help`。



## 配置外部日志主机
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} 会在内存中保留数量有限的日志信息。记录信息时，较新的信息会将旧的信息替换掉。要保留所有日志信息，可以将日志保存到外部日志主机，例如第三方日志管理服务或其他主机。


要将应用程序和系统中的日志流式传输到外部日志主机，请完成以下步骤：

  1. 确定日志记录端点。

	 可以将日志发送到第三方日志聚集器，例如 Papertrail、Splunk 或 Sumologic。还可以将日志发送到 syslog 主机、使用 TLS（传输层安全性）加密的 syslog 主机或 HTTPS POST 端点。对于不同的日志主机，用于获取日志记录端点的方法有所不同。

  2. 创建用户提供的服务实例。

	 使用 `cf create-user-provided-service` 命令（或此命令的简短版本 `cups`）来创建用户提供的服务实例：
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;
	 
	 用户提供的服务实例的名称。

	 &lt;logging_endpoint&gt;

	 {{site.data.keyword.Bluemix_notm}} 向其发送日志的日志记录端点。请参阅下表，以将 *logging_endpoint* 替换为您的值：

	 <table>
	 <caption>表 1. 日志记录端点值</caption>
     <thead>
     <tr>
     <th>日志记录端点</th>
     <th>命令</th>
	 <th>注释</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog 主机</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>例如，要允许将日志记录到 Papertrail，请输入 `cf cups my-logs -l syslog://<papertrail-url>`。将 `<papertrail-url>` 替换为 Papertrail 中您的日志记录端点的 URL。</td>
     </tr>
	 <tr>
     <td>syslog-tls 主机</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>证书必须受认证中心信任。不要使用自签名证书。</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>此端点必须位于公共因特网上，并可由 {{site.data.keyword.Bluemix_notm}} 进行访问</td>
     </tr>
     </tbody>
     </table>
  3. 将服务实例与应用程序绑定。

	 使用以下命令将服务实例绑定到应用程序：

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;
	 
	 应用程序的名称。

	 &lt;service_name&gt;

	 用户提供的服务实例的名称。

  4. 重新编译打包应用程序。键入 `cf restage appname` 以使更改生效。


### 示例：将 Cloud Foundry 应用程序日志以流方式传送到 Splunk
{: #splunk}

在本示例中，名为 Jane 的开发者使用 IBM Virtual Servers Beta 和 Ubuntu 映像，创建了一个虚拟服务器。Jane 尝试以流方式，将 Cloud Foundry 应用程序日志从 {{site.data.keyword.Bluemix_notm}} 传送到 Splunk。

  1. 要开始该操作，Jane 设置了 Splunk。

     a. Jane 从[下载 Splunk Light 站点 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} 下载了 Splunk Light，然后使用以下命令对其进行了安装。该软件安装在 */opt/splunk*。

	    

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane 安装并修补 RFC5424 syslog 技术附加组件，以与 {{site.data.keyword.Bluemix_notm}} 集成。有关安装附加组件的指示信息的更多信息，请参阅 [Cloud Foundry 准则 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}。

	    Jane 使用以下命令安装附加组件：

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        然后，Jane 通过将 */opt/splunk/etc/apps/rfc5424/default/transforms.conf* 替换为新的包含以下文本的 *transforms.conf* 文件，对附加组件进行修补：

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. 设置完 Splunk 之后，Jane 必须在 Ubuntu 机器上打开一些端口，以接受传入的 syslog 漏出（端口 5140）和 Splunk Web UI（端口 8000），因为缺省情况下，{{site.data.keyword.Bluemix_notm}} 虚拟服务器已设置防火墙。

	    **注：**iptable 配置此时已经可供 Jane 评估时使用，并且这是一项临时配置。要在生产环境中的 Bluemix 虚拟服务器上配置防火墙设置，请参阅[网络安全组 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 文档以获取详细信息。

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   然后，Jane 使用以下命令来运行 Splunk：

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane 配置 Splunk 设置，以从 {{site.data.keyword.Bluemix_notm}} 接受 syslog 漏出。她必须针对 syslog 漏出创建数据输入。

     a. 在 Splunk Web 界面中，Jane 单击**数据 > 数据输入**。此时将显示 Splunk 支持的输入类型列表。

     b. 她选择 **TCP**，因为 syslog 漏出使用 TCP 协议。

     c. 在 **TCP** 窗格的**端口**字段中，她输入 **5140**，将其他字段保留空白，然后单击**下一步**。

     d. 从**源类型**列表中，她选择**未分类 > rfc5424_syslog**。

     e. 对于**方法**类型，她选择 **IP**。

     f. 在**索引**字段中，Jane 单击**创建新索引**。她将新索引命名为“bluemix”，然后单击**保存**。

     g. 最后，在**复查**窗口中，Jane 确认设置正确，然后单击**提交**，以启用此数据输入。

  3. 在 {{site.data.keyword.Bluemix_notm}} 中，Jane 创建了 syslog 漏出服务，并将该服务绑定到某个应用程序。

     a. Jane 通过 cf CLI，使用以下命令，创建 syslog 漏出服务：

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **注：** *dummyhost* 不是实名。它用于隐藏实际主机名。

     b. Jane 将 syslog 漏出服务绑定到其空间内的某个应用程序，然后重新编译打包该应用程序。

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane 尝试使用该应用程序，然后在 Splunk Web 界面输入以下查询字符串：

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane 在其 Splunk Web 界面中看到日志流。虽然 Jane 安装的 Splunk 是 Splunk Light，但是她仍可以每天保留 500MB 日志。

## 在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 中为 Cloud Foundry 应用程序进行日志记录
{: #hybrid_apps_logs_ov}


在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 中，Cloud Foundry 应用程序随附内置日志记录功能。您可以在 {{site.data.keyword.Bluemix_notm}} 控制台上查看从应用程序收集的数据。
{:shortdesc}

Cloud Foundry 应用程序使用 Cloud Foundry loggregator 从应用程序外部监视和转发日志。您无需在应用程序内部安装代理程序。

### 硬件需求


| **需求** |    **1 个节点**     | **3 个节点（针对高可用性）** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| 内存 | 80 GB | 240 GB |
| 本地存储器 | 2.98 TB | 8.94 TB |
{: caption="表 2. {{site.data.keyword.Bluemix_local_notm}} 的日志记录硬件需求" caption-side="top"}

### 设置

在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 中，缺省情况下所有应用程序的日志都处于活动状态。要查看有关读取标准日志的信息，请参阅[为 Cloud Foundry 上运行的应用程序进行日志记录](#logging_for_bluemix_apps)。此外，还可以在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 环境中启用高级日志记录功能。

* 要确认是否在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 环境中启用了高级日志记录功能，请执行[查看日志](#hybrid_apps_logs_dash)中的步骤。如果没有**高级视图**按钮，说明此功能未启用。

* 要向环境添加高级日志记录功能，请执行 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 或 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 文档中的步骤。

### 日志保留时间

在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry 应用程序中，缺省情况下日志数据存储 30 天。

## 在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 中查看 Cloud Foundry 应用程序的日志
{: #hybrid_apps_logs_dash}

您可以查看正在 {{site.data.keyword.Bluemix_dedicated_notm}} 和 {{site.data.keyword.Bluemix_local_notm}} 上运行的应用程序的日志。
{:shortdesc}

要查看应用程序日志，请执行以下步骤。
1. 选择正在运行的应用程序。
2. 单击**日志**。在**日志**视图中，可以查看正在运行的应用程序的日志。
4. 单击**高级视图**按钮。**高级视图**将使用 Kibana 来显示日志的更详细视图；Kibana 是使用日志和带时间戳记的数据来创建定制可视化项的可视化工具。有关使用高级视图的更多信息，请参阅 [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html) 文档。

接下来，可以定制 Kibana 仪表板。有关更多信息，请参阅[在 Kibana 仪表板中定制日志显示](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom)。
