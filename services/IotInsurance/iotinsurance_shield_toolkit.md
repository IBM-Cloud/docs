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


# Shield toolkit
{: #iot4i_shield_toolkit}
Use shields to protect property and users by identifying hazards and creating appropriate automated responses. Use or modify the shields that are included in the {{site.data.keyword.iotinsurance_short}} shields library or create and implement your own shields by using the instructions and examples that follow.
{:shortdesc}

## About shields.
A shield is a set of rules and defined actions that can be triggered by specific conditions in the input that is received from a sensor. For example, you could create a shield with a rule that causes a text message to be sent whenever the sensor detects a water leak.

## Using shields from the {{site.data.keyword.iotinsurance_short}} shields library

You can find a wide assortment of predefined shields in the [{{site.data.keyword.iotinsurance_short}} shields library ![External link icon](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}. View the README file on that site for instructions to download and begin using the shields.

## Creating your own shield
This example shows you how to set up your environment, define a shield, create a user, and then associate the shield with the user.  You can also optionally create promotions and simulated hazards.  

Code samples for creating a simple shield for water leaks are shown in the following sections. A full set of example code is available in the [iot4i-api-examples-nodejs GitHub repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/).

### Prerequisites
Before you begin, ensure that the following prerequisites are in place:

- [Node.js](https://nodejs.org/en/) installed on your computer.  
- A Node.js-enabled runtime environment such as Eclipse.
- Git software and access to the [GitHub source code repository for the API examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Alternatively, you can download the [archive with the source code files](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Prepared source code.  
  To prepare the source code, complete these steps:
  1. Clone or download the [GitHub source code repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) to your computer.
  2. Install the project's open source prerequisites by using a command line to go to the folder that contains the cloned source code files, and running `npm install` command.

### Setting up your environment
{: #environment}
To configure your environment to send REST API calls, you must configure the URL for the API in the config.js file. The aggregator URL can be ignored in this context.

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

### Creating a shield definition
{: #create_shield_def}

Method: POST  
API: /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

Create a shield definition in the createShield.js file.  The following example shows a simple shield that detects a water leak.

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

where:
- **UUID** - The universal unique identifier (UUID) of the shield.
- **actions** - A list of actions that are triggered when a hazard is created. In this example, information about the hazard is sent to the user's app by using an iOS push notification.

### Creating a shield code
{: #create_shield_code}
Create a shield code in the shieldCode.js file to define how the shield engine processes a payload.

The following example shows a shield code that can be used to process a water leak payload for the shield that was shown in the previous examples.

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

Each shield code contains resources that are defined in resource/shield.js statements. Each of the following resources includes an example that can be used with the shield, payload, and user that are shown in previous examples.

  - Shield name  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - Shield delay - The delay in milliseconds between hazards.  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - Shield universal unique identifier (UUID)  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - Entry condition - The condition and attributes that are required for the shield engine to process the payload. In the example, the condition is that the payload must contain the attribute **liquid_detected**.  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - The core of the shield that calculates and runs an algorithm to determine whether a hazard is present. In the following example, the only required attribute is **liquid_detected**,  but safelets can be used to define complex algorithms.  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - Message - The message that is sent to the user if the hazard is processed.
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - Shield execution - The function that is used to run the shield directly, instead of waiting for the shield engine  to run all relevant shields automatically.  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - Register shield - A predefined function that must be called in the shield code to register the shield in the shield engine. The **undefined** value in the example represents the preprocessing function, which is not needed in this particular example. In some shields, the preprocessing function can be used to rearrange the data in the payload. For example, if temperature readings are reported in Fahrenheit and the safelet requires Celsius, the preprocessing function can be used to convert the temperatures to the required value.  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### Creating a user
{: #create_user}

Method: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

Create a user in the createUser.js file. The following example shows how to create a single user.

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

where:
- **username** - The unique key for the user that is used to identify every entity that is associated with the user, such as devices, shields, and promotions.
- **password** - Only the password's hash is stored in the database.
- **DeviceId** - The identifier that is used to register the user in {{site.data.keyword.iot_full}}. The value is the same as the username.
- **accessLevel** - The value defines the API endpoints that the user can access:
  - 100 - mobile app
  - 10 - dashboard
  - 1 - system administrator

### Creating a shield association
{: #create_shield_assoc}

Method: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

Create a shield association that links the shield to the user in the createUserShieldAssociation.js.

The following example shows a shield association for the shield and the user that were created in the previous sections.

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### Creating a simulated hazard
{: #create_sim_hazard}

Method: POST  
API: /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

You can create a simulated hazard payload to test your shields.

The following example shows how to create a payload that activates the shield that was created in the previous example and sends an alert to the associated user.

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


### Creating a promotion
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} can send promotions to the homeowner by using the mobile app. Create promotions by using the createPromotion.js file.

The following example shows how to create a promotion for an authorized plumber.

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

You can optionally deploy your mobile app and use [the instructions in the ioti-mobile GitHub repository](https://github.com/ibm-watson-iot/ioti-mobile) to connect as the user that you created in the previous section.

# Related Links
{: #rellinks}

## API Reference
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API Examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Related Links
{: #general}
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
