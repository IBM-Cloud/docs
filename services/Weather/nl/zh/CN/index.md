---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.weather_short}} 入门
{: #insights_weather_overview}

使用 {{site.data.keyword.weatherfull}} 可将来自 The Weather Company (TWC) 的数据合并到 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

**注意：**目前，在以下国家或地区，
**可能无法**购买或使用
{{site.data.keyword.weather_short}} 服务：阿富汗、亚美尼亚、
阿塞拜疆、巴林、孟加拉国、不丹、文莱、柬埔寨、中国、塞浦路斯、格鲁吉亚
、印度尼西亚、伊朗、伊拉克、日本、约旦、哈萨克斯坦、科威特、吉尔
吉斯斯坦、老挝、黎巴嫩、马来西亚、马尔代夫、蒙古、缅甸、尼泊尔、阿曼、
巴基斯坦、菲律宾、卡塔尔、俄罗斯、沙特阿拉伯、新加坡、阿拉伯、韩国、斯
里兰卡、叙利亚、塔吉克斯坦、东帝汶、土耳其、土库曼斯坦、阿拉伯联
合酋长国、乌兹别克斯坦、越南、也门。
当有其他信息可用时，会更新此列表。

如果您的现有应用程序使用 [Insights for Weather 服务](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window}，那么在引入 {{site.data.keyword.weather_short}} 之后的 90 天内，您的应用程序可继续运作而无需进行任何修改。
要利用新添加的 API 和改进的定价模型，您可以将应用程序迁移到新服务。


开始之前，请先在仪表板中，使用运行时（如 Liberty for Java），创建 {{site.data.keyword.Bluemix_notm}} Web 应用程序。等待应用程序供应，然后向应用程序添加 {{site.data.keyword.weather_short}} 服务。

将应用程序绑定到 {{site.data.keyword.weather_short}} 后，即可使用唯一凭证来供应服务实例。您的应用程序使用这些凭证与 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，来检索天气数据。

请遵循下列步骤，从 `VCAP_SERVICES` 检索服务凭证，并将服务实例与应用程序相集成。

1. 浏览至应用程序概述页面。
2. 转至**环境变量**部分。这将显示每个服务的 `VCAP_SERVICES` 信息。
3. 记下 {{site.data.keyword.weather_short}} 服务中的用户名和密码值。要尝试使用 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，必须在系统提示登录时输入这些凭证。`VCAP_SERVICES` 类似于以下示例：

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**注：**每个区域都是独立的。不能将在一个区域中为您供应的服务凭证用于向另一个区域中的服务进行认证。
未输入正确的凭证将导致响应主体中显示*未授权*消息。

# 相关链接
{: #rellinks}
## 样本
{: #samples}
* [{{site.data.keyword.weather_short}} 演示应用程序](http://weather-company-data-demo.{APPDomain}){: new_window}
* [{{site.data.keyword.weather_short}} 深入学习视频](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + Weather 样本应用程序](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - 裸机、纽约出租车数据和 Insights for Weather（YouTube 教程）](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

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
* [Adding a service to your application](/docs/services/reqnsi.html){: new_window}
* [端到端开发](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 价格表](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
