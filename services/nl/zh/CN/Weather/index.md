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

*上次更新时间：2016 年 4 月 6 日*

使用 {{site.data.keyword.weatherfull}} 可将来自 The Weather Company (TWC) 的数据合并到 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

以下指示信息将逐步指导您完成创建应用程序、将应用程序绑定到 Insights for Weather 服务，以及检索服务凭证以便与 [REST API](https://twcservice.{APPDomain}/rest-api/) 进行交互的过程。

### 创建应用程序
{: #create_an_app}

出于演示目的，您使用 Liberty for Java 运行时创建了应用程序，但以下常规过程可适用于其他运行时。

1. 如果没有现有的应用程序，请在仪表板中，单击**创建应用程序**。
2. 系统要求您选择应用程序模板时，请单击 **Web**。
3. 系统要求您选择入门模板时，请单击 **Liberty for Java**。
4. 单击**继续**。
5. 在**应用程序名称**字段中，输入应用程序的名称。
6. 单击**完成**。等待应用程序供应。

### 添加 Insights for Weather 服务
{: #add_insights_for_weather_service}

执行以下步骤向应用程序添加 Insights for Weather 服务。
1. 打开**目录**菜单。
2. 在**数据和分析**部分中，单击 **Insights for Weather** 磁贴。
3. 在**应用程序**下拉列表中，选择应用程序。
4. 单击**使用**。
5. 系统提示时，单击**重新编译打包**以重新启动应用程序。

### 检索 Insights for Weather 凭证
{: #retrieve_weather_credentials}

将应用程序绑定到 Insights for Weather 后，即可使用唯一凭证来供应服务实例。这些凭证存储在应用程序的 `VCAP_SERVICES` 中，对于支持服务之间进行交互是必需的。

1. 浏览至应用程序概述页面。
2. 转至**环境变量**部分。这将显示每个服务的 `VCAP_SERVICES` 信息。
3. 记下 Insights for Weather 服务中的 username 和 password 值。要尝试使用 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}，必须在系统提示登录时输入这些凭证。`VCAP_SERVICES` 类似于以下示例：

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

# 相关链接
## 样本
* [Insights for Weather 演示](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 兼容运行时 {:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般信息
* [关于 Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Adding a service to your application](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [端到端开发](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}价格表](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
