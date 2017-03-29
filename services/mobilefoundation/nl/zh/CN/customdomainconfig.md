---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 为 Mobile Foundation 服务器配置定制域
{: #configcustomdomain}

{{site.data.keyword.mobilefoundation_short}} 供应 {{site.data.keyword.mfserver_short_notm}}，其可通过域名基于<!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> {{site.data.keyword.Bluemix_notm}}**区域**的 URL 进行访问。您还可以配置自己的定制域。
{:shortdesc}

该<!--container group is created with a--> URL 或路径是使用基于 {{site.data.keyword.Bluemix_notm}} `区域`的缺省域名进行创建的。

  |域 |  区域  |    
  |:----- | :----- |    
  |`mybluemix.net` | 美国南部 |    
  |`eu-gb.mybluemix.net` | 英国  |
  |`au-syd.mybluemix.net` | 悉尼  |      
  {: caption="Table 1. Application domain names based on Region in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

为了可以使用您自己的域，将需要执行以下步骤来配置定制域：

1.	通过选择其中一个受支持套餐创建 {{site.data.keyword.mobilefoundation_short}} 服务实例来创建 {{site.data.keyword.mfserver_short_notm}} 实例。

+ 将要使用的定制域添加到 {{site.data.keyword.Bluemix_notm}} `组织`。转至**管理组织 > 域 > 添加域**以添加您自己的域。

+ 为<!--container group-->服务器设置路径以使用定制域。

+ 转至您的域所对应的 DNS 提供者，添加 CNAME 条目，这会将流量从您的域路由到正在运行<!--container group-->服务器的缺省 {{site.data.keyword.Bluemix_notm}} 路径。

+ 如果要为定制域配置 `https`，请将域的 SSL 证书上传到 {{site.data.keyword.Bluemix_notm}} 中。要执行此操作，请转至**管理组织 > 域**，选择要为其配置 SSL 证书的定制域，单击**上传证书**以上传域的 SSL 证书。请参阅 [SSL 证书和 Bluemix 定制域 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/){: new_window}，以了解更多信息。
