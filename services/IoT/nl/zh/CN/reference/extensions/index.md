---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 外部服务集成
{: #ref-index}

通过外部服务集成，可在 {{site.data.keyword.iot_full}} 组织中访问第三方或外部服务中的数据和操作。

## Jasper
{: #jasper}

Jasper 是一款用于 SIM 设备的管理平台。Jasper 集成到 {{site.data.keyword.iot_short_notm}} 仪表板中，从而可通过 {{site.data.keyword.iot_short_notm}} 组织仪表板管理 Jasper 设备。

### Jasper 的受支持操作

我们的平台所提供的内置 Jasper 集成提供了对以下 Jasper 操作的支持：

- 查看总体 Jasper 数据
  - 显示：状态、套餐、本月至今数据使用情况、本月至今 SMS 使用情况、本月至今语音使用情况、超额限制、添加日期和修改日期。
- 更改 SIM 激活状态。
  - 选择：库存、可随时激活、已激活、已取消激活和已废弃。
- 查看 SIM 使用情况
  - 显示：周期开始日期、计费数据和数据总量、计费 SMS 和 SMS 总量、计费语音和语音总量。
  - 可以使用 YYYY-MM-DD 格式设置周期开始日期。
- 将 SMS 发送到 SIM
- 更改套餐

完成以下配置步骤后，可在连接了 Jasper 的设备的设备向下钻取中访问受支持的操作。

### 用于 Jasper 的 REST API
要访问用于 Jasper 的 REST API，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部链接图标](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window} 文档中的“Jasper 扩展”部分。

### Jasper 的配置

要将 Jasper 服务连接到 {{site.data.keyword.iot_short_notm}} 组织，必须首先完成两个配置阶段。首先，必须将 {{site.data.keyword.iot_short_notm}} 连接到 Jasper 服务，然后必须配置 {{site.data.keyword.iot_short_notm}} 设备。


1. 启用 Jasper 扩展。要启用 Jasper 与 {{site.data.keyword.iot_short_notm}} 组织的集成，请完成以下步骤：
  1. 从 {{site.data.keyword.iot_short_notm}} 仪表板选择**扩展**。
  2. 在**扩展**页面上，单击**添加扩展**。
  3. 单击 Jasper 旁的**添加**。
  4. 输入 Jasper 用户名、密码、访问键和域标识。
  5. 单击**完成**。

2. 配置设备
您可以配置同时连接到您的 {{site.data.keyword.iot_short_notm}} 组织和 Jasper 帐户的设备以在 {{site.data.keyword.iot_short_notm}} 仪表板中显示 Jasper 中的数据。  
**重要信息：**在执行“添加设备”过程时，无法应用 Jasper 配置，只有先前连接的设备可使用 Jasper 进行配置。  
要配置连接了 Jasper 的设备，请完成以下步骤：
 1. 在 {{site.data.keyword.iot_short_notm}} 仪表板的“设备”选项卡中，找到要配置的连接了 Jasper 的设备。
 2. 选择此设备以打开*设备向下钻取*视图。
 3. 向下滚动到*扩展配置*。
 4. 通过使用以下 JSON 格式输入扩展配置，然后单击**确认更改**以保存配置。  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

成功配置组织后，会在*设备向下钻取*视图中*扩展配置*部分下显示*扩展*部分。

## AT&T
{: #att}

### AT&T 的受支持操作

AT&T 扩展支持以下 AT&T 操作：

- 查看总体 AT&T 数据
  - 显示：状态、套餐、本月至今数据使用情况、本月至今 SMS 使用情况、本月至今语音使用情况、超额限制、添加日期和修改日期。
- 更改 SIM 激活状态。
  - 选择：库存、可随时激活、已激活、已取消激活和已废弃。
- 查看 SIM 使用情况
  - 显示：周期开始日期、计费数据和数据总量、计费 SMS 和 SMS 总量、计费语音和语音总量。
  - 可以使用 YYYY-MM-DD 格式设置周期开始日期。
- 将 SMS 发送到 SIM
- 更改套餐

### 用于 AT&T 的 REST API
要访问用于 AT&T 的 REST API，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部链接图标](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window} 文档中的“AT&T 扩展”部分。

### AT&T 的配置

要将 {{site.data.keyword.iot_short_notm}} 组织连接到 AT&T，必须完成组织配置和设备配置。

要配置 {{site.data.keyword.iot_short_notm}} 平台，请完成以下步骤。

1. 启用 AT&T 扩展。要启用 AT&T 与 {{site.data.keyword.iot_short_notm}} 组织的集成，请完成以下步骤：
  1. 从 {{site.data.keyword.iot_short_notm}} 仪表板选择**扩展**。
  2. 在**扩展**页面上，单击**添加扩展**。
  3. 单击 AT&T 旁的**添加**。
  4. 输入 AT&T 用户名、密码、访问键和域标识。
  5. 单击**完成**。

要将您的 {{site.data.keyword.iot_short_notm}} 组织与 AT&T 帐户相连接，首先必须完成两个配置阶段。完成组织配置，然后配置设备。


2. 配置设备
您可以配置同时连接到您的 {{site.data.keyword.iot_short_notm}} 组织和 AT&T 帐户的设备以在 {{site.data.keyword.iot_short_notm}} 仪表板中显示 AT&T 中的数据。  
**重要信息：**在执行“添加设备”过程时，无法应用 AT&T 配置，只有先前连接的设备可使用 AT&T 进行配置。  
要配置连接了 AT&T 的设备，请完成以下步骤：
 1. 在 {{site.data.keyword.iot_short_notm}} 仪表板的“设备”选项卡中，找到要配置的连接了 AT&T 的设备。
 2. 选择此设备以打开*设备向下钻取*视图。
 3. 向下滚动到*扩展配置*。
 4. 通过使用以下 JSON 格式输入扩展配置，然后单击**确认更改**以保存配置。  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

成功配置组织后，会在*设备向下钻取*视图中*扩展配置*部分下显示*扩展*部分。

## ARM mbed 连接器
{: #arm}

通过 ARM mbed 连接器，可将 ARM mbed 设备连接到 {{site.data.keyword.iot_short_notm}}。ARM mbed 扩展允许 {{site.data.keyword.iot_short_notm}} 将数据发送到 ARM mbed 门户网站，以及从 ARM mbed 门户网站接收数据。

### 安装配置


1. 启用 ARM mbed 连接器扩展。要启用 ARM mbed 连接器扩展，请完成以下步骤：
  1. 从 {{site.data.keyword.iot_short_notm}} 仪表板，选择**设置**并浏览到**扩展**。
  2. 在**扩展**菜单中，单击**添加扩展**。
  3. 单击 ARM mbed 连接器扩展旁的**添加**。
  4. 输入 ARM mbed 访问键和域标识。可以使用 ARM mbed 门户网站 (https://connector.mbed.com) 来找到这些值。
  5. 通过单击**检查连接**按钮来检查凭证。
  6. 单击**完成**。

### 有效内容格式

来自 ARM mbed 平台的入局消息有两种类型：通知和异步响应。{{site.data.keyword.iot_short_notm}} 可以向已连接到 ARM mbed 平台的设备发送命令。

#### 通知

通知根据设备或传感器数据的更改而生成。{{site.data.keyword.iot_short_notm}} 处理消息后，会按照与直接连接到 {{site.data.keyword.iot_short_notm}} 的设备相同的方式将该消息发送到设备事件主题。对于在连接到 ARM mbed 平台的设备上发起的通知，使用的事件类型为 `notify`。

以下代码样本显示了 ARM mbed 平台 API 发送的通知的有效内容格式：

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### 异步响应

{{site.data.keyword.iot_short_notm}} 向连接到 ARM mbed 平台的设备发送命令时，设备会将确认消息发回 {{site.data.keyword.iot_short_notm}}。此确认消息称为*异步响应*，并使用事件类型 `asyncResponse`。

以下代码样本显示了 ARM mbed 云服务发送的异步响应的有效内容格式：

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### 向 ARM mbed 平台发送命令

{{site.data.keyword.iot_short_notm}} 可以向已连接到 ARM mbed 平台的设备发送命令。向 ARM mbed 平台发送的命令必须使用以下 JSON 格式。

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
所选择的方法是区分大小写的。必须跳过资源路径的第一个“/”。


有效内容应该发布到以下主题：

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

通过 Orange 扩展，可从连接到 {{site.data.keyword.iot_short_notm}} 且安装了 Orange SIM 卡的设备查看 SIM 卡数据。

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Orange 的受支持操作

如果您的设备连接到 {{site.data.keyword.iot_short_notm}} 服务且具有 Orange SIM 卡，那么可使用 Orange 扩展来查看以下 SIM 卡数据：

- SIM 序列号
- 激活状态
- 上次状态更改
- 上次状态刷新
- 位置状态

### 用于 Orange 的 REST API
要访问用于 Orange 的 REST API，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部链接图标](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window} 文档中的“Orange 扩展”部分。

### Orange 的配置

要启用 Orange 扩展，请执行以下操作：

1. 从 {{site.data.keyword.iot_short_notm}} 仪表板选择**扩展**。
2. 在**扩展**页面上，单击**添加扩展**。
3. 单击 Orange 扩展旁的**添加**。
4. 输入 Orange 用户名和密码。
6. 单击**完成**。

启用 Orange 扩展后，必须配置具有 Orange SIM 卡的每个设备以显示 Orange SIM 数据。

1. 在 {{site.data.keyword.iot_short_notm}} 仪表板的“设备”选项卡中，找到要配置的 Orange SIM 设备。
2. 选择此设备并向下滚动到*扩展配置*。
3. 通过使用以下 JSON 格式输入扩展配置，然后单击**确认更改**以保存配置。

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
成功配置组织后，会在*设备向下钻取*视图中*扩展配置*部分下显示*扩展*部分。


## 历史数据存储
{: #historical_data}

通过历史数据存储扩展，可以找到并配置 IoT 数据的兼容消息存储服务，例如 [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) 或 [{{site.data.keyword.messagehub_full}}](../../message_hub.html)。

## 定制设备管理软件包
{: #device_mgmt}

设备管理是 {{site.data.keyword.iot_short_notm}} 的核心功能，但是，也可以对其进行扩展以开发其他功能。定制设备管理软件包必须由有效的 JSON 构成，并至少定义一个定制设备管理操作。

有关定制设备管理功能的更多信息（包括必需 JSON 格式的示例），请参阅[设备管理定制扩展](../../devices/device_mgmt/custom_actions.html){: new_window}。

### 添加定制设备管理软件包

可以使用 {{site.data.keyword.iot_short_notm}} 仪表板或 API 来添加定制设备管理软件包。

要使用 {{site.data.keyword.iot_short_notm}} 仪表板来添加定制设备管理软件包，请执行以下操作：

1. 在 {{site.data.keyword.iot_short_notm}} 仪表板的导航栏中，单击**设置**。
2. 单击**定制设备管理软件包**。
3. 单击**添加软件包**按钮。
4. 选择软件包文件，然后单击**打开**。

要使用 API 来添加定制设备管理软件包，请参阅 [{{site.data.keyword.iot_short_notm}} API 文档 ![外部链接图标](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}。

## 区块链
{: #blockchain}

通过具有 Blockchain 的 {{site.data.keyword.iot_short_notm}}，IoT 设备可为 Blockchain 事务提供数据，这会将数据存储在 Blockchain 的不可变分类帐中，并在智能合同业务规则中使用这些数据。{{site.data.keyword.iot_short_notm}} 将设备数据映射为 Blockchain 的智能合同所需的数据格式，并将其传递到 Blockchain 光纤网以存储在 Blockchain 分类帐中。

### Blockchain 的受支持操作
- 通过设备事件触发智能合同更新。
- 运行智能合同业务逻辑以使用设备事件数据更新分类帐状态。
- 使用监视 UI 来监视 Blockchain、事务和分类帐状态。

### Blockchain 的配置

{{site.data.keyword.iot_short_notm}} Blockchain 集成是一款服务产品，缺省情况下在 {{site.data.keyword.iot_short_notm}} 中未激活。要在您的组织中激活此功能，请完成以下步骤：
 1. 从 {{site.data.keyword.iot_short_notm}} 仪表板选择**扩展**。
 2. 在**扩展**页面上，单击**添加扩展**。
 3. 单击“区块链”扩展旁的**添加**。
 4. 在“区块链”磁贴中，单击**设置**。
 3. 在**激活区块链**部分中，单击**了解更多**链接以转至 [IoT Blockchain 服务产品页面 ![外部链接图标](../../../../icons/launch-glyph.svg)](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}。
 4. 单击**开始使用区块链项目**以填充并提交*探索 IoT 和区块链的潜力*表单。  
 5. 请求得到批准后，IBM 将联系您来为您的组织启用区块链集成。
 6. 通过执行 [{{site.data.keyword.iot_short_notm}} 区块链集成](../../bl_blockchain_integration.html)中的步骤，返回到组织的 {{site.data.keyword.iot_short_notm}} 仪表板以完成此设置。



## The Weather Company
{: #weathercompany}

The Weather Company 扩展将天气数据与现有 {{site.data.keyword.iot_short_notm}} 设备相组合。如果使用 API 发起了更新位置请求，或者设备已使用设备管理消息设置其位置，那么来自 The Weather Company 的天气数据会显示在设备详细信息视图中。

**注：**只有受管设备可以设置其自己的位置。所有非受管设备必须使用 API 手动设置其位置。有关设置设备位置的更多信息，请参阅[更新位置请求](../../devices/device_mgmt/index.html#update-location)。

### 用于 The Weather Company 的 REST API 
要访问用于 The Weather Company 的 REST API，请参阅
[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部链接图标](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} 文档中“设备位置天气”部分。

### 天气数据

要查看针对设备位置检索到的天气数据，请在**设备**窗格中找到相应设备，并单击该设备。在详细设备视图中，向下滚动到**扩展**部分。列出了以下天气数据：

- 当前天气。
- 当前温度。
- 预测的最高和最低温度。
- 相对湿度。
- 气压。
- 能见度。
- 风速。
- 风向。
- 纬度。
- 经度。

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
