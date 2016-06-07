---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 关于 Insights for Weather
{: #about_weather}

*上次更新时间：2016 年 5 月 19 日*

使用 {{site.data.keyword.weatherfull}} 可将来自 The Weather Company (TWC) 的数据合并到 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

您可以将天气观察数据和预测添加到 {{site.data.keyword.Bluemix_notm}} 应用程序，然后使用 [Insights for Weather REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} 显示地理位置所指定区域的天气数据。The Weather Company 是最全面的历史和预测天气数据提供者。可捕获所有形式的天气数据，包括降水、气压、风力和雷暴。

可以使用 REST API 来检索以下信息：

* 对于指定地理位置，从当前时间开始未来 24 小时的每小时天气预测。
* 对于指定地理位置，未来 10 天的每天天气预测，包括白天和晚上分段的预测。此预测包含最长 256 个字符的预测描述文本字符串，以及与请求的位置和语言相应的度量单位。
* 对于指定地理位置观察到的最新天气数据。此天气数据包含温度、降水、风向和风速、湿度、气压、露点、能见度和紫外线 (UV) 辐射。
* 对于指定地理位置和指定时间范围观察到的天气数据。此数据源自物理观察站。此 API 将返回最新天气状况的天气观察数据，以及一直到（且包含）过去 24 小时的观察数据。

有关 Weather Company 的天气用语和图标的更多信息，请参阅[图标代码、用语和图像](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}。您还可以[下载图标集](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}以在应用程序中使用。

## 定价模型
{: #pricing_models}

定价模型基于每天对 Insights for Weather API 的调用数，将按月向客户收费。在应用程序中，除了调用数有限制外，您可以测试任何地理区域、预测类型或时间序列观察数据的天气数据。免费套餐、基本套餐和高级套餐可以在无合同的情况下进行购买。这些套餐分别允许您的应用程序每天进行 500、5,000 或 50,000 个 API 调用。

还可以针对结算周期期间部署的每个服务实例购买多个高级套餐。如果您的应用程序每天使用超过 50,000 个调用或每分钟超过 1,000 个调用，那么您需要与 IBM 订立一份服务持续供应的合同。

根据所选套餐，当应用程序达到所允许的 API 调用限制时，那么进行下一个 API 调用不会成功，直到您的应用程序允许请求更多 API 调用为止。

例如，如果您使用的是基本套餐，那么即使超出套餐限制，应用程序在 1 分钟内可以进行 500 个 API 调用，但是在 5 分钟内将不允许进行下一个 API 调用。因此，用户可能会注意到应用程序中天气数据刷新有延迟。必须确保开发可以处理这些限制的应用程序，并且不大量请求 API 调用。可以改为监视应用程序的 API 调用使用量。可以通过检查 API 调用返回的项数，验证应用程序是否达到其套餐限制。

## 反馈与支持
{: #feedback_support}

如果对使用 Insights for Weather 创建应用程序有技术方面的问题，请在 [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window} 上发布您的问题，并使用 **bluemix** 和 **weather** 标记您的问题。

如果使用此服务时遇到任何问题，请使用 [IBM developerWorks Answers 论坛](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}。请包含 **insights-weather** 和 **bluemix** 标记以允许 IBM 可以更好地为您提供支持。

有关对 Bluemix 问题进行故障诊断的相关信息，请参阅[故障诊断](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}。
有关通过论坛搜索信息与询问问题，以及联系支持的详细信息，请参阅[获取客户支持](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}。
