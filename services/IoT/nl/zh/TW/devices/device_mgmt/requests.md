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


# 裝置管理要求
{: #requests}


{{site.data.keyword.iot_full}} 提供可針對一個以上的裝置而起始的動作。使用儀表板或 REST API，即可起始這些動作。可用動作的類型為**裝置動作**及**韌體動作**。

## 使用儀表板起始裝置管理要求
{: #initiating-dm-dashboard}

使用「裝置」頁面的**動作**標籤，即可透過儀表板來起始要求。按一下**起始動作**來選取動作、選取裝置，然後指定所選動作可支援的任何其他參數。

## 使用 REST API 起始裝置管理要求
{: #initiating-dm-api}

使用下列 REST API 範例，即可起始要求：  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

如需裝置管理要求內文的相關資訊，請參閱 [API 文件 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}。

## 裝置動作
{: #device-actions}

裝置可以指定其在發佈管理要求時支援裝置動作。裝置動作要求會向 {{site.data.keyword.iot_short_notm}} 指出裝置可以回應裝置重新開機及裝置重設動作。


## 裝置動作 - 重新開機
{: #device-actions-reboot}

使用 {{site.data.keyword.iot_short_notm}} 儀表板，或使用 REST API，即可起始重新開機裝置動作。

若要使用 REST API 起始裝置重新開機，請將 POST 要求發出至：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供下列資訊：

- 動作 `device/reboot`
- 要重新開機的裝置清單，上限為 5000 個裝置

裝置重新開機要求範例：

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

起始要求之後，會將 MQTT 訊息發佈至重新開機要求內文中指定的所有裝置。必須針對每一個裝置送回回應，以指出是否可以起始重新開機動作。如果可以立即起始此作業，請將 `rc` 參數設為 `202`。如果重新開機嘗試失敗，請將 `rc` 參數設為 `500`，並據以設定 `message` 參數。如果不支援重新開機，請將 `rc` 參數設為 `501`，並選擇性地據以設定 `message` 參數。

裝置在重新開機之後傳送「管理裝置」要求時，重新開機動作即完成。

### 裝置重新開機要求的主題

伺服器會將重新開機要求發佈至下列主題上的裝置：

```
iotdm-1/mgmt/initiate/device/reboot
```

### 裝置重新開機要求的訊息格式


要求格式：

```
Incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

回應格式：

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## 裝置動作 - 重設為原廠設定
{: #device-actions-factory-reset}

使用 {{site.data.keyword.iot_short_notm}} 儀表板，或使用 REST API，即可起始重設為原廠設定動作。

若要使用 REST API 起始裝置重設為原廠設定，請將 POST 要求發出至：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供下列資訊：

- 動作 `device/factoryReset`
- 要重設的裝置清單，最多 5000 個裝置

下列範例提供範例裝置重設要求：

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

起始裝置重設要求時，會將 MQTT 訊息發佈至要求內文中指定的所有裝置。必須針對每一個裝置傳回回應，以指出是否可以起始重設為原廠設定動作。如果可以立即起始此動作，則回應碼設為 `202`。如果重設為原廠設定嘗試失敗，請將 `rc` 參數設為 `500`，並據以設定 `message` 參數。如果不支援重設為原廠設定動作，請將 `rc` 參數設為 `501`，並選擇性地據以設定 `message` 參數。

裝置在重設為原廠設定之後傳送「管理裝置」要求時，重設為原廠設定動作即完成。

### 重設為原廠設定要求的主題

伺服器會將下列要求發佈至裝置：

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### 重設為原廠設定要求的訊息格式


要求格式：

```
The following topic shows the incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

回應格式：

```
The following topic shows an outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## 韌體動作
{: #firmware-actions}

已知位於裝置上的韌體層次會儲存在 `deviceInfo.fwVersion` 屬性中。`mgmt.firmware` 屬性是用來執行韌體更新以及觀察其狀態。

**重要事項：**受管理裝置必須支援 `mgmt.firmware` 屬性的觀察，才能支援韌體動作。

韌體更新處理程序分成不同的動作：
- 下載韌體
- 更新韌體

每一個韌體動作的狀態都會儲存在裝置的不同屬性中。`mgmt.firmware.state` 屬性說明韌體下載的狀態。下表說明可針對 `mgmt.firmware.state` 屬性設定的可能值：

 |值 |狀態  | 意義 |
 |:---|:---|:---|
 |0  | 閒置        | 裝置未下載韌體。 |  
 |1  | 下載中 | 裝置正在下載韌體。 |
 |2  | 已下載  | 裝置已順利下載韌體更新，並且準備好進行安裝。 |


`mgmt.firmware.updateStatus` 屬性說明韌體更新的狀態。`mgmt.firmware.updateStatus` 屬性的可能值如下：

|值 |狀態 | 意義 |  
|:---|:---|:---|
|0 | 成功 | 韌體已順利更新。 |
|1 | 進行中 | 韌體更新已起始，但尚未完成。|
|2 | 記憶體不足 | 在作業期間偵測到記憶體不足狀況。|
|3 | 連線中斷     | 在韌體下載期間連線已中斷。 |
|4 | 驗證失敗 | 韌體未通過驗證。 |
|5 | 映像檔不受支援   | 裝置不支援已下載的韌體映像檔。 |
|6 | URI 無效         | 裝置無法從提供的 URI 下載韌體。 |

## 韌體動作 - 下載
{: #firmware-actions-download}

使用 {{site.data.keyword.iot_short_notm}} 儀表板，或使用 REST API，即可起始下載韌體動作。

若要使用 REST API 起始韌體下載，請將 POST 要求發出至：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供下列資訊：

- 動作 `firmware/download`
- 接收映像檔的裝置清單，最多 5000 個裝置
- 韌體映像檔的 URI（選用）
- 要驗證映像檔的驗證字串（選用）
- 韌體名稱（選用）
- 韌體版本（選用）

下列範例顯示下列所有範例訊息所根據的韌體下載要求：

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

如果未指定任何選用性參數，則會略過下列處理程序中的第一個步驟。

{{site.data.keyword.iot_short_notm}} 中的裝置管理伺服器使用「裝置管理通訊協定」將要求傳送至裝置，如此便會起始韌體下載。下載處理程序包含下列步驟：

1. 在主題 `iotdm-1/device/update` 上傳送韌體詳細資料更新要求。
更新要求可讓裝置驗證所要求的韌體是否與目前安裝的韌體不同。如果不同，請將 `rc` 參數設為 `204`，即轉換為狀態 `Changed`。
  
下列範例顯示針對先前傳送的韌體下載要求範例預期為哪一則訊息，而在偵測到差異時會傳送哪一個回應：
```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

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

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   此回應會觸發下一個要求。
2. 傳送韌體下載狀態 `iotdm-1/observe` 的觀察要求。
觀察要求會驗證裝置是否準備好啟動韌體下載。可以立即開始下載時，請將 `rc` 參數設為 `200`（正常）、將 `mgmt.firmware.state` 屬性設為 `0`（閒置），並將 `mgmt.firmware.updateStatus` 屬性設為 `0`（閒置）。下列程式碼是 {{site.data.keyword.iot_short_notm}} 與裝置之間的範例交換：
   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

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

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
這項交換會觸發最後一個步驟。  

3. 在主題 `iotdm-1/mgmt/initiate/firmware/download` 上傳送下載要求：

   下載要求會告知裝置以啟動韌體下載。如果可以立即起始動作，請將 `rc` 參數設為 `202`。下列程式碼提供起始下載要求的範例：

   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

使用此方式起始韌體下載之後，裝置需要向 {{site.data.keyword.iot_short_notm}} 報告下載狀態。裝置會透過將訊息發佈至 `iotdevice-1/notify` 主題來報告狀態，其中 `mgmt.firmware.state` 屬性設為 `1`（`下載中`）或 `2`（`已下載`）。
下列範例顯示如何起始韌體下載的範例：

```
Outgoing message from device:

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


Wait some time...


Outgoing message from device:

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



在 `mgmt.firmware.state` 屬性設為 `2` 的情況下發佈通知之後，會在 `iotdm-1/cancel` 主題上觸發要求。此要求會取消觀察 `mgmt.firmware` 屬性。
傳送 `rc` 參數設為 `200` 的回應之後，韌體下載即完成。下列程式碼提供範例：

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

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


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

下列資訊適用於錯誤處理：

- 如果 `mgmt.firmware.state` 屬性不是 `0`（閒置），請傳送包含回應碼 `400` 及選用性訊息文字的錯誤。
- 如果 `mgmt.firmware.uri` 屬性未設定或不是有效的 URI，請將 `rc` 參數設為 `400`。
- 如果韌體下載嘗試失敗，請將 `rc` 參數設為 `500`，並選擇性地據以設定 `message` 參數。
- 如果不支援韌體下載，請將 `rc` 參數設為 `500`，並選擇性地據以設定 `message` 參數。
- 裝置收到執行要求時，請將 `mgmt.firmware.state` 屬性從 `0`（閒置）變更為 `1`（下載中）。
- 下載順利完成時，請將 `mgmt.firmware.state` 屬性設為 `2`（已下載）。
- 如果下載期間發生錯誤，請將 `mgmt.firmware.state` 屬性設為 `0`（閒置），並將 `mgmt.firmware.updateStatus` 屬性設為下列其中一個錯誤狀態值：
  - 2（記憶體不足）
  - 3（連線中斷）
  - 6（URI 無效）
- 如果已設定韌體驗證器，裝置會嘗試驗證韌體映像檔。如果映像檔驗證失敗，請將 `mgmt.firmware.state` 屬性設為 `0`（閒置），並將 `mgmt.firmware.updateStatus` 屬性設為錯誤狀態值 `4`（驗證失敗）。

## 韌體動作 - 更新
{: #firmware-actions-update}

使用 REST API 起始所下載韌體的安裝，方法是將 POST 要求發出至：

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

提供下列資訊：

- 動作 `firmware/update`
- 接收映像檔的裝置清單，裝置類型全部相同。
- 韌體映像檔的 URI（選用）
- 要驗證映像檔的驗證字串（選用）
- 韌體名稱（選用）
- 韌體版本（選用）

下列程式碼是範例要求：

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

如果指定任何選用性參數，則裝置收到的第一則訊息為裝置更新要求。此裝置更新要求與韌體下載要求的第一則訊息類似。

若要監視韌體更新的狀態，{{site.data.keyword.iot_short_notm}} 會先在主題 `iotdm-1/observe` 上觸發觀察程式要求。裝置準備好啟動更新處理程序時，會傳送 `rc` 參數設為 `200`、`mgmt.firmware.state` 屬性設為 `0` 且 `mgmt.firmware.updateStatus` 屬性設為 `0` 的回應。

下列程式碼提供範例：

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

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

Outgoing response from device:

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



順利下載韌體更新之後，{{site.data.keyword.iot_short_notm}} 中的裝置管理伺服器會使用「裝置管理通訊協定」，要求所指定的裝置使用主題 `iotdm-1/mgmt/initiate/firmware/update` 來起始韌體安裝。
如果可以立即起始此作業，請將 `rc` 參數設為 `202`。如果之前未順利下載韌體，請將 `rc` 參數設為 `400`。

下列程式碼顯示範例：

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

若要完成韌體更新要求，裝置會使用針對其 `iotdevice-1/notify` 主題發佈的狀態訊息，向 {{site.data.keyword.iot_short_notm}} 報告其更新狀態。
完成韌體更新時，會將 `mgmt.firmware.updateStatus` 屬性設為 `0`（成功），並將 `mgmt.firmware.state` 屬性設為 `0`（閒置）。然後，即可將所下載的韌體映像檔從裝置中刪除，並將 `deviceInfo.fwVersion` 屬性設為 `mgmt.firmware.version` 屬性的值。

下列程式碼提供通知訊息的範例：

```
Outgoing message from device:

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

{{site.data.keyword.iot_short_notm}} 收到已完成韌體更新的通知時，會在 `iotdm-1/cancel` 主題上觸發最後一個要求，以取消 `mgmt.firmware` 屬性的觀察。


傳送 `rc` 參數設為 `200` 的回應時，韌體更新要求即完成，如下列範例所示：

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

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


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

下列清單提供一些有用資訊來進行錯誤及處理程序處理：

- 如果韌體更新嘗試失敗，請將 `rc` 參數設為 `500`，並選擇性地將 `message` 參數設為包含相關資訊。
- 如果不支援韌體更新，請將 `rc` 參數設為 `501`，並選擇性地將 `message` 參數設為包含相關資訊。
- 如果 `mgmt.firmware.state` 屬性不是 `2`（已下載），請傳送 `rc` 參數設為 `400` 及選用性訊息文字的錯誤。
- 否則，請將 `mgmt.firmware.updateStatus` 屬性設為 `1`（進行中），而且一般會啟動韌體安裝。
- 如果韌體安裝失敗，請將 `mgmt.firmware.updateStatus` 屬性設為下列其中一個值：
  - `2`（記憶體不足）
  - `5`（映像檔不受支援）


**重要事項：**必須同時設定列為 `mgmt.firmware` 屬性一部分的所有參數，以便在有 `mgmt.firmware` 的目前觀察時，只傳送單一通知訊息。

## 裝置動作及韌體動作的秘訣

下列秘訣示範執行裝置及韌體動作所需的完整流程。

- [WIoT Platform 中的裝置管理 - 回復及重設為原廠設定 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [裝置起始的韌體更新 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [平台起始的韌體更新 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [使用背景執行的平台起始的韌體更新 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [韌體回復及重設為原廠設定 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
