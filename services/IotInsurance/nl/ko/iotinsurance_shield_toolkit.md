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


# 실드 툴킷 사용
{: #iot4i_shield_toolkit}
실드를 통해 위험을 식별하고 적절한 자동 응답을 작성하여 재산 및 사용자를 보호합니다. {{site.data.keyword.iotinsurance_short}} 실드 라이브러리에 포함된 실드를 사용 또는 수정하거나 다음에 소개되는 지시사항 및 예제를 사용하여 사용자 자신의 실드를 작성해서 구현하십시오.
{:shortdesc}

## 실드 정보.
실드는 센서에서 수신되는 입력의 특정 조건으로 트리거될 수 있는 정의된 조치 및 규칙 세트입니다. 예를 들어, 센서에서 누수를 발견할 때마다 텍스트 메시지가 전송되도록 하는 규칙으로 실드를 작성할 수 있습니다.

## {{site.data.keyword.iotinsurance_short}} 실드 라이브러리에서 실드 사용

[{{site.data.keyword.iotinsurance_short}} 실드 라이브러리 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}에서 사전 정의된 다양한 실드를 찾을 수 있습니다. 사이트의 README 파일에 있는 지시사항을 참조하여 실드를 다운로드하고 사용하십시오.

## 사용자 고유의 실드 작성
이 예에서는 환경을 설정하고 실드를 정의하며 사용자를 작성한 다음 실드를 사용자와 연관시키는 방법을 보여줍니다. 선택적으로 프로모션 및 시뮬레이션된 위험을 생성할 수도 있습니다.   

누수에 대비한 단순 실드를 생성하는 코드 샘플이 다음 섹션에 표시됩니다. 전체 예제 코드 세트는 [iot4i-api-examples-nodejs GitHub 저장소](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/)에 있습니다. 

### 전제조건
시작하기 전에 다음 전제조건에 부합하는지 확인하십시오. 

- 컴퓨터에 설치된 [Node.js](https://nodejs.org/en/).   
- Eclipse와 같은 Node.js 사용 런타임 환경. 
- Git 소프트웨어와 [API 예제의 GitHub 소스 코드 저장소](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)에 대한 액세스 권한. 또는 [소스 코드 파일로 아카이브](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)를 다운로드할 수 있습니다. 
- 준비된 소스 코드.   
  소스 코드를 준비하려면 다음 단계를 완료하십시오. 
  1. [GitHub 소스 코드 저장소](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)를 컴퓨터에 복제하거나 다운로드하십시오. 
  2. 복제된 소스 코드 파일을 포함하는 폴더로 이동하는 명령행을 사용하고 `npm install` 명령을 실행하여 프로젝트의 오픈 소스 필수 소프트웨어를 설치하십시오. 

### 환경 설정
{: #environment}
REST API 호출을 전송하는 환경을 구성하려면 config.js 파일에 API의 URL을 구성해야 합니다. 이 컨텍스트에서는 수집기 URL을 무시할 수 있습니다. 

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

### 실드 정의 작성
{: #create_shield_def}

메소드: POST   
API: /shield  
https://iot4i-api-docs.mybluemix.net/#!/shield/addShield

createShield.js 파일에 실드 정의를 작성하십시오. 다음 예에서는 누수를 발견하는 단순 실드를 보여줍니다. 

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

여기서 나타내는 의미는 다음과 같습니다. 
- **UUID** - 실드의 UUID(universal unique identifier)입니다. 
- **actions** - 위험 사항이 생성될 때 트리거될 조치 목록입니다. 이 예에서는 iOS 푸시 알림을 사용하여 위험 정보를 사용자 앱으로 전송합니다. 

### 실드 코드 작성
{: #create_shield_code}
shieldCode.js 파일에 실드 코드를 작성하여 실드 엔진의 페이로드 처리 방법을 정의하십시오. 

다음 예는 이전 예에 표시된 실드의 누수 페이로드를 처리할 수 있는 실드 코드를 보여줍니다. 

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

각 실드 코드에는 resource/shield.js 문에 정의된 리소스가 포함되어 있습니다. 다음 개별 리소스에는 이전 예에 표시된 실드, 페이로드, 사용자와 함께 사용할 수 있는 예제가 포함되어 있습니다. 

  - 실드 이름  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - 실드 지연 - 위험 사이의 지연(밀리초)  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - 실드의 UUID(universal unique identifier)  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - 입력 조건 - 페이로드를 처리할 실드 엔진에 필요한 조건과 속성입니다. 이 예에서 조건은 페이로드에 **liquid_detected** 속성이 포함되어야 하는 것입니다.   
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - 위험이 있는지 파악하는 알고리즘을 계산하고 실행하는 실드 코어입니다. 다음 예에서 유일한 필수 속성은 **liquid_detected**이지만 Safelet을 사용하여 복합 알고리즘을 정의할 수 있습니다.   
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - 메시지 - 위험이 처리된 경우 사용자에게 전송되는 메시지입니다. 
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - 실드 실행 - 실드 엔진에서 모든 관련 실드를 자동으로 실행하기를 대기하는 대신 실드를 직접 실행하는 데 사용하는 함수입니다.   
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - 등록 실드 - 실드 엔진에 실드를 등록하기 위해 실드 코드로 호출해야 하는 사전 정의된 함수입니다. 예제의 **undefined** 값은 이 예제에서는 필요하지 않은 선행 처리 함수를 나타냅니다. 일부 실드에서는 선행 처리 함수를 사용하여 페이로드의 데이터를 재배치할 수 있습니다. 예를 들어, 온도를 화씨로 보고하지만 Safelet에서 섭씨를 사용하는 경우 선행 처리 함수를 사용하여 온도를 필요한 값으로 변환할 수 있습니다.   
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### 사용자 작성
{: #create_user}

메소드: POST   
API: /user  
https://iot4i-api-docs.mybluemix.net/#!/user/addUser

createUser.js 파일에 사용자를 작성하십시오. 다음 예에서는 단일 사용자 작성 방법을 보여줍니다. 

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

여기서 나타내는 의미는 다음과 같습니다. 
- **username** - 사용자와 연관된 개별 엔티티를 식별하는 데 사용하는 사용자의 고유 키입니다(예: 디바이스, 실드, 프로모션). 
- **password** - 비밀번호의 해시만 데이터베이스에 저장됩니다. 
- **DeviceId** - {{site.data.keyword.iot_full}}에 사용자를 등록하는 데 사용하는 ID입니다. 이 값은 사용자 이름과 같습니다. 
- **accessLevel** - 이 값은 사용자가 액세스할 수 있는 API 엔드포인트를 정의합니다. 
  - 100 - 모바일 앱
  - 10 - 대시보드
  - 1 - 시스템 관리자

### 실드 연관 작성
{: #create_shield_assoc}

메소드: POST   
API: /user  
https://iot4i-api-docs.mybluemix.net/#!/shieldassociation/addShieldAssociation

실드를 createUserShieldAssociation.js의 사용자와 연결하는 실드 연관을 작성합니다.

다음 예는 이전 섹션에서 작성한 실드와 사용자의 실드 연관을 보여줍니다. 

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### 시뮬레이션된 위험 작성
{: #create_sim_hazard}

메소드: POST   
API: /sendPayloadToMQTT  
https://iot4i-api-docs.mybluemix.net/#!/global/sendPayloadToMQTT

시뮬레이션된 위험 페이로드를 작성하여 실드를 테스트할 수 있습니다. 

다음 예에서는 이전 예에서 작성한 실드를 활성화하고 연관된 사용자에게 경보를 전송하는 페이로드를 작성하는 방법을 보여줍니다. 

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


### 프로모션 작성
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}}에서는 모바일 앱을 사용하여 주택 소유자에게 프로모션을 발송할 수 있습니다. createPromotion.js 파일을 사용하여 프로모션을 작성하십시오. 

다음 예에서는 권한 부여된 배관기사를 위한 프로모션 작성 방법을 보여줍니다. 

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

선택적으로 모바일 앱을 배치하고 [ioti-mobile GitHub 저장소의 지시사항](https://github.com/ibm-watson-iot/ioti-mobile)을 사용하여 이전 섹션에서 작성한 사용자로 연결할 수 있습니다. 
