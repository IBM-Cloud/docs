---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# 启用 SMS 和语音消息传递
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} 支持与 Twilio 集成，以启用 SMS 和语音消息传递。Twilio 是第三方应用程序，可安装在 {{site.data.keyword.Bluemix_notm}} 仪表板中。
{: shortdesc}

## 先决条件
要启用语音消息传递，您必须具有授权的 Twilio 帐户和 Twilio 呼叫方电话号码。如果使用 Twilio 免费帐户，您还必须授权一个电话号码来接收呼叫或消息。有关更多信息，请参阅 [Twilio 文档 ![外部链接图标](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}。

## 创建和配置 Twilio 实例
1. 在安装了 {{site.data.keyword.iotinsurance_short}} 的相同 {{site.data.keyword.Bluemix_notm}} 组织和空间中创建 Twilio 实例。
    1. 登录到 [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net)。
    2. 选择**目录**选项卡。
    3. 找到服务目录的“移动”部分，然后单击 **Twilio**。

    **提示：**单击[此处 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window} 可直接转至 Twilio 页面。
{: tip}

    4. 在 Twilio 页面上，提供凭证并绑定应用程序，如下所示：

      1. 输入 `Twilio-00` 作为服务名称。**重要信息：**您必须使用 `Twilio-00` 才能成功连接到 {{site.data.keyword.iotinsurance_short}}。

      2. 输入 Twilio 凭证。

      3. 在**连接到**菜单中，选择 iot4i-action-engine 应用程序以将 Twilio 实例绑定到 {{site.data.keyword.iotinsurance_short}}。

      4. 单击**创建**。  

    Twilio 应用程序将安装到您的环境中。系统将显示一条消息，提示您重新编译打包或重新启动 iot4i-action-engine 应用程序以启用绑定。您可以现在重新启动，也可以等到在下一步中添加新环境变量后再重新启动。

2. 为 iot4i-action-egine 组件创建名为 TWILIO_FROM_NUMBER 的环境变量。
    1. 在 Bluemix 仪表板中，打开 iot4i-action-engine 应用程序。
    2. 选择**运行时**，然后单击**环境变量**。
    3. 在**用户定义**部分中，单击**添加**。
    4. 在“名称”列中，输入 `TWILIO_FROM_NUMBER`，然后在“值”列中，输入支持 Twilio 语音和 SMS 的号码。
    5. 单击**保存**。

3. 通过单击“路径”按钮旁的“重新启动”图标，重新启动 Iot4i-action-engine 应用程序。

## 将 SMS 和语音操作添加到保障中

要将 SMS 和语音功能添加到保障中，必须将以下操作添加到保障定义中：
  - `send-sms`
  - `phone-call`

有关包含操作列表的保障示例，请参阅[创建样本保障示例 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}。在该示例中，SMS 和语音操作可添加到包含 `email` 和 `pushios` 操作的操作列表中。

有关创建保障的更多信息，请参阅[使用保障工具箱](iotinsurance_shield_toolkit.html)。
