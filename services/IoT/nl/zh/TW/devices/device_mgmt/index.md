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


# 裝置管理通訊協定
{: #index}

## 簡介
{: #introduction}

{{site.data.keyword.iot_full}} 可辨識兩種類別的裝置：**受管理裝置**及**未受管理裝置**。

**受管理裝置**定義為包含裝置管理代理程式的裝置。裝置管理代理程式是一套邏輯，可讓裝置使用「裝置管理通訊協定」來與 {{site.data.keyword.iot_short_notm}} Device Management 服務互動。受管理裝置可以執行裝置管理作業，包括位置更新、韌體下載與更新、重新開機及重設為原廠設定。

「裝置管理通訊協定」定義一組支援的作業。裝置管理代理程式可支援一部分作業，但必須支援**管理**及**取消管理**作業。支援韌體動作作業的裝置也必須支援觀察。

「裝置管理通訊協定」是以 MQTT 傳訊通訊協定為建置基礎。如需「裝置管理通訊協定」如何與 MQTT 互動的相關資訊，請參閱[裝置的 MQTT 連線功能](../mqtt.html)。


### 裝置管理生命週期

1. 使用儀表板或 REST API，以在 {{site.data.keyword.iot_short_notm}} 中建立裝置及其關聯的裝置類型。
2. 裝置連接至 {{site.data.keyword.iot_short_notm}}，並使用**受管理裝置**作業而變成受管理裝置。
3. 您可以使用裝置作業來檢視及操作裝置的 meta 資料。「裝置機型」文件中概述這些作業（例如，韌體更新及裝置重新開機作業）。如需裝置機型的相關資訊，請參閱[裝置機型](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html)。
4. 裝置可以使用「裝置管理通訊協定」來傳遞有關其位置、診斷資訊及錯誤碼的更新。
5. 若要處理大型裝置母體中的已廢止裝置，**受管理裝置**作業要求會包含選用性的 lifetime 參數。lifetime 參數是秒數，裝置必須在這段時間內提出另一個**管理裝置**要求，來避免被分類為休眠及變成未受管理裝置。
6. 裝置解除任務時，您可以使用儀表板或 REST API，將它從 {{site.data.keyword.iot_short_notm}} 中移除。

請參閱秘訣：[將 Raspberry Pi 當作受管理裝置連接至 IBM Watson IoT Platform ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/){: new_window}。

### 回覆碼摘要


下表顯示在裝置管理生命週期期間的各種階段所產生的回覆碼。

|回覆碼 |訊息 |
|:---|:---|
|200   |作業成功|
|202   |已接受（用於起始指令）|
|204   |已變更（用於屬性更新）|
|400   |不正確的要求（例如，如果裝置未處於此指令的適當狀態）|
|404   |找不到屬性（如果將作業發佈至無效主題，也適用）|
|409   |由於發生衝突而無法更新資源（例如，同時間有兩個要求正在更新資源，因此可以稍後再重試更新）|
|500   |非預期的裝置錯誤|
|501   |未實作作業|


## 管理裝置要求
{: #manage_device_request}

裝置使用「管理裝置」要求來變成受管理裝置。在連接至 {{site.data.keyword.iot_short_notm}} 之後，「管理裝置」要求必須是裝置所傳送的第一個裝置管理要求。裝置管理代理程式一般只要啟動或重新啟動，就會傳送這類型的要求。

**重要事項：**任何受管理裝置都需要支援此作業。


### 管理裝置要求的主題

裝置會將「管理裝置」要求發佈至下列主題：

```
iotdevice-1/mgmt/manage
```

伺服器會在下列主題上回應「管理裝置」要求：

```
iotdm-1/response
```




### 管理裝置要求的訊息格式


在「管理裝置」要求中，`d` 欄位及其所有子欄位都是選用性欄位。`metadata` 及 `deviceInfo` 欄位值在傳送時會取代傳送端裝置的對應屬性。

選用性的 `lifetime` 欄位指定時間長度（以秒為單位），裝置必須在這段時間內傳送另一個「管理裝置」要求，才能避免被分類為休眠以及變成未受管理裝置。如果省略 `lifetime` 欄位，或設為 `0`，則受管理裝置不會變成休眠。`lifetime` 欄位的最低支援設定是 `3600` 秒（即 1 小時）。

選用性的 `supports.deviceActions` 及 `supports.firmwareActions` 欄位指出裝置管理代理程式的功能。如果設定 `supports.deviceActions`，則代理程式支援重新開機及重設為原廠設定動作。若裝置無法區分重新開機與重設為原廠設定，則這兩個動作可以使用相同的行為。如果設定 `supports.firmwareActions`，代理程式同時支援韌體下載及韌體更新動作。

下列範例顯示要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

下列範例顯示回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### 管理裝置要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|


## 取消管理裝置要求
{: #manage-unmanage}


裝置不再需要管理時，會使用「取消管理裝置」要求。裝置變成未受管理時，{{site.data.keyword.iot_short_notm}} 就不會再將新的裝置管理要求傳送至裝置。未受管理裝置會繼續發佈錯誤碼、日誌訊息及位置訊息。  
**重要事項：**任何受管理裝置都需要支援此作業。

### 取消管理裝置要求的主題


裝置會將「取消管理裝置」要求發佈至下列主題：

```
iotdevice-1/mgmt/unmanage
```

伺服器會在下列主題上回應「取消管理裝置」要求：

```
iotdm-1/response
```

### 取消管理裝置要求的訊息格式

要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 取消管理裝置要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|


## 更新位置要求
{: #update-location}

裝置會使用「更新位置」要求來管理裝置的位置資料。使用下列方式可以在 {{site.data.keyword.iot_short_notm}} 中更新裝置的位置 meta 資料：

#### 自動裝置位置更新
- 裝置會通知 {{site.data.keyword.iot_short_notm}} 有關位置更新。裝置會從 GPS 接收端擷取其位置，並將裝置管理訊息傳送至 {{site.data.keyword.iot_short_notm}} 實例來更新其位置。時間戳記會擷取從 GPS 接收端中擷取位置的時間。即使傳送位置更新訊息時發生延遲，時間戳記仍然有效。如果裝置管理訊息中省略時間戳記，則會使用訊息回執的日期和時間來更新位置 meta 資料。

#### 使用 REST API 的手動裝置位置更新
- 登錄裝置時，您可以使用 {{site.data.keyword.iot_short_notm}} REST API 來手動設定靜態裝置的位置 meta 資料。您也可以稍後再修改位置。時間戳記設定是選用項目，但省略時，會在裝置的位置 meta 資料中設定現行日期和時間。

### 裝置所觸發的位置更新

可以判定其位置的裝置可以選擇將位置變更通知 {{site.data.keyword.iot_short_notm}} 裝置管理伺服器。

### 裝置所觸發的更新位置要求的主題


裝置會將「更新位置」要求發佈至下列主題：

```
iotdevice-1/device/update/location
```

伺服器會在下列主題上回應「更新位置」要求：

```
iotdm-1/response
```

### 使用者或應用程式所觸發的位置更新


使用者或應用程式更新作用中受管理裝置的位置時，裝置會擷取更新訊息。




### 使用者或應用程式所觸發的更新位置要求的主題


伺服器會將「更新位置」要求發佈至下列主題：

```
iotdm-1/device/update
```

### 更新位置要求的訊息格式


`measuredDateTime` 欄位是位置測量的日期。`updatedDateTime` 欄位是裝置資訊的更新日期。基於效率，{{site.data.keyword.iot_short_notm}} 有時會對位置資訊進行批次更新，因此更新會略為延遲。必須使用「全球大地坐標系統 (World Geodetic System 1984, WGS84)」來指定緯度及經度（十進位制）。

只要更新位置，就會將提供的緯度、經度、海拔高度及不確定性值視為單次的多值更新。緯度與經度是必要項目，每次更新時兩者都必須提供。海拔高度及不確定性則是選用項目，可以省略。

如果在某次更新時提供了選用值，然後在之後的更新中省略這些值，則之前的值會被後面的更新刪除。每一個更新都視為完整多值設定。

### 裝置所觸發的位置更新


要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 更新位置要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|


### 使用者或應用程式所觸發的位置更新


下列範例概述有效負載格式：

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**附註：**未使用 `reqID` 參數，因為裝置不需要回應。

## 更新裝置屬性要求
{: #update-attributes}

藉由使用 REST API，{{site.data.keyword.iot_short_notm}} 可以將要求傳送至裝置，以更新下列一個以上裝置屬性的值：


|屬性 | 相關資訊|
|:---|:---|
|location  | 請參閱[更新位置](index.html#update-location)|
|metadata  | 選用|
|deviceInfo | 選用|
|mgmt.firmware | 請參閱[韌體更新處理程序](requests.html#firmware-actions-update)|

### 更新裝置屬性要求的主題


伺服器會將「裝置更新」要求發佈至下列主題：

```
iotdm-1/device/update
```


### 更新裝置屬性要求的訊息格式


下列範例概述要求的有效負載格式：

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## 新增錯誤碼要求
{: #diag-add-error-code}

裝置可以選擇使用「新增錯誤碼」要求類型，來通知 {{site.data.keyword.iot_short_notm}} 裝置管理伺服器有關其錯誤狀態的變更。

### 新增錯誤碼要求的主題


裝置會將「新增錯誤碼」要求發佈至下列主題：

```
iotdevice-1/add/diag/errorCodes
```

### 新增錯誤碼要求的訊息格式


與 `errorCode` 相關聯的值就是現行裝置錯誤碼，而且必須新增至 {{site.data.keyword.iot_short_notm}}。

要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 新增錯誤碼要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|


## 清除錯誤碼要求
{: #diag-clear-error-codes}

裝置可以要求 {{site.data.keyword.iot_short_notm}} 使用「清除錯誤碼」要求類型來清除裝置的所有錯誤碼。

### 清除錯誤碼要求的主題


裝置會將此要求發佈至下列主題：

```
iotdevice-1/clear/diag/errorCodes
```

### 清除錯誤碼要求的訊息格式


要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 清除錯誤碼要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|


## 新增日誌要求
{: #diag-add-log}

裝置可以選擇是否通知 {{site.data.keyword.iot_short_notm}} 裝置管理支援有關新增日誌項目的變更。日誌項目包含日誌訊息、時間戳記、嚴重性及選用性 base64 編碼的二進位診斷資料。

### 新增日誌要求的主題
裝置會將此要求發佈至下列主題：

```
iotdevice-1/add/diag/log
```


### 新增日誌要求的訊息格式

下表說明送出訊息屬性的格式：

|屬性 |說明 |
|:---|:---|
|`message`|指定需要新增至 {{site.data.keyword.iot_short_notm}} 的診斷訊息|
|`timestamp`|指定 ISO8601 格式之日誌項目的日期和時間 |
|`data`|指定選用性 base64 編碼的診斷資料|
|`severity`|指定訊息的嚴重性（0：參考資訊、1：警告、2：錯誤）|


要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### 新增日誌要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|

## 清除日誌要求
{: #diag-clear-logs}

裝置可以要求 {{site.data.keyword.iot_short_notm}} 使用「清除日誌」要求類型來清除裝置的所有日誌項目。

### 清除日誌要求的主題


裝置會將「清除日誌」要求發佈至下列主題：

```
iotdevice-1/clear/diag/log
```

### 清除日誌要求的訊息格式


要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the device:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 清除日誌要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確，或裝置不在資料庫中。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|

## 觀察屬性變更要求
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} 可以將「觀察屬性變更」要求傳送至裝置，以使用「觀察屬性變更」要求類型來觀察一個以上裝置屬性的變更。裝置收到要求時，只要所觀察屬性的值變更，就必須將通知要求傳送至 {{site.data.keyword.iot_short_notm}}。

**重要事項：**裝置必須實作、觀察、通知及取消作業，才能支援[韌體動作 - 更新](requests.html#firmware-actions-update)要求類型。

### 觀察屬性變更要求的主題


伺服器會將「觀察屬性變更」要求發佈至下列主題：

```
iotdm-1/observe
```

### 觀察屬性變更要求的訊息格式


`fields` 陣列是裝置機型的裝置屬性陣列。如果指定複式欄位（例如 `mgmt.firmware`），則預期會同時更新其基礎欄位，因此只會產生單一通知訊息。

如果 `rc` 參數的值不是 `200`，則可以指定回應中使用的 `message` 參數。如果無法擷取任何指定的參數值，則在找不到裝置時，必須將 `rc` 參數的值設為 `404`，如果是任何其他原因，則必須設為 `500`。找不到參數的值時，`fields` 陣列應該包含元素，其 `field` 設為每個無法讀取的參數名稱。應該省略 `value` 參數。若要將回應碼參數設為 `200`，必須指定 `field` 及 `value`，其中 `value` 是 `field` 參數值所識別之屬性的現行值。

要求格式：

```
Incoming message from the server:

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

回應格式：

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## 取消屬性觀察要求
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} 可以將要求傳送至裝置，以使用「取消屬性觀察」要求類型來取消一個以上裝置屬性的現行觀察。要求的 `fields` 部分是裝置機型的裝置屬性名稱陣列（例如，`location`、`mgmt.firmware` 或 `mgmt.firmware.state` 參數）。

如果 `rc` 參數的值不是 `200`，則必須指定 `message` 參數。

**重要事項：**裝置必須實作、觀察、通知及取消作業，才能支援[韌體動作 - 更新](requests.html#firmware-actions-update)要求類型。

### 取消屬性觀察要求的主題


伺服器會將「取消屬性觀察」要求發佈至下列主題：

```
iotdm-1/cancel
```


### 取消屬性觀察要求的訊息格式


要求格式：

```
Incoming message from the server:

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

回應格式：

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## 通知屬性變更要求
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} 可以使用「通知屬性變更」要求類型，來提出特定屬性或一組值的觀察要求。一或數個屬性的值變更時，裝置必須傳送包含最新值的通知。

`field_name` 參數的值是已變更屬性的名稱，而 `field_value` 是屬性的現行值。屬性可以是複式欄位。如果因單一作業而更新複式欄位中的多個值，則只會傳送單一通知訊息。

順利處理通知要求時，會將 `rc` 參數的值設為 `200`。如果要求不正確，則會將 `rc` 參數的值設為 `400`。如果觀察不到通知要求中指定的參數，則會將 `rc` 參數的值設為 `404`。

**重要事項：**裝置必須實作、觀察、通知及取消作業，才能支援[韌體動作 - 更新](requests.html#firmware-actions-update)要求類型。


### 通知屬性變更要求的主題


裝置會將「通知屬性變更」要求發佈至下列主題：

```
iotdevice-1/notify
```


### 通知屬性變更要求的訊息格式


要求格式：

```
Outgoing message from the device:

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

回應格式：

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### 通知屬性變更要求的回應碼

|回應碼 |訊息 |
|:---|:---|
|200   |作業成功。|
|400   |輸入訊息不符合預期格式，或其中一個值超出有效範圍。|
|404   |主題名稱不正確、裝置不在資料庫中，或是沒有針對所報告欄位的觀察。|
|409   |裝置資料庫更新期間發生衝突。若要解決此衝突，請簡化作業（必要的話）。|
|500   |發生內部錯誤。|
