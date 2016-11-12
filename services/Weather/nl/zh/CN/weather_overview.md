---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 关于 {{site.data.keyword.weather_short}}
{: #about_weather}

使用 {{site.data.keyword.weatherfull}} 可将来自 The Weather Company (TWC) 的数据合并到 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

您可以将天气观察数据和预测添加到 {{site.data.keyword.Bluemix_notm}} 应用程序，然后使用 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} 显示地理位置所指定区域的天气数据。The Weather Company 是最全面的历史和预测天气数据提供者。可捕获所有形式的天气数据，包括降水、气压、风力和雷暴。

可以使用 REST API 来检索以下信息：

* 对于指定地理位置，从当前时间开始未来 48 小时的每小时天气预测。
* 对于指定地理位置，从当前时间开始未来 3、5、7 或 10 天的每天预测，包括白天和晚上分段的预测。此预测包含最长 256 个字符的预测描述文本字符串，以及与请求的位置和语言相应的度量单位。
* 从当天开始未来 3 天、5 天、7 天或 10 天的每日天气预测，将每日天气预测细分为上午、下午、晚上和整晚分段。
* 对于指定地理位置观察到的最新天气数据。此天气数据包含温度、降水、风向和风速、湿度、气压、露点、能见度和紫外线 (UV) 辐射。
* 对于指定地理位置观察到的天气数据，包括之前 24 小时的数据。此数据源自物理观察站。
* 政府发布的天气警报，包括美国国家气象局、加拿大环境部和欧洲 MeteoAlarm 发布的天气监测、警告、预警和公告。
* 年历服务，提供来自国家气象局观察站的每日或每月历史天气数据，时间跨度为 10 到 30 年或更长。
* 位置映射服务，提供查找位置名或地理位置代码（经度和纬度）的能力，用于检索匹配请求的位置集。

## 定价模型
{: #pricing_models}

定价模型基于每分钟对 REST API 的调用数。每月对客户进行收费。免费和基本套餐允许您每分钟最多进行 10 个 API 调用。标准和高级套餐分别允许您每分钟进行 150 个和 375 个API 调用。每一种套餐都有允许的最大 API 调用数。

在应用程序中，除了调用数有限制外，您可以测试任何地理区域、预测类型或时间序列观察数据的天气数据。免费套餐、基本套餐、标准套餐和高级套餐可以在无合同的情况下进行购买。免费套餐允许您的应用程序进行 10,000 个调用。其余套餐分别允许您的应用程序每个月进行 150,000、2 百万或 5 百万个 API 调用。

还可以针对结算周期期间部署的每个服务实例购买多个付费套餐。如果您的应用程序使用超过 10,000 个调用，那么您需要与 IBM 订立一份服务持续供应的合同。

根据所选套餐，当应用程序达到所允许的每分钟 API 调用限制时，那么进行下一个 API 调用不会成功，直到您的应用程序允许请求更多 API 调用为止。

例如，如果您使用的是标准套餐，那么即使超出套餐限制（每分钟 150 个调用），应用程序*可以*在 1 分钟内进行 500 个 API 调用，但是在 5 分钟内将不允许进行下一个 API 调用。因此，用户可能会注意到应用程序中天气数据刷新有延迟。必须确保开发可以处理这些限制的应用程序，并且不大量请求 API 调用。可以改为监视应用程序的 API 调用使用量。可以通过检查 API 调用返回的项数，验证应用程序是否达到其套餐限制。

根据所选套餐，当应用程序达到所允许的每月 API 调用限制时，将会对下一个 API 调用收取每 10,000 个 API 调用平均 1.70 美元的费用。

## 反馈与支持
{: #feedback_support}

您可以通过搜索信息或在论坛提问来获取帮助。您还可以开具支持凭单。

使用论坛提问时，标记您的问题以便
{{site.data.keyword.Bluemix_notm}} 开发团队可以看到。


* 如果对使用 {{site.data.keyword.weather_short}} 开发
或部署应用程序有技术方面的问题，请在
[Stack
Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window} 上发布您的问题，并使用
**ibm-bluemix** 和 **weather**
标记您的问题。
* 如果使用此服务或入门指示信息时遇到任何问题，请使用
[IBM
developerWorks Answers 论坛](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}。请包含 bluemix 和 weather 标记。
* 如果您对将应用程序从 Insights for Weather 迁移到
{{site.data.keyword.weather_short}} 存在疑问，请在
[IBM
developerWorks](http://www.ibm.com/developerworks){:new_window} 上联系我们。

请参阅[获取帮助](https://console.{DomainName}/docs/support/index.html#getting-help){: new_window}以获取有关使用论坛的更多详细信息。

请参阅[联系支持](https://console.{DomainName}/docs/support/index.html#contacting-support){: new_window}以获取有关开具 IBM 支持凭单或有关支持级别和凭单严重性的信息。
