---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.graphfull}} 시작하기
{: #gettingstartedtemplate}
마지막 업데이트 날짜: 2016년 7월 27일
{: .last-updated}

{{site.data.keyword.graphfull}}는 REST 기반의 HTTP API 인터페이스를 통해 액세스할 수 있는
전체적으로 관리되는 그래프 데이터베이스 서비스입니다.
이를 사용하여 그래프 데이터베이스 기능이 필요한 모바일 및 웹 애플리케이션을 빌드하십시오.
{:shortdesc}

{{site.data.keyword.graphfull}}는 v3 호환 가능 API를 사용하는 고성능 그래프 애플리케이션을 빌드하기 위해
[Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;
스택을 기반으로 합니다.
스택은 익숙한 환경을 기반으로 하는 추가적인 유연성 및 기능을 제공합니다.
{{site.data.keyword.Bluemix}} 대시보드를 사용하면
{{site.data.keyword.graphfull}} 서비스를 {{site.data.keyword.Bluemix_short}} 애플리케이션과
쉽게 통합할 수 있습니다.

두 가지 방법으로 {{site.data.keyword.graphfull}}를 사용하여 작업할 수 있습니다.

*	{{site.data.keyword.graphfull}} 단순화된 API 명령 사용
*	전체 Apache TinkerPop v3 조회 언어(Gremlin) 사용

{{site.data.keyword.graphfull}} 기능은 HTTP REST 엔드포인트를 사용하여 API로 사용 가능합니다.
이러한 엔드포인트는 HTTP를 사용하여 API 요청을 작성하고 결과를 얻음으로써
애플리케이션이 {{site.data.keyword.graphfull}} 서비스에 연결하고 이를 사용할 수 있는 쉬운 방법을 제공합니다.
선택한 애플리케이션 프로그래밍 언어와 함께 제공되는 HTTP 기능을 사용하여 엔드포인트에 액세스하십시오.
또는 명령 인터페이스 또는 `curl` 스크립트를 사용하여 동일한 효과를 얻을 수 있습니다.
API 참조는 {{site.data.keyword.graphfull}} 서비스에 의해 제공되는 다양한 기능 및 사용 예를 제공합니다.

또한 애플리케이션은 {{site.data.keyword.graphfull}} 서비스를 사용하는 태스크에 대해 Gremlin이라 불리는
Apache TinkerPop 조회 언어를 사용할 수 있습니다.
JSON 문서에 Gremlin 조회를 포함시킨 다음 문서를 `/gremlin` 서비스 엔드포인트에 전달하십시오.
{{site.data.keyword.graphfull}}와 함께 Gremlin을 사용하는 예는 전체 문서에서 제공됩니다.

다음 단계를 완료하여 {{site.data.keyword.graphfull}} 서비스를 시작하십시오.

1.	{{site.data.keyword.graphfull}} 서비스의 [인스턴스를 작성하십시오](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance). 
2.	인스턴스가 작성될 때 생성된 세 개의 필수 값을 기록하십시오. 해당 값은 서비스 타일을 클릭한 후에 `서비스 신임 정보` 탭에서 사용 가능합니다.
	*	IBM Graph 엔드포인트: `apiURL`
	*	서비스 인스턴스 사용자 이름 `username`
	*	서비스 인스턴스 비밀번호 `password`
3.	{{site.data.keyword.graphfull}} 태스크에 대한 애플리케이션 또는 스크립트에서 세 개의 필수 값을 사용하십시오. 예는 전체 문서에서 제공됩니다.

# 관련 링크
{: #rellinks}

## 학습서 및 샘플
{: #samples}

* [예](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## API 참조
{: #api}

* [IBM Graph용 REST API](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [IBM Graph와 함께 Gremlin 사용](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## 관련 링크
{: #general}

* [전체 문서](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [스택 오버플로우](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
