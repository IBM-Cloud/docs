---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}

# 关于 {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}
*上次更新时间：2016 年 9 月 19 日*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} 是完全集成的 IoT 生产实例，允许应用程序与互联家电、传感器和网关进行通信，以及使用这些互联家电、传感器和网关收集的数据。
{:shortdesc}

{{site.data.keyword.iotelectronics}} 使用 {{site.data.keyword.iot_full}} 服务，将智能电器与您开发的应用程序相连接。它还会使用 {{site.data.keyword.iot_short_notm}} 来帮助您分析和理解来自家电的数据。您可以建立规则以识别需要注意的状况，并定义自动响应，如发送电子邮件、执行 Node-RED 工作流程或连接到 Web 服务。  

## 查找 Starter
{: #iot4eFindingStarter}
您可以在 {{site.data.keyword.Bluemix_notm}} 目录的[样板](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/)部分，查找 {{site.data.keyword.iotelectronics}} Starter。  

## 使用 {{site.data.keyword.iotelectronics}} 您可以执行的操作
{: #Features_iote}
通过使用模拟家电和数据，快速浏览 {{site.data.keyword.iotelectronics}} 解决方案的功能。

### 连接模拟家电
创建模拟家电，并将它们连接到平台，以查看流式实时数据。使用基于 Web 的应用程序，来模拟家电如何接收命令并执行操作。模拟故障以生成通知和警报。出于演示目的，洗衣机将用作 {{site.data.keyword.iotelectronics}} Starter 内的模拟家电。选择连接的家电可以是任何类型的智能电子设备。  

### 尝试样本消费者移动应用程序
使用 iOS 电话，查看家电所有者可以如何与家电进行交互。使用平台和 {{site.data.keyword.Bluemix_notm}}，发送命令到家电，并从家电接收更新。模拟故障事件并在移动应用程序中查看结果。

### 连接您拥有的电子设备
将您拥有的家电安全地连接到云，并开始定制自己的应用程序。提供一系列经过验证的示例和诀窍，您可进行修改并用于概念验证、测试和试验。

## {{site.data.keyword.iotelectronics}} Starter 的功能
{: #whatsInStarter}
入门模板样板会部署集成的 {{site.data.keyword.iotelectronics}} 解决方案。系统会为您自动绑定和部署所有组件。通过使用模拟家电和数据，入门模板应用程序使您能够快速浏览解决方案的功能。样本移动应用程序为您显示消费者可以如何进行注册、接收警报和控制互联家电。您可以使用样本作为起点，来创建自己的应用程序，并从自己的家电收集数据。解决方案中包含以下服务和应用程序：

![{{site.data.keyword.iotelectronics}} 体系结构。此图在主题的主体中进行描述。](images/IoT4E_architecture.svg "{{site.data.keyword.iotelectronics}} 体系结构")

{{site.data.keyword.iotelectronics}} Starter 使用 {{site.data.keyword.iotelectronics}} 服务和 API 与 {{site.data.keyword.iot_short_notm}} 连接。入门模板应用程序和样本移动应用程序与 {{site.data.keyword.iotelectronics}} 服务进行通信，并通过 {{site.data.keyword.amafull}} 相互连接。入门模板中包含以下组件：

**{{site.data.keyword.iotelectronics}} 服务**支持用户和家电注册与通知。

**{{site.data.keyword.iot_full}}** 允许应用程序与连接的家电、传感器和网关进行通信，以及使用这些对象收集的数据。

<!-- **{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your appliances, visualize what's happening now, and respond to emerging conditions by using automated actions. -->

**{{site.data.keyword.amafull}}** 允许移动应用程序的用户使用现有的社交帐户登录，并确保与后端系统的通信安全。

**{{site.data.keyword.sdk4nodefull}}** 允许您开发、部署和扩展服务器端 JavaScript&reg; 应用程序，并提供增强的性能、安全性和可维护性。

**样本移动应用程序**允许您使用 iOS 电话查看模拟家电的状态，并与模拟家电进行通信。在[使用移动应用程序](iotelectronics_config_mobile.html)中找到如何获取移动应用程序。

# 相关链接
{: #rellinks}
## 组件
{: #general}
* [{{site.data.keyword.iot_short}} 文档](https://new-console.ng.bluemix.net/docs/services/IoT/index.html#gettingstartedtemplate)
* [{{site.data.keyword.amafull}} 文档](https://new-console.ng.bluemix.net/docs/services/mobileaccess/index.html)
* [{{site.data.keyword.sdk4nodefull}} 文档](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)


## API 文档
{: #api}
*  [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)  
*  [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)
