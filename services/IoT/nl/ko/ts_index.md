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

# {{site.data.keyword.iot_short_notm}} 문제점 해결
{: #ts}

여기에는 {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.iot_full}}을 사용하는 데 대한 일반 문제점 해결 질문에 대한 응답이 있습니다.
{:shortdesc}

## {{site.data.keyword.iot_short_notm}} 조직에 액세스하는 문제점
{: #access-expiry-problem}

소유한 {{site.data.keyword.iot_short_notm}} 조직에 로그인할 수 없습니다.
{:shortdesc}

`https://internetofthings.ibmcloud.com`을 사용하거나 조직 URL을 사용하여 직접 {{site.data.keyword.iot_short_notm}} 조직에 로그인할 수 없습니다.
{: tsSymptoms}

{{site.data.keyword.iot_short_notm}} 조직에 대한 액세스 권한이 만료되었을 수 있습니다. {{site.data.keyword.Bluemix}}를 사용하여 작성된 {{site.data.keyword.iot_short_notm}} 조직은 기본적으로 임시 사용자 프로파일을 사용합니다.
{: tsCauses}

{{site.data.keyword.Bluemix_notm}}를 사용하여 {{site.data.keyword.iot_short_notm}} 조직에 액세스하고 사용자 프로파일의 만기 설정을 변경하여 이 문제점을 해결할 수 있습니다. 사용자 만기 설정을 변경하려면 다음을 수행하십시오. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.iot_short_notm}} 서비스를 여십시오. 
2. 탐색줄에서 **멤버**를 클릭하십시오. 
3. **편집** 아이콘을 클릭하십시오. 
4. **액세스 만료** 상자를 선택 취소하고 **저장**을 클릭하십시오.
{: tsResolve}

## {{site.data.keyword.iot_short_notm}}에 연결 문제점
{: #connection_problem}

{{site.data.keyword.iot_short_notm}}에 대한 연결이 예상치 못하게 삭제되거나 연결이 끊깁니다.
{:shortdesc}

{{site.data.keyword.iot_short_notm}}에 연결하려고 하면 디바이스나 애플리케이션에서 오류가 발생합니다.
{: tsSymptoms}

두 디바이스에서 동일한 클라이언트 ID와 신임 정보를 사용하여 연결 중일 수 있습니다. 클라이언트 ID당 하나의 고유한 연결만 허용됩니다. 동일한 ID를 사용하여 두 개가 동시에 연결할 수 없습니다. 애플리케이션에서는 동일한 API 키를 공유할 수 있지만 MQTT에서는 클라이언트 ID가 항상 고유해야 합니다.
{: tsCauses}

동일한 신임 정보를 사용하여 두 디바이스가 연결하지 않도록 하면 이 문제점을 해결할 수 있습니다.
{: tsResolve}

## {{site.data.keyword.iot_short_notm}}에서 간헐적으로 디바이스의 연결이 끊깁니다.
{: #disconnection_problem}

{{site.data.keyword.iot_short_notm}}에 대한 디바이스 연결이 간헐적으로 예상치 못하게 삭제됩니다.
{:shortdesc}

{{site.data.keyword.iot_short_notm}} 서비스에 연결된 디바이스가 간헐적으로 연결이 끊깁니다. 디바이스가 다시 연결되지만 잠시 후에 예상치 못하게 다시 연결이 끊깁니다.
{: tsSymptoms}

연결할 때 너무 낮은 MQTT ping 옵션 값을 사용하여 연결 제한시간이 초과된 것처럼 보이기 때문일 수 있습니다. 예를 들어 클라이언트 MQTT가 잘못 설정되면 ping이 제때에 수신되지 않으므로 연결이 닫힙니다.
{: tsCauses}

연결의 ping 및 KeepAlive 매개변수를 제대로 설정했는지 확인하여 이 문제점을 수정할 수 있습니다.   
{: tsResolve}


## {{site.data.keyword.iot_short_notm}} 도움 및 지원 받기
{: #gettinghelp}

{{site.data.keyword.iot_short_notm}} 사용 시 문제점 또는 질문이 있으면 정보를 검색하거나 포럼을 통해 질문하여 도움을 받을 수 있습니다. 지원 티켓도 열 수 있습니다.

포럼을 사용하여 질문하는 경우 {{site.data.keyword.Bluemix_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오.

* {{site.data.keyword.iot_short_notm}}을 사용하여 앱 개발 또는 배치에 대한 기술적 질문이 있는 경우 [스택 오버플로우 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window}에 게시하고 질문에 "ibm-bluemix" 및 "watson-iot" 태그를 지정하십시오. 
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* 서비스 및 시작하기 지시사항에 대한 질문은 [IBM developerWorks dW Answers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window} 포럼을 사용하십시오. "watson-iot" 및 "bluemix" 태그를 포함하십시오.

포럼 사용에 대한 세부사항은 [도움 받기](https://www.{DomainName}/docs/support/index.html#getting-help)를 참조하십시오.

IBM 지원 센터 티켓 열기에 대한 정보나 지원 레벨 및 티켓 심각도에 대한 정보는 [지원 센터에 문의 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.{DomainName}/docs/support/index.html#contacting-support)를 참조하십시오. 
