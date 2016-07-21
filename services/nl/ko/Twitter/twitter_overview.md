---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.twittershort}} 정보
{: #about_twitter}

*마지막 업데이트 날짜: 2016년 5월 13일*
{: .last-updated}

{{site.data.keyword.twitterfull}}를 사용하여 Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} 또는 [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} 스트림의 Twitter 컨텐츠를 {{site.data.keyword.Bluemix}} 애플리케이션에 통합합니다.
{:shortdesc}

Content Store가 새로 고침되고 실시간으로 인덱싱되어 검색을 동적이고 빠르게 만들어줍니다. 이 서비스는 [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}의 심도있는 자연어 처리 알고리즘에 기반하여 여러 언어에 대한 감성과 통찰로 트윗을 풍요롭게 해줍니다. Twitter 데이터 스트림의 실시간 처리가 완벽하게 지원되는데, 이는 쿼리 매개변수와 키워드 세트를 통해 구성 가능합니다. {{site.data.keyword.twittershort}}에는 검색을 사용자 정의하고 트윗 및 감정 상태를 JSON 형식으로 리턴할 수 있도록 하는 RESTful API가 포함되어 있습니다. 리턴된 트윗은 Twitter 데이터를 위한 [Gnip Activity Stream](http://support.gnip.com/sources/twitter/data_format.html){: new_window} 형식을 유지합니다.

{{site.data.keyword.twittershort}} 서비스는 Twitter Decahose 및 PowerTrack 스트림을 실시간으로 분석하여 각 트윗의 작성자에게 다음과 같은 상태 정보를 제공합니다.
* 성
* 영구 위치(국가, 시, 도별로 정의됨)

또한 다음 정보도 트윗 컨텐츠에 제공됩니다. 

* 감정(영어, 독일어, 프랑스어 및 스페인어 트윗에 대한 긍정, 부정, 양면성 또는 중립 감정 표현) 
* 트윗에 긍정/부정의 감정 구문 포함(영어, 독일어, 프랑스어 및 스페인어 트윗의 경우) 

{{site.data.keyword.twittershort}} 검색 결과의 유효성을 검증하기 위해 서비스는 특정 트윗이 Twitter에서 아직 액세스 가능한지 확인하는 REST API 메소드를 제공합니다.  

## 피드백 및 지원 
{: #feedback_support}

{{site.data.keyword.twitterfull}} 팀은 여러분의 의견을 기다리고 있습니다. 

이 서비스에서 문제점을 발견하면
IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} 포럼을 방문하십시오. 이전에 제출된 질문에 대한 응답을 검색하거나 질문을 하십시오.
**insights-twitter** 및 **bluemix** 태그를 포함하여 응답 시간을 향상시키십시오. 

developerWorks Answers에서 다루지 않은 질문이 있으면
[스택 오버플로우](http://stackoverflow.com/search?q=twitter+bluemix){: new.window}에 질문을 게시하고 질문을 **twitter** 및 **bluemix**로 태그 지정하십시오. 

또한 [Bluemix 플랫폼](https://developer.ibm.com/bluemix/support/#status){: new.window}의 상태를 보거나
[지원 티켓을 열 수 있습니다](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. 자세한 정보는 [문제점 해결](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}을 참조하십시오. 
