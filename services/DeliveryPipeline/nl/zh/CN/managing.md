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
上次更新时间：2016 年 8 月 30 日
{: .last-updated}

您可以管理、配置和扩展 IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 集成。
{:shortdesc}

完成以下任务，以管理、配置和扩展管道。

## 控制访问权
{: #deliverypipeline_access}

您可以限制何人能够运行阶段或修改管道。要这样做，请转至“管道设置”页面，您可以通过单击“管道：所有阶段”页面上的**阶段配置**图标，来访问此页面。

![管道设置齿轮图标](./images/pipeline_settings.png)

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

通过配置作业使用受支持的服务，您可以扩展构建和部署管道的功能。例如，测试作业可以运行静态代码扫描，而构建作业可以全球化字符串。


有关扩展管道功能的更多信息，请参阅[扩展 {{site.data.keyword.deliverypipeline}} 服务的功能](./deliverypipeline_extension.html)。

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
