---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iot_short_notm}} Starter 入门
{: #gettingstartedtemplate}
<!-- Provide and appropriate ID above -->
*上次更新时间：2016 年 6 月 27 日*
{: .last-updated}

通过使用 {{site.data.keyword.iot_short_notm}} Starter 样板，开始使用 {{site.data.keyword.iot_full}}。使用 Starter，您可以快速模拟设备、创建卡、生成数据并开始在 {{site.data.keyword.iot_short_notm}} 仪表板中分析和显示数据。
{: shortdesc}

Starter 会自动部署和连接以下服务：

{{site.data.keyword.iot_short_notm}} - 该平台为您提供多功能 IoT 工具箱，其中包括网关设备、设备管理和强大的应用程序访问。通过使用 {{site.data.keyword.iot_short_notm}}，您可以从组织收集已连接的设备数据，并对实时数据执行分析。

{{site.data.keyword.sdk4nodefull}} - 创建运行 Node-RED 的运行时环境。

{{site.data.keyword.cloudantfull}} - Node-RED 用于存储元数据的数据库。

## 关于 {{site.data.keyword.iot_short_notm}}
{: #about_iotplatform}
{{site.data.keyword.iot_short_notm}} 提供对 IoT 设备和数据的强大应用程序访问，可帮助您快速编写分析应用程序、可视化仪表板和移动 IoT 应用程序。
通过 {{site.data.keyword.iot_short_notm}}，您可以执行强大的设备管理操作，并存储和访问设备数据，连接各种设备和网关设备。{{site.data.keyword.iot_short_notm}} 通过使用 MQTT 和 TLS，提供与设备之间的安全通信。

## 关于 Node-RED
{: #about_nodered}
Node-RED 是一款以全新且有趣的方法，将硬件设备、API 和在线服务连接在一起的工具。您可以使用 Node-RED 创建模拟温度调节装置，以向 {{site.data.keyword.iot_short_notm}} 服务发送模拟数据。您可以创建卡，以在 {{site.data.keyword.iot_short_notm}} 仪表板中显示实时数据。有关更多信息，请参阅 [Node-RED 文档](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)。

## 浏览
{: #gettingaround}
当您执行以下步骤时，您将在浏览器中使用三个不同的选项卡：
  1. *{{site.data.keyword.Bluemix_notm}} 仪表板* - 使用 {{site.data.keyword.Bluemix_notm}} 仪表板，可以查看部署的状态、阅读文档并启动仪表板。
  2. *{{site.data.keyword.iot_short_notm}} 仪表板* - 使用该仪表板，可以处理此服务。您可以使用该仪表板，来定义设备类型、注册设备、监视传入传感器数据、创建数据可视化卡，并查看实时数据可视化。
  3. *Node-RED* - 以 node.js Web 应用程序运行，您将配置并运行设备模拟器流程，并使用其他流程，来处理来自 {{site.data.keyword.iot_short_notm}} 的数据。

## 在 {{site.data.keyword.iot_short_notm}} 中定义模拟设备
{: #definingsimdev}
向 {{site.data.keyword.iot_short_notm}} 注册设备：
  1.	在 {{site.data.keyword.Bluemix_notm}} 中，转至已部署应用程序的概述选项卡。
  2.	在“连接”部分或选项卡中，单击 {{site.data.keyword.iot_short_notm}} 框。
  3.	单击“启动”仪表板，以在新浏览器窗口中打开 {{site.data.keyword.iot_short_notm}} 仪表板。
  4.	选择设备
  5.	单击“添加设备”
  6.	在“添加设备”对话框中，单击“创建设备类型”。
  7.	在“创建设备类型”对话框中，单击“创建设备类型”。
  8. 输入设备类型的描述性名称和描述，如温度调节装置。
  9.	跳过：定义模板。
  10.	跳过元数据。
  11.	单击“创建”以添加新设备类型。
  12.	单击“下一步”，以添加设备（已预先选择“选择设备类型”）。
  13.	输入设备标识，如 LivingRoomThermo1。
  14.	跳过：输入设备元数据。
  15.	单击“下一步”以添加与自动生成的认证令牌的设备连接。
  16.	验证摘要信息是否正确，然后单击“添加”以添加连接。
  17.	在打开的设备信息页面中，复制并保存设备信息：
      -	组织标识
      -	设备类型
      -	设备标识
      - 认证方法
      - 认证令牌

**提示**：在接下来的几步中，您将需要“组织标识”、“设备类型”和“设备标识”，来最终化 Node-RED 应用程序的配置，以完成连接。

## 配置并运行 Node-RED 设备模拟器。
{: #confignodered}
配置 Node-RED 设备模拟器。使用设备模拟器，将 MQTT 设备消息发送到 {{site.data.keyword.iot_short_notm}}。设备模拟器会将温度和湿度信息发送到 {{site.data.keyword.iot_short_notm}}。

1. 在 Bluemix 仪表板中，通过选择**查看应用程序**或者单击链接（例如 http:// myIoTApp.mybluemix.net），来打开 Node-RED。
2.	单击**转至 Node-RED 流程编辑器**，以打开编辑器。
3.	双击“设备模拟器”流程中的蓝色“**发送**到 {{site.data.keyword.iot_short_notm}}”节点。
  1.	验证认证为 Bluemix 服务
  2.	从注册的设备粘贴“设备类型”。
  3.	从注册的设备粘贴“设备标识”。
  4.	单击“确定”。
4.	在 Node-RED 流程编辑器的右上角，单击**部署**。
5.	配置“Node-RED 温度监视器”流程
  1.	双击“设备模拟器”流程中的蓝色“IBM IoT 应用程序输入”节点。
  2.	将认证更改为 Bluemix 服务
  3.	针对“设备类型”、“设备标识”、“事件”和“格式”选择“所有”。
  4.	单击“确定”。
6.	在 Node-RED 流程编辑器的右上角，单击**部署**。
7.	验证设备连接
  1.	在其他浏览器选项卡或窗口中，返回到 {{site.data.keyword.iot_short_notm}} 仪表板。
  2.	选择“设备”并单击 LivingRoomThermo1 或添加的设备名称（如果不同的话）。此时将打开设备信息页面。通过此视图，您可以查看设备的连接状态。设备状态为已断开连接。
  3.	回到 Node-RED 流程编辑器，单击灰色“发送数据”节点上的按钮，以生成资产有效内容。
有效内容包含以下数据点：
  ```
  {"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
  ```
  4.	在右窗格的调试选项卡中，验证已创建消息。
  5.	在 {{site.data.keyword.iot_short_notm}} 设备信息页面中，验证您在“传感器信息”部分中，看到从设备接收到相同的数据点。

8.	将样本 IoT 设备连接到 {{site.data.keyword.iot_short_notm}}，以查看设备数据。

## 在 {{site.data.keyword.iot_short_notm}} 中创建卡以显示实时数据
{: #createcards}
要创建卡，请执行以下任务。

### 每隔 3 秒自动生成数据
1. 在 Node-RED 选项卡中，双击“发送数据”节点
2.	将“频率”设置为“每隔 3 秒”
3.	部署

### 在仪表板中创建新卡
1. 转至 {{site.data.keyword.iot_short_notm}} 仪表板浏览器选项卡。
2. 选择“电路板”。
3. 单击“创建新电路板”。
4. 为其提供名称，如“家庭环境”。
5. 创建。
6. 单击“添加新卡”（用于温度）。
   1.	在“设备”下，选择“实时图表”。
   2.	将源数据记录在卡上，检查您的设备“LivingRoomThermo1”，然后单击“下一步”。
   3. 连接新数据集。
       - 名称：温度
       - 事件：更新
       - 属性：temp
       - 类型：浮点
       - 单位：°C
       - 精度：2
       - 最小值：0
       - 最大值：50
       - 下一个
  4. 卡预览。
       - 选择 L
       - 下一个
  5. 卡信息。
       - 标题：温度
  6.	提交。
  7.	温度卡会显示在仪表板上，且包含实时温度数据的图形。
7.	单击“添加新卡”（用于湿度）。
  1.	在“设备”下，选择“显示更多”。
  2.	选择“标尺”。
  3.	将源数据记录在卡上，检查您的设备，然后单击“下一步”。
  4.	连接新数据集。
       -	名称：湿度
       -	事件：更新
       -	属性：humidity
       -	类型：浮点
       -	单位：“相对湿度 %”
       -	精度：1
       -	最小值：10
       -	最大值：95
       -	下一个
  5.	卡预览。
       -	设置
          -	阈值下限：40，一般
          -	中间值：良好
          -	阈值上限：50%，一般
       -	选择 M
       -	下一个
  6.	卡信息。
       -	标题：湿度
  7.	提交。
  8.	湿度卡会显示在仪表板上，且包含显示实时湿度数据的标尺。
8.	单击“添加新卡”（用于位置）。
  1.	在“设备”下，选择“显示更多”。
  2.	选择“值”。
  3.	将源数据记录在卡上，检查您的设备“LivingRoomThermo1”，然后单击“下一步”。
  4.	连接新数据集。
       -	名称：纬度
       -	事件：更新
       -	属性：location.latitude
       -	类型：浮点
       -	单位：“°N”
       -	精度：2
       -	最小值：-180
       -	最大值：180
  5. 连接新数据集。
       -	名称：经度
       -	事件：更新
       -	属性：location.longitude
       -	类型：浮点
       -	单位：“°E”
       -	精度：2
       -	最小值：-180
       -	最大值：180
       -  下一个
  6.	卡预览。
       -	选择 L
       -	下一个
  7.	卡信息。
       -	标题：位置
  8.	提交。
9.	观察新卡随 Node-RED 流程生成的模拟器数据进行实时更新。
**注**：Node-RED 会持续发送数据，直到您将其停止为止。
10.	在 Node-RED 流程编辑器中，将“发送数据”节点更新为“频率：无”。
11.	部署。

## 后续步骤？
{: #whatsnext}
现在，您的模拟设备正在将数据发送到 {{site.data.keyword.iot_short_notm}}，您可以继续反复执行 IoT 项目。

1. [搜索 IoT 诀窍](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot)，以连接物理设备（如 Raspberry Pi）并将数据发送到 {{site.data.keyword.iot_short_notm}}。
2. [部署样本 node.js 应用程序，以对设备数据进行可视化处理。](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)
3.	用密码保护 Node-RED 流程编辑器。缺省情况下，任何人员都可以打开编辑器来访问和修改流程。要用密码保护编辑器，请执行以下任务：
  1.	在 Bluemix 仪表板中，选择应用程序的“环境变量”页面。
  2.	添加以下用户定义的变量：
       -	NODE_RED_USERNAME - 用于保护编辑器的用户名
       -	NODE_RED_PASSWORD - 用于保护编辑器的密码
  3.	单击“保存”。


# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}
* [连接设备的诀窍](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} Play 组织](https://play.internetofthings.ibmcloud.com/){:new_window}
* [将 Intel Galileo 连接到 {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [连接 ARM&reg; mbed&trade; IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [将 Raspberry Pi 连接到 {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API 参考
{: #api}
* [{{site.data.keyword.iot_short}} API 文档](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}


## 相关链接
{: #general}
* [{{site.data.keyword.iot_short_notm}} 文档](https://www.bluemix.net/docs/services/IoT/iotplatform_overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} Starter 文档](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html){:new_window}
