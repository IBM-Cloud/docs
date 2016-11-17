---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.weather_short}} 정보
{: #about_weather}

{{site.data.keyword.weatherfull}}를 사용하여 TWC(The Weather Company)의 기상 데이터를
{{site.data.keyword.Bluemix}} 애플리케이션에 통합할 수 있습니다.
{:shortdesc}

기상 관측 및 예보를 {{site.data.keyword.Bluemix_notm}}
애플리케이션에 추가하고
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}를 사용하여 위치정보에서 지정되는 영역의 기상 데이터를 표시할 수 있습니다.
"The Weather Company"는 과거와 미래의 기상 데이터를 제공하는 최고의 종합적 제공업체입니다. 강우량, 기압, 바람 및 뇌우를 포함하여 모든 형태의
기상 데이터를 캡처합니다. 

REST API를 사용하여 다음 정보를 검색할 수 있습니다.

* 지정한 위치정보에 대해 현재 시간부터 시작하는 그 다음 48시간 동안의 시간별 기상 예보입니다.
* 지정한 위치정보에 대해 주간 및 야간 세그먼트의 예보를 포함하는 현재 일부터 그 다음 각 3, 5, 7 또는 10일 동안의 일별 예보입니다. 이 예보에는 해당 위치에 대한 적절한 측정 단위를 사용하여 요청된 언어로 작성된 최대 256자의 예보 서술 텍스트 문자열이 포함되어 있습니다.
* 현재 일부터 그 다음 각 3, 5, 7 또는 10일 동안의 일별 예보이며, 이는 각 일별 예보를 오전, 오후, 저녁 및 심야 세그먼트로 구분합니다.
* 지정한 위치정보에 대해 관측된 현재 기상 데이터. 이 기상 데이터에는 기온, 강우량, 풍향과 풍속, 습도, 기압, 이슬점, 시계 및 자외선(UV)이 포함됩니다.
* 이전의 24시간까지 지정한 위치정보에 대한 관측된 기상 데이터입니다. 이 데이터는 실제 관측 스테이션으로부터 얻습니다. 
* National Weather Service(미국), Environment Canada 및 MeteoAlarm(유럽)에서 발행된 기상 감시, 경고, 명령문 및 보안 권고문을 포함하는 정부 발행 기상 경보입니다.
* 10 - 30년 이상의 기간에서 National Weather Service 관측소의 히스토리 일별 또는 월별 기상 데이터를 제공하는 연감 서비스입니다.
* 사용자 요청에 맞는 위치 세트를 검색하기 위해 위치 이름 또는 지오코드(위도 및 경도)를 검색하는 기능을 제공하는 위치 맵핑 서비스입니다.

## 가격 책정 모델
{: #pricing_models}

가격 책정 모델은 REST
API에 대한 분당 호출 수에 기반합니다. 클라이언트에게 월별로 청구됩니다. 무료 및 기본 플랜을 통해
분당 최대 10개의 API 호출을 작성할 수 있습니다. 표준 및 프리미엄 플랜을 통해서는
각각 분당 150 및 375개의 API 호출을 작성할 수 있습니다. 각 플랜에는
허용된 최대 API 호출 수가 있습니다.

임의 지역, 예보 유형 또는 시계열 관측에 대해 애플리케이션에서
기상 데이터를 테스트할 수 있으며 호출 횟수에만 제한이 있습니다. 무료, 기본, 표준 및 프리미엄 플랜은 계약 없이
구입할 수 있습니다. 무료 사용제를 통해 사용자의 앱이 10,000개의 호출을 작성할 수 있습니다. 나머지
플랜을 통해서는 사용자의 앱이 각각 월별로 15만, 2백만
또는 5 백만개의 API 호출을 작성할 수 있습니다.

또한 청구 기간 동안 배치된 각 서비스 인스턴스에 대해
여러 유료 사용제를 구입할 수 있습니다. 앱에서 10,000개가 넘는 호출을 사용하는 경우
서비스를 계속해서 제공받으려면 IBM과 계약을 체결해야 합니다.

사용자의 앱이 사용자가 선택한 플랜에 기반하여 작성하도록 허용된 분당 API 호출 수의 한계에 도달하면,
작성되는 그 다음 API 호출은 앱이 추가 API 호출을 요청하도록 허용될 때까지
실패합니다.

예를 들어, 표준 플랜을 사용 중인 경우 앱에서는
플랜의 한계(분당 150개의 호출)를 초과해도 1분에 500개의 API 호출을 작성하는 것이 *가능*하지만,
그 다음 API 호출은 5분 이후까지 허용되지 않습니다. 그러므로 앱에서
기상 데이터 새로 고치기 지연이 있을 수 있습니다.
해당 한계를 처리할 수 있는 앱을 개발하고 API 호출의 버스트를 요청하지 않았는지
확인해야 합니다. 그 대신, 앱의 API 호출 사용량을 모니터할 수 있습니다. API 호출에 의해
리턴되는 항목 수를 확인하여 앱이 이 계획의 한계에 도달하는지 여부를 확인할 수 있습니다.

사용자의 앱이 사용자가 선택한 플랜에 기반하여 작성하도록 허용된 월별 API 호출 수의 한계에 도달하면,
그 다음 API 호출은
10,000개의 API 호출마다 $1.70의 제한 초과 비율로 청구됩니다.

## 피드백 및 지원
{: #feedback_support}

정보를 검색하거나 포럼에서 질문하여 도움을 받을 수 있습니다. 지원 티켓을 열 수도 있습니다.

포럼을 사용하여 질문하는 경우, {{site.data.keyword.Bluemix_notm}} 개발 팀에 표시되도록 해당 질문에 태그를 지정하십시오.

* {{site.data.keyword.weather_short}}에서 앱 개발 또는 배치에 대한 기술적 질문이 있으면 [스택 오버플로우](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window}에 질문을 게시하고 **ibm-bluemix** 및 **weather**로 질문에 태그를 지정하십시오.
* 서비스에 문제가 있거나 지시사항을 시작하는 데 문제가 있으면 [IBM developerWorks Answers 포럼](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}을 사용하십시오. **bluemix** 및 **weather** 태그를 포함하십시오.
* Insights for Weather에서 {{site.data.keyword.weather_short}}까지 앱을 마이그레이션하는 데 대한 질문이 있으면
[IBM developerWorks](http://www.ibm.com/developerworks){:new_window}에서 문의해 주십시오.

포럼 사용에 대한 자세한 내용은 [도움말 가져오기](https://console.{DomainName}/docs/support/index.html#getting-help){: new_window}를 참조하십시오.

IBM 지원 티켓 열기 또는 지원 레벨과 티켓 심각도에 대한 정보는 [지원 문의](https://console.{DomainName}/docs/support/index.html#contacting-support){: new_window}를 참조하십시오.
