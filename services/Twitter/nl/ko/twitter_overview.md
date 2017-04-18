---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.twittershort}} 정보
{: #about_twitter}

{{site.data.keyword.twitterfull}}를 사용하여 Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} 또는 [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} 스트림의 Twitter 컨텐츠를 {{site.data.keyword.Bluemix}} 애플리케이션에 통합합니다.
{:shortdesc}

Content Store가 새로 고침되고 실시간으로 인덱싱되어 검색을 동적이고 빠르게 만들어줍니다. 이 서비스는 [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}의 심도있는 자연어 처리 알고리즘에 기반하여 여러 언어에 대한 감성과 통찰로 트윗을 풍요롭게 해줍니다. Twitter 데이터 스트림의 실시간 처리가 완벽하게 지원되는데, 이는 쿼리 매개변수와 키워드 세트를 통해 구성 가능합니다. {{site.data.keyword.twittershort}}에는 검색을 사용자 정의하고 트윗 및 감정 상태를 JSON 형식으로 리턴할 수 있도록 하는 RESTful API가 포함되어 있습니다. 리턴된 트윗은 Twitter 데이터를 위한 [Gnip Activity Stream](http://support.gnip.com/){: new_window} 형식을 유지합니다.

{{site.data.keyword.twittershort}} 서비스는 Twitter Decahose 및 PowerTrack 스트림을 실시간으로 분석하여 각 트윗의 작성자에게 다음과 같은 상태 정보를 제공합니다.
* 성
* 영구 위치(국가, 시, 도별로 정의됨)

또한 다음 정보도 트윗 컨텐츠에 제공됩니다. 

* 감정(영어, 독일어, 프랑스어 및 스페인어 트윗에 대한 긍정, 부정, 양면성 또는 중립 감정 표현) 
* 트윗에 긍정/부정의 감정 구문 포함(영어, 독일어, 프랑스어 및 스페인어 트윗의 경우) 

{{site.data.keyword.twittershort}} 검색 결과의 유효성을 검증하기 위해 서비스는 특정 트윗이 Twitter에서 아직 액세스 가능한지 확인하는 REST API 메소드를 제공합니다.  

## 피드백 및 지원 
{: #feedback_support}

문제점 또는 질문이 있으면 정보를 검색하거나 포럼을 통해 질문을 하여 도움을 얻을 수 있습니다. 지원 티켓도 열 수 있습니다.

포럼을 사용하여 질문을 하는 경우 IBM Bluemix 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오. 
* {{site.data.keyword.twittershort}}로 앱을 개발하거나 배치하는 데 관한 기술 질문이 있으면 스택 오버플로우에 질문을 게시하고 **bluemix** 및 **twitter**로 질문에 태그를 지정하십시오. 
* 서비스에 대한 질문 및 시작하기 지시사항은 IBM [developerWorks dW 응답](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} 포럼을 사용하십시오. **insights-twitter** 및 **bluemix** 태그를 포함하십시오.

포럼을 사용하는 데 관한 세부사항은 [도움말](https://new-console.ng.bluemix.net/docs/support/index.html#getting-help){: new.window}을 참조하십시오. 

IBM 지원 티켓을 여는 데 관한 정보 또는 지원 레벨 및 티켓 심각도는 [지원 센터에 문의](https://new-console.ng.bluemix.net/docs/support/index.html#contacting-support){: new.window}를 참조하십시오.
