---

copyright:
  years: 2016
lastupdated: "2016-02-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 트리거 및 규칙 작성
{: #openwhisk_triggers}


{{site.data.keyword.openwhisk}} 트리거 및 규칙은 플랫폼에 이벤트 주도적인 기능을 제공합니다. 외부 및 내부 이벤트 소스의 이벤트는 트리거를 채널로 사용하며 규칙은 조치가 이러한 이벤트에 대해 반응하도록 허용합니다.
{: shortdesc}

## 트리거 작성
{: #openwhisk_triggers_create}

트리거는 이벤트 클래스에 대해 이름 지정된 채널입니다. 다음은 트리거의 예입니다.
- 위치 업데이트 이벤트의 트리거
- 웹 사이트에 대한 문서 업로드 트리거
- 수신 이메일 트리거

트리거는 키-값 쌍 사전을 사용하여 *실행*(활성화)될 수 있습니다. 이 사전을 *이벤트*라고 부르기도 합니다. 조치와 같이 각 트리거 실행으로 인해 활성화 ID가 발생합니다.

트리거는 사용자에 의해 명시적으로 실행되거나 외부 이벤트 소스에 의해 사용자 대신 실행될 수 있습니다.
*피드*는 {{site.data.keyword.openwhisk_short}}에 의해 이용될 수 있는 트리거 이벤트를 실행하기 위해 외부 이벤트 소스를 구성하는 편리한 방법입니다. 피드의 예는 다음과 같습니다.
- 데이터베이스 내의 문서가 추가되거나 수정될 때마다 트리거 이벤트를 실행하는 Cloudant 데이터 변경 피드
- Git 저장소에 대한 커미트마다 트리거 이벤트를 실행하는 Git 피드

## 규칙 사용
{: #openwhisk_rules_use}

규칙은 하나의 트리거를 하나의 조치와 연관시키며 트리거를 실행할 때마다 입력으로 트리거 이벤트를 사용하여 해당 조치가 호출됩니다.

적절한 규칙 세트를 사용하여 단일 트리거 이벤트가
다중 조치를 호출하거나 조치가 다중 트리거의
이벤트에 대한 응답으로 호출될 수 있습니다.

예를 들어, 다음 조치가 있는 시스템을 고려해 보십시오.
- 이미지에서 오브젝트를 발견하여 분류하는 `classifyImage` 조치
- 이미지의 작은 그림 버전을 작성하는 `thumbnailImage` 조치

또한 다음 트리거를 실행하는 두 개의 이벤트 소스가 있다고 가정해 보십시오. 
- 새 트윗이 게시될 때 실행되는 `newTweet` 트리거
- 이미지가 웹 사이트에 업로드될 때 실행되는 `imageUpload` 트리거

단일 트리거 이벤트가 다중 조치를 호출하고 다중 트리거가 동일한 조치를 호출하도록 규칙을 설정할 수 있습니다.
- `newTweet -> classifyImage` 규칙
- `imageUpload -> classifyImage` 규칙
- `imageUpload -> thumbnailImage` 규칙

세 규칙은 다음 동작을 설정합니다. 트윗 및 업로드된 이미지 둘 다의 이미지가 분류되고 업로드된 이미지가 분류되고 작은 그림 버전이 작성됩니다.

## 트리거 작성 및 실행
{: #openwhisk_triggers_fire}

특정 이벤트가 발생할 때 트리거가 실행되거나 수동으로 트리거가 실행될 수 있습니다.

예를 들어, 사용자 위치 업데이트를 전송하도록 트리거를 작성하고 수동으로 트리거를 실행할 수 있습니다.

1. 다음 명령을 입력하여 트리거를 작성하십시오.

  ```
  wsk trigger create locationUpdate
  ```
  {: pre}

  ```
  ok: created trigger locationUpdate
  ```
  {: screen}

2. 트리거 세트를 나열하여 작성된 트리거를 확인하십시오.

  ```
  wsk trigger list
  ```
  {: pre}

  ```
  triggers
  /someNamespace/locationUpdate                            private
  ```
  {: screen}

  지금까지 이벤트가 실행될 수 있는 이름 지정된 "채널"을 작성했습니다.

3. 다음으로 트리거 이름 및 매개변수를 지정하여 트리거 이벤트를 실행하십시오.

  ```
  wsk trigger fire locationUpdate --param name Donald --param place "Washington, D.C."
  ```
  {: pre}

  ```
  ok: triggered locationUpdate with id fa495d1223a2408b999c3e0ca73b2677
  ```
  {: screen}

대조할 수반되는 규칙 없이 실행되는 트리거는 영향을 미치지 않습니다.
트리거를 패키지 내부에 작성할 수 없으며 네임스페이스에 직접 작성해야 합니다. 

## 규칙을 사용하여 트리거와 조치 연관
{: #openwhisk_rules_assoc}

규칙은 트리거를 조치와 연관시키는 데 사용됩니다. 트리거 이벤트가 실행될 때마다 이벤트 매개변수를 사용하여 조치가 호출됩니다.

예를 들어, 위치 업데이트가 게시될 때마다 hello 조치를 호출하는 규칙을 작성하십시오.

1. 사용할 조치 코드를 사용하여 'hello.js' 파일을 작성하십시오. 
  ```
  function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. 트리거 및 조치가 있는지 확인하십시오. 
  ```
  wsk trigger update locationUpdate
  ```
  {: pre}

  ```
  wsk action update hello hello.js
  ```
  {: pre}

3. 규칙을 작성하십시오. 규칙은 작성 즉시 사용 가능합니다. 즉, 트리거의 활성화에 곧바로 응답할 수 있습니다. 세 가지 매개변수는 규칙, 트리거 및 조치의 이름입니다. 
  ```
  wsk rule create myRule locationUpdate hello
  ```
  {: pre}

  언제든지 규칙이 사용되지 않도록 선택할 수 있습니다. 
  ```
  wsk rule disable myRule
  ```
  {: pre}

4. locationUpdate 트리거를 실행하십시오. 이벤트를 실행할 때마다 이벤트 매개변수와 함께 hello 조치가 호출됩니다. 
  ```
  wsk trigger fire locationUpdate --param name Donald --param place "Washington, D.C."
  ```
  {: pre}

  ```
  ok: triggered locationUpdate with id d5583d8e2d754b518a9fe6914e6ffb1e
  ```
  {: screen}

5. 최신 활성화를 검사하여 조치가 호출되었는지 확인하십시오. 
  ```
  wsk activation list --limit 1 hello
  ```
  {: pre}

  ```
  activations
  9c98a083b924426d8b26b5f41c5ebc0d             hello
  ```
  {: screen}

  ```
  wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
  ```
  {: pre}
  ```
  {
     "payload": "Hello, Donald from Washington, D.C."
  }
  ```
  {: screen}

  hello 조치가 이벤트 페이로드를 수신하고 예상 문자열을 리턴한 것을 볼 수 있습니다.

동일한 트리거를 다른 조치와 연관시키는 다중 규칙을 작성할 수 있습니다.
트리거 및 규칙은 패키지에 속할 수 없습니다. 그러나 규칙은 패키지에 속한 조치와
연결시킬 수 있습니다. 예: 
  ```
  wsk rule create recordLocation locationUpdate /whisk.system/utils/echo
  ```
  {: pre}

시퀀스와 함께 규칙을 사용할 수도 있습니다. 예를 들어, `anotherRule` 조치에서 활성화된 조치
시퀀스 `recordLocationAndHello`를 작성할 수 있습니다.
  ```
  wsk action create recordLocationAndHello --sequence /whisk.system/utils/echo,hello
  wsk rule create anotherRule locationUpdate recordLocationAndHello
  ```
  {: pre}
 
