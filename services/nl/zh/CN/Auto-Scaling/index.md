{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}} 服务入门
{: #autoscaling}

*上次更新时间：2015 年 1 月 18 日*

在 {{site.data.keyword.Bluemix_notm}} 中，您可以自动管理应用程序的容量。使用 {{site.data.keyword.autoscalingfull}} 服务，以自动提高或降低您的应用程序的计算能力。应用程序实例数会根据您定义的 {{site.data.keyword.autoscaling}} 策略自动调整。
{:shortdesc} 

## 在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.autoscaling}} 服务
{: #as-service}

要使用 {{site.data.keyword.autoscaling}} 服务，请完成以下步骤：

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，单击*添加服务或 API*，然后从服务目录中的 DevOps 部分选择 {{site.data.keyword.autoscaling}} 服务。此时会打开新窗口，其中显示 {{site.data.keyword.autoscaling}} 服务的概述。
2. 选择要绑定 {{site.data.keyword.autoscaling}} 服务的应用程序，并单击*创建*。<br/>
*请记住：*只能将一个 {{site.data.keyword.autoscaling}} 服务绑定到一个应用程序。如果应用程序已经与其他 {{site.data.keyword.autoscaling}} 服务绑定，请不要在此步骤中选择该应用程序。否则，将遇到 CWSCV2004E 错误。<br/>这将显示“重新编译打包应用程序”窗口。
3. 在“重新编译打包应用程序”窗口中，单击*重新编译打包*，以在使用刚刚添加的新 {{site.data.keyword.autoscaling}} 服务之前重新编译打包应用程序。重新编译打包应用程序完成后，可以开始为您的应用程序配置 {{site.data.keyword.autoscaling}} 服务。
4. 要为应用程序配置 {{site.data.keyword.autoscaling}}，请在 {{site.data.keyword.Bluemix_notm}} 用户界面中，单击绑定了 {{site.data.keyword.autoscaling}} 服务的应用程序。
5. 在仪表板的服务部分，单击 *Auto-Scaling* 图标。
6. 如果尚未执行此操作，请通过单击*创建 {{site.data.keyword.autoscaling}} 策略*为应用程序定义 {{site.data.keyword.autoscaling}} 策略。

现在，您可以为应用程序配置 {{site.data.keyword.autoscaling}} 策略、查看度量值统计信息或扩展历史记录。
<dl>
<dt>策略配置</dt>
<dd>使用此部分可创建或编辑扩展规则，以指定触发特定扩展活动的条件。<ul>
<li> 对于 Liberty for Java™ 应用程序，您可以定义 JVM 堆、内存和吞吐量的扩展规则。<li> 对于 Node.js 应用程序，您可以定义内存的扩展规则。<li> 对于 Ruby 应用程序，您可以定义内存的扩展规则。</ul>
*注：*您可以为多个度量值类型定义多个扩展规则。不过，{{site.data.keyword.autoscaling}} 服务不会检测扩展策略之间是否有冲突。定义扩展策略时，您必须确保多个扩展规则之间不相互冲突。否则，因应用程序在这一分钟向内扩展，而在下一分
钟向外扩展，您可能会看到实例总数变化不定。<br/><br/>如果您的应用程序工作负载在高峰时间和空闲时间动态更改，那么可以创建扩展日程安排，以处理不同时间段内的不同扩展需求。使用日程安排中指定的“最小实例计数”参数来定义应用程序实例数的基线，同时
动态扩展规则仍适用于触发向内扩展和向外扩展操作的日程安排。</dd>
<dt>度量值统计信息</dt>
<dd>显示应用程序各个实例的度量值统计信息。您可以查看平均统计信息，还可以选择特定实例来查看其统计信息。</dd>
<dt>扩展历史记录</dt>
<dd>显示应用程序的扩展历史记录。<ul>
<li> 过去一周：显示过去一周的扩展历史记录。<li> 过去一个月：显示过去一个月的扩展历史记录。<li> 定制范围：您可以设置时间段。</ul>
*注：*您可以通过选择“扩展状态”或“向内/向外扩展”来过滤历史记录。</dd>
</dl>


## {{site.data.keyword.autoscaling}} 服务的策略字段
{: #policyfields}

| 字段名称  | 描述 |
|-------------|----------------------|
|*允许的最大实例计数* |	可以启动的最大应用程序实例数。如果应用程序实例当前的数量等于此值，{{site.data.keyword.autoscaling}} 服务不再向外扩展应用程序。缺省最小实例计数是指可以启动的最小应用程序实例数。如果实例的数量等于此值，{{site.data.keyword.autoscaling}} 服务不再向内扩展应用程序。 |
| *度量值类型*	| 	可监视的受支持度量值类型。有关更多信息，请参阅“表 2”。 |
| *向外扩展* | 	指定触发向外扩展操作的阈值，以及触发向外扩展操作时要增加的实例数。 |
| *向内扩展* |	指定触发向内扩展操作的阈值，以及触发向内扩展操作时要减少的实例数。 |
| *统计信息窗口* |	过去一段时间长度，在此期间，收到的度量值被识别为有效。仅当时间戳记在此期间内时，度量值才有效。“统计信息窗口”参数的单位是秒。 |
| *违规持续时间*	| 过去一段时间长度，在此期间，可能会触发扩展操作。当所收集的度量值超过阈值上限或低于阈值下限（超过指定的时间）时，会触发扩展操作。“违规持续时间”参数的单位是秒。 |
| *向内扩展冷却期* | 发生向内扩展操作后，会在“向内扩展冷却期”参数所指定的时间长度内忽略其他扩展请求。此参数的单位是秒。 |
| *向外扩展冷却期*	| 发生向外扩展操作后，会在“向外扩展冷却期”参数所指定的时间长度内忽略其他扩展请求。此参数的单位是秒。 |
| *时区*	| 日程安排应用的时区。 |
| *开始时间*  |	重现日程安排的开始时间。 |
| *结束时间*    |	重现日程安排的结束时间。	|
| *重复日期*	|	重现日程安排应用时的日期。 |
| *最小实例计数* |	日程安排中指定时间段内可以对应用程序启动的最小实例数。 |
| *开始日期和时间* |	日程安排的开始日期和时间设置为特定日期。 |
| *结束日期和时间* |	日程安排的结束日期和时间设置为特定日期。	|

表 1. 扩展策略中的策略字段

| 度量值名称 | 描述 | 支持的应用程序类型 |
|-------------|----------------------| ------------------- |
| *JVM 堆* |	JVM 堆内存的使用百分比。	| Liberty for Java |
| *内存*   |	内存的使用百分比。	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *吞吐量* | 每秒处理的请求数。| Liberty for Java |
| *响应时间* |	已处理的请求的响应时间。	| Liberty for Java |

表 2. 支持的度量值名称

## 错误消息
{: #errmsgs}
本部分列出了 {{site.data.keyword.autoscaling}} 服务生成的警告和错误消息。
 
### CWSCV2004E 其他 {{site.data.keyword.autoscaling}} 服务已经绑定到该应用程序。
**只能将一个 {{site.data.keyword.autoscaling}} 服务绑定到一个应用程序。要将 {{site.data.keyword.autoscaling}} 服务绑定到已经与其他 {{site.data.keyword.autoscaling}} 服务绑定的应用程序时，会发生此错误。**

请选择没有与其他任何 {{site.data.keyword.autoscaling}} 服务绑定的其他应用程序，然后将目标 {{site.data.keyword.autoscaling}} 服务绑定到此应用程序。如果在其他所有情况下都遇到此错误，请联系 IBM 支持人员。

### CWSCV6001E API 服务器无法解析 API 的输入 JSON 字符串：{0}。
**解析输入 JSON 字符串时发生问题。**

请对照 API 文档检查输入 JSON，并更正其中的错误。

### CWSCV6002E API 服务器无法解析 API 的输出 JSON 字符串：{0}。
**解析输入 JSON 字符串时发生问题。**

请联系云管理员，以获取更多信息。

### CWSCV6003E API 的输入 JSON {1} 中的输入 JSON 字符串格式错误：{0}。
**解析输入 JSON 字符串时发现格式错误。**

请对照 API 文档检查输入 JSON，并更正其中的错误。

### CWSCV6004E API 的输出 JSON {1} 中的输出 JSON 字符串格式错误：{0}。
**解析输出 JSON 字符串时发现格式错误。**

请联系云管理员，以获取更多信息。

### CWSCV6005E {0} 期间发生内部服务器错误。
**处理请求时发生内部服务器错误。**

请联系云管理员，以获取更多信息。

### CWSCV6006E 调用 CloudFoundry API 失败：{0}
**调用 CloudFoundry API 时发生错误。**

请联系云管理员，以获取更多信息。

### CWSCV6007E 未找到应用程序：{0}
**未找到应用程序。**

请检查应用程序信息，以获取更多信息。

### CWSCV6008E 检索应用程序 {0} 的信息时发生以下错误：{1} 
**检索应用程序信息失败，并伴随一些错误。**

请检查应用程序信息，以获取更多信息。

### CWSCV6009E 未找到应用程序 {1} 的服务 {0}。
**找不到此应用程序的服务。**

请检查此应用程序的服务绑定，以获取更多信息。

### CWSCV6010E 找不到应用程序 {0} 的策略
**找不到此应用程序的策略。**

请检查应用程序配置，以获取更多信息。

### CWSCV6011E {0} 期间内部认证失败
**内部认证失败。**

请联系云管理员，以获取更多信息。


# 相关链接
## 样本
* [Tutorial: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Lab](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [Rest API of IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## 常规
* [{{site.data.keyword.Bluemix_notm}} 价格表](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}} 先决条件](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

