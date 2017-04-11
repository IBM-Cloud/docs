---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}  
{:codeblock: .codeblock}
{:pre: .pre}


# 设备管理请求
{: #requests}


{{site.data.keyword.iot_full}} 提供了可以对一个或多个设备启动的操作。这些操作可以使用仪表板或 REST API 来启动。可用操作的类型为**设备操作**和**固件操作**。

## 使用仪表板发起设备管理请求
{: #initiating-dm-dashboard}

请求可以通过使用仪表板中“设备”页面的**操作**选项卡来启动。单击**启动操作**可以选择操作、选择设备，以及指定所选操作支持的其他任何参数。

## 使用 REST API 发起设备管理请求
{: #initiating-dm-api}

请求可以使用以下 REST API 样本来发起：  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

有关设备管理请求的主体的更多信息，请参阅 [ API 文档 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}。

## 设备操作
{: #device-actions}

设备可以在发布管理请求时，指定其支持的设备操作。设备操作请求向 {{site.data.keyword.iot_short_notm}} 指示，设备能够响应设备重新引导和设备重置操作。


## 设备操作 - 重新引导
{: #device-actions-reboot}

可以使用 {{site.data.keyword.iot_short_notm}} 仪表板或 REST API 来启动重新引导设备操作。

要使用 REST API 启动设备重新引导操作，请将 POST 请求发出到：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供以下信息：

- 操作 `device/reboot`
- 要重新引导的设备列表，最多包含 5000 台设备

示例设备重新引导请求：

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

发起请求后，会向重新引导请求主体中指定的所有设备发布一条 MQTT 消息。对于每个设备，都必须发回一个响应，以指示是否可以启动重新引导操作。如果此操作可以立即启动，那么将 `rc` 参数设置为 `202`。如果重新引导尝试失败，那么将 `rc` 参数设置为 `500`，并相应地设置 `message` 参数。如果不支持重新引导，那么将 `rc` 参数设置为 `501`，并可选择相应地设置 `message` 参数。

设备在重新引导后发送“管理设备”请求时，重新引导操作即完成。

### 设备重新引导请求的主题

服务器会将重新引导请求发送到以下主题上的设备：

```
iotdm-1/mgmt/initiate/device/reboot
```

### 设备重新引导请求的消息格式


请求格式：

```
来自服务器的入局消息：

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

响应格式：

```
来自设备的出局消息：

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## 设备操作 - 恢复出厂设置
{: #device-actions-factory-reset}

可以使用 {{site.data.keyword.iot_short_notm}} 仪表板或 REST API 来启动恢复出厂设置操作。

要使用 REST API 启动设备恢复出厂设置操作，请将 POST 请求发出到：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供了以下信息：

- 操作 `device/factoryReset`
- 要恢复出厂设置的设备的列表，最多 5000 台设备

以下样本提供了设备恢复出厂设置请求示例：

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

发起设备恢复出厂设置请求后，会向请求主体中指定的所有设备发布一条 MQTT 消息。对于每个设备，都必须返回一个响应，以指示是否可以启动恢复出厂设置操作。如果此操作可以立即启动，那么响应代码会设置为 `202`。如果恢复出厂设置尝试失败，那么将 `rc` 参数设置为 `500`，并相应地设置 `message` 参数。如果不支持恢复出厂设置操作，那么将 `rc` 参数设置为 `501`，并可选择相应地设置 `message` 参数。

设备在恢复出厂设置后发送“管理设备”请求时，恢复出厂设置操作即完成。

### 恢复出厂设置请求的主题

服务器将向设备发布以下请求：

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### 恢复出厂设置请求的消息格式


请求格式：

```
以下主题显示来自服务器的入局消息：

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

响应格式：

```
以下主题显示来自设备的出局消息：

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## 固件操作
{: #firmware-actions}

设备上已知的固件级别存储在 `deviceInfo.fwVersion` 属性中。`mgmt.firmware` 属性用于执行固件更新并观察其状态。

**重要信息：**受管设备必须支持观察 `mgmt.firmware` 属性，才能支持固件操作。

固件更新过程分为不同的操作：
- 下载固件
- 更新固件

每个固件操作的状态都会存储在设备上的单独属性中。`mgmt.firmware.state` 属性描述了固件下载的状态。下表描述了可以为 `mgmt.firmware.state` 属性设置的可能的值：

 |值 |状态  | 含义 |
 |:---|:---|:---|
 |0  | 空闲        | 设备未在下载固件。 |  
 |1  | 正在下载 | 设备正在下载固件。 |
 |2  | 已下载  | 设备已成功下载固件更新，随时可进行安装。 |


`mgmt.firmware.updateStatus` 属性描述了固件更新的状态。`mgmt.firmware.updateStatus` 属性可能的值为：

|值 |状态 | 含义 |  
|:---|:---|:---|
|0 | 成功 | 固件已成功更新。 |
|1 | 正在进行 | 固件更新已启动，但尚未完成。|
|2 | 内存耗尽 | 操作期间检测到内存耗尽情况。|
|3 | 连接断开     | 固件下载期间连接断开。 |
|4 | 验证失败 | 固件未通过验证。 |
|5 | 不受支持的映像   | 设备不支持所下载的固件映像。 |
|6 | URI 无效         | 设备无法从提供的 URI 下载固件。 |

## 固件操作 - 下载
{: #firmware-actions-download}

可以使用 {{site.data.keyword.iot_short_notm}} 仪表板或 REST API 来启动下载固件操作。

要使用 REST API 启动固件下载操作，请将 POST 请求发出到：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供了以下信息：

- 操作 `firmware/download`
- 用于接收映像的设备列表（最多包含 5000 台设备）
- 固件映像的 URI（可选）
- 用于验证映像的验证字符串（可选）
- 固件名称（可选）
- 固件版本（可选）

以下样本显示了以下所有示例消息所基于的固件下载请求：

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

如果未指定任何可选参数，那么会跳过以下流程中的第一步。

{{site.data.keyword.iot_short_notm}} 中的设备管理服务器使用设备管理协议向设备发送请求，以启动固件下载操作。下载过程由以下步骤组成：

1. 在 `iotdm-1/device/update` 主题上发送固件详细信息更新请求。
更新请求让设备验证请求的固件是否不同于当前安装的固件。如果有差异，那么将 `rc` 参数设置为 `204`，这会转换为状态“`已更改`”。
  
以下示例显示了对于先前发送的示例固件下载请求应该会收到的消息，以及检测到差异时发送的响应：
```
   来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   来自设备的出局响应：

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   此响应将触发下一个请求。
2. 发送对固件下载状态的观察请求 `iotdm-1/observe`。
观察请求验证设备是否已准备好启动固件下载。下载可以立即启动时，将 `rc` 参数设置为 `200`（`正常`），将 `mgmt.firmware.state` 属性设置为 `0`（`空闲`），并将 `mgmt.firmware.updateStatus` 属性设置为 `0`（`空闲`）。以下代码是 {{site.data.keyword.iot_short_notm}} 与设备之间的示例交换：
   ```
   来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   来自设备的出局响应：

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
此交换会触发最后一个步骤。  

3. 在 `iotdm-1/mgmt/initiate/firmware/download` 主题上发送下载请求：

   下载请求通知设备启动固件下载。如果此操作可以立即启动，那么将 `rc` 参数设置为 `202`。以下代码提供了发起下载请求的示例：

   ```
   来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   来自设备的出局响应：

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

固件下载操作以这种方式启动后，设备需要向 {{site.data.keyword.iot_short_notm}} 报告下载状态。设备通过将消息发布到 `iotdevice-1/notify`-topic 来报告状态，其中 `mgmt.firmware.state` 属性设置为 `1`（`正在下载`）或 `2`（`已下载`）。
以下样本显示了启动固件下载操作的示例：

```
来自设备的出局消息：

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


请稍候...


来自设备的出局消息：

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



在发布了通知，并且 `mgmt.firmware.state` 属性设置为 `2` 后，将在 `iotdm-1/cancel`-topic 上触发请求。此请求会取消观察 `mgmt.firmware` 属性。
发送了将 `rc` 参数设置为 `200` 的响应后，固件下载即完成。以下代码提供了示例：

```
来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


来自设备的出局消息：

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

以下信息对于错误处理非常有用：

- 如果 `mgmt.firmware.state` 属性不为 `0`（“空闲”），那么发送具有响应代码 `400` 和可选的消息文本的错误。
- 如果 `mgmt.firmware.uri` 属性未设置或不是有效的 URI，那么将 `rc` 参数设置为 `400`。
- 如果固件下载尝试失败，那么将 `rc` 参数设置为 `500`，并可选择相应地设置 `message` 参数。
- 如果不支持固件下载，那么将 `rc` 参数设置为 `500`，并可选择相应地设置 `message` 参数。
- 设备收到执行请求后，将 `mgmt.firmware.state` 属性从 `0`（空闲）更改为 `1`（正在下载）。
- 下载成功完成时，将 `mgmt.firmware.state` 属性设置为 `2`（已下载）。
- 如果下载期间发生错误，那么将 `mgmt.firmware.state` 属性设置为 `0`（空闲），并将 `mgmt.firmware.updateStatus` 属性设置为以下某个错误状态值：
  - 2（内存耗尽）
  - 3（连接断开）
  - 6（URI 无效）
- 如果设置了固件验证器，设备将尝试验证固件映像。如果映像验证失败，那么将 `mgmt.firmware.state` 属性设置为 `0`（空闲），并将 `mgmt.firmware.updateStatus` 属性设置为错误状态值 `4`（验证失败）。

## 固件操作 - 更新
{: #firmware-actions-update}

所下载固件的安装是使用 REST API 通过向以下地址发送 POST 请求来启动的：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供了以下信息：

- 操作 `firmware/update`
- 用于接收映像的设备列表（所有设备都属于同一设备类型）。
- 固件映像的 URI（可选）
- 用于验证映像的验证字符串（可选）
- 固件名称（可选）
- 固件版本（可选）

以下代码是示例请求：

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

如果指定了任何可选参数，那么设备接收的第一条消息是设备更新请求。此设备更新请求与固件下载请求的第一条消息类似。

要监视固件更新的状态，{{site.data.keyword.iot_short_notm}} 会首先在 `iotdm-1/observe` 主题上触发观察器请求。设备准备好启动更新过程时，会发送一个响应，其中 `rc` 参数设置为 `200`，`mgmt.firmware.state` 属性设置为 `0`，并且 `mgmt.firmware.updateStatus` 属性设置为 `0`。

以下代码提供了示例：

```
来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

来自设备的出局响应：

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



固件更新成功下载后，{{site.data.keyword.iot_short_notm}} 中的设备管理服务器会使用设备管理协议来请求指定的设备通过 `iotdm-1/mgmt/initiate/firmware/update` 主题启动固件安装。
如果此操作可以立即启动，那么将 `rc` 参数设置为 `202`。如果固件先前未成功下载，那么将 `rc` 参数设置为 `400`。

以下代码显示了示例：

```
来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

来自设备的出局响应：

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

为了完成固件更新请求，设备会使用在其 `iotdevice-1/notify`-topic 上发布的状态消息，向 {{site.data.keyword.iot_short_notm}} 报告更新状态。
固件更新完成后，`mgmt.firmware.updateStatus` 属性会设置为 `0`（成功），并且 `mgmt.firmware.state` 属性会设置为 `0`（空闲）。然后，可以从设备中删除下载的固件映像，并且 `deviceInfo.fwVersion` 属性会设置为 `mgmt.firmware.version` 属性的值。

以下代码提供了通知消息的示例：

```
来自设备的出局消息：

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

{{site.data.keyword.iot_short_notm}} 接收到已完成固件更新的通知时，会在 `iotdm-1/cancel`-topic 上触发最后的请求，以取消观察 `mgmt.firmware` 属性。


发送了将 `rc` 参数设置为 `200` 的响应后，固件更新请求即完成，如以下示例中所示：

```
来自 {{site.data.keyword.iot_short_notm}} 的入局请求：

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


来自设备的出局消息：

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

以下列表提供了错误和过程处理的一些有用信息：

- 如果固件更新尝试失败，那么将 `rc` 参数设置为 `500`，并可选择将 `message` 参数设置为包含相关信息。
- 如果不支持固件更新，那么将 `rc` 参数设置为 `501`，并可选择将 `message` 参数设置为包含相关信息。
- 如果 `mgmt.firmware.state` 属性不为 `2`（已下载），那么发送将 `rc` 参数设置为 `400` 且具有可选的消息文本的错误。
- 否则，将 `mgmt.firmware.updateStatus` 属性设置为 `1`（正在进行），并且通常会启动固件安装。
- 如果固件安装失败，那么将 `mgmt.firmware.updateStatus` 属性设置为以下某个值：
  - `2`（内存耗尽）
  - `5`（不支持的映像）


**重要信息：**作为 `mgmt.firmware` 属性一部分列出的所有参数都必须同时进行设置，这样当存在 `mgmt.firmware` 的当前观察时，只会发送单个通知消息。

## 关于设备操作和固件操作的诀窍

以下诀窍演示了执行设备和固件操作所需的完整流程。

- [DeviceManagement in WIoT Platform – Roll Back & Factory Reset ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [DeviceInitiated Firmware Update ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [PlatformInitiated Firmware Update ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update with Background Execution ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Firmware Roll Back & Factory Reset ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
