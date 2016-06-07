---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Weather 入门
{: #insights_weather_overview}

*上次更新时间：2016 年 5 月 19 日*

使用 {{site.data.keyword.weatherfull}} 可将来自 The Weather Company (TWC) 的数据合并到 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

**注：**Insights for Weather 服务目前未在日本提供。

开始之前，请先在仪表板中，使用运行时（如 Liberty for Java），创建 {{site.data.keyword.Bluemix_notm}} Web 应用程序。等待应用程序供应，然后向应用程序添加 Insights for Weather 服务。

将应用程序绑定到 Insights for Weather 后，即可使用唯一凭证来供应服务实例。您的应用程序使用这些凭证与 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，来检索天气数据。

请遵循下列步骤，从 `VCAP_SERVICES` 检索凭证，并将服务实例与应用程序相集成。

1. 浏览至应用程序概述页面。
2. 转至**环境变量**部分。这将显示每个服务的 `VCAP_SERVICES` 信息。
3. 记下 Insights for Weather 服务中的用户名和密码值。要尝试使用 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，必须在系统提示登录时输入这些凭证。`VCAP_SERVICES` 类似于以下示例：

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**注：**每个区域都是独立的。不能将在一个区域中为您供应的服务凭证用于向另一个区域中的服务进行认证。未输入正确的凭证将导致响应主体中显示“未授权”消息。 

# 相关链接
{: #rellinks}
## 样本
{: #samples}
* [Insights for Weather 演示](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 兼容运行时 
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般信息
{: #general}
* [Adding a service to your application](../reqnsi.html){: new_window}
* [端到端开发](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}价格表](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
