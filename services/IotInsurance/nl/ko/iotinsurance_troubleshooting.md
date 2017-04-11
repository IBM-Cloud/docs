---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iotinsurance_short}} 문제점 해결
{: #ts}

{{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.iotinsurance_full}} 사용과 관련된 일반적인 문제점 해결 질문에 대한 답변입니다.
{:shortdesc}

## 앱 배치 문제점
{: #deployingapps}
{{site.data.keyword.Bluemix_notm}} 조직에 충분한 여유 메모리가 없으면 {{site.data.keyword.iotinsurance_short}}에 대한 앱을 배치하지 못할 수도 있습니다. 앱이 사용하는 메모리를 줄이거나 사용자 계정에 할당된 메모리를 늘릴 수 있습니다.
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} 서비스를 열 때 배치 기능이 사용 가능하지 않으면 앱을 배치할 수 없습니다.
{: tsSymptoms}

배치 기능을 사용하기 위해서는 최소 2GB의 여유 메모리가 사용자의 조직에 있어야 합니다. 시험판 계정에는 최대 2GB 메모리가 할당되어 있습니다. {{site.data.keyword.iotinsurance_short}}가 아닌 서비스 또는 앱을 작성한 경우 조직에 {{site.data.keyword.iotinsurance_short}} 앱을 배치할 수 있는 충분한 메모리가 없습니다.
{: tsCauses}

계정의 메모리 할당을 늘리거나 서비스 및 앱에서 사용하는 메모리를 줄일 수 있습니다.
- 계정의 메모리 할당을 늘리기 위해 [시험판 계정을 유료 계정으로 전환](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)할 수 있습니다.
- 사용 중인 메모리를 빠르게 줄이려면 {{site.data.keyword.iotinsurance_short}}가 아닌 모든 서비스와 앱을 제거하십시오. 변경이 적용되도록 {{site.data.keyword.iotinsurance_short}} 서비스를 다시 시작하십시오. 
- 총 2GB가 넘는 메모리를 유료 계정의 경우 기타 앱이나 서비스에서 사용하는 메모리 양을 조정하여 기타 앱 또는 서비스를 제거하는 것을 피할 수 있습니다. 자세한 정보는 [조직의 메모리 한계 초과](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)를 참조하십시오.
{: tsResolve}

## 성능 문제
{: #performance_issues}

최대 활동 기간 중에는 성능이 느려질 수 있습니다.
{:shortdesc}

API 호출을 자주 수행하는 시스템은 응답 시간이 지연될 수 있습니다.
{: tsSymptoms}

기본적으로 {{site.data.keyword.iotinsurance_short}}에서는 {{site.data.keyword.cloudantfull}}의 평가판 버전을 배치합니다. 이 버전은 초당 수행할 수 있는 API 호출 수를 제한합니다.
{: tsCauses}

{{site.data.keyword.cloudant}} 표준 버전으로 업그레이드하십시오.
{: tsResolve}

## {{site.data.keyword.iotinsurance_short}} 도움 및 지원 받기
{: #gettinghelp}

{{site.data.keyword.iotinsurance_full}} 사용 시 문제가 있거나 질문이 있는 경우, {{site.data.keyword.Bluemix_notm}}의 내용을 확인하거나 정보를 검색하여 도움말을 가져오거나 포럼을 통해 질문할 수 있습니다. 또한 지원 티켓을 열 수도 있습니다. 

- {{site.data.keyword.Bluemix_notm}} 사용 가능 여부는 [Bluemix 상태 페이지 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window}로 이동하여 확인할 수 있습니다.

- 포럼을 검토하여 같은 문제가 있는 다른 사용자가 있는지 확인할 수 있습니다. 포럼을 통해 질문하는 경우 {{site.data.keyword.Bluemix_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오. 
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- {{site.data.keyword.iotinsurance_short}}로 앱을 개발하거나 배치하는 것과 관련된 기술적 질문이 있는 경우, 해당 질문을 [Stack Overflow ![외부 링크 아이콘](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window}에 게시하고 질문에 "ibm-bluemix" 및 "iot-for-insurance"로 태그를 지정하십시오. 
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- 서비스 및 시작하기 지시사항에 관한 질문은 [IBM developerWorks dW Answers ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window} 포럼을 사용하십시오. "iot-for-insurance" 및 "bluemix" 태그를 포함하십시오. 

포럼 사용에 대한 세부사항은 [도움 받기](https://www.{DomainName}/docs/support/index.html#getting-help)를 참조하십시오. 

- 그래도 문제를 해결할 수 없으면 IBM 지원 티켓을 개설하십시오. IBM 지원 티켓 개설 방법이나 지원 레벨 및 티켓 심각도 정보는 [지원 문의](../support/index.html#contacting-support)를 참조하십시오. 
