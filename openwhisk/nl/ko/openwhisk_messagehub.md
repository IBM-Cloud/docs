---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Message Hub 패키지 사용
{: #openwhisk_catalog_message_hub}

이 패키지를 사용하면 기본 고성능 Kafka API를 사용하여 이용 중인 메시지를 공개하기 위한 [Message Hub](https://developer.ibm.com/messaging/message-hub) 인스턴스와 통신할 수 있습니다.
{: shortdesc}

## IBM MessageHub 인스턴스를 청취하는 트리거 작성
{: #openwhisk_catalog_message_hub_trigger}

메시지가 Message Hub 인스턴스에 게시될 때 반응하는 트리거를 작성하려면 `/messaging/messageHubFeed`라는 이름의 피드를 사용해야 합니다. 이 피드 조치는 다음 매개변수를 지원합니다.

|이름|유형|설명|
|---|---|---|
|kafka_brokers_sasl|JSON 문자열 배열|이 매개변수는 Message Hub 인스턴스에서 브로커를 구성하는 `<host>:<port>` 문자열의 배열입니다.|
|user|문자열|Message Hub 사용자 이름|
|password|문자열|Message Hub 비밀번호|
|topic|문자열|트리거가 청취하게 하려는 주제|
|kafka_admin_url|URL 문자열|Message Hub 관리 REST 인터페이스의 URL|
|isJSONData|부울(선택사항 - 기본값=false)|`true`로 설정하면 제공자가 트리거 페이로드로서 메시지 값을 전달하기 전에 이 메시지 값을 JSON으로 구문 분석하려고 시도합니다.|
|isBinaryKey|부울(선택사항 - 기본값=false)|`true`로 설정하면 제공자가 트리거 페이로드로서 키 값을 전달하기 전에 이 키 값을 Base64로 인코딩합니다.|
|isBinaryValue|부울(선택사항 - 기본값=false)|`true`로 설정하면 제공자가 트리거 페이로드로서 메시지 값을 전달하기 전에 이 메시지 값을 Base64로 인코딩합니다.|

이 매개변수 목록이 위압적으로 보일 수 있지만 패키지 새로 고치기 CLI 명령을 사용하여 자동으로 설정할 수 있습니다. 

1. OpenWhisk를 위해 사용 중인 현재 조직 및 영역 아래 Message Hub 서비스의 인스턴스를 작성하십시오. 

2. 청취하려는 주제가 Message Hub에 이미 있는지 확인하거나 새 주제를 작성하십시오(예: `mytopic`).

3. 네임스페이스 내의 패키지를 새로 고치십시오. 새로 고치면 사용자가 작성한 Message Hub 서비스 인스턴스에 대한 패키지 바인딩이 자동으로 작성됩니다. 

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  이제 패키지 바인딩에는 Message Hub 인스턴스와 연관된 신임 정보가 포함됩니다. 

4. 지금 필요한 작업은 새 메시지가 Message Hub 주제에 게시될 때 실행할 트리거를 작성하는 것입니다.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Bluemix 외부에서 Message Hub 패키지 설정

Bluemix 외부에 Message Hub를 설정하려면 Message Hub 서비스에 대한 패키지 바인딩을 수동으로 작성해야 합니다. 이 경우 Message Hub 서비스 신임 정보와 연결 정보가 필요합니다. 

1. Message Hub 서비스에 대해 구성된 패키지 바인딩을 작성하십시오. 

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. 이제 새 메시지가 Message Hub 주제에 게시될 때 실행할 새 패키지를 사용하여 트리거를 작성할 수 있습니다.

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## 메시지 청취
{: #openwhisk_catalog_message_hub_listen}

트리거 작성 후 시스템은 메시징 서비스에서 지정된 주제를 모니터링합니다. 새 메시지가 게시되는 경우 트리거가 실행됩니다. 

해당 트리거의 페이로드에는 트리거가 마지막으로 실행된 이후 게시된 메시지 배열인 `messages` 필드가 포함됩니다. 배열의 각 메시지 오브젝트에 다음 필드가 포함됩니다. 
- topic
- partition
- offset
- key
- value

Kafka 용어에서 이러한 필드는 따로 설명할 필요가 없습니다. 하지만 `key`에는 `key`가 바이너리 데이터를 전송할 수 있게 하는 선택적 기능 `isBinaryKey`가 있습니다. 또한 `value`에는 특수 고려사항이 있어야 합니다. 선택적 필드 `isJSONData` 및 `isBinaryValue`는 JSON 및 바이너리 메시지를 처리하는 데 사용할 수 있습니다. 이 `isJSONData`와 `isBinaryValue` 필드는 함께 사용할 수 없습니다.

예를 들어, 트리거 작성 시 `isBinaryKey`가 `true`로 설정된 경우, `key`가 실행된 트리거의 페이로드에서 리턴될 때 Base64 문자열로 인코딩됩니다.

예를 들어, `일부 키`의 `key`가 `true`로 설정된 `isBinaryKey`로 게시된 경우 트리거 페이로드는 다음과 같습니다.

```json
{
    "messages": [
    {
      "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

트리거가 작성될 때 `isJSONData` 매개변수가 `false`로 설정된 경우(또는 설정되지 않은 경우) `value` 필드는 게시된 메시지의 원시 값이 됩니다. 그러나 트리거가 작성될 때 `isJSONData`가 `true`로 설정된 경우에는 시스템에서 최대한 이 값을 JSON 오브젝트로 구문 분석하려고 시도합니다. 구문 분석에 성공하면 트리거 페이로드의 `value`는 결과적으로 생성되는 JSON 오브젝트가 됩니다. 

예를 들어, `isJSONData`가 `true`로 설정된 상태에서 `{"title": "Some string", "amount": 5, "isAwesome": true}` 메시지가 게시되는 경우 트리거 페이로드는 다음과 유사하게 보일 수 있습니다. 

```json
{
  "messages": [
    {
      "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

그러나 `isJSONData`가 `false`로 설정된 상태에서 동일한 메시지 컨텐츠가 게시되는 경우 트리거 페이로드는 다음과 유사하게 보일 수 있습니다. 

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

`isJSONData`와 유사하게 트리거 작성 중에 `isBinaryValue`가 `true`로 설정된 경우 트리거 페이로드의 결과 `value`는 Base64 문자열로 인코딩됩니다.

예를 들어, `Some data`의 `value`가 `true`로 설정된 `isBinaryValue`로 게시된 경우 트리거 페이로드는 다음과 같습니다.

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

동일한 메시지가 `true`로 설정된 `isBinaryData` 없이 게시되는 경우 트리거 페이로드는 다음 예와 비슷합니다.

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### 메시지가 일괄처리됨
트리거 페이로드에 메시지 배열이 포함되어 있는 것을 알 수 있습니다. 이는 메시징 시스템으로 메시지를 매우 빠르게 생성하는 경우 피드는 게시된 메시지를 한 번의 트리거 실행으로 일괄 처리하려고 시도한다는 것을 의미합니다. 이렇게 하면 더욱 신속하고 효율적으로 트리거에 메시지를 게시할 수 있습니다. 

트리거에 의해 실행되는 조치를 코딩할 때 페이로드의 메시지 수는 기술적으로 제한이 없지만 항상 0보다 크다는 사실을 기억하십시오. 다음은 일괄처리된 메시지의 예입니다. (*오프셋* 값의 변경사항에 주의하십시오.)
 
 ```json
 {
   "messages": [
    {
      "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Message Hub에 메시지 생성
OpenWhisk 조치를 사용하여 Message Hub에 메시지를 편리하게 생성하려는 경우 `/messaging/messageHubProduce` 조치를 사용할 수 있습니다. 이 조치는 다음 매개변수를 사용합니다.

|이름|유형|설명|
|---|---|---|
|kafka_brokers_sasl|JSON 문자열 배열|이 매개변수는 Message Hub 인스턴스에서 브로커를 구성하는 `<host>:<port>` 문자열의 배열입니다.|
|user|문자열|Message Hub 사용자 이름|
|password|문자열|Message Hub 비밀번호|
|topic|문자열|트리거가 청취하게 하려는 주제|
|value|문자열|생성할 메시지의 값|
|key|문자열(선택사항)|생성할 메시지의 키|

`wsk package refresh`를 사용하여 처음 세 개의 매개변수를 자동으로 바인드할 수 있는 경우 다음은 모든 필수 매개변수를 사용한 조치 호출의 예입니다.

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "This is the content of my message"
```
{: pre}

## 예

### OpenWhisk를 IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage 및 IBM Data Science Experience와 통합
OpenWhisk를 IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage, IBM Data Science Experience(Spark) 서비스와 통합하는 예는 [여기에서 찾을 수 있습니다](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0).

## 참조
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
