---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 保障工具包
{: #iot4i_shield_toolkit}
使用保障通过识别危险并创建相应的自动响应来保护财产和用户。通过使用下面的指示信息和示例，来使用或修改 {{site.data.keyword.iotinsurance_short}} 保障库中包含的保障或创建并实施自己的保障。
{:shortdesc}

## 关于保障。
保障是一组规则和定义的操作，从传感器接收到的输入中的特定条件会触发这些操作。例如，您可以使用某个规则来创建保障，通过该规则，在传感器检测到漏水时会发送短信。

## 从 {{site.data.keyword.iotinsurance_short}} 保障库使用保障

您可以在 [{{site.data.keyword.iotinsurance_short}} 保障库 ![外部链接](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window} 中找到各种预定义保障。请查看该站点上的自述文件，以获取下载和开始使用保障的指示信息。

## 创建自己的保障
此示例显示了如何设置环境，定义保障，创建用户，然后将保障与用户相关联。您还可以选择创建升级和模拟危险。
  

以下各部分中说明了用于创建简单漏水保障的代码样本。[iot4i-api-examples-nodejs GitHub 存储库](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/)中提供了一组完整的示例代码。

### 先决条件
开始之前，请确保满足以下先决条件：

- 已在计算机上安装 [Node.js](https://nodejs.org/en/)。  
- 支持 Node.js 的运行时环境，例如 Eclipse。
- Git 软件以及对 [API 示例的 GitHub 源代码存储库](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)的访问权。或者，您可以下载[带有源代码文件的归档](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)。
- 准备好的源代码。  
要准备源代码，请完成以下步骤：
  1. 将 [GitHub 源代码存储库](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)克隆或下载到您的计算机。
  2. 通过使用命令行转至包含克隆的源代码文件的文件夹并运行 `npm install` 命令来安装项目的开放式源代码必备软件。

### 设置环境
{: #environment}
要将环境配置为发送 REST API 调用，必须在 config.js 文件中配置 API 的 URL。在此上下文中可忽略聚集器 URL。

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

### 创建保障定义
{: #create_shield_def}

方法：POST  
API：/shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

在 createShield.js 文件中创建保障定义。以下示例显示了用于检测漏水的简单保障。

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
- **UUID** - 保障的通用唯一标识 (UUID)。
- **actions** - 发生危险时触发的操作的列表。在此示例中，会使用 iOS 推送通知将有关危险的信息发送到用户的应用程序。

### 创建保障代码
{: #create_shield_code}
在 shieldCode.js 文件中创建保障代码，以定义保障引擎如何处理有效内容。

以下示例显示的保障代码可用于为先前示例中所示的保障处理漏水有效内容。

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

每个保障代码都会包含 resource/shield.js 语句中定义的资源。以下每个资源都包含一个示例，可用于先前示例中所示的保障、有效内容和用户。

  - 保障名称  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - 保障延迟时间 - 危险间隔的延迟时间（以毫秒为单位）。  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - 保障通用唯一标识 (UUID)  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - 输入条件 - 保障引擎处理有效内容所需的条件和属性。在此示例中，条件是有效内容必须包含属性 **liquid_detected**。  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - 保障的核心，用于计算并运行算法来确定是否存在危险。在以下示例中，唯一必需的属性是 **liquid_detected**，但 safelet 还可用于定义复杂算法。  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - 消息 - 处理危险后发送给用户的消息。
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - 保障执行 - 此函数用于直接运行保障，而不等待保障引擎自动运行所有相关保障。  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - 注册保障 - 预定义的函数，在保障引擎中注册保障时必须在保障代码中调用此函数。示例中的 **undefined** 值表示预处理函数，在此特定示例中并不需要。在某些保障中，该预处理函数可用于重新安排有效内容中的数据。例如，如果报告的温度读数为华氏，而 safelet 需要摄氏时，可使用该预处理函数将温度转换为所需的值。  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### 创建用户
{: #create_user}

方法：POST  
API：/user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

在 createUser.js 文件中创建用户。以下示例显示了如何创建单个用户。

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
- **username** - 用户的唯一键，用于标识与用户关联的每个实体，例如设备、保障和升级。
- **password** - 数据库中只存储密码的散列。
- **DeviceId** - 用于在 {{site.data.keyword.iot_full}} 中注册用户的标识。此值与 usename 相同。
- **accessLevel** - 此值定义用户可以访问的 API 端点：
  - 100 - 移动应用程序
  - 10 - 仪表板
  - 1 - 系统管理员

### 创建保障关联
{: #create_shield_assoc}

方法：POST  
API：/user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

在 createUserShieldAssociation.js 中创建用于将保障链接到用户的保障关联。

以下示例显示了在先前部分中创建的保障与用户之间的保障关联。

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### 创建模拟危险
{: #create_sim_hazard}

方法：POST  
API：/sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

您可以创建模拟危险有效内容来测试保障。

以下示例显示了如何创建有效内容来激活在先前示例中创建的保障，并向关联用户发送警报。

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


### 创建升级
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} 可以使用移动应用程序向房主发送升级。使用 createPromotion.js 文件来创建升级。

以下示例显示了如何为授权的水管工创建升级。

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

您可以选择以先前部分中创建的用户身份来部署移动应用程序并使用 [ioti-mobile GitHub 存储库中的指示信息](https://github.com/ibm-watson-iot/ioti-mobile)进行连接。

# 相关链接
{: #rellinks}

## API 参考
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API 示例](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## 相关链接
{: #general}
* [开发人员支持论坛](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [堆栈溢出支持论坛](http://stackoverflow.com/questions/tagged/ibm-bluemix)
