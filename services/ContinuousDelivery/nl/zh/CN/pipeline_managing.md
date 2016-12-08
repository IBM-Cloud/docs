---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 管理管道
{: #deliverypipeline_managing}
上次更新时间：2016 年 11 月 17 日
{: .last-updated}

您可以管理、配置和扩展 IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 集成。
{:shortdesc}

完成以下任务，以管理、配置和扩展管道。

## 环境属性和资源
{: #deliverypipeline_envprop}

您可以使用环境属性和预安装的资源，来与 {{site.data.keyword.deliverypipeline}} 服务进行交互。例如，您可能会将它们引入作业脚本或测试命令。有关更多信息，请参阅 [{{site.data.keyword.deliverypipeline}} 服务的环境属性和资源](./deploy_var.html)。

您可以将自己的环境属性通过其**环境属性**选项卡添加到阶段。环境属性可用于阶段中的每一个作业。

您可以通过“环境属性”选项卡，添加四种类型的属性：
* **文本**：具有单行值的属性关键字。
* **文本区域**：具有多行值的属性关键字。
* **安全**：具有单行值的属性关键字。该值显示为星号。
* **属性**：项目存储库中的文件。此文件可以包含多个属性。每一个属性必须位于自己的行上。要分隔键值对，请使用等号 (=)。

## 扩展管道的功能
{: #deliverypipeline_extend}

通过配置作业使用受支持的服务，您可以扩展管道的功能。例如，测试作业可以运行静态代码扫描，而构建作业可以全球化字符串。


有关扩展管道功能的更多信息，请参阅[扩展 {{site.data.keyword.deliverypipeline}} 服务的功能](./deliverypipeline_extension.html)。

