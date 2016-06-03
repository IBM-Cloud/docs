---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#监视和日志记录
{: #monitoringandlogging}

*上次更新时间：2016 年 5 月 11 日*

通过监视应用程序和复查日志，您可以跟进应用程序的执行和数据流，从而更好地了解部署情况。此外，还可以减少找到任何问题并进行修复所需的时间和精力。
{:shortdesc}

{{site.data.keyword.Bluemix}} 应用程序可以是广泛分布的多实例应用程序，并且应用程序的执行及其数据可以在许多服务中共享。在这种复杂的环境中，监视应用程序和复查日志对您管理应用程序非常重要。

{{site.data.keyword.Bluemix_notm}} 具有内置日志记录机制，可在应用程序运行时为应用程序生成日志文件。在日志中，可以查看为应用程序生成的错误、警告和参考消息。此外，还可以配置应用程序，以便将日志消息写入日志文件中。有关日志格式和如何查看日志的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 应用程序的日志记录](#logging_for_bluemix_apps)。

通过监视应用程序，您可以查看和控制应用程序部署。通过监视，您可以完成以下任务：

* 收集和监视应用程序实例的性能信息，并检查这些实例是否运行正常。
* 深入了解应用程序操作，例如检测潜在瓶颈或何时需要升级。
* 预估资源使用情况和费用。

为了使您的部署在 {{site.data.keyword.Bluemix_notm}} 平台上稳定运行，您希望及时检测到问题，并有效地确定原因。为了实现此目标，请在设计应用程序时将故障诊断考虑在内，并在应用程序部署到 {{site.data.keyword.Bluemix_notm}} 后使用服务或工具进行监视和日志记录。

##监视在 Cloud Foundry 上运行的应用程序
{: #monitoring_bluemix_apps}

使用 Cloud Foundry 基础架构在 {{site.data.keyword.Bluemix_notm}} 上运行应用程序时，您会希望实时了解性能信息，例如运行状态、资源使用情况和流量度量值。通过这些性能信息，您可以相应地进行决策或执行操作。

要监视 {{site.data.keyword.Bluemix_notm}} 应用程序，请使用以下某种方法：

* {{site.data.keyword.Bluemix_notm}} 服务。Monitoring and Analytics 提供了可用于监视应用程序性能的服务。此外，此服务还提供了分析功能，例如日志分析。有关更多信息，请参阅 [Monitoring and Analytics](../services/monana/index.html)。
* 第三方选项。例如，[New Relic](http://newrelic.com/){:new_window}。

##在 Cloud Foundry 上运行的应用程序的日志记录
{: #logging_for_bluemix_apps}

使用 Cloud Foundry 基础架构在 {{site.data.keyword.Bluemix_notm}} 上运行应用程序时，会自动创建日志文件。在从部署到运行时的任何阶段遇到错误时，都可以检查日志，以获取可能有助于解决问题的线索。

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



###日志格式
{: #log_format}

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
<p>生成日志的组件。以下列表提供了所有组件的定义：</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>应用程序。组件应用程序后跟一个斜杠和一个数字，数字指示应用程序实例。其中，0 表示第一个实例，1 表示第二个实例，依此类推。</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API。</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent。</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator。</dd>

<dt><strong>RTR</strong></dt>
<dd>路由器。</dd>

<dt><strong>STG</strong></dt>
<dd>编译打包。</dd>
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

###查看日志
{: #viewing_logs}

您可以在三个位置查看 Cloud Foundry 应用程序的日志：

  * [{{site.data.keyword.Bluemix_notm}} 仪表板](#viewing_logs_UI){:new_window}
  * [命令行界面](#viewing_logs_cli){:new_window}
  * [外部日志主机](#thirdparty_logging){:new_window}

#### 在 {{site.data.keyword.Bluemix_notm}} 仪表板中查看日志
{: #viewing_logs_UI}

要查看部署或运行时日志，请完成以下步骤：
1. 登录到 {{site.data.keyword.Bluemix_notm}}，然后在“仪表板”上单击应用程序的磁贴。这将显示应用程序详细信息页面。
2. 在左侧导航栏中，单击**日志**。

在**日志**控制台中，可以查看应用程序最近的日志或实时查看尾部日志。此外，可以按日志类型和通道来过滤日志。

**注**：在两次应用程序崩溃和部署之间，不会持久存储日志。



#### 通过命令行界面查看日志
{: #viewing_logs_cli}

要通过命令行界面查看日志，请从以下选项中进行选择：

<ul>
<li>部署应用程序时跟踪日志。<p>将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，可使用 **cf logs** 命令来显示应用程序日志以及与应用程序进行交互的系统组件的日志。在 cf 命令行界面中，可以键入以下命令。有关 cf 日志的更多信息，请参阅 <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Cloud Foundry 中的日志类型及其消息</a></p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>显示最近一段时间的日志。</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>显示自运行此命令以来生成的日志。</dd>
</dl>
<div class="note tip"><span class="tiptitle">提示：</span>在一个命令行窗口中运行 <span class="keyword cmdname">cf push</span> 或 <span class="keyword cmdname">cf start</span> 命令时，可以在另一个命令行窗口中输入 <samp class="ph codeph">cf logs appname --recent</samp> 来实时查看日志。</div>
</li>

<li>部署应用程序后查看日志。<p>如果启用了应用程序日志记录，那么在运行时遇到应用程序问题时，可以查看以下应用程序日志。应用程序日志有助于确定错误的原因。</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>此日志文件会记录细颗粒度的参考事件，用于调试目的。您可以使用此日志来对 buildpack 执行问题进行故障诊断。</p>
<p>要将数据生成到 <span class="ph filepath">buildpack.log</span> 文件中，必须使用以下命令来启用 buildpack 跟踪：<pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>要查看此日志，请输入以下命令：<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>此日志文件会在编译打包任务的主要步骤之后记录消息。您可以使用此日志来对编译打包问题进行故障诊断。</p>
<p>要查看此日志，请输入以下命令：<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**注：**有关如何启用应用程序日志记录的信息，请参阅[调试运行时错误](../debug/index.html#debugging-runtime-errors)。




###过滤日志
{: #filtering_logs}

要查看感兴趣的日志或排除不想查看的内容，可以在 cf 命令行界面中将 **cf logs** 命令与过滤选项（例如，**cut** 和 **grep**）一起使用。

* 要查看部分而不是完整的详细日志，请使用 **cut** 选项。例如，要显示组件和消息信息，请使用以下命令：```
cf logs appname --recent | cut -c 29-40,46- 
```

有关 **grep** 选项的更多信息，请键入 cut --help。
* 要显示包含特定关键字的日志条目，请使用 **grep** 选项。例如，要显示包含关键字 [APP 的日志条目，可以使用以下命令：```
cf logs appname --recent | grep '\[App'
```
有关 **grep** 选项的更多信息，请键入 `grep --help`。



### 配置外部日志主机
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} 会在内存中保留数量有限的日志信息。记录信息时，较新的信息会将旧的信息替换掉。要保留所有日志信息，可以将日志保存到外部日志主机，例如第三方日志管理服务或其他主机。

要将应用程序和系统中的日志流式传输到外部日志主机，请完成以下步骤：

  1. 确定日志记录端点。 
     
	 可以将日志发送到第三方日志聚集器，例如 Papertrail、Splunk 或 Sumologic。还可以将日志发送到 syslog 主机、使用 TLS（传输层安全性）加密的 syslog 主机或 HTTPS POST 端点。对于不同的日志主机，用于获取日志记录端点的方法有所不同。

  2. 创建用户提供的服务实例。
     
	 使用 ```cf create-user-provided-service``` 命令（或此命令的简短版本 ```cups``）来创建用户提供的服务实例：
```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 **service_name**
	 
	 用户提供的服务实例的名称。
	 
	 **logging_endpoint**
	 
	 {{site.data.keyword.Bluemix_notm}} 向其发送日志的日志记录端点。请参阅下表，以将 *logging_endpoint* 替换为您的值：
	 
	 <table>
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
	 cf bind-service appname <service_name>
	```
	 **appname**
	 
	 应用程序的名称。
	 
	 **service_name**
	 
	 用户提供的服务实例的名称。
	 
  4. 重新编译打包应用程序。输入 ```cf restage appname``` 以使更改生效。 

#### 查看外部主机中的日志
{: #viewing_logs_external}

	 
生成日志后，经过短暂延迟即可查看外部日志主机中的消息，这些消息类似于在 {{site.data.keyword.Bluemix_notm}} 用户界面中或通过 cf 命令行界面查看的消息。如果您有应用程序的多个实例，那么会聚集日志，这样就可以查看该应用程序的所有日志。此外，在两次应用程序崩溃和部署之间，不会持久存储日志。

**注：**您在命令行界面中查看的日志并不是 syslog 格式，并且可能与外部日志主机中显示的消息不完全一致。 


