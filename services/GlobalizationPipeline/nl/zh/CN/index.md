---

copyright:
  years: 2015, 2017
lastupdated: "2016-09-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.GlobalizationPipeline_short}} 入门
{: #globalizationpipeline}


{{site.data.keyword.GlobalizationPipeline_full}} 是一种提供机器翻译和编辑功能的服务，可快速翻译 Web 或手机 UI。使用其仪表板、RESTful API 以及与应用程序 Delivery Pipeline 的集成，您可以将应用程序发布到全球客户，而无需重新构建或重新部署应用程序。
{:shortdesc}

您可以使用 {{site.data.keyword.GlobalizationPipeline_short}} 服务与 {{site.data.keyword.Bluemix}} 中的任何应用程序，或者自行取消绑定。您可以轻而易举地快速创建、维护和修改翻译，而无需离开 DevOps 环境。

从 {{site.data.keyword.GlobalizationPipeline_short}} 界面，您可以快速翻译 {{site.data.keyword.Bluemix_notm}} 应用程序。有关使用 RESTful API 翻译应用程序的更多信息，请参阅 [API 参考](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}。 


## 创建束
{: #globalizationpipeline_creatingbundles}

使用 {{site.data.keyword.GlobalizationPipeline_short}} 服务，您可以创建束，其包含要翻译的应用程序的资源文件。资源文件可以是 Java 属性文件、AMD I18N 文件或 JSON 文件，且必须以代表应用程序中 UI 字符串的键值对形式包含内容。有关受支持文件类型的详细信息和示例，请参阅[使用束](./bundles.html){: new_window}。

要创建束，请完成以下步骤：

<ol>
<li>从<strong>概述</strong>选项卡中，单击<strong>新建束</strong>。</li>

<li>提供束的相关信息：</li>
<table>
<thead>
<tr>
<th>字段</th>
<th>必填</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>束标识</strong></td>
<td>是</td>
<td>用于识别束的唯一名称。</td>
</tr>
<tr>
<td><strong>源语言</strong></td>
<td>是</td>
<td>源文件的母语。</td>
</tr>
<tr>
<td><strong>资源文件</strong></td>
<td>否</td>
<td>要翻译的<a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/bundles.html>资源文件</a>。文件大小上限为 2MB。将上传指定的资源文件。</td>
</tr>
<tr>
<td><strong>文件格式</strong></td>
<td>否</td>
<td>要上传的文件类型。</td>
</tr>
<tr>
<td><strong>目标语言</strong></td>
<td>否</td>
<td>要翻译为的目标语言。</td>
</tr>
</tbody>
</table>

<p><strong>注：</strong>要更改针对束提供机器翻译的语言服务，请单击 <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/managing_translations.html#globalizationpipeline_service_to_service>MT 配置</a>选项卡，以查看其他受支持的机器翻译引擎。</p>

<li>单击<strong>保存</strong></li></ol>


创建束之后，已上传的资源文件即会翻译为您指定的所有目标语言。新束会添加到“束”选项卡，您可以在这里：

* 添加或移除语言
* 编辑生成的翻译
* 更新束中使用的源文件并重新生成翻译

## 导入已翻译的束
{: #globalizationpipeline_importtranslatedbundlesintoservice}

或者，如果您已经翻译了资源文件，那么您可以将它们导入到新束中。有关更多信息，请参阅 [{{site.data.keyword.GlobalizationPipeline_short}} 的 Java 客户端工具](https://github.com/IBM-Bluemix/gp-java-tools)。

**注：**如果已更新原始源文件，那么在该文件中定义的键和值会与最新的源文件版本同步，以便仅翻译已更改的键和值。

## 估算 {{site.data.keyword.GlobalizationPipeline_short}} 数据使用情况
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_short}} 将您的翻译存储在后端数据库中。要估算活动数据的大小，您可以参考数据存储估算公式：

`<expected resource data storage size in MB> ˜= 0.0005 * <number of key/value pairs in the source resource> * <number of languages including the source language>`

根据公式，典型束的大小为 `(length of key + length of value in UTF-8 = ˜40 bytes)`。

例如，如果您具有 100 个键值对且将它们翻译为 9 种语言，那么估算存储大小为 0.0005 100 (9+1) = 0.5 MB。实际大小可能会因随翻译一起存储的实际键值大小和元数据而有所不同。

使用 Bluemix [定价计算器](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3)，来确定每月服务成本。


# 相关链接
{: #rellinks}
## 教程与样本
{: #samples}

* [Node.js 样本](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Ruby 样本](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Java 客户端](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Java 工具](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [JavaScript 客户端](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [AngularJS 客户端](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Ruby 客户端](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Python 客户端](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## API 参考
{: #api}

* [IBM Globalization Pipeline RESTful API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## 相关链接
{: #general}

* [将 Globalization Pipeline 与 Delivery Pipeline 集成](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix 价格表](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix 先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
