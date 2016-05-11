---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.iotrtinsights_full}} 入门
{: #gettingstartedtemplate}
*上次更新时间：2016 年 2 月 11 日*

通过 {{site.data.keyword.iotrtinsights_full}} on Bluemix ({{site.data.keyword.iotrtinsights_short}})，可以对来自 Internet of Things 设备的实时数据执行分析，并深入了解这些设备的运行状况以及您的总体运营状况。
{:shortdesc}

您必须设置 {{site.data.keyword.iot_full}} 服务 ({{site.data.keyword.iot_short}}) 以将分析引擎连接到设备后，才能开始使用 {{site.data.keyword.iotrtinsights_short}}。可以使用现有 {{site.data.keyword.iot_short}} 服务，也可以创建新服务。要快速启动并运行此服务，可以将 Internet of Things 手机应用程序及其关联的 {{site.data.keyword.iot_short}} 服务部署到您的组织。

要快速启动并运行此服务，请执行以下步骤：
1. 将 {{site.data.keyword.iotrtinsights_short}} 服务部署到您的 Bluemix 组织。
  1. 在您的 Bluemix 帐户仪表板中，单击**使用服务或 API**。
  2. 找到服务目录的 Internet of Things 部分，并选择 **{{site.data.keyword.iotrtinsights_short}}**。
  3. 在 {{site.data.keyword.iotrtinsights_short}} 页面上，验证“添加服务”中的选择内容：  
    - 空间 - 验证您是否将该服务部署在 {{site.data.keyword.iot_short}} 服务部署所在的空间中。
    - 应用程序 - 保留未绑定状态。
    - 服务名称 -（可选）将服务名称更改为容易记住的名称。此名称会显示在 Bluemix 仪表板的 IoT {{site.data.keyword.iotrtinsights_short}} 磁贴中。
    - 所选套餐 - 根据您的需要，选择“免费套餐”或“购买套餐”。  
    > **重要信息：**使用免费 {{site.data.keyword.iotrtinsights_short}} 套餐时，每个组织只能部署该服务的一个实例。
  4. 单击**使用**以将 {{site.data.keyword.iotrtinsights_short}} 部署到您的 Bluemix 服务。
2. 可选：使用 IoT {{site.data.keyword.iotrtinsights_short}} 时，将您的手机用作 IoT 设备。
使用 Internet of Things 手机应用程序可快速将您的智能手机设置为充当 IoT 设备，以便可将其用于验证您的 {{site.data.keyword.iotrtinsights_short}} 环境，并开始定义对数据的实时分析。有关 Internet of Things 手机应用程序的更多信息，请参阅 [Internet of Things 手机应用程序](https://github.com/ibm-messaging/IoT-html5-phone)项目。

  要创建应用程序并将您的手机连接到 {{site.data.keyword.iot_full}}，请执行以下步骤：
  1. 单击下面的按钮以启动部署过程：
  [![“部署到 Bluemix”图标。](images/deploy_to_bluemix.png "“部署到 Bluemix”图标")](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "将 IoT 手机部署到 Bluemix")  
  > **注：**部署 Internet of Things 手机应用程序还会部署自动绑定到该手机应用程序的 {{site.data.keyword.iot_short}} 服务 (*iot-phone-iotf-service*)。将此 {{site.data.keyword.iot_short}} 添加为数据源，以测试 Internet of Things 手机应用程序。它还会创建该应用程序使用的 Cloudant NoSQL DB 服务 (*iot-phone-cloudant-cloudantNoSQLDB*)。

  2. 如果系统提示您对 IBM Single Sign On 服务（OAuth 同意）执行自助核准访问，请单击**核准**。  
  >**提示：**如果您没有 Bluemix 帐户，那么可以注册以激活免费 Bluemix 试用。
  2. 将“应用程序名称”字段更改为容易记住的名称；我们在这些指示信息的其余部分中都将此称为*手机应用程序*。此名称将显示在 Bluemix 仪表板的应用程序磁贴中，并且作为将您手机连接到 {{site.data.keyword.iot_short}} 时将使用的 URL 的一部分。
  2. 单击**部署**。
  2. 部署过程完成后，如果您看到“成功”消息，请返回到 Bluemix 仪表板。
  *手机应用程序*磁贴和 *iot-phone-iotf-service* 磁贴已添加到您的帐户。
  1. 在 Bluemix 仪表板中，单击*手机应用程序*磁贴。
  2. 从您的手机，打开浏览器并转至显示在应用程序名称下方的“路径 URL”。系统提示时，请输入您选择的设备标识，用于在 {{site.data.keyword.iot_short}} 和 IoT {{site.data.keyword.iotrtinsights_short}} 仪表板中将您的手机识别为设备。
  3. 单击**连接**以将您的手机连接到 {{site.data.keyword.iot_short}} *iot-phone-iotf-service*。
  视图会刷新，以显示从您的手机发送到 {{site.data.keyword.iot_short}} 的数据。
2. 创建并配置 Internet of Things 服务。  
> **提示：**如果部署了 Internet of Things 手机应用程序，那么 *iot-phone-iotf-service* 已经创建，因此可以跳过此步骤。  

  1. 登录到 Bluemix 组织，然后选择要在其中部署 IoT {{site.data.keyword.iotrtinsights_short}} 的空间。
  2. 在 Bluemix 仪表板中，单击**使用服务或 API**。
  3. 找到服务目录的 Internet of Things 部分，并选择 **Internet of Things**。
  4. 在 {{site.data.keyword.iot_full}} 页面上，验证“添加服务”中的选择内容，然后单击**使用**，以将 {{site.data.keyword.iot_short}} 添加到您的 Bluemix 服务。
  部署了 {{site.data.keyword.iot_short}} 服务后，会转至“服务管理”页面。
3. 找到连接 API 密钥。
如果创建了新的 {{site.data.keyword.iot_short}} 服务，那么现在必须创建用于连接这两个服务的 API 密钥。如果是使用现有服务，那么可以使用现有密钥。  
  1. 在 Bluemix 仪表板中，单击 Internet of Things 磁贴。  
  >**注：**如果使用的是 Internet of Things 手机应用程序，请单击 *iot-phone-iotf-service* 磁贴。  

  1. 单击**启动仪表板**以打开 {{site.data.keyword.iot_full}} 仪表板。
  2. 浏览至**访问 > API 密钥**。
  3. 单击**生成 API 密钥**。
  3. 记下显示在 {{site.data.keyword.iot_short}} 仪表板顶部的 API 密钥、认证令牌和组织标识。
  在 IoT {{site.data.keyword.iotrtinsights_short}} 中可使用这些信息来连接服务。
4. 连接您的 {{site.data.keyword.iot_short}} 服务与 IoT {{site.data.keyword.iotrtinsights_short}} 服务。
  1. 在 Bluemix 仪表板中，单击 IoT {{site.data.keyword.iotrtinsights_short}} 磁贴。  
  2. 在“服务”页面中，单击**添加数据源**。
  2. 在 {{site.data.keyword.iotrtinsights_short}} 控制台的“管理数据源”页面中，单击**添加新数据源**。
  3. 为数据源提供描述性名称，并提供先前收集的以下信息：
    - 组织标识
    - API 密钥
    - 认证令牌
  4. 单击 ![“创建”图标。](images/create.png "“创建”图标") 以创建数据源并连接到该数据源。
4. 开始使用 {{site.data.keyword.iotrtinsights_short}}。
现在，您可以通过添加用户、连接设备、配置仪表板以查看相关设备数据，以及设置警报，从而开始使用 {{site.data.keyword.iotrtinsights_short}}。
>**选择 {{site.data.keyword.iotrtinsights_short}} 实例：**如果已授权您以操作员或管理员身份访问任何其他 {{site.data.keyword.iotrtinsights_short}} 实例，那么您可以在这些实例之间快速切换。在 {{site.data.keyword.iotrtinsights_short}} 控制台中，单击您的用户名，然后选择要访问的实例。   

# 相关链接
## 样本
* [Internet of Things 手机应用程序](https://github.com/ibm-messaging/IoT-html5-phone)
* [developerWorks Internet of Things Recipes](https://developer.ibm.com/recipes/)
* [使用 Internet of Things Starter 应用程序创建应用程序](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## API
* [API 文档](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## 常规
* [关于](iotrtinsights_overview.html)   
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [{{site.data.keyword.iot_full}} 入门](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [IBM developerWorks 上的 dW Answers](https://developer.ibm.com/answers/topics/iot-real-time/)
