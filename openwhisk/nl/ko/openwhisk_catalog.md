---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 사용 가능 서비스 사용 
{: #openwhisk_ecosystem}
*마지막 업데이트 날짜: 2016년 3월 28일*

{{site.data.keyword.openwhisk}}에서 패키지 카탈로그는 유용한 기능으로 앱을 강화하고 에코시스템 내에서 외부 서비스에 액세스할 수 있는 쉬운 방법을 제공합니다. {{site.data.keyword.openwhisk_short}} 사용 가능 외부 서비스의 예로는 Cloudant, The Weather Company, Slack 및 GitHub 등이 있습니다.
{: shortdesc}

카탈로그는 `/whisk.system` 네임스페이스에서 패키지로 사용 가능합니다. 명령행 도구를 사용하여 카탈로그를 찾는 방법에 대한 정보는 [패키지 찾아보기](./openwhisk_packages.html#openwhisk_packagedisplay)를 참조하십시오.

다음 주제에서는 카탈로그 내의 일부 패키지를 문서화하는 방법에 대해 설명합니다.

## Cloudant 패키지 사용
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 패키지를 사용하면 Cloudant 데이터베이스를 사용하여 작업할 수 있습니다. 다음 조치 및 피드를 포함합니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 패키지 | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, includeDoc, overwrite | Cloudant 데이터베이스와 함께 작동 |
| `/whisk.system/cloudant/read` | 조치 | dbname, includeDoc, id | 데이터베이스에서 문서 읽기 |
| `/whisk.system/cloudant/write` | 조치 | dbname, overwrite, doc | 데이터베이스에 문서 쓰기 |
| `/whisk.system/cloudant/changes` | 피드 | dbname, includeDoc | 데이터베이스에 대한 변경 시 트리거 이벤트 실행 |

다음 주제에서는 `/whisk.system/cloudant` 패키지 내에서의 Cloudant 데이터베이스 설정, 연관된 패키지 구성 및 조치 및 피드 사용에 대해 설명합니다.

### {{site.data.keyword.Bluemix_notm}} 내에서 Cloudant 데이터베이스 설정

{{site.data.keyword.Bluemix}}에서 {{site.data.keyword.openwhisk_short}}를 사용하는 경우, {{site.data.keyword.openwhisk_short}}가 {{site.data.keyword.Bluemix_notm}} Cloudant 서비스 인스턴스에 대한 패키지 바인딩을 자동으로 작성합니다. {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.openwhisk_short}} 및 Cloudant를 사용하고 있지 않은 경우 다음 단계로 건너뛰십시오.

1. {{site.data.keyword.Bluemix_notm}} [대시보드](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net)에서 Cloudant 서비스 인스턴스를 작성하십시오.

  서비스 인스턴스의 이름, {{site.data.keyword.Bluemix_notm}} 조직 및 사용자가 속한 영역을 기억하십시오.

2. {{site.data.keyword.openwhisk_short}} CLI가 사용자가 이전 단계에서 사용한 {{site.data.keyword.Bluemix_notm}} 조직 및 영역에 해당되는 네임스페이스에 있는지 확인하십시오.

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  또는 `wsk property set --namespace`를 사용하여 액세스 가능한 목록에서 네임스페이스를 설정할 수 있습니다.

3. 네임스페이스 내의 패키지를 새로 고치십시오. 일반적으로 새로 고치기는 사용자가 작성한 Cloudant 서비스 인스턴스에 대한 패키지 바인딩을 작성합니다.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  사용자의 {{site.data.keyword.Bluemix_notm}} Cloudant 서비스 인스턴스에 해당되는 패키지 바인딩의 완전한 이름이 표시되어야 합니다.

4. 이전에 작성된 패키지 바인딩이 Cloudant {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 호스트 및 신임 정보를 사용하여 구성되었는지 확인하십시오.

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### {{site.data.keyword.Bluemix_notm}} 외부에서 Cloudant 데이터베이스 설정

{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.openwhisk_short}}를 사용하지 않거나 {{site.data.keyword.Bluemix_notm}}의 외부에서 Cloudant 데이터베이스를 설정하려면 Cloudant 계정에 대한 패키지 바인딩을 수동으로 작성해야 합니다. Cloudant 계정 호스트 이름, 사용자 이름 및 비밀번호가 필요합니다.

1. Cloudant 계정에 대해 구성된 패키지 바인딩을 작성하십시오.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
  ```
  {: pre}

2. 패키지 바인딩이 있는지 확인하십시오.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### Cloudant 데이터베이스에 대한 변경 청취

`changes` 피드를 사용하여 Cloudant 데이터베이스에 대한 모든 변경 시 트리거를 실행하도록 서비스를 구성할 수 있습니다.

1. 앞에서 작성한 패키지 바인딩의 `changes`를 사용하여 트리거를 작성하십시오. `/myNamespace/myCloudant`를 사용자의 패키지 이름으로 대체하십시오.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. 활성화를 위해 폴링하십시오.

  ```
  wsk activation poll
  ```
  {: pre}

3. Cloudant 대시보드에서 기존 문서를 수정하거나 새 문서를 작성하십시오.

4. 각 문서 변경에 대한 `myCloudantTrigger` 트리거의 새 활성화를 관찰하십시오.

**참고**: 새 활성화를 관찰할 수 없으면 Cloudant 데이터베이스에 대한 읽기 및 쓰기에 관한 후속 절을 참조하십시오. 아래의 읽기 및 쓰기 테스트 단계는 Cloudant 신임 정보가 올바른지 확인하는 데 도움을 줍니다.

이제 규칙을 작성하고 규칙을 조치에 연관시켜 문서 업데이트에 반응할 수 있습니다.

생성된 이벤트의 컨텐츠는 트리거를 생성할 때의 `includeDocs` 매개변수값에 따라 다릅니다. true로 설정하면 실행되는 각 트리거 이벤트에 수정된 Cloudant 문서가 포함됩니다. 예를 들어, 다음과 같이 수정된 문서를 고려해 보십시오.

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

이 예의 코드는 해당되는 `_id`, `_rev` 및 `name` 매개변수가 있는 트리거 이벤트를 생성합니다. 실제로 트리거 이벤트의 JSON 표시는 문서와 동일합니다.

그렇지 않은 경우, `includeDocs`가 false이면 이벤트에 다음 매개변수가 포함됩니다.

- `id`: 문서 ID입니다.
- `seq`: Cloudant에 의해 생성된 시퀀스 ID입니다.
- `changes`: 오브젝트의 배열이며 각각 문서의 개정 ID를 포함하는 `rev` 필드를 가집니다.

트리거 이벤트의 JSON 표시는 다음과 같습니다.

  ```
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```


### Cloudant 데이터베이스에 쓰기

조치를 사용하여 `testdb`라는 Cloudant 데이터베이스에 문서를 저장할 수 있습니다. 이 데이터베이스가 Cloudant 계정에 존재하는지 확인하십시오.

1. 앞에서 작성한 패키지 바인딩 내의 `write` 조치를 사용하여 문서를 저장하십시오. `/myNamespace/myCloudant`를 사용자의 패키지 이름으로 대체하십시오.

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. 문서를 Cloudant 대시보드에서 찾아서 문서가 존재하는지 확인하십시오.

  `testdb`에 대한 대시보드 URL은 다음과 유사합니다. `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


### Cloudant 데이터베이스에서 읽기

조치를 사용하여 `testdb`라는 Cloudant 데이터베이스에서 문서를 페치할 수 있습니다. 이 데이터베이스가 Cloudant 계정에 존재하는지 확인하십시오.

1. 앞에서 작성한 패키지 바인딩 내의 `read` 조치를 사용하여 문서를 페치하십시오. `/myNamespace/myCloudant`를 사용자의 패키지 이름으로 대체하십시오.

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}


## Alarm 패키지 사용
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 패키지는 지정된 빈도로 트리거를 실행하기 위해 사용할 수 있습니다. 이는 시스템 백업 조치를 매시간마다 호출하는 것과 같이 반복 작업 또는 태스크를 설정하는 데 유용합니다.

패키지에는 다음 피드가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 패키지 | - | 알람 및 주기적 유틸리티 |
| `/whisk.system/alarms/alarm` | 피드 | cron, trigger_payload, maxTriggers | 정기적으로 트리거 이벤트 실행 |


### 정기적으로 트리거 이벤트 실행

`/whisk.system/alarms/alarm` 피드는 지정된 빈도로 트리거 이벤트를 실행하기 위해 알람 서비스를 구성합니다. 매개변수는 다음과 같습니다.

- `cron`: 협정 세계시(UTC)로 트리거를 실행할 시점을 표시하는 Unix crontab 구문 기반의 문자열입니다. 문자열은 공백으로 구분되는 여섯 개 필드의 시퀀스입니다. `X X X X X X `. cron 구문 사용에 대한 세부사항은 https://github.com/ncb000gt/node-cron을 참조하십시오. 

- `trigger_payload`: 이 매개변수의 값은 트리거가 실행될 때마다 트리거의 컨텐츠가 됩니다.

- `maxTriggers`: 이 한계에 도달하면 트리거 실행이 중지됩니다. 기본값은 1000입니다.

다음은 트리거 이벤트에서 `name` 및 `place` 값을 사용하여 매 20초마다 한 번 실행될 트리거를 작성하는 예입니다.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

생성된 각 이벤트는 `trigger_payload` 값에서 지정된 값을 매개변수로 포함합니다. 이 경우, 각 트리거 이벤트는 `name=Odin` 및 `place=Asgard` 매개변수를 갖게 됩니다.


## Weather 패키지 사용
{: #openwhisk_catalog_weather}

`/whisk.system/weather` 패키지는 The Weather Company API를 호출하는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 패키지 | apiKey | The Weather Company의 서비스 |
| `/whisk.system/weather/forecast` | 조치 | apiKey, latitude, longitude | Weather.com 10일 예보 |

필수는 아니지만 `apiKey` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 이 방법의 경우, 패키지에서 조치를 호출할 때마다 키를 지정할 필요가 없습니다.

### 위치에 대한 날씨 예보 가져오기

`/whisk.system/weather/forecast` 조치는 The Weather Company에서 API를 호출하여 위치에 대한 10일 날씨 예보를 리턴합니다. 매개변수는 다음과 같습니다.

- `apiKey`: 10일 예보 API를 호출할 자격이 있는 The Weather Company에 대한 API 키입니다.
- `latitude`: 위치의 위도 좌표입니다.
- `longitude`: 위치의 경도 좌표입니다.

다음은 패키지 바인딩을 작성한 다음 10일 예보를 가져오는 예입니다.

1. 사용자의 API 키를 사용하여 패키지 바인딩을 작성하십시오.

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. 패키지 바인딩에서 `forecast` 조치를 호출하여 날씨 예보를 가져오십시오.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## Watson 패키지 사용
{: #openwhisk_catalog_watson}

`/whisk.system/watson` 패키지는 다양한 Watson API를 호출하는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/watson` | 패키지 | username, password | Watson 분석 API에 대한 조치 |
| `/whisk.system/watson/translate` | 조치 | translateFrom, translateTo, translateParam, username, password | 텍스트 변환 |
| `/whisk.system/watson/languageId` | 조치 | payload, username, password | 언어 식별 |

필수는 아니지만 `username` 및 `password` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 이 방법의 경우, 패키지에서 조치를 호출할 때마다 신임 정보를 지정할 필요가 없습니다.

### 텍스트 변환

`/whisk.system/watson/translate` 조치는 텍스트를 한 언어에서 다른 언어로 변환합니다. 매개변수는 다음과 같습니다.

- `username`: Watson API 사용자 이름입니다.
- `password`: Watson API 비밀번호입니다.
- `translateParam`: 변환할 입력 매개변수입니다. 예를 들어, `translateParam=payload`이면 조치에 전달된 `payload` 매개변수의 값이 변환됩니다.
- `translateFrom`: 소스 언어의 두 자리 코드입니다.
- `translateTo`: 대상 언어의 두 자리 코드입니다.

다음은 패키지 바인딩을 작성하고 일부 텍스트를 변환하는 예입니다.

1. Watson 신임 정보를 사용하여 패키지 바인딩을 작성하십시오.

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. 패키지 바인딩에서 `translate` 조치를 호출하여 일부 텍스트를 영어에서 프랑스어로 변환하십시오.

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### 일부 텍스트의 언어 식별

`/whisk.system/watson/languageId` 조치는 일부 텍스트의 언어를 식별합니다. 매개변수는 다음과 같습니다.

- `username`: Watson API 사용자 이름입니다.
- `password`: Watson API 비밀번호입니다.
- `payload`: 식별할 텍스트입니다.

다음은 패키지 바인딩을 작성하고 일부 텍스트의 언어를 식별하는 예입니다.

1. Watson 신임 정보를 사용하여 패키지 바인딩을 작성하십시오.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. 패키지 바인딩에서 `languageId` 조치를 호출하여 언어를 식별하십시오.

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu a venir'
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


## Slack 패키지 사용
{: #openwhisk_catalog_slack}

`/whisk.system/slack` 패키지는 [Slack API](https://api.slack.com/)를 사용하는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 패키지 | url, channel, username | Slack API와 상호작용 |
| `/whisk.system/slack/post` | 조치 | text, url, channel, username | Slack 채널에 메시지 게시 |

필수는 아니지만 `username`, `url` 및 'channel' 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 바인딩을 사용하면, 패키지에서 조치를 호출할 때마다 값을 지정할 필요가 없습니다.

### Slack 채널에 메시지 게시

`/whisk.system/slack/post` 조치는 메시지를 지정된 Slack 채널에 게시합니다. 매개변수는 다음과 같습니다.

- `url`: Slack 웹후크 URL입니다.
- `channel`: 메시지를 게시할 Slack 채널입니다.
- `username`: 메시지를 게시할 사용자 이름입니다.
- `text`: 게시할 메시지입니다.

다음은 Slack을 구성하고 패키지 바인딩을 작성하여 메시지를 채널에 게시하는 예입니다.

1. 팀을 위해 Slack [수신 웹후크](https://api.slack.com/incoming-webhooks)를 구성하십시오.

  Slack이 구성된 후에 `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`와 같은 웹후크 URL을 가져와야 합니다. 다음 단계에서 이 URL이 필요합니다.

2. Slack 신임 정보, 게시할 채널 및 게시할 때 사용할 사용자 이름을 사용하여 패키지 바인딩을 작성하십시오.

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. 패키지 바인딩에서 `post` 조치를 호출하여 사용자의 Slack 채널에 메시지를 게시하십시오.

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hello from OpenWhisk!'
  ```
  {: pre}


## GitHub 패키지 사용
{: #openwhisk_catalog_github}

`/whisk.system/github` 패키지는 [GitHub API](https://developer.github.com/)를 사용하는 편리한 방법을 제공합니다.

패키지에는 다음 피드가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 패키지 | username, repository, accessToken | GitHub API와 상호작용 |
| `/whisk.system/github/webhook` | 피드 | events, username, repository, accessToken | GitHub 활동 시 트리거 이벤트 실행 |

필수는 아니지만 `username`, `repository` 및 `accessToken` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 바인딩을 사용하면, 패키지에서 피드를 사용할 때마다 값을 지정할 필요가 없습니다.

### GitHub 활동과 함께 트리거 이벤트 실행

`/whisk.system/github/webhook` 피드는 지정된 GitHub 저장소에 활동이 있을 때 트리거를 실행하는 서비스를 구성합니다. 매개변수는 다음과 같습니다.

- `username`: GitHub 저장소의 사용자 이름입니다.
- `repository`: GitHub 저장소입니다.
- `accessToken`: GitHub 개인 액세스 토큰입니다. [토큰을 작성](https://github.com/settings/tokens)할 때, repo:status 및 public_repo 범위를 선택하십시오. 또한 저장소에 미리 정의된 웹후크가 없는지 확인하십시오.
- `events`: 관심 있는 [GitHub 활동 유형](https://developer.github.com/v3/activity/events/types/)입니다.

다음은 GitHub 저장소에 대한 새 커미트가 있을 때마다 실행될 트리거를 작성하는 예입니다.

1. GitHub [개인 액세스 토큰](https://github.com/settings/tokens)을 생성하십시오.

  액세스 토큰은 다음 단계에서 사용됩니다.


2. 액세스 토큰을 사용하여 GitHub 저장소에 대해 구성된 패키지 바인딩을 작성하십시오.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. `myGit/webhook` 피드를 사용하여 GitHub `push` 이벤트 유형에 대한 트리거를 작성하십시오.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

