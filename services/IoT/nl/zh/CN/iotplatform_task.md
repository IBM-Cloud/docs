---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 连接设备
{: #iotplatform_task}

必须将 IoT 设备连接到 {{site.data.keyword.iot_full}}，才可开始从其接收数据。将设备连接到 {{site.data.keyword.iot_short_notm}} 涉及向 {{site.data.keyword.iot_short_notm}} 注册该设备，然后使用注册信息来配置该设备以连接到 {{site.data.keyword.iot_short_notm}}。
{:shortdesc}

## 开始之前
{: #byb}

启动连接过程之前，必须确保您的设备满足与 {{site.data.keyword.iot_short_notm}} 通信的以下需求：

- 您的设备必须能够使用 HTTP 或 MQTT 协议进行通信。
- 设备消息必须符合 {{site.data.keyword.iot_short_notm}} 消息有效内容需求。

有关更多信息，请参阅[在 Watson IoT Platform 上开发设备](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html)。

完成以下步骤以将您的设备连接到 {{site.data.keyword.iot_short_notm}}。

## 步骤 1：向 {{site.data.keyword.iot_short_notm}} 注册您的设备  
{: #iotplatform_subtask1}

注册设备涉及将设备分类为某种设备类型、为设备指定名称以及提供设备信息。然后，提供连接令牌，或接受 {{site.data.keyword.iot_short_notm}} 生成的令牌。

可以从 {{site.data.keyword.iot_short_notm}} 仪表板一次添加一个设备，也可使用 [{{site.data.keyword.iot_short_notm}} API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration){: new_window} 一次添加一个或多个设备。

要从 {{site.data.keyword.iot_short_notm}} 仪表板添加设备，请执行以下操作：

1. 单击 {{site.data.keyword.Bluemix}} 仪表板中的 {{site.data.keyword.iot_short_notm}} 服务磁贴。

2. 在服务页面上，单击**启动**以开始管理 {{site.data.keyword.iot_short_notm}} 组织。

  此时，{{site.data.keyword.iot_short_notm}} Web 控制台将在新浏览器选项卡中打开，URL 如下：

 ```
 https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview
 ```

    其中，*org_id* 是 [{{site.data.keyword.iot_short_notm}} 组织](iotplatform_overview.html#organizations){: new_window}的标识。

3. 在“概述”仪表板中，从菜单窗格选择**设备**，然后单击**添加设备**。
5. 为要添加的设备选择或创建设备类型。
  
连接到 {{site.data.keyword.iot_short_notm}} 的每个设备都必须与一种设备类型相关联。设备类型是共享公共特征的设备组。  
向 {{site.data.keyword.iot_short_notm}} 组织添加第一个设备时，**设备类型**菜单中没有任何设备类型。必须先创建一种设备类型：
 1. 单击**创建设备类型**。
 2. 输入设备类型名称（如 `my_device_type`）以及设备类型描述。   
 **重要信息**：设备类型名称不得超过 36 个字符，仅可包含以下字符：
 <ul>
  <li>字母数字字符（a-z、A-Z 和 0-9）</li>
  <li>连字符（-）</li>
  <li>下划线 (&lowbar;)</li>
  <li>句点 (.)</li>
  </ul>
 3. 可选：输入设备类型属性和元数据。
     
 **提示：**您可以稍后添加和编辑属性及元数据。
 4. 单击**创建**以添加新设备类型。
10. 单击**下一步**以开始添加具有所选设备类型的设备的过程。
11. 输入设备标识（如 `my_first_device`）。
  
设备标识用于在 {{site.data.keyword.iot_short_notm}} 仪表板中标识设备，还是用于将设备连接到 {{site.data.keyword.iot_short_notm}} 的必需参数。  
**重要信息**：设备标识不得超过 36 个字符，仅可包含以下字符：
 <ul>
 <li>字母数字字符（a-z、A-Z 和 0-9）</li>
 <li>连字符 (-)</li>
 <li>下划线 (&lowbar;)</li>
 <li>句点 (.)</li>  
 </ul>
 **提示：**对于连接网络的设备，设备标识可以是（例如）不带任何分隔冒号的设备 MAC 地址。  
12. 可选：单击**其他字段**以添加设备信息（例如，序列号、制造商和模型等）。  
 **提示：**您可以稍后添加和编辑此信息。
12. 可选：输入设备 JSON 元数据。  
 **提示：**您可以稍后添加和编辑设备元数据。
13. 单击**下一步**以完成设备的添加。
14. 验证摘要信息是否正确，然后单击**添加**以添加连接。  
**提示：**您可以选择接受自动生成的认证令牌，或自己提供认证令牌。  
如果选择创建自己的令牌，请确保令牌的长度在 8 到 36 个字符之间，并且仅包含字母数字字符和以下特殊字符：
 - 连字符 (-)
 - 下划线 (&lowbar;)
 - 惊叹号 (!)
 - 与号 (&)
 - 电子邮件符号 (@)
 - 问号 (?)
 - 星号 (\*)
 - 加号 (+)
 - 句点 (.)
 - 左右括号  

 **重要信息：**此令牌不能包含重复的字符序列、字典单词、用户名或其他预定义序列。
15. 在设备信息页面中，复制并保存以下设备信息：  
 - 组织标识，例如 `tubo8x`
 - 设备类型，例如 `my_device_type`
 - 设备标识，例如 `my_first_device`
 - 认证方法，例如 `token`
 - 认证令牌，例如 `PtBVriRqIg4uh)_-Kl`  
  **提示：**您将需要“组织标识”、“认证令牌”、“设备类型”和“设备标识”来配置设备以连接到 {{site.data.keyword.iot_short_notm}}。  

恭喜，您已注册设备。现在可配置您的设备以连接到 {{site.data.keyword.iot_short_notm}}

## 步骤 2：将您的设备连接到 {{site.data.keyword.iot_short_notm}}
{: #iotplatform_subtask2}

向 {{site.data.keyword.iot_short_notm}} 注册设备后，可使用注册信息来连接该设备并开始接收设备数据。

{{site.data.keyword.iot_short_notm}} 支持很多设备类型。用于连接设备的基本过程通常包括以下步骤：
- 设置您的设备以实现 MQTT 消息传递并使用“组织标识”、“认证令牌”、“设备类型”和“设备标识”以进行认证。  
- 通过使用 MQTT 协议将设备消息发送到 {{site.data.keyword.iot_short_notm}} 组织。

**提示：**很多连接诀窍适用于常用设备。有关诀窍的列表，请参阅 IBM.com 上提供的[设备连接诀窍 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){: new_window}。

连接设备时需要以下信息：
- URL：*org_id*.messaging.internetofthings.ibmcloud.com  
其中，*org_id* 是 {{site.data.keyword.iot_short_notm}} 组织的标识。
- 端口：
 - 1883
 - 8883（已加密）
 - 443 (websocket)
- 设备标识：d:*org_id*:*device_type*:*device_id*  
此参数组合可唯一标识您的设备。
- 用户名：use-token-auth  
此值指示您正在使用令牌授权。
- 密码：*认证令牌*  
此值是注册设备时所定义的或为设备分配的唯一令牌。
- 事件主题格式：iot-2/evt/*event_id*/fmt/*format_string*  
 其中，*event_id* 指定 {{site.data.keyword.iot_short_notm}} 中显示的事件名称，*format_string* 是事件的格式（例如，JSON）。
- 消息格式：JSON
   
 {{site.data.keyword.iot_short_notm}} 支持多种格式（例如，JSON 和文本）。

有关连接您的设备的更多信息，请参阅技术文档中的[设备的 MQTT 连接](devices/mqtt.html)。


[组织管理 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} API 文档还包含所需信息。

## 关于连接设备的诀窍

以下诀窍描述了用于向 Watson IoT Platform 注册并连接设备的完整流程。

- [How to Register Devices in IBM Watson IoT Platform ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/){: new_window}

- [Connecting Raspberry Pi as a Device to Watson IoT using Node-RED ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

- [Connect an Arduino Uno device to the IBM Watson IoT Platform ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/){: new_window}

- [Connectinga Sense HAT to Watson IoT using Node-RED ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/){: new_window}

- [Connecting Raspberry Pi with Windows IoT Core as a Device to Watson IoT Platform ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/){: new_window}
