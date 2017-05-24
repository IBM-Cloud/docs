---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 入门模板入门
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

通过使用 {{site.data.keyword.iot_short_notm}} Starter GitHub 项目开始使用 {{site.data.keyword.iot_full}}。通过使用该入门模板，您可以快速模拟设备，创建卡，生成数据，开始分析数据并在 {{site.data.keyword.iot_short_notm}} 仪表板中显示数据。  
{:shortdesc}

## 概述
{: #overview}  

该入门模板会自动部署并连接这些服务：
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>包含网关管理、设备管理和应用程序访问在内的 IoT Web 服务。通过使用 {{site.data.keyword.iot_short_notm}}，您可以从组织收集已连接的设备数据，并运行实时数据分析。
</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>Node-RED 在其中运行的运行时环境。</br>有关更多信息，请参阅 [{{site.data.keyword.sdk4nodefull}} 入门模板文档](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html)。</dd>
<dd>Node-RED 这款工具以全新的有趣方式将硬件设备、API 和在线服务连接在一起。您可以使用 Node-RED 来创建模拟温度调节装置，该装置将模拟数据发送到 {{site.data.keyword.iot_short_notm}} 服务。您可以创建用于在 {{site.data.keyword.iot_short_notm}} 仪表板中显示实时数据的卡。</br>有关更多信息，请参阅 [Node-RED 文档](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)。</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Node-RED 在其中存储元数据的数据库。</dd>
</dl>

## 开始之前
{: #byb}  

- 所需帐户  
开始之前，您需要先有一个 [IBM Bluemix 帐户](https://bluemix.net/registration)。

- 来回切换  
在后续过程中，为了能在各个任务之间轻松切换，请在浏览器的不同选项卡中打开 {{site.data.keyword.Bluemix_notm}} 仪表板、{{site.data.keyword.iot_short_notm}} 仪表板以及 Node-RED 应用程序。
<dl>
<dt>*{{site.data.keyword.Bluemix_notm}} 仪表板*</dt>
<dd>查看部署状态，阅读文档，并启动仪表板。</dd>
<dt>*{{site.data.keyword.iot_short_notm}} 仪表板*</dt>
<dd>定义设备类型，注册设备，监视传入传感器数据，创建数据可视化卡，并查看实时数据可视化。</dd>
<dt>*Node-RED*</dt>
<dd>配置并运行设备模拟器流程，使用其他流程来处理来自 {{site.data.keyword.iot_short_notm}} 的数据。</dd>
</dl>

## 步骤 1：部署 {{site.data.keyword.iot_short_notm}} 入门模板
{: #deployStarter}

执行下列步骤以部署该入门模板样本应用程序：

1. 部署入门模板应用程序。
 1. 单击 <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a> 在 Bluemix 中创建新的 Continuous Delivery 工具链：（通过 Continuous Delivery）  
 **提示：**如果更希望从命令行进行部署，那么可以在 GitHub 的 IBM Watson IoT 组织中[查找 {{site.data.keyword.iot_short_notm}} 入门模板](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter)。
 2. 在系统提示时，登录 IBM Bluemix。
 3. 如果需要，可以选择要部署入门模板应用程序的 Bluemix 组织。
 4. 可以保留该工具链的名称，也可以根据需要更新其名称。该名称被用作缺省应用程序名称以及应用程序 URL 的根目录：`<app-name>.mybluemix.net`
 5. 单击**创建**。  
**提示：**单击 **Delivery Pipeline** 磁贴可监视第一次部署的进度。
 6. 部署完成后，单击**查看应用程序**可在新选项卡中打开新的 Node-RED 应用程序。
2. 找到入门模板应用程序服务的位置。
 1. 在 Bluemix 菜单中，选择**仪表板**。
 2. 在*全部服务*下找到下列服务：
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. 在*全部应用程序*下找到该工具链：
    - default-toolchain-{id}}


## 步骤 2：在 {{site.data.keyword.iot_short_notm}} 中定义模拟设备
{: #definingsimdev}

完成下列步骤以模拟使用温度调节装置监视客厅温度、湿度和位置的场景。

1.	启动 {{site.data.keyword.iot_short_notm}} 仪表板。
  1. 在 Bluemix 仪表板中，在*全部服务*下，单击 {{site.data.keyword.iot_short_notm}} 实例的名称。
**提示：**实例名称中通常包含 `iotp-starter`。
  2. 单击**启动**在新的浏览器选项卡中打开 {{site.data.keyword.iot_short_notm}} 仪表板。   
缺省情况下，将显示`全部板`页面。
2. 创建设备类型。
  1.	在主菜单中，选择**设备**，然后单击**添加设备**。
  2.	在“添加设备”页面中，单击**创建设备类型**。
  3.	在“创建设备类型”页面中，单击**创建设备类型**。
  4. 输入该设备类型的唯一名称（例如`温度调节装置`），然后单击**下一步**。
  5. 可选：可以选择在接下来的两页中定义模板和元数据，也可以在每页上单击**下一步**轻松跳过。
  6.	单击**创建**以添加设备类型。
3.	添加使用新创建的设备类型的设备。
  1. 在“添加设备”页面中，您刚刚创建的设备类型会显示在设备类型列表中。单击**下一步**以添加使用该设备类型的设备。
  2. 输入唯一的设备标识（例如`客厅温度调节装置1`）。
  3. 可选：可以选择在“添加设备”页面上提供描述性数据或者在下一页上输入设备元数据，也可以在每页上单击**下一步**轻松跳过这些页面。
  4. 在“安全性”页面上，单击**下一步**以生成设备的认证令牌。
  5. 在“摘要”页面上，验证信息是否正确，然后单击**添加**以添加该设备。单击**返回**以返回到上一页。
4.	记下在“您的设备凭证”页面上显示的信息。   
要配置模拟器和显示数据，需要用到以下信息：
 - 组织标识
 - 设备类型
 - 设备标识
 - 认证方法
 - 认证令牌

## 步骤 3：配置并运行 Node-RED 设备模拟器。  
{: #confignodered}  
配置 Node-RED 设备模拟器以将 MQTT 设备消息以及温度和湿度信息发送到 {{site.data.keyword.iot_short_notm}}。

1. 启动 Node-RED 流程编辑器。
  1. 在 Bluemix 仪表板中，在*全部应用程序*下，单击工具链的名称。  
**提示：**工具链名称中通常包含 `default-toolchain...`。
  2. 在工具链仪表板中，单击**路径**并选择该路径链接以打开 Node-RED 实例。  
  2. 单击**转至 Node-RED 流程编辑器**，以打开编辑器。
2. 部署设备。
  1. 在“设备模拟器”流程中，双击蓝色的**发送到 IBM IoT Platform** 节点。
  2. 验证认证是否已设为 **Bluemix 服务**。
  3. 输入设备的**设备类型**和**设备标识**，然后单击**完成**。
  4. 单击**部署**以部署设备。
3. 配置 Node-RED 温度监视流程。
  1. 在“设备模拟器”流程中，双击蓝色的 **IBM IoT 应用程序进入**节点。
  2. 在“认证”中，选择 **Bluemix 服务**。
  3.	“设备类型”、“设备标识”、“事件”和“格式”都选择**全部**。
  4.	单击**完成**。
  5.  单击**部署**以部署监视。
4. 验证设备连接。
  1.	打开 {{site.data.keyword.iot_short_notm}} 仪表板。  
**提示：**如果 {{site.data.keyword.iot_short_notm}} 仪表板尚未在其他选项卡中打开，请返回 {{site.data.keyword.Bluemix_notm}} 仪表板，单击 {{site.data.keyword.iot_short_notm}} 实例的名称，然后单击**启动仪表板**。
  2. 在主菜单中，选择**设备**。
  3. 单击您添加的设备的名称。   
设备信息会显示设备的连接状态。
  4.	在 Node-RED 流程编辑器中，双击**发送数据**节点，将“重复”值设为**时间间隔**，将频率设为每 `3` 秒。
  5. 单击**完成**。
  6. 单击**部署**以部署更改。  
有效内容中包含数据点，如以下示例中所示：
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. 可选：打开“调试”选项卡以验证是否正在创建消息。
    1. 在标题部分的菜单中，选择**查看**。
    2. 选择**显示侧边栏**。
    3. 单击“调试”选项卡以查看消息。
  8. 在“{{site.data.keyword.iot_short_notm}} 设备信息”页面中，验证在“传感器信息”部分中能否看到设备的数据点。


## 步骤 4：在 {{site.data.keyword.iot_short_notm}} 中创建用于显示实时数据的卡  
{: #createcards}  
创建板和卡以在 {{site.data.keyword.iot_short_notm}} 仪表板中显示设备数据。有关板和卡的更多信息，请参阅[使用板和卡实现实时数据可视化](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)。

1. 创建板
  1. 打开 {{site.data.keyword.iot_short_notm}} 仪表板。  
  **提示：**如果 {{site.data.keyword.iot_short_notm}} 仪表板尚未在其他选项卡中打开，请返回 {{site.data.keyword.Bluemix_notm}} 仪表板，单击 {{site.data.keyword.iot_short_notm}} 实例的名称，然后单击**启动仪表板**。  
  2. 创建用于包含模拟设备卡的板。
    1. 如果未显示“全部板”页面，请在 {{site.data.keyword.iot_short_notm}} 仪表板主菜单中选择**板**，然后单击**新建板**。
    2. 输入板的名称（例如`住宅环境`），然后单击**下一步**。
    3. 在下一个页面上，单击**提交**。  
  3. 单击刚刚创建的板以将其打开。
2. 创建用于显示温度的卡
  1. 在“设备”部分中，单击**添加新卡**，然后选择**折线图**卡类型。
  2. 从设备列表中选择设备，然后单击**下一步**。
  3. 单击**连接新数据集**。
  4. 在“创建值卡”页面中，选择或输入下列值，然后单击**下一步**。
    - 事件：update
    - 属性：temp
    - 名称：温度
    - 类型：浮点数
    - 单位：°C
    - 精度：2
    - 最小：0
    - 最大：50
  5. 在“卡预览”页面中，为折线图大小选择 **L**，然后单击**下一步**。
  6. 在“卡信息”页面中，将卡名称更改为**温度**，然后单击**提交**。   
温度卡会显示在仪表板上，其中包含实时温度数据的折线图。
3. 创建用于显示湿度的卡
  1. 在“设备”部分中，单击**添加新卡**，然后选择**标尺**卡类型。
  2. 从设备列表中选择设备，然后单击**下一步**。
  3. 单击**连接新数据集**。
  4. 在“创建值卡”页面中，选择或输入下列值，然后单击**下一步**。事件：update
     - 属性：humidity
     - 名称：湿度
     - 类型：浮点数
     - 单位：%
     - 精度：1
     - 最小：10
     - 最大：95
  5. 在“卡预览”页面中，为标尺大小选择 **M**，然后单击**下一步**。
  6. 在“卡信息”页面中，将卡名称更改为**湿度**，然后单击**提交**。   
湿度卡会显示在仪表板上，其中包含显示实时温度数据的标尺。  

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## 后续步骤  
{: #whats-next}  
现在您的模拟设备已经在向 {{site.data.keyword.iot_short_notm}} 发送数据，因此您可以继续迭代 IoT 项目。
 - 观察卡是否显示 node-RED 流程所生成的数据。  
Node-Red 会一直发送数据，直到您将其停止为止。要停止模拟数据，请停止下列步骤：
    1.	在 Node-RED 流程编辑器中，双击灰色的**发送数据**节点，将“重复”值设为**时间间隔**，将频率设为每 **3** 秒。
    2. 单击**完成**。
    3. 单击**部署**以部署更改。

 - 连接物理设备。  
[搜索 IoT 诀窍](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot)以连接如 Raspberry Pi 等物理设备，并将数据发送到 {{site.data.keyword.iot_short_notm}}。

 - 体验可视化选项。  
[部署样本 node.js 应用程序以实现设备数据可视化](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)。

 -	密码保护 Node-RED 流程编辑器。   
缺省情况下，编辑器会为访问和修改流程的所有用户打开。要使用密码保护编辑器，请执行下列任务：
    1.	在 {{site.data.keyword.Bluemix_notm}} 仪表板中，单击入门模板应用程序的名称以打开应用程序页面。
    2. 单击**运行时**以显示“运行时”页面。
    3. 单击**环境变量**以显示“环境变量”页面。
    4. 在**用户定义**部分中，单击**添加**，然后输入下列用户定义的变量：
         -	NODE_RED_USERNAME - 用于保护编辑器安全的用户名
         -	NODE_RED_PASSWORD - 用于保护编辑器安全的密码
    3.	单击**保存**。
