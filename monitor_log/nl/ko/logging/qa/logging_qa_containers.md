---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 자주 묻는 질문과 응답
{: #logging_qa}

다음은 {{site.data.keyword.Bluemix}} 로깅 기능을 사용하는 데 대한 일반적인 질문의 응답입니다.
{:shortdesc}

* [Kibana의 내 컨테이너에서 생성된 JSON 로그를 볼 수 없으면 어떻게 합니까?](logging_qa.html#logging_qa_no_JSON_data_kibana)


## Kibana의 내 컨테이너에서 생성된 JSON 로그를 볼 수 없으면 어떻게 합니까?
{: #logging_qa_no_JSON_data_kibana}

JSON 로그가 stdout로서 Docker 로그에 전송되면 JSON으로서 구문 분석되지 않으므로, 해당 순서를 변경하기 위해 @timestamp 필드로 정렬할 수 없습니다. 

표시되는 @timestamp 값은 로그가 ElasticSearch에서 수신된 때의 시간소인입니다. 

로그가 컨테이너에서 생성된 때를 반영하는 시간소인이 메시지 필드의 일부로 표시됩니다.

메시지 필드를 여러 개의 필드로 분리하려면 stdout가 아닌 파일에 JSON을 로그하십시오. 그런 다음 Kibana의 로그를 정렬하십시오.
