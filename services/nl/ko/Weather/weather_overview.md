---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Weather 정보
{: #about_weather}

*마지막 업데이트 날짜: 2016년 5월 19일*

{{site.data.keyword.weatherfull}}를 사용하여 TWC(The Weather Company)의 기상 데이터를
{{site.data.keyword.Bluemix}} 애플리케이션에 통합할 수 있습니다.
{:shortdesc}

사용자는 기상 관측 및 예보를 {{site.data.keyword.Bluemix_notm}} 애플리케이션에 추가할 수 있으며,
[Insights for Weather REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}를
사용하여 위치정보에서 지정하는 지역의 기상 데이터를 표시할 수 있습니다.
"The Weather Company"는 과거와 미래의 기상 데이터를 제공하는 최고의 종합적 제공업체입니다. 강우량, 기압, 바람 및 뇌우를 포함하여 모든 형태의
기상 데이터를 캡처합니다. 

REST API를 사용하여 다음 정보를 검색할 수 있습니다.

* 지정한 위치정보에 대해 현재 시간부터 시작하여 그 다음 24시간 동안의 시간별 기상 예보
* 지정한 위치정보에 대해 주간 및 야간 세그먼트의 예보를 포함하는 그 다음 10일 동안의 일별 기상 예보. 이 예보에는 해당 위치에 대한 적절한 측정 단위를 사용하여 요청된 언어로 작성된 최대 256자의 예보 서술 텍스트 문자열이 포함되어 있습니다.
* 지정한 위치정보에 대해 관측된 현재 기상 데이터. 이 기상 데이터에는 기온, 강우량, 풍향과 풍속, 습도, 기압, 이슬점, 시계 및 자외선(UV)이 포함됩니다.
* 지정한 위치정보와 시간 범위에 대해 관측된 기상 데이터. 이 데이터는 실제 관측 스테이션으로부터 얻습니다. 이 API는 현재 상태에 대한 기상 관측 및 이전 24시간을 포함하여 최대 24시간 동안의 지난 관측을 리턴합니다.

"The Weather Company"의 기상 문구와 아이콘에 대한 자세한 정보는 [아이콘 코드, 문구 및 이미지](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}를 참조하십시오.
앱에서 사용할 [아이콘 세트를 다운로드](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}할 수도 있습니다. 

## 가격 책정 모델
{: #pricing_models}

가격 책정 모델은 고객에게 월별로 비용 청구되는 Insights for Weather API에 대한
일별 호출을 기반으로 합니다. 임의 지역, 예보 유형 또는 시계열 관측에 대해 애플리케이션에서
기상 데이터를 테스트할 수 있으며 호출 횟수에만 제한이 있습니다. 무료, 기본 및 프리미엄
계획은 계약없이 구입할 수 있습니다. 이 계획으로 앱에서 하루당 각각 500, 5,000 또는 50,000회의
API 호출을 할 수 있습니다.

또한 청구 기간 동안 배치된 각 서비스 인스턴스에 대해
여러 프리미엄 계획을 구입할 수 있습니다. 앱에서 하루당 50,000회를 초과하거나 분당 1,000회를 초과하는 호출을 하는 경우
서비스를 계속하여 제공받으려면 IBM과 계약을 체결해야 합니다.


선택한 계획을 기본으로 작성할 수 있는 API 호출의 한계에 도달하면
앱에서 더 많은 API 호출 요청을 허용할 때까지 작성된 다음 API 호출이
실패합니다. 

예를 들어, 기본 계획을 사용하는 경우 앱에서는
계획의 한계를 초과하더라도 분당 500회의 API 호출을 작성할 수 있지만
다음 API 호출은 5분 이후에 허용됩니다. 그러므로 앱에서
기상 데이터 새로 고치기 지연이 있을 수 있습니다.
해당 한계를 처리할 수 있는 앱을 개발하고 API 호출의 버스트를 요청하지 않았는지
확인해야 합니다. 그 대신, 앱의 API 호출 사용량을 모니터할 수 있습니다. API 호출에 의해
리턴되는 항목 수를 확인하여 앱이 이 계획의 한계에 도달하는지 여부를 확인할 수 있습니다.

## 피드백 및 지원
{: #feedback_support}

Insights for Weather에서 앱 작성과 관련된 기술적 질문사항이 있으면
[스택 오버플로우](http://stackoverflow.com/search?q=weather+bluemix){:new_window}에
질문을 게시하고 **bluemix** 및 **weather**로 질문에 태그를 지정하십시오. 

이 서비스에서 문제가 발생하면 [IBM developerWorks Answers 포럼](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}을 활용하십시오.
IBM의 추가 지원을 받으려면 **insights-weather** 및 **bluemix** 태그를 포함하십시오. 

Bluemix 관련 문제점 해결에 대한 정보는
[문제점 해결](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}을 참조하십시오.
정보 검색, 포럼을 통해 질문하기와 지원 문의에 대한 세부사항은
[고객 지원 받기](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}를 참조하십시오. 
