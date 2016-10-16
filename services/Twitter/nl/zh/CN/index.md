{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter 入门 {: #insights_twitter_overview}

*上次更新时间：2016 年 5 月 13 日*
{: .last-updated}

使用 {{site.data.keyword.twitterfull}} 可将 Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} 或 [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} 流中的 Twitter 内容包含在 {{site.data.keyword.Bluemix}} 应用程序中。
{:shortdesc}

要开始使用 {{site.data.keyword.twittershort}}，首先使用运行时（如 Liberty for Java）创建 Bluemix Web 应用程序，然后向应用程序添加 {{site.data.keyword.twittershort}} 服务。当 {{site.data.keyword.twittershort}} 服务绑定到应用程序时，即会使用唯一凭证来供应服务实例。应用程序使用这些凭证与 REST API，来搜索和使用 Twitter 内容。请遵循以下步骤，从 VCAP_SERVICES 检索凭证，并将服务实例与应用程序相集成。

1. 浏览至应用程序概述页面。
2. 转至**环境变量**部分。此时将显示每个服务的 `VCAP_SERVICES` 信息。
3. 请记下 {{site.data.keyword.twittershort}} 服务中的 username 和 password 值。为了测试 REST API 参考文档中的操作，您需要输入这些凭证。例如，`VCAP_SERVICES` 将类似于以下片段：

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

# 相关链接
{: #rellinks}
## 样本
{: #samples}
* [交互式 Decahose 搜索演示](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks：Decahose 搜索演示的教程和源代码](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [分析“美国狙击手”票房数据 (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [设置 Insights 动手实验室](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## API
{: #api}
* [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## 兼容运行时 
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## 一般信息
{: #general}
* [{{site.data.keyword.Bluemix_notm}} 服务中的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [向应用程序添加服务](../reqnsi.html){: new_window}
* [端到端开发](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 价格表](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

