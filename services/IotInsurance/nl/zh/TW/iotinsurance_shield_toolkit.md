---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 使用防護工具箱
{: #iot4i_shield_toolkit}
使用防護可透過識別危害及建立適當的自動回應來保護內容及使用者。使用或修改 {{site.data.keyword.iotinsurance_short}} 防護程式庫中包含的防護，或使用下列指示及範例建立並實作您自己的防護。
{:shortdesc}

## 關於防護
防護是一組規則及定義動作，可以由接收自感應器的輸入中的特定狀況觸發。例如，您可以建立防護，其規則導致每當感應器偵測到漏水時就傳送文字訊息。

## 使用來自 {{site.data.keyword.iotinsurance_short}} 防護程式庫的防護

您可以在 [{{site.data.keyword.iotinsurance_short}} 防護程式庫 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window} 中找到一套廣泛的預先定義防護。檢視該網站上的 README 檔，以取得下載和開始使用防護的指示。

## 建立自己的防護
此範例顯示如何設定環境、定義防護、建立使用者，然後建立防護與使用者的關聯。您也可以選擇性地建立促銷活動及模擬的危害。
  

下列各節會顯示用於建立漏水之簡單防護的程式碼範例。[iot4i-api-examples-nodejs GitHub 儲存庫](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/)會提供一組完整範例程式碼。

### 必要條件
開始之前，請確定已具有下列必要條件：

- 電腦上所安裝的 [Node.js](https://nodejs.org/en/)。  
- 已啟用 Node.js 的運行環境（例如 Eclipse）。
- Git 軟體及 [API 範例的 GitHub 原始碼儲存庫](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)的存取。或者，您可以下載[保存與原始碼檔案](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)。
- 備妥的原始碼。
    
若要準備原始碼，請執行下列動作：
  1. 將 [GitHub 原始碼儲存庫](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)複製或下載至電腦。
  2. 使用指令行以移至包含所複製原始碼檔案的資料夾，並執行 `npm install` 指令，來安裝專案的開放程式碼必要條件。

### 設定環境
{: #environment}
若要配置環境來傳送 REST API 呼叫，您必須在 config.js 檔案中配置 API 的 URL。在此環境定義中可以忽略聚集器 URL。

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### 建立防護定義
{: #create_shield_def}

方法：POST  
API：/shield  
https://iot4i-api-docs.mybluemix.net/#!/shield/addShield

在 createShield.js 檔案中建立防護定義。下列範例顯示用來偵測漏水的簡單防護。

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

其中：
- **UUID** - 防護的通用唯一 ID (UUID)。
- **actions** - 建立危害時所觸發的動作清單。在此範例中，會使用 iOS 推送通知，將危害的相關資訊傳送至使用者的應用程式。

### 建立防護程式碼
{: #create_shield_code}
在 shieldCode.js 檔案中建立防護程式碼，以定義防護引擎如何處理有效負載。

下列範例所顯示的防護程式碼可以用來處理先前範例中所顯示之防護的漏水有效負載。

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

每一個防護程式碼都會包含 resource/shield.js 陳述式中所定義的資源。下列每一個資源都會包括範例，而這個範例可以與先前範例中所顯示的防護、有效負載及使用者搭配使用。

  - 防護名稱  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - 防護延遲 - 危害之間的延遲（毫秒）。  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - 防護通用唯一 ID (UUID)  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - 項目條件 - 防護引擎處理有效負載所需的條件及屬性。在此範例中，條件是有效負載必須包含屬性 **liquid_detected**。  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - 計算及執行演算法來判定危害是否存在的防護核心。在下列範例中，唯一需要的屬性是 **liquid_detected**，但 Safelet 可以用來定義複雜演算法。  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - 訊息 - 處理危害時傳送至使用者的訊息。
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - 防護執行 - 用來直接執行防護的函數，而不是等待防護引擎自動執行所有相關的防護。  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - 登錄防護 - 防護程式碼中必須呼叫以在防護引擎中登錄防護的預先定義函數。範例中的 **undefined** 值代表這個特定範例中不需要的前置處理函數。在部分防護中，可以使用前置處理函數來重新排列有效負載中的資料。例如，如果以華氏報告溫度讀數，而 Safelet 需要攝氏，則可以使用前置處理函數，將溫度轉換為必要值。  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### 建立使用者
{: #create_user}

方法：POST  
API：/user  
https://iot4i-api-docs.mybluemix.net/#!/user/addUser

在 createUser.js 檔案中建立使用者。下列範例顯示如何建立單一使用者。

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

其中：
- **username** - 使用者的唯一索引鍵，用來識別每個與使用者相關聯的實體（例如裝置、防護及促銷活動）。
- **password** - 僅密碼的雜湊會儲存在資料庫中。
- **DeviceId** - 用來在 {{site.data.keyword.iot_full}} 中登錄使用者的 ID。值與 username 相同。
- **accessLevel** - 此值定義使用者可以存取的 API 端點：
  - 100 - 行動應用程式
  - 10 - 儀表板
  - 1 - 系統管理者

### 建立防護關聯
{: #create_shield_assoc}

方法：POST  
API：/user  
https://iot4i-api-docs.mybluemix.net/#!/shieldassociation/addShieldAssociation

在 createUserShieldAssociation.js 中，建立將防護鏈結至使用者的防護關聯。

下列範例顯示前面各節中所建立之防護及使用者的防護關聯。

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### 建立模擬的危害
{: #create_sim_hazard}

方法：POST  
API：/sendPayloadToMQTT  
https://iot4i-api-docs.mybluemix.net/#!/global/sendPayloadToMQTT

您可以建立模擬的危害有效負載，以測試防護。

下列範例顯示如何建立有效負載，這個有效負載啟動前一個範例中所建立的防護，並將警示傳送給關聯使用者。

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### 建立促銷活動
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} 可以使用行動應用程式，以將促銷活動傳送給屋主。使用 createPromotion.js 檔案來建立促銷活動。

下列範例顯示如何建立授權水管工的促銷活動。

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

您可以選擇性地部署行動應用程式，以及使用 [ioti-mobile GitHub 儲存庫中的指示](https://github.com/ibm-watson-iot/ioti-mobile)以您在前一節中建立的使用者身分進行連接。
