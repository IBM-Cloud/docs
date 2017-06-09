---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 关于 Deployment Risk

{{site.data.keyword.DRA_short}} 提供了有关部署（尤其是风险方面）的大量信息。您可以使用这些信息在 Delivery Pipeline 中通过策略和检测点来自动保障质量。
{:shortdesc}

在工具链中打开 {{site.data.keyword.DRA_short}} 后，单击 **Deployment Risk**。在其中，可以了解编译打包和生产环境中应用程序的概况，并可向下钻取以了解代码覆盖、测试性能和安全报告。仪表板中会自动填充管道的 {{site.data.keyword.DRA_short}} 测试生成的最新信息。

可以使用 Deployment Risk 在工具链中通过策略和检测点来强制实施质量标准。策略由规则集构成；检测点强制实施策略。例如，可创建“单元测试和测试覆盖”策略，此策略要求构建符合单元测试和测试覆盖标准。然后，将引用此策略的检测点添加到 Continuous Delivery 过程。不符合此策略的构建会在该检测点处停止。 

## 集成信息

Deployment Risk 与 {{site.data.keyword.deliverypipeline}}（{{site.data.keyword.contdelivery_full}} 的一部分）和 Jenkins 项目相集成。在高级别，这两者的使用指示信息非常类似。  

如果使用的是 {{site.data.keyword.deliverypipeline}}，请执行以下步骤：

1. [创建策略和规则](risk_policies.html)以供 {{site.data.keyword.DRA_short}} 管理。
2. [准备管道阶段](risk_cd.html)，以便与 {{site.data.keyword.DRA_short}} 相集成。
3. 在管道中[创建或编辑测试作业](risk_cd.html)，以用于将结果上传到 {{site.data.keyword.DRA_short}}。
4. 向管道[添加检测点](risk_cd.html)，管道将基于这些结果和策略做出升级决策。
5. 运行管道并[查看结果](results.html)。

如果使用的是 Jenkins，请执行以下步骤：

1. [创建策略和规则](risk_policies.html)以供 {{site.data.keyword.DRA_short}} 管理。
2. [安装并配置 Jenkins 插件](risk_jenkins.html)。
3. [创建测试作业和检测点，如插件指示信息中所述](risk_jenkins.html)。测试会将结果上传到 {{site.data.keyword.DRA_short}} 进行分析，而检测点会使用这些结果来做出升级决策。
4. 运行项目并[查看结果](results.html)。 

不管您如何构建和部署代码，结果都一样：符合标准的构建将通过 Deployment Risk 检测点，而不符合标准的构建则会停止。 

## 先决条件
{: #prerequisites}

除了 [{{site.data.keyword.DRA_short}} 入门](/docs/services/DevOpsInsights/index.html)中所述的配置外，Deployment Risk 还需要另外一些配置。

要使用 Deployment Risk，需要下面两项：

* {{site.data.keyword.deliverypipeline}} 实例或 Jenkins 项目
* 要用于评估项目的测试
