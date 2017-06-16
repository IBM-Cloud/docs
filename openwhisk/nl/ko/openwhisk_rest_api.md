---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk REST API 사용
{: #openwhisk_rest_api}

일단 OpenWhisk 환경이 사용되면 REST API 호출로 웹 앱 또는 모바일 앱에서 OpenWhisk를 사용할 수 있습니다. 

조치, 활성화, 패키지, 규칙 및 트리거 관련 API에 대한 세부사항은 [OpenWhisk API 문서](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json)를 참조하십시오. 


REST API를 통해 시스템의 모든 기능을 사용할 수 있습니다. 조치, 트리거, 규칙, 패키지, 활성화 및 네임스페이스에 대해 콜렉션 및 엔티티 엔드포인트가 있습니다. 

다음은 콜렉션 엔드포인트입니다. 
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}`는 OpenWhisk API 호스트 이름입니다(예: openwhisk.ng.bluemix.net, 172.17.0.1, 192.168.99.100, 192.168.33.13 등).
`{namespace}`에 대해서는 `_` 문자를 사용하여 사용자의 *기본 네임스페이스*를 지정할 수
있습니다. 

콜렉션 엔드포인트에서 GET 요청을 수행하여 콜렉션에서 엔티티의 목록을 페치할 수 있습니다. 

각 엔티티 유형마다 엔티티 엔드포인트가 있습니다. 
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

네임스페이스 엔드포인트와 활성화 엔드포인트는 GET 요청만 지원합니다. 조치 엔드포인트, 트리거 엔드포인트, 규칙 엔드포인트, 패키지 엔드포인트는 GET, PUT, DELETE 요청을 지원합니다. 조치, 트리거, 규칙의 엔드포인트는 POST 요청도 지원하며 이 요청은 조치와 트리거를 호출하고 규칙을 사용 또는 사용 안함으로 설정하는 데 사용됩니다.  

모든 API는 HTTP 기본 인증으로 보호됩니다.
[wskadmin](../tools/admin/wskadmin) 도구를 사용하여 새 네임스페이스 및 인증을 생성할 수 있습니다.
기본 인증 신임 정보는 `~/.wskprops` 파일의 `AUTH` 특성에 있으며 콜론으로 구분됩니다.
또한 CLI에서 `wsk property get --auth`를 실행하여 이러한 신임 정보를 검색할 수도 있습니다. 


다음은 `whisk.system` 네임스페이스에서 모든 패키지의 목록을 가져오는 [cURL](https://curl.haxx.se) 명령 도구를 사용하는 예제입니다. 

```bash
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
[
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

이 예제에서는 인증이 `-u` 플래그를 사용하여 전달되었으며, 이 값을 URL의 일부로서 `https://$AUTH@{APIHOST}`로 전달할 수도 있습니다. 

OpenWhisk API는 웹 클라이언트에서 요청-응답 호출을 지원합니다. OpenWhisk는 교차-원본 리소스 공유 헤더가 포함된 `OPTIONS` 요청에 응답합니다. 현재 모든 원본이 허용되며(즉, 액세스-제어-허용-원본이 "`*`"임) 액세스-제어-허용-헤더가 권한과 컨텐츠-유형을 산출합니다. 

**주의:** 현재 OpenWhisk는 네임스페이스당 하나의 키만 지원하므로, 단순한 시험 용도 외에 CORS를 사용하는 것은 권장되지 않습니다. [웹 조치](webactions.md) 또는 [API 게이트웨이](apigateway.md)를 사용하여 조치를 공용으로 노출하고, CORS가 필요한 클라이언트 애플리케이션에는 OpenWhisk 권한 키를 사용하지 마십시오. 

## CLI 상세 모드 사용
{: #openwhisk_rest_api_cli_v}
OpenWhisk CLI는 OpenWhisk REST API에 대한 인터페이스입니다.
`-v` 플래그를 사용하여 CLI를 상세 모드로 실행할 수 있으며, 이는 HTTP 요청과 응답에 대한 모든 정보를 인쇄합니다. 

현재 사용자에 대한 네임스페이스 값을 가져오도록 하겠습니다. 
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

보이는 바와 같이 인쇄된 정보는 HTTP 요청의 특성을 제공하며, 이는 기본 권한 헤더 `Basic XXXYYYY`를 사용하여 URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces`에서 HTTP 메소드 `GET`을 수행합니다.
참고로, 권한 값은 base64 인코딩된 OpenWhisk 권한 문자열입니다.
응답은 컨텐츠 유형 `application/json`입니다. 

## 조치
{: #openwhisk_rest_api_actions}
조치를 작성하거나 업데이트하려면 조치 콜렉션에서 `PUT` 메소드로 HTTP 요청을 전송하십시오. 예를 들어, 단일 파일 컨텐츠를 사용하여 `hello` 이름의 `nodejs:6` 조치를 작성하려면 다음을 사용하십시오. 
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

조치에 대한 블로킹 호출을 수행하고 입력 매개변수 `name`이 포함된 본문 및 `POST` 메소드로 HTTP 요청을 전송하려면 다음을 사용하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
다음 응답을 받습니다.
```json
{
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
      "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
단지 `response.result`를 가져오려면 조회 매개변수 `result=true`로 명령을 다시 실행하십시오.
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
다음 응답을 받습니다.
```json
{
  "payload": "hello John"
}
```

## 어노테이션 및 웹 조치
{: #openwhisk_rest_api_webactions}
웹 조치로서 조치를 작성하려면 웹 조치에 대해 `web-export=true`의 [어노테이션](annotations.md)을 추가해야 합니다. 웹-조치가 공용으로 액세스 가능하므로 `final=true` 어노테이션을 사용하여 사전 정의된 매개변수를 보호해야 합니다(즉, 이를 최종으로 처리함). CLI 플래그 `--web true`를 사용하여 조치를 작성하거나 업데이트하는 경우, 이 명령은 어노테이션 `web-export=true` 및 `final=true` 모두를 추가합니다. 

조치에 설정할 전체 어노테이션 목록을 제공하여 curl 명령을 실행하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
이제 OpenWhisk 권한 없이 공용 URL로 이 조치를 호출할 수 있습니다. 예를 들어, URL 끝에 `.json` 또는 `.http` 등의 선택적 확장이 포함된 웹 조치 공용 URL을 사용하여 호출을 시도해 보십시오.
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
}
```
참고로 이 예제 소스 코드는 `.http`에서는 작동하지 않습니다. 수정 방법은 [웹 조치](webactions.md) 문서를 참조하십시오.

## 시퀀스
{: #openwhisk_rest_api_sequences}
조치 시퀀스를 작성하려면 첫 번째 조치의 출력이 다음 조치에 대한 입력으로 전달될 수 있도록 원하는 순서로 시퀀스를 구성하는 조치의 이름을 제공하여 이를 작성해야 합니다. 

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

`/whisk.system/utils/split` 및 `/whisk.system/utils/sort` 조치로 시퀀스를 작성하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

조치의 이름을 지정할 때는 완전한 이름을 사용해야 합니다. 

## 트리거
{: #openwhisk_rest_api_triggers}
트리거를 작성하기 위해 필요한 최소 정보는 트리거의 이름입니다. 트리거가 실행될 때 규칙을 통해 조치에 전달되는 기본 매개변수를 포함할 수도 있습니다. 

이름이 `events`이고 기본 매개변수 `type`에 값 `webhook`이 설정된 트리거를 작성하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

이제 이 트리거를 실행해야 하는 이벤트가 있을 때마다 이는 OpenWhisk 권한 키를 사용하여 `POST` 메소드로 HTTP 요청을 취합니다. 

`temperature` 매개변수로 트리거 `events`를 실행하려면 다음 HTTP 요청을 전송하십시오. 

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### 피드 조치로 트리거
{: #openwhisk_rest_api_triggers_feed}
피드 조치를 사용하여 작성될 수 있는 특수 트리거가 있습니다. 피드 조치는 트리거에 대한 이벤트가 있을 때마다 트리거 실행을 담당하는 피드 제공자의 구성에 도움을 주는 조치입니다. [feeds.md] 문서에서 이러한 피드 제공자에 대하여 자세히 알아보십시오. 

피드 조치를 활용할 수 있는 트리거에는 periodic/alarms, Slack, Github, Cloudant/Couchdb, messageHub/Kafka 등이 있습니다. 자체 피드 조치 및 피드 제공자를 작성할 수도 있습니다. 

이름이 `periodic`이고 2시간마다 실행되도록 빈도를 지정한 트리거를 작성하도록 하겠습니다(예: 02:00:00, 04:00:00, ...).

CLI를 사용하면 하나의 명령으로 이를 수행할 수 있습니다. 
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
보이는 바와 같이 `-v` 플래그를 사용하므로 두 개의 HTTP 요청이 전송됩니다. 하나는 트리거 `periodic`을 작성하며, 다른 하나는 2시간마다 트리거를 실행하도록 피드 제공자를 구성하는 매개변수로 피드 조치 `/whisk.system/alarms/alarm`을 호출합니다.

REST API에서 동일한 작업을 수행하려면 우선 트리거를 작성합니다. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

보이는 바와 같이 `feed` 어노테이션은 트리거에 저장됩니다. 나중에 이 어노테이션을 사용하여 트리거를 삭제할 때 사용할 피드 조치를 알 수 있습니다. 

이제 트리거가 작성되었으므로 피드 조치를 호출하도록 하겠습니다. 
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

트리거 삭제는 트리거 작성과 유사합니다. 이번에는 트리거를 삭제하고 또한 피드 조치를 사용하여 트리거에 대한 핸들러를 삭제하도록 피드 제공자를 구성합니다. 

피드 조치를 호출하여 피드 제공자에서 트리거 핸들러를 삭제합니다. 
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

이제 `DELETE` 메소드를 사용하여 HTTP 요청으로 트리거를 삭제합니다. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## 규칙
{: #openwhisk_rest_api_rules}
트리거를 조치와 연관시키는 규칙을 작성하려면 요청 본문에 트리거와 조치를 제공하여 `PUT` 메소드로 HTTP 요청을 전송하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

규칙을 사용하거나 사용하지 않을 수 있으며, 상태 특성을 업데이트하여 규칙의 상태를 변경할 수 있습니다. 예를 들어, `t2a` 규칙을 사용하지 않으려면 `POST` 메소드로 요청 `status: "inactive"`의 본문을 전송하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## 패키지
{: #openwhisk_rest_api_packages}
패키지에서 조치를 작성하려면, 우선 패키지를 작성하여 이름이 `iot`인 패키지를 작성한 후에 `PUT` 메소드로 HTTP 요청을 전송해야 합니다. 

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## 활성화
{: #openwhisk_rest_api_activations}
마지막 3개 활성화의 목록을 가져오려면 조회 매개변수 `limit=3`을 전달하여 `GET` 메소드로 HTTP 요청을 사용하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

결과 및 로그를 포함한 활성화의 모든 세부사항을 가져오려면 활성화 ID를 경로 매개변수로 전달하여 `GET` 메소드로 HTTP 요청을 전송하십시오. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
