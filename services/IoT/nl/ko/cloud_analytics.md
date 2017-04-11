---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 클라우드 분석
{: #cloud_analytics}

{{site.data.keyword.iot_short}} 클라우드 분석을 사용하면 실시간 디바이스 데이터를 기반으로 하며 충족 시에 경보 및 선택적 조치를 트리거하는 규칙 조건을 지정합니다.     
{: shortdesc}

예를 들어, 디바이스를 떨어뜨리거나 디바이스의 온도가 급등할 때 경보가 사용자 디바이스의 대시보드로 전송되며 이메일이 관리자에게 발송되는지를 확인하는 규칙을 작성할 수 있습니다. 

## 시작하기 전에
{: #byb}
규칙에서 조건으로 사용할 디바이스 특성이 스키마에 맵핑되었는지 확인하십시오. 자세한 정보는 [디바이스 연결](iotplatform_task.html) 및 [스키마 작성](im_schemas.html)을 참조하십시오. 

또한 [{{site.data.keyword.iot_short}} Cloud Analytics와 함께 규칙 및 조치 사용 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} 레시피를 검토하여 Cloud Analytics에서 사용되는 규칙과 조치를 파악하십시오. 

## 규칙 및 조치 관리  
{: #managing_rules}

**규칙** 대시보드를 사용하여 조직에 대한 규칙 및 조치를 작성하고 관리할 수 있습니다. 

디바이스에 대해 트리거된 규칙 및 경보에 대한 개요를 가져오려면 다음 보드를 사용하십시오. 

 |보드 이름 | 설명 |  
 |:---|:---|  
  |규칙 중심 분석 | 조직에 대한 규칙을 표시합니다. 추가 카드에는 트리거된 경보, 연관된 디바이스, 디바이스 특성 및 경보 정보가 나열되어 있습니다.  |  
 |디바이스 중심 분석 | 조직에 연결된 디바이스를 표시합니다. 추가 카드에는 선택된 디바이스에 대한 경보, 선택된 디바이스에 대한 정보, 디바이스 특성 및 경보 정보가 표시되어 있습니다.  |

 기본 분석 보드에 대한 자세한 정보는 [보드 및 카드를 사용하여 실시간 데이터 시각화](data_visualization.html#default_boards)를 참조하십시오. 


## 규칙 작성
{: #rules}

규칙은 실시간 디바이스 데이터를 사전 정의된 임계값이나 기타 특성 데이터와 일치시켜서 조건이 충족되면 경보를 트리거하는 조건 기반의 의사결정 지점입니다. {{site.data.keyword.iot_short}} 대시보드에 표시되는 경보와 함께, 규칙이 트리거될 때 비즈니스 로직을 실행하도록 하나 이상의 조치를 추가할 수 있습니다. 

**중요:** 디바이스 유형에 대한 규칙을 작성하려면 우선 디바이스 유형에 대한 스키마를 작성해야 합니다. 자세한 정보는 [디바이스 유형 스키마 작성](im_schemas.html)을 참조하십시오. 

규칙을 작성하려면 다음을 수행하십시오.
1. {{site.data.keyword.iot_short}} 대시보드에서 **규칙**으로 이동하십시오. 
2. **규칙 작성**을 클릭하고 규칙에 이름을 부여하며 설명을 제공한 후에 규칙이 적용되는 디바이스 유형을 선택하고 **다음**을 클릭하십시오.   
3. 규칙 로직을 설정하려면 규칙에 대한 트리거로 사용할 하나 이상의 IF 조건을 추가하십시오.   
병렬 행에서 조건을 추가하여 이를 OR 조건으로 적용하거나, 순차 열에서 조건을 추가하여 이를 AND 조건으로 적용할 수 있습니다.  
**중요:** 두 개의 특성을 비교하는 조건을 트리거하거나 AND를 사용하여 순차적으로 결합된 둘 이상의 특성 조건을 트리거하려면 트리거링 데이터 점이 동일한 디바이스 메시지에 포함되어 있어야 합니다. 데이터가 둘 이상의 메시지에서 수신되면, 조건 또는 순차 조건이 트리거되지 않습니다.  
**예제:**  
매개변수값이 지정된 값보다 크면 단순 규칙이 경보를 트리거함:
조건 = `temp_cpu>80`  
임계값의 조합이 충족되면 보다 복잡한 규칙이 트리거됨:
조건 = `temp_cpu>60 AND cpu_load>90`   

4. 규칙에 대한 조건부 트리거 요구사항을 구성하십시오.  
일정 기간 동안 규칙에 대해 트리거되는 경보의 수를 제어하기 위해 규칙에 대한 조건부 트리거 요구사항을 구성할 수 있습니다.   
**중요:** 조건부 트리거링은 규칙의 임의의 조건에서 작동합니다. 예를 들어, 규칙에 OR을 사용하여 설정된 다섯 개의 서로 다른 병렬 조건이 있으면 true인 각 조건은 조건부 트리거 개수에 포함됩니다.
규칙에 대한 조건부 트리거링을 설정하려면 다음을 수행하십시오. 
 1. 규칙 편집기에서 기본 **조건이 충족될 때마다 트리거** 링크를 클릭하여 빈도 설정 요구사항 대화 상자를 여십시오. 
 2. 규칙에서 사용할 조건부 트리거를 선택하고 구성하십시오. 
 <ul>
 <li>조건이 충족될 때마다 트리거</li>
 <li>M *단위 시간*에 조건이 N번 충족되면 트리거</li>
 </ul>  
 조건부 트리거의 추가적인 세부 설명은 [조건부 규칙 트리거](#conditional "조건부 트리거링 개요")를 참조하십시오.
5. 규칙 조건이 충족되면 발생하는 하나 이상의 조치를 작성하거나 선택하십시오.  
조치에 대한 자세한 정보는 [규칙에서 조치 사용](#shared "조치 작성")을 참조하십시오.    
예를 들어, 조치를 사용하여 이메일을 발송하거나 웹훅을 게시할 수 있습니다. 
3. **선택사항:** 규칙에 대한 경보 우선순위를 선택하십시오.   
우선순위는 **규칙 기반 분석** 보드에서 표시되는 경보를 분류하는 데 사용됩니다. 기본 우선순위는 '낮음'입니다. 
6. 규칙이 충족되면 **저장**을 클릭하여 활성화 없이 저장하거나 **활성화**를 클릭하여 규칙을 저장하고 활성화하십시오. 

규칙이 작성되었습니다. 규칙을 활성화하는 경우, 규칙의 조건이 충족되면 경보가 **보드 > 규칙 기반 분석** 보드에 추가되며 규칙 조치가 실행됩니다. 

## 조건부 규칙 트리거
{: #conditional}

일정 기간 동안 규칙에 대해 트리거되는 경보의 수를 제어하기 위해 규칙에 대한 조건부 트리거 요구사항을 구성할 수 있습니다. 

메시지 빈도 및 규칙 조건에 따라, 규칙은 트리거 조건이 충족된 후에 상당히 많이 트리거할 수 있습니다. 예를 들어, 조건이 `temp >= 90`이며 온도가 상승하여 91에서 안정화되면 규칙이 각 수신 메시지와 함께 트리거됩니다. 디바이스 메시지의 빈도와 규칙이 실행되도록 설정된 조치에 따라, 경보의 이 볼륨은 빠르게 이메일 받은 편지함을 채우거나 추가적인 값을 제공하지 않는 메시지로 Twitter 피드를 가득 채울 수 있습니다. 

**중요:** 조건부 트리거링은 규칙의 모든 조건에 대해 작동합니다. 예를 들어, 규칙에 OR을 사용하여 설정된 다섯 개의 서로 다른 병렬 조건이 있으면 충족되는 각 조건이 조건부 트리거 개수에 포함됩니다. 

조건 | 설명
------------- | -------------
조건이 충족될 때마다 트리거 | 이 규칙은 조건이 충족될 때마다 트리거됩니다.
*M* *일/시간/분/사용자 지정*에 조건이 *N*번 충족되면 트리거 | 규칙은 선택된 기간에 조건이 *N*번 충족되면 트리거된 후에, 구성된 기간이 경과할 때까지는 다시 트리거되지 않습니다. </br>예제: 조건부 트리거 요구사항 =`Trigger only once if conditions are met 4 times in 30 minutes`. 디바이스는 매 5분마다 하나의 새 메시지를 전송합니다. 정오에 온도가 처음으로 90도를 초과하며, 이는 조건을 충족합니다. 조건부 트리거 카운터가 시작되지만, 규칙은 아직 트리거되지 않습니다. 15분 이후 `temp > 90`을 표시하는 세 개의 추가 메시지가 수신되면 규칙이 트리거됩니다. 그리고 규칙은 온도와는 무관하게 추가로 15분 동안에는 트리거되지 않습니다.
첫 시점의 조건이 충족될 때만 트리거되며, 조건이 더 이상 충족되지 않으면 재설정됩니다.  | 규칙은 조건이 충족될 때 트리거되지만, 역시 조건을 충족하는 연속 메시지에 대해서는 트리거되지 않습니다. 트리거링 기준은 규칙 조건을 충족하지 않는 첫 번째 메시지에 의해 재설정됩니다.
*M* *일/시간/분/사용자 지정*에 대한 조건이 유지되는 경우 트리거하십시오. | 일정 시간 간격 동안 수신된 모든 데이터 점이 조건에 맞거나 추가 데이터 점이 수신되지 않으면 선택한 시간 간격 후에 규칙이 트리거됩니다. 처음에 조건이 충족되면 시간 간격이 시작됩니다.



## 규칙에서 조치 사용
{: #shared}

경보 대시보드의 경보 표시와 함께, {{site.data.keyword.iot_short}}은 여러 유형의 규칙 트리거된 조치를 지원합니다(예: 이메일 발송 및 웹훅 게시). 

규칙 편집기에서 직접 조치를 작성하거나 조치 탭에서 조치를 작성한 후에 규칙을 작성할 때 조치를 선택할 수 있습니다. 

조치 탭에서 조치를 작성하려면 다음을 수행하십시오. 
1. {{site.data.keyword.iot_short}} 대시보드에서 **규칙**으로 이동하십시오. 
2. 규칙 대시보드에서 **조치** 탭을 선택하십시오. 
2. **조치 작성**을 클릭하고 조치에 이름과 설명을 지정한 다음 조치 유형을 선택하고 **다음**을 클릭하십시오. 
3. 작성 중인 조치의 유형에 대해 필수 매개변수를 제공하십시오.  
조치 유형:  
 - [이메일 발송](#email "이메일 발송")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [웹훅](#webhook "웹훅")
4. 새 조치를 작성하려면 **확인**을 클릭하십시오. 

이제 규칙 편집기에서 조치를 사용할 수 있습니다. 

**참고:** 이후의 예제는 모두 규칙 조건 `temp_cpu >= 80`을 사용하여 디바이스의 `temp_cpu` 특성이 표현하는 온도가 80도를 초과할 때 서비스 엔지니어에게 알리는 조치를 표시합니다. 

### 이메일 발송  
{: #email}
이메일 발송 조치를 사용하여 규칙이 트리거될 때 하나 이상의 수신인에게 이메일을 발송할 수 있습니다. 

예제: [이메일 발송](#emailex).

다음 매개변수는 이메일 발송 조치를 구성하는 데 사용됩니다. 

매개변수 | 설명
---|---
이름 | 경보 대시보드에서 사용되는 조치의 이름입니다.
설명 | 조치에 대한 간략한 설명입니다.
제목 | 이메일의 제목 행입니다. 기본 제목 행은 "IBM Watson IoT 경보: 메일 조치"입니다.
수신 | 경보를 본인에게만 또는 이메일 주소의 쉼표로 분리된 목록으로 발송하도록 선택하십시오. 본인에게 발송하도록 선택하는 경우, 이메일은 자신이 로그인한 {{site.data.keyword.iot_short}}의 이메일 주소로 발송됩니다.
참조 | 없음 또는 이메일 주소의 쉼표로 분리된 목록입니다.
이메일의 본문은 규칙이 트리거된 시점에 디바이스의 메시지로부터 자동으로 작성됩니다.   
**중요:** 기본적으로, 이메일에는 민감한 정보가 포함될 수 있는 디바이스 데이터가 포함되지 않습니다. 디바이스 데이터를 포함하도록 **데이터 포함** 설정을 변경하십시오.

#### 예제: 이메일 발송 사용
{: #emailex}

이 예제에서 조치는 이메일 발송 기능을 사용하여 이메일을 기본 서비스 엔지니어에게 발송하고 또한 백업 이메일을 해당 관리자에게 발송하도록 조치가 구성되어 있습니다. 

이메일 조치를 작성하려면 다음을 수행하십시오.
1. {{site.data.keyword.iot_short}} 대시보드에서 **규칙**으로 이동하십시오. 
2. **조치 작성**을 클릭하십시오. 
4. 조치 이름 `Send service request email`을 입력하십시오. 
5. 설명 `Send an email to the service engineer and his manager`를 입력하십시오. 
3. **이메일** 유형을 선택하십시오. 
6. 수신 필드에서 **특정 사용자**를 선택하고 `service.engineer@company.com`을 입력하십시오. 
7. 참조 필드에서 **특정 사용자**를 선택하고 `service.manager@company.com`을 입력하십시오. 
8. 제목 행에서 `Service required`를 입력하십시오. 
10. **데이터 포함**을 선택하여 이메일에 디바이스 데이터를 포함하십시오. 
11. **완료**를 클릭하여 조치를 저장하십시오.   


### IFTTT  
{: #ifttt}

IFTTT 조치를 사용하여 규칙이 트리거될 때 IFTTT 레시피를 트리거할 수 있습니다. IFTTT 레시피로서 조치 트리거링에 대한 자세한 정보는 IFTTT 사이트의 [Maker 채널 ![외부 링크 참조](../../icons/launch-glyph.svg "외부 링크 참조")](https://ifttt.com/maker){: new_window}을 참조하십시오. 

예제: [IFTTT를 사용하여 Trello 카드 게시](#iftttex).

다음 매개변수는 IFTTT 조치를 구성하는 데 사용됩니다. 

매개변수 | 설명
---|---
이름 | 경보 대시보드에서 사용되는 조치의 이름입니다.
설명 | 조치에 대한 간략한 설명입니다.
키 | 이벤트를 트리거하는 데 사용할 Maker 채널 키입니다.
이벤트 | Maker 이벤트의 트리거로서 구성된 이벤트 이름입니다. 서로 다른 트리거로 여러 레시피를 작성할 수 있으며, 여기서 각각의 이벤트 이름은 상이합니다.
값 1-3 | 이러한 매개변수에서 임의의 컨텐츠를 전달할 수 있으며, 이는 IFTTT 레시피의 조치에 전달됩니다. **팁:** [변수 대체](#variable_substitution)를 사용하여 헤더에 추가 데이터를 동적으로 포함할 수 있습니다.

#### 예제: IFTTT를 사용하여 Trello 카드 게시{: #iftttex}

이 예제에서는 IFTTT를 사용하여 Trello의 서비스 요청 목록에 카드를 게시하도록 조치가 구성되어 있습니다. 

Trello의 카드 게시 조치를 작성하려면 다음을 수행하십시오. 
1.	IFTTT에서 Trello 채널에 연결하십시오. 
2.	IFTTT에서 Maker 채널에 연결하십시오. IFTTT 키를 기록하십시오. {{site.data.keyword.iot_short_notm}}에서 IFTTT에 연결하려면 이 키가 필요합니다. 
5.	IFTTT에서 레시피를 작성하십시오. 
 1. **THIS**를 클릭하십시오. 
 2. **Maker** 채널을 선택하십시오.   
 2. **웹 요청 수신**을 클릭하십시오. 
 3. 이벤트 이름 `post-Trello-card`을 입력하십시오. 
 4. **THAT**을 클릭하십시오. 
 5. **Trello** 채널을 선택하십시오. 
 6. 카드가 작성되는 Trello 보드를 선택하십시오. 
 7. 카드가 추가되는 목록 이름을 입력하십시오. 
 8. 제목 및 설명을 편집하십시오. 
 9. @service.engineer 및 @service.manager 구성원을 지정하십시오. 
 8. **조치 작성**을 클릭하십시오.    
3. {{site.data.keyword.iot_short}} 대시보드에서 **규칙 > 조치**로 이동하고 다음 매개변수를 갖는 새 조치를 작성하십시오. 
<ul>
<li>유형 - **IFTTT**</li>
<li>이름 - `Post service request card`</li>
<li>설명 - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>키 - IFTTT 키</li>
<li>이벤트 - `post-Trello-card`</li>
<li>선택사항으로, 값 1-3에 대한 값을 추가하십시오. **팁:** [변수 대체](#variable_substitution)를 사용하여 디바이스 데이터를 동적으로 포함할 수 있습니다. </li>
</ul>
4. **확인**을 클릭하여 조치를 저장하십시오. 


### Node-RED
{: #nodered}

Node-RED 조치를 사용하여 규칙이 트리거될 때 Node-RED 애플리케이션에 연결할 수 있습니다. Node-RED 사용에 대한 자세한 정보는 [Internet of Things 스타터 애플리케이션에서 앱 작성](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html)을 참조하십시오. 

예제: [Node-RED를 사용하여 문자 메시지 전송](#noderedex).

다음 매개변수는 Node-RED 조치를 구성하는 데 사용됩니다. 

매개변수 | 설명
---|---
이름 | 경보 대시보드에서 사용되는 조치의 이름입니다.
설명 | 조치에 대한 간략한 설명입니다.
URL | 대상 Node-RED HTTP 입력 노드의 URL입니다.
사용자 이름 | Node-RED 서비스에서 필요하면 포함됩니다.
비밀번호 | Node-RED 서비스에서 필요하면 포함됩니다. **중요:** 비밀번호는 일반 텍스트로 전송됩니다.
본문 | 기본적으로, 본문 필드는 [변수 대체](#variable_substitution)에 나열된 모든 변수로 사전에 채워집니다.

#### 예제: Node-RED를 사용하여 문자 메시지 전송
{: #noderedex}

이 예제에서는 Twilio 노드의 Node-RED를 사용하여 문자 메시지를 서비스 엔지니어에게 전송하도록 조치가 구성되어 있습니다. 

문자 메시지 전송 조치를 작성하려면 다음을 수행하십시오. 
1. Twilio에서, Twilio 계정으로부터 문자 메시지 전송에 사용할 새 메시지 전달 서비스를 찾거나 작성하십시오. 관련 정보는 [Twilio 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.twilio.com/help){: new_window}를 참조하십시오. 
2. Bluemix에서, Node-RED URL `http://mynodered.mybluemix.net/red/`로 Node-RED 계정에 액세스하거나 이를 설정하십시오. 자세한 정보는 Bluemix 문서의 [Node-RED 스타터에서 앱 작성](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) 주제를 참조하십시오. 
3. Node-RED에서, 두 개의 단순 노드 플로우를 작성하십시오(예: [RTI-alert]->[SMS]).  
여기서 첫 번째 노드는 http 노드이며, 두 번째 노드는 twilio 노드입니다. 
 1. "http" 입력 노드를 추가하고 이를 다음 속성으로 구성하십시오. 
  <ul>
  <li>메소드 - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>이름 - RTI 조치</li>
  </ul>
  2. "http 응답" 출력 노드를 추가하고, 한 쪽의 출력 포트를 다른 쪽의 입력 포트로 끌어옴으로써 이와 "http" 입력 노드를 함께 연결하십시오. 
  3. "twilio" 출력 노드를 추가하고 이를 다음 속성으로 구성하십시오. 
  <ul>
  <li>서비스 - **외부 서비스**</li>
  <li>Twilio - 새 twilio-api 추가</li>
  <li>SMS 대상 - `Phone number for the service engineer`</li>
  <li>이름 - **SMS**</li>
  </ul>
  4. 노드를 함께 연결  
  하나의 출력 포트를 다른 하나의 입력 포트로 끌어와서 http 및 twilio 노드를 함께 연결하십시오. 
  5. **배치** 단추를 클릭하여 플로우를 서버에 배치하십시오. 
4. {{site.data.keyword.iot_short}} 대시보드에서 **규칙 > 조치**로 이동하고 다음 매개변수를 갖는 새 조치를 작성하십시오. 
 - 유형 - **Node-RED**
 - 이름 - `Send text using Node-RED and Twilio`
 - 설명 - `Send a text message alert to the service engineer.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. **완료**를 클릭하여 조치를 저장하십시오. 



### 웹훅
{: #webhook}

웹훅 조치를 사용하여 경보가 트리거될 때 웹훅 사용 웹 서비스에 대해 HTTP 요청을 작성할 수 있습니다. 예를 들어, 디바이스의 센서가 비정상적인 읽기를 보고하는 경우에는 웹훅을 사용하여 자산에 대한 서비스 요청을 열 수 있습니다. 

예제: [웹훅을 사용하여 슬랙에 게시](#webhookex).

다음 매개변수는 웹훅 조치를 구성하는 데 사용됩니다. 

매개변수 | 설명
---|---
이름 | 경보 대시보드에서 사용되는 조치의 이름입니다.
설명 | 조치에 대한 간략한 설명입니다.
URL | 대상 웹훅 사용 서버의 URL입니다. **팁:** [변수 대체](#variable_substitution)를 사용하여 URL에 추가 데이터를 동적으로 포함할 수 있습니다.
메소드 | 실행할 웹훅 호출의 유형입니다. GET, HEAD, OPTIONS, PATCH, PUT, POST 또는 DELETE 유형 중에서 하나를 선택하십시오.
사용자 이름 | 웹 서비스에서 필요하면 포함됩니다.
비밀번호 | 웹 서비스에서 필요하면 포함됩니다. **중요:** 비밀번호는 일반 텍스트로 전송됩니다.
헤더 | 헤더는 키 및 값 쌍에서 구성됩니다. **팁:** [변수 대체](#variable_substitution)를 사용하여 헤더에 추가 데이터를 동적으로 포함할 수 있습니다.
컨텐츠 유형 | 본문의 컨텐츠 유형입니다(JSON, XML, WWW 양식 URL 인코딩 또는 일반 텍스트). OPTIONS, PATCH, PUT, POST 및 DELETE 메소드에 사용할 수 있습니다.
본문 | 웹훅 호출의 본문입니다. OPTIONS, PATCH, PUT, POST 및 DELETE 메소드에 사용할 수 있습니다. 기본적으로, 본문 필드는 [변수 대체](#variable_substitution)에 나열된 모든 변수로 사전에 채워집니다. **중요:** 별도의 특정 필드를 본문에 포함하도록 웹훅 서버에서 요구할 수 있습니다. 예를 들어, 슬랙 웹훅에는 "텍스트" 필드가 포함되어야 합니다.    

#### 예제: 웹훅을 사용하여 슬랙에 게시
{: #webhookex}

이 예제에서는 웹훅을 사용하여 #service-requests 슬랙 채널에 메시지를 게시하도록 조치가 구성되어 있습니다. 

슬랙에 게시 조치를 작성하려면 다음을 수행하십시오. 
1. 슬랙에서, 채널 #service-requests에 대한 수신 웹훅 통합을 설정하십시오. 웹훅 URL을 기록하십시오. 자세한 정보는 [Slack 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://api.slack.com/incoming-webhooks){: new_window}를 참조하십시오. 
2. {{site.data.keyword.iot_short}} 대시보드에서 **규칙 > 조치**로 이동하고 다음 매개변수를 갖는 새 조치를 작성하십시오. 
 - 이름 - `Post service request on Slack`
 - 유형 - **웹훅**
 - URL - `Your Slack webhooks URL`
 - 메소드 - **POST**
 - 컨텐츠 유형 - `application/json`
 - 본문   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **중요:** 슬랙 웹훅에는 최소한 "텍스트" 필드가 포함되어야 합니다. 관련 정보는 Slack 문서에서 [수신 웹훅 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks "Slack 문서"){: new_window}을 참조하십시오.
11. **완료**를 클릭하여 조치를 저장하십시오. 


### 변수 대체  
{: #variable_substitution}

다음 변수 대체를 포함하여 디바이스 데이터를 동적으로 포함하십시오. 변수는 이중 중괄호로 묶어야 합니다. 

변수 | 설명
---|---
**URL, 헤드 및 본문** |
`{{timestamp}}` | 메시지의 시간소인입니다.
`{{orgId}}` | {{site.data.keyword.iot_short_notm}} 서비스의 조직 ID입니다.
`{{tenantId}}` | 더 이상 사용되지 않음: {{site.data.keyword.iotrtinsights_full}} 서비스의 ID입니다.
`{{deviceId}}` | 디바이스의 ID입니다.
`{{ruleName}}` | 조치가 포함된 규칙의 이름입니다.
`{{ruleID}}` | 조치가 포함된 규칙의 ID입니다.
**본문만** |
`{{ruleDescription}}`| 조치가 포함된 규칙의 설명입니다.
`{{ruleCondition}}` | 조치를 트리거한 규칙 조건입니다.
`{{message}}` | 규칙을 트리거한 데이터 점 값이 포함된 원시 디바이스 메시지입니다.

## 클라우드 분석에 대한 레시피

다음 레시피는 다양한 유스 케이스에 대해 클라우드 분석 기능을 사용하는 방법을 설명합니다. 

- [Real Time Data Analysis Using IBM Watson™ IoT Platform Analytics ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Predictive Analytics on IOT Sample Data ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [Device List Card SIMPLIFIES Real Time Device Monitoring on WIoTP Dashboard ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Perform Actions in IBM Watson IoT Platform Cloud Analytics ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Use IBM Data Science Experience to detect time series anomalies ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
