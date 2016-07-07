---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为 {{site.data.keyword.mobilefoundation_short}} 服务器配置定制域
{: #configcustomdomain}

*上次更新时间：2016 年 6 月 15 日*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} 在 {{site.data.keyword.containerlong}} 上将 {{site.data.keyword.mfserver_short_notm}} 作为容器组供应。容器组将映射到域名基于 {{site.data.keyword.Bluemix_notm}} **区域**的 URL。您还可以配置自己的定制域。
{:shortdesc}

容器组使用缺省域名基于 {{site.data.keyword.Bluemix_notm}} `区域`的 URL 或路径创建。

*表 1. 基于 {{site.data.keyword.Bluemix_notm}}* 中的“区域”的应用程序域名

  |域 |  区域  |    
  |:----- | :----- |    
  |`mybluemix.net` | 美国达拉斯  |    
  |`eu-gb.mybluemix.net` | 英国伦敦  |    
  |`au-syd.mybluemix.net`  | 澳大利亚悉尼 |  

为了可以使用您自己的域，将需要执行以下步骤来配置定制域：

1.	通过选择其中一个受支持套餐创建 {{site.data.keyword.mobilefoundation_short}} 服务实例来创建 {{site.data.keyword.mfserver_short_notm}} 实例。

+ 将要使用的定制域添加到 {{site.data.keyword.Bluemix_notm}} `组织`。转至**管理组织 > 域 > 添加域**以添加您自己的域。

+ 设置容器组的路径以使用定制域。

+ 转至您的域所对应的 DNS 提供者，添加 CNAME 条目，这会将流量从您的域路由到正在运行容器组的缺省 {{site.data.keyword.Bluemix_notm}} 路径。

+ 如果要为定制域配置 `https`，请将域的 SSL 证书上传到 {{site.data.keyword.Bluemix_notm}} 中。要执行此操作，请转至**管理组织 > 域**，选择要为其配置 SSL 证书的定制域，单击**上传证书**以上传域的 SSL 证书。请参阅 [SSL 证书和 Bluemix 定制域](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/)，以获取更多信息。
