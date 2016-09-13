---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 조치 예제

이메일 발송, IFTTT, Node-RED, 웹훅 조치 유형은 태스크 실행을 위한 매우 다양한 옵션을 제공하며 사용자의 상상력과 다른 도구에서 사용하는 커넥터에 대해서만 제한을 받습니다. 예를 들어 Slack에 디바이스 상태 메시지를 게시하고 서비스 담당자에게 문자 메시지를 보내며 디바이스 서비스 요청을 작성하는 등의 조치가 있습니다.
{: shortdesc}

아래 예제는 규칙 조건 `temp >= 100`을 사용하여 디바이스의 온도 데이터 포인트로 표시되는 온도가 100도를 초과할 때 서비스 엔지니어에게 알리는 조치를 나타냅니다.


규칙 조건이 발생할 때 다음 조치 유형 중 하나 이상을 트리거할 수 있습니다.  
 - [이메일 발송](#emailex "이메일 발송")
 - [웹훅](#webhookex "웹훅")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## 이메일 발송 사용{: #emailex}
이 예제에서는 Real-Time Insights 이메일 발송 기능을 사용하여 기본 서비스 엔지니어에게 이메일을 발송하고, 또한 엔지니어의 관리자에게 백업 이메일을 발송하도록 조치를 구성합니다.

이메일 조치를 작성하려면 다음을 수행하십시오.
1. Real-Time Insights에서 **분석 > 조치**로 이동하십시오.
2. **새 조치 추가**를 클릭하십시오.
3. **이메일 발송** 유형을 선택하십시오.
4. 조치 이름 `서비스 요청 이메일 발송`을 입력하십시오.
5. 설명 `서비스 엔지니어와 관리자에게 이메일 발송`을 입력하십시오.
6. 수신인 필드에 `service.engineer@company.com`을 입력하십시오.
7. 참조 필드에 `service.manager@company.com`을 입력하십시오.
8. 제목 행에 `서비스가 요청되었습니다.`를 입력하십시오.
9. "{{site.data.keyword.iotrtinsights_short}} 경보"라는 접두어를 붙이도록 선택하여 이메일의 출처를 명확히 표시하십시오.
10. 이메일에 디바이스 정보를 포함하려면 **이메일 메시지에 디바이스 데이터 포함하지 않음** 선택란을 지우십시오.
11. **확인**을 클릭하여 조치를 저장하십시오.   




## 웹훅을 사용하여 Slack에 게시{: #webhookex}

이 예제에서는 웹훅을 사용하여 #service-requests Slack 채널에 메시지를 게시하도록 조치를 구성합니다.

Slack에 게시 조치를 작성하려면 다음을 수행하십시오.
1. Slack에서 채널 #service-requests에 대한 수신 웹훅 통합을 설정하십시오. 웹훅 URL을 기록하십시오. 자세한 정보는 [Slack 문서](https://api.slack.com/incoming-webhooks)를 참조하십시오.
2. Real-Time Insights에서 **분석 > 조치**로 이동한 후 다음 매개변수를 갖는 새 조치를 작성하십시오.
 - 유형 - **웹훅**
 - 이름 - `Slack에 서비스 요청 게시`
 - URL - `사용자의 Slack 웹훅 URL`
 - 메소드 - **POST**
 - 컨텐츠 유형 - application/json
 - **사용자 정의된 메시지 본문 사용** 선택
 - 본문
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```
 {: codeblock}  
 **중요:** Slack 웹훅은 최소한 "text" 필드를 포함해야 합니다. 자세한 정보는 Slack 문서의 [Incoming Webhooks](https://api.slack.com/incoming-webhooks "Slack 문서")를 참조하십시오. 
11. **확인**을 클릭하여 조치를 저장하십시오.

## Node-RED를 사용하여 문자 메시지 발송{: #noderedex}

이 예제에서는 Twilio 노드와 함께 Node-RED를 사용하여 서비스 엔지니어에게 문자 메시지를 발송하도록 조치를 구성합니다.

문자 메시지 발송 조치를 작성하려면 다음을 수행하십시오.
1. Twilio에서, Twilio 계정으로부터 문자 메시지를 발송하기 위해 사용할 새 메시지 전달 서비스를 작성하거나 찾으십시오. 자세한 정보는 [Twilio 문서](https://www.twilio.com/help)를 참조하십시오.
1. Bluemix에서, Node-RED URL `http://mynodered.mybluemix.net/red/`를 사용하여 Node-RED 계정을 설정하고 액세스하십시오. 자세한 정보는 Bluemix 문서에서 [Node-RED 스타터로 앱 작성](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) 주제를 참조하십시오.
2. Node-RED에서, [RTI-alert]->[SMS]와 같은 단순한 두 개의 노드 플로우를 작성하십시오.
여기서 첫 번째 노드는 http 노드이고, 두 번째 노드는 twilio 노드입니다.
 1. "http" 입력 노드를 추가하고 다음 속성으로 구성하십시오.
  <ul>
  <li>Method - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Name - RTI 조치</li>
  </ul>
  2. "http response" 출력 노드를 추가하고, 하나의 출력 포트와 다른 하나의 입력 포트 사이를 끌어서 "http response" 출력 노드와 "http" 입력 노드를 함께 연결하십시오.
  3. "twilio" 출력 노드를 추가하고 다음 속성으로 구성하십시오.
  <ul>
  <li>Service - **외부 서비스**</li>
  <li>Twilio - 새 twilio-api 추가</li>
  <li>SMS to - `서비스 엔지니어의 전화번호`</li>
  <li>Name - **SMS**</li>
  </ul>
  4. 노드를 서로 연결
  하나의 출력 포트와 다른 하나의 입력 포트 사이를 끌어서 http와 twilio 노드를 함께 연결하십시오.
  5. **Deploy** 단추를 클릭하여 서버에 플로우를 배치하십시오.
3. {{site.data.keyword.iotrtinsights_short}}에서, **분석 > 조치**로 이동하여 다음 매개변수를 갖는 조치를 작성하십시오.
 - 유형 - **Node-RED**
 - 이름 - `Node-RED 및 Twilio를 사용하여 텍스트 발송`
 - 설명 - `서비스 엔지니어에게 문자 메시지 경보를 발송합니다. `
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - 본문
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```
 {: codeblock}
4. **확인**을 클릭하여 조치를 저장하십시오.

## IFTTT를 사용하여 Trello 카드 게시 {: #iftttex}

이 예제에서는 IFTTT를 사용하여 Trello의 서비스 요청 목록에 카드를 게시하도록 조치를 구성합니다.

Trello에 카드 게시 조치를 작성하려면 다음을 수행하십시오.
1.	IFTTT에서, Trello 채널에 연결하십시오.
2.	IFTTT에서, Maker 채널에 연결하십시오. IFTTT 키를 기록하십시오. 이는 Real-Time Insights에서 IFTTT에 연결할 때 필요합니다.
5.	IFTTT에서, 레시피를 작성하십시오.
 1. **THIS**를 클릭하십시오.
 2. **Maker** 채널을 선택하십시오.  
 2. **Receive a web request**를 클릭하십시오.
 3. 이벤트 이름 `post-Trello-card`를 입력하십시오.
 4. **THAT**을 클릭하십시오.
 5. **Trello** 채널을 선택하십시오.
 6. 카드를 작성할 Trello 보드를 선택하십시오.
 7. 카드를 추가할 목록 이름을 입력하십시오.
 8. 제목과 설명을 편집하십시오.
 9. @service.engineer 및 @service.manager 구성원을 지정하십시오.
 8. **Create Action**을 클릭하십시오.   
3. {{site.data.keyword.iotrtinsights_short}}에서, **분석 > 조치**로 이동하여 다음 매개변수를 갖는 조치를 작성하십시오.
<ul>
<li>유형 - **IFTTT**</li>
<li>이름 - `서비스 요청 카드 게시`</li>
<li>설명 - `IFTTT를 사용하여 Trello의 서비스 요청 목록에 카드를 게시합니다. `</li>
<li>키 - 사용자의 IFTTT 키</li>
<li>이벤트 - `post-Trello-card`</li>
<li>선택적으로 값 1에서 3까지의 값을 추가하십시오. **팁:**  [변수 대체](actions.html#variable_substitution)를 사용하여 디바이스 데이터를 동적으로 포함할 수 있습니다.</li>
</ul>
4. **확인**을 클릭하여 조치를 저장하십시오.
