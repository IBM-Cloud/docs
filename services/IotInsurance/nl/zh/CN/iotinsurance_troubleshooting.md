---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iotinsurance_short}} 故障诊断
{: #ts}

下面介绍了有关在 {{site.data.keyword.Bluemix_notm}} 上使用 {{site.data.keyword.iotinsurance_full}} 时常见的故障诊断问题的答案。
{:shortdesc}

## 部署应用程序的问题
{: #deployingapps}
如果在 {{site.data.keyword.Bluemix_notm}} 组织中没有足够的可用内存，那么可能无法为 {{site.data.keyword.iotinsurance_short}} 部署应用程序。您可以减少应用程序所使用的内存，也可以增加您帐户的内存配额。
{:shortdesc}

在打开 {{site.data.keyword.iotinsurance_short}} 服务时，未启用部署功能，因此无法部署任何应用程序。
{: tsSymptoms}

在您的组织中，必须提供不少于 2GB 的可用内存，才能启用部署功能。试用帐户的最大内存配额为 2GB。如果创建了 {{site.data.keyword.iotinsurance_short}} 以外的服务或应用程序，那么您组织的可用内存将不够部署 {{site.data.keyword.iotinsurance_short}} 应用程序。
{: tsCauses}

您可以增加帐户的内存配额，也可以减少服务和应用程序所使用的内存。
- 要增加帐户的内存配额，您可以[将试用帐户转换为付费帐户](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)。
- 要快速减少正在使用的内存，请移除 {{site.data.keyword.iotinsurance_short}} 以外的所有服务和应用程序。重新启动 {{site.data.keyword.iotinsurance_short}} 服务以使更改生效。
- 如果使用内存总量超过 2GB 的付费帐户，就可以调整其他应用程序或服务所使用的内存量，这样就不必除去这些应用程序和服务。有关信息，请参阅[超过组织的内存限制](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)。
{: tsResolve}

## 性能问题
{: #performance_issues}

在峰值活动时间段内，可能会遇到性能下降。
{:shortdesc}

频繁进行 API 调用的繁忙系统可能会遇到响应时间延迟。
{: tsSymptoms}

缺省情况下，{{site.data.keyword.iotinsurance_short}} 会部署试用版本的 {{site.data.keyword.cloudantfull}}。此版本限制了每秒可以进行的 API 调用数。
{: tsCauses}

升级到标准版本的 {{site.data.keyword.cloudant}}。
{: tsResolve}

## 获取关于 {{site.data.keyword.iotinsurance_short}} 的帮助和支持
{: #gettinghelp}

如果您在使用 {{site.data.keyword.iotinsurance_full}} 时遇到任何问题或疑问，可以检查 {{site.data.keyword.Bluemix_notm}}，或者通过论坛搜索信息或进行提问来获取帮助。您还可以提交支持凭单。

- 您可以通过转至 [Bluemix 状态页面 ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window} 来检查 {{site.data.keyword.Bluemix_notm}} 是否可用。

- 可以查看论坛以了解是否有其他用户遇到相同问题。使用论坛进行提问时，请对问题进行标记，以便 {{site.data.keyword.Bluemix_notm}} 开发团队能看到您的问题。
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- 有关使用 {{site.data.keyword.iotinsurance_short}} 开发或部署应用程序的技术问题，请将问题发布到 [Stack Overflow ![外部链接图标](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} 上，并使用“ibm-bluemix”和“iot-for-insurance”标注问题。
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- 有关服务和入门指示信息的问题，请使用 [IBM developerWorks dWAnswers ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window} 论坛。请加上“iot-for-insurance”和“bluemix”标记。

请参阅[获取帮助](https://www.{DomainName}/docs/support/index.html#getting-help)，以获取有关使用论坛的更多详细信息。

- 如果仍不能解决问题，可以提交 IBM 支持凭单。有关提交 IBM 支持凭单或者有关支持级别和凭单严重性的信息，请参阅[联系支持人员](../support/index.html#contacting-support)。
