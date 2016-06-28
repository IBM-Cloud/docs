---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# 使用 {{site.data.keyword.iotelectronics}} Starter 创建应用程序
*上次更新时间：2016 年 6 月 14 日*

{{site.data.keyword.iotelectronics_full}} 是集成的端到端解决方案，通过该解决方案，您的应用程序可以与相连接的设备进行通信，并控制、分析和更新相连接的设备。入门模板包括入门模板应用程序，通过该应用程序，您可以创建和控制模拟设备和样本移动应用程序，使您能够从移动设备控制那些设备。
{:shortdesc}

**先决条件**：  
确保您已从 Bluemix 目录的“样板”部分部署 {{site.data.keyword.iotelectronics}} Starter。这样做可自动部署入门模板的组件应用程序和服务，包括 {{site.data.keyword.amafull}}。

要开始使用 {{site.data.keyword.iotelectronics}}，请完成后续部分中所述的下列任务：

1. 通过配置 {{site.data.keyword.amashort}}，启用与样本移动应用程序的通信。
2. 使用 {{site.data.keyword.iotelectronics}} Starter Web 应用程序，创建模拟设备。
3. 安装并连接样本移动应用程序。

## 配置 {{site.data.keyword.amashort}}
{: #configureMCA}
要使用移动应用程序，您必须配置 {{site.data.keyword.amashort}}，如下所示：
1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板中，打开 [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)。
2. 在**定制**部分中，选择**配置**。
3. 输入下列认证凭证：
  - **域名**：myRealm
  - **URL**：https://<*myIoT4eStarterApp*>.mybluemix.net  

    **提示：**确保在 URL 中使用安全的 `https://` 前缀。您可以单击**移动选项**，查找入门模板应用程序的 URL。
4. 保存。

  有关详细指示信息，请参阅[配置 {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA)

##创建模拟设备
要创建模拟设备，请执行下列步骤：
1. 在 {{site.data.keyword.Bluemix_notm}} 仪表板中，启动 {{site.data.keyword.iotelectronics}} 应用程序
2. 等待`您的应用程序正在运行`状态消息，然后单击**查看应用程序**，以显示入门模板应用程序。  
3. 选择**远程控制连接的设备**
4. 滚动到**接下来选择或添加新的模拟洗衣机**，然后单击“添加”(+) 按钮。此时将创建新洗衣机。

## 安装并连接样本移动应用程序
要安装并连接样本移动应用程序，请执行下列步骤：

*注*：您必须具有 iOS 设备，才能使用样本移动应用程序。

1. 在您的手机上，打开 App Store，并搜索 `ibm iot`。选择 **IBM IoT for Electronics** 并安装。
2. 通过扫描入门模板应用程序中找到的“连接 QR 码”，将您的手机连接到组织。
3. 通过扫描入门模板应用程序中找到的“设备 QR 码”，连接您的模拟设备。

  有关详细指示信息，请参阅[将移动应用程序连接到 {{site.data.keyword.iotelectronics}} 环境](iotelectronics_config_mobile.html#iot4e_connecting_mobile)

##后续工作
查看使用 {{site.data.keyword.iotelectronics}} 可以执行的操作。

- 浏览入门模板应用程序，以了解企业制造商可以如何监视连接到 {{site.data.keyword.iot_short_notm}} 的设备。
- 浏览样本移动应用程序，以了解设备所有者可以如何注册其设备并与之进行互动。
- 手动使得设备发生故障，以向制造商和设备所有者触发警报、通知和操作。
- 将运作数据与用户数据相关联，以了解您的产品和设备如何运作，以及何人正在对其进行操作。


# 相关链接
{: #rellinks}
## API 文档
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## 组件
{: #general}

* [{{site.data.keyword.iotelectronics_full}} 文档](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## 样本
{: #samples}
* [样本移动应用程序](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
