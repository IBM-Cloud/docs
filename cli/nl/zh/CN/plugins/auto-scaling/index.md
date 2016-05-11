---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Auto-Scaling CLI
{: #autoscalingcli}

*上次更新时间：2016 年 2 月 25 日*

您可以使用 {{site.data.keyword.autoscaling}} CLI for {{site.data.keyword.Bluemix_notm}} 来配置 {{site.data.keyword.autoscaling}} 服务。{{site.data.keyword.autoscaling}} CLI 支持 Linux64、Win64 和 OSX，提供的功能类似于 Auto-Scaling RESTful API。
{: shortdesc}

开始之前，请先安装 {{site.data.keyword.Bluemix_notm}} CLI。有关指示信息，请参阅[下载 {{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window}。

## 添加 {{site.data.keyword.Bluemix_notm}} CLI 插件

安装 {{site.data.keyword.Bluemix_notm}} CLI 后，可以添加 {{site.data.keyword.autoscaling}} CLI 插件。

完成以下步骤来添加存储库并安装该插件：
1. 要添加 {{site.data.keyword.Bluemix_notm}} CLI 插件存储库，请运行以下命令：
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. 要安装 {{site.data.keyword.autoscaling}} CLI 插件，请运行以下命令：
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## 附加 Auto-Scaling 策略

可以将 Auto-Scaling 策略附加到特定应用程序。运行以下命令：

```bx as policy-attach <APP_NAME> -p <policy_file>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">要附加 Auto-Scaling 策略的应用程序的名称。</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">描述 Auto-Scaling 策略的 JSON 文件的名称。有关更多详细信息，请参阅 <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">{{site.data.keyword.autoscaling}} RESTful API 文档</a>。</dd>
</dl>


## 生成 Auto-Scaling 策略

可以通过回答命令行界面上的问题来生成 Auto-Scaling 策略。根据您的输入，将以您输入的名称保存包含 Auto-Scaling 策略定义的 JSON 文件。如果未输入文件名，那么策略内容将直接显示在命令行上，而不保存到文件。运行以下命令：

```bx as policy-create```
{: codeblock}


## 显示 Auto-Scaling 策略

可以显示应用程序的 Auto-Scaling 策略。该策略的内容会直接显示到命令行。运行以下命令：

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">要显示其 Auto-Scaling 策略的应用程序的名称。缺省情况下，JSON 结构会转换成一系列用户可读的输出。</dd>
</dl>

**提示：**您还可以使用 **--json** 选项更好地显示原始 JSON 响应。


## 取消附加 Auto-Scaling 策略

可以从应用程序中除去 Auto-Scaling 策略。运行以下命令：

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">要取消附加其 Auto-Scaling 策略的应用程序的名称。</dd>
</dl>


## 启用或禁用 Auto-Scaling 策略

可以启用或禁用特定应用程序的 Auto-Scaling 策略。运行以下命令：

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">要启用或禁用其 Auto-Scaling 策略的应用程序的名称。</dd>
</dl>


## 显示应用程序的自动扩展历史记录

可以显示特定应用程序的自动扩展活动历史记录。自动扩展历史记录表将显示在命令行界面中。

```bx as history-show <APP_NAME>  [--start-date=<start_timestamp>]  [--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">要显示其 Auto-Scaling 策略历史记录的应用程序的名称。
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">历史记录范围的开始时间戳记。支持的格式为 `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`。缺省情况下，此时间戳记设置为早于当前时间的 50 小时。有关时间戳记格式的详细信息，请参阅 <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats standard</a>。
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">历史记录范围的结束时间戳记。支持的格式为 `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`。缺省情况下，此时间戳记设置为当前时间。有关时间戳记格式的详细信息，请参阅 <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats standard</a>。
</dl>

**提示：**您还可以使用 **--json** 选项更好地显示原始 JSON 响应。

# 相关链接
## 常规
* [{{site.data.keyword.autoscaling}} 服务](../../../services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C Date and Time Formats standard](https://www.w3.org/TR/NOTE-datetime){: new_window}


