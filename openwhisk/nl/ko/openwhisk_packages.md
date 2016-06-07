---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 패키지 사용 및 작성
{: #openwhisk_packages}
*마지막 업데이트 날짜: 2016년 3월 28일*

{{site.data.keyword.openwhisk}}에서 패키지를 사용하여 일련의 연관된 조치를 번들화하고 이를 다른 사용자와 공유할 수 있습니다.

패키지는 *조치* 및 *피드*를 포함할 수 있습니다.
- 조치는 {{site.data.keyword.openwhisk_short}}에서 실행되는 코드 조각입니다. 예를 들어, Cloudant 패키지에는 Cloudant 데이터베이스에 대한 레코드를 읽고 쓰는 조치가 포함됩니다.
- 피드는 트리거 이벤트를 실행하기 위해 외부 이벤트 소스를 구성하는 데 사용됩니다. 예를 들어, Alarm 패키지에는 지정된 빈도로 트리거를 실행할 수 있는 피드가 포함됩니다.

패키지를 포함하여 모든 {{site.data.keyword.openwhisk_short}} 엔티티는 *네임스페이스*에 속하며 엔티티의 완전한 이름은 `/namespaceName[/packageName]/entityName`입니다. 자세한 정보는 [이름 지정 가이드라인](./openwhisk_reference.html#openwhisk_entities)을 참조하십시오.

다음 절에서는 패키지를 찾고 그 안에서 트리거 및 피드를 사용하는 방법에 대해 설명합니다. 또한 자신의 패키지를 카탈로그에 컨트리뷰션하는 데 관심이 있으면 패키지 작성 및 공유에 대한 절을 참조하십시오.

## 패키지 찾아보기
{: #openwhisk_packagedisplay}

여러 패키지가 {{site.data.keyword.openwhisk_short}}에 등록되어 있습니다. 네임스페이스 내의 패키지 목록을 가져오고 엔티티를 패키지에 나열하고 패키지 내의 개별 엔티티에 대한 설명을 가져올 수 있습니다.

1. `/whisk.system` 네임스페이스 내의 패키지 목록을 가져오십시오.

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
  ```
  {: screen}

2. `/whisk.system/cloudant` 패키지 내의 엔티티 목록을 가져오십시오.

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```
  {: screen}

  이 출력은 Cloudant 패키지가 두 개의 조치(`read` 및 `write`), 한 개의 트리거 피드(`changes`)를 제공하는 것을 보여줍니다. `changes` 피드는 지정된 Cloudant 데이터베이스에 문서가 추가될 때 트리거가 실행되도록 만듭니다.

  또한 Cloudant 패키지는 `username`, `password`, `host` 및 `port` 매개변수를 정의합니다. 이러한 매개변수는 조치 및 피드가 유의미하도록 지정되어야 합니다. 매개변수는 조치가 특정 Cloudant 계정에 대해 작동하도록 허용합니다. 예를 들어, 다음과 같습니다.

3. `/whisk.system/cloudant/read` 조치에 대한 설명을 가져오십시오.

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```
  {: screen}

  이 출력은 Cloudant `read` 조치에 검색할 데이터베이스 및 문서 ID를 포함하여 세 개의 매개변수가 필요함을 표시합니다.


## 패키지에서 조치 호출
{: #openwhisk_package_invoke}

기타 조치의 경우와 마찬가지로 패키지에서 조치를 호출할 수 있습니다. 다음 몇 가지 단계는 다른 매개변수를 사용하여 `/whisk.system/samples` 패키지에서 `greeting` 조치를 호출하는 방법을 보여줍니다.

1. `/whisk.system/samples/greeting` 조치에 대한 설명을 가져오십시오.

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```
  {: screen}

  `greeting` 조치에 두 개의 매개변수(`name` 및 `place`)가 사용되는 것에 주의하십시오.

2. 매개변수 없이 조치를 호출하십시오.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  매개변수가 지정되지 않았기 때문에 출력은 일반 메시지입니다.

3. 매개변수를 사용하여 조치를 호출하십시오.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  조치에 전달된 `name` 및 `place` 매개변수가 출력에 사용되고 있음에 주의하십시오.


## 패키지 바인딩 작성 및 사용
{: #openwhisk_package_bind}

패키지에서 직접 엔티티를 사용할 수도 있으나 동일한 매개변수를 매번 조치에 전달해야 합니다. 패키지에 바인딩하고 기본 매개변수를 지정하여 이를 방지할 수 있습니다. 이러한 매개변수는 패키지 내의 조치에 의해 상속됩니다.

예를 들어, `/whisk.system/cloudant` 패키지에서 기본 `username`, `password` 및 `dbname` 값을 패키지 바인딩에서 설정하면 해당 값이 자동으로 패키지 내의 모든 조치에 전달됩니다.

다음 단순 예제에서 `/whisk.system/samples` 패키지에 바인딩할 수 있습니다.

1. `/whisk.system/samples` 패키지에 바인딩하고 기본 `place` 매개변수값을 설정하십시오.

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```
  {: screen}

2. 패키지 바인딩의 설명을 가져오십시오.

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
  ```
  {: screen}

  `/whisk.system/samples` 패키지 내의 모든 조치를 `valhallaSamples` 패키지 바인딩에서 사용할 수 있습니다.

3. 패키지 바인딩에서 조치를 호출하십시오.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  결과를 보면, 사용자가 `valhallaSamples` 패키지 바인딩을
작성할 때 설정한 `place` 매개변수를 조치에서 상속했음을 알 수 있습니다.

4. 조치를 호출하고 기본 매개변수값을 겹쳐쓰십시오.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  조치 호출과 함께 지정된 `place` 매개변수값이 `valhallaSamples` 패키지 바인딩에서 설정된 기본값을 겹쳐쓰는 것을 알 수 있습니다.


## 트리거 피드 작성 및 사용
{: #openwhisk_package_trigger}

피드는 {{site.data.keyword.openwhisk_short}} 트리거에 대해 해당 이벤트를 실행하도록 외부 이벤트 소스를 구성하는 편리한 방법을 제공합니다. 이 예는 Alarm 패키지에서 피드를 사용하여 매초 트리거를 실행하고 규칙을 사용하여 매초 조치를 호출하는 방법을 보여줍니다.

1. `/whisk.system/alarms` 패키지에서 피드의 설명을 가져오십시오.

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```
  {: screen}

  `/whisk.system/alarms/alarm` 피드는 두 개의 매개변수를 사용합니다.
  - `cron`: 트리거를 실행할 시기의 crontab 스펙입니다.
  - `trigger_payload`: 각 트리거 이벤트에서 설정할 페이로드 매개변수값입니다.

2. 매 8초마다 실행되는 트리거를 작성하십시오.

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```
  {: screen}

3. 다음 조치 코드를 사용하여 'hello.js' 파일을 작성하십시오.

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. 조치가 있는지 확인하십시오.

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. `everyEightSeconds` 트리거가 실행될 때마다 `hello` 조치를 호출하는 규칙을 작성하십시오.

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ok: rule myRule is activating
  ```
  {: screen}

6. 활성화 로그에 대한 폴링에 의해 조치가 호출되는지 확인하십시오.

  ```
  wsk activation poll
  ```
  {: pre}

  트리거, 규칙 및 조치에 대해 매 8초마다 활성화가 표시되어야 합니다. 조치가 매 호출에 대해 `{"name":"Mork", "place":"Ork"}` 매개변수를 수신합니다.


## 패키지 작성
{: #openwhisk_packages_create}

패키지는 연관된 조치 및 피드 세트를 구성하는 데 사용됩니다.
또한 패키지 내의 모든 엔티티에 걸쳐 매개변수가 공유되도록 허용합니다.

내부에 단순 조치가 있는 사용자 정의 패키지를 작성하려면 다음 예를 시도해 보십시오.

1. "custom"이라는 패키지를 작성하십시오.

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```
  {: screen}

2. 패키지의 요약을 가져오십시오.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
  ```
  {: screen}

  패키지가 비어 있습니다.

3. 다음 조치 코드를 포함하는 `identity.js`라는 파일을 작성하십시오. 이 조치는 모든 입력 매개변수를 리턴합니다.

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. `custom` 패키지에서 `identity` 조치를 작성하십시오.

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```
  {: screen}

  패키지에서 조치를 작성하려면 패키지 이름을 조치의 접두부로 사용해야 합니다. 패키지 중첩은 허용되지 않습니다. 패키지는 조치만 포함할 수 있으며 다른 패키지는 포함할 수 없습니다.

5. 패키지의 요약을 다시 가져오십시오.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  이제 네임스페이스에서 `custom/identity` 조치를 볼 수 있습니다.

6. 패키지에서 조치를 호출하십시오.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


패키지 내의 모든 엔티티에 대해 기본 매개변수를 설정할 수 있습니다. 패키지 내의 모든 조치에 의해 상속된 패키지 레벨 매개변수를 설정하여 이를 수행할 수 있습니다. 작동 방법을 보려면 다음 예를 시도해 보십시오.

1. 두 매개변수(`city` 및 `country`)를 사용하여 `custom` 패키지를 업데이트하십시오.

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. 패키지 및 조치에 매개변수를 표시하고 패키지 내의 `identity` 조치가 패키지에서 매개변수를 상속하는 방법을 보십시오.

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. 조치가 실제로 매개변수를 상속하는지 확인하려면 매개변수 없이 identity 조치를 호출하십시오.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. 일부 매개변수를 사용하여 identity 조치를 호출하십시오. 호출 매개변수가 패키지 매개변수와 병합되어 호출 매개변수가 패키지 매개변수를 대체합니다.

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## 패키지 공유
{: #openwhisk_packages_share}

패키지를 구성하는 조치 및 피드가 디버그되고 테스트된 후에 패키지가 모든 {{site.data.keyword.openwhisk_short}} 사용자와 공유될 수 있습니다. 패키지를 공유하면 사용자가 패키지를 바인딩하고 패키지에서 조치를 호출하고 {{site.data.keyword.openwhisk_short}} 규칙 및 시퀀스 조치를 작성할 수 있습니다.

1. 모든 사용자와 패키지를 공유하십시오.

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. 패키지의 `publish` 특성을 표시하여 true인지 확인하십시오.

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, projecting publish
  true
  ```
  {: screen}


이제 기타 사용자가 패키지에 대해 바인딩하거나 패키지에서 조치를 직접 호출하는 것을 포함하여 사용자의 `custom` 패키지를 사용할 수 있습니다. 기타 사용자가 패키지를 바인딩하거나 패키지에서 조치를 호출하려면 패키지의 완전한 이름을 알아야 합니다. 공유 패키지 내의 조치 및 피드는 *public*입니다. 패키지가 개인용이면 모든 컨텐츠 또한 개인용입니다.

1. 패키지 및 조치의 완전한 이름을 표시하려면 패키지의 설명을 가져오십시오.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  앞의 예에서 `myNamespace` 네임스페이스를 사용하여 작업하며 이 네임스페이스가 완전한 이름에 표시됩니다.

