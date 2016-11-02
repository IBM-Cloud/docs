---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 故障诊断
{: #troubleshooting}

下面介绍了有关在 {{site.data.keyword.Bluemix_notm}} 上使用 {{site.data.keyword.iotinsurance_full}} 时常见的故障诊断问题的答案。
{:shortdesc}

## 部署应用程序的问题
{: #deployingapps}

如果在 {{site.data.keyword.Bluemix_notm}} 组织中没有足够的可用内存，那么可能无法为 {{site.data.keyword.iotinsurance_short}} 部署应用程序。您可以减少应用程序所使用的内存，也可以增加您帐户的内存配额。

### 问题描述

在打开 {{site.data.keyword.iotinsurance_short}} 服务时，未启用部署功能，因此无法部署任何应用程序。

### 问题原因

在您的组织中，必须提供不少于 2GB 的可用内存，才能启用部署功能。试用帐户的最大内存配额为 2GB。如果创建了 {{site.data.keyword.iotinsurance_short}} 以外的服务或应用程序，那么您组织的可用内存将不够部署 {{site.data.keyword.iotinsurance_short}} 应用程序。

### 解决方法

您可以增加帐户的内存配额，也可以减少服务和应用程序所使用的内存。

  - 要增加帐户的内存配额，您可以[将试用帐户转换为付费帐户](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)。

  - 要快速减少正在使用的内存，请移除 {{site.data.keyword.iotinsurance_short}} 以外的所有服务和应用程序。重新启动 {{site.data.keyword.iotinsurance_short}} 服务以使更改生效。

  - 如果使用内存总量超过 2GB 的付费帐户，就可以调整其他应用程序或服务所使用的内存量，这样就不必除去这些应用程序和服务。有关信息，请参阅[超过组织的内存限制](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)。
