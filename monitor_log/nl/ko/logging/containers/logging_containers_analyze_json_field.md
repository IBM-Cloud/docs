---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 컨테이너 로그 항목의 일부인 JSON 메시지 필드 분석
{: #logging_containers_analyze_json_field}

Kibana에서 컨테이너 로그 데이터를 분석하기 위해 새 검색을 정의하고 JSON 형식 메시지 필드에 정의된 문자열 유형 필드에 필터를 적용할 수 있습니다.
{:shortdesc}

다음 단계를 완료하여 Kibana에서 JSON 유형 필드를 분석하십시오.

1. JSON 메시지 필드를 여러 필드로 분리하려면 JSON 형식의 메시지를 STDOUT이 아닌 파일에 로그하십시오. 

    JSON 로그 항목을 컨테이너의 Docker 로그 파일에 STDOUT으로 보내면 이 로그 항목이 JSON으로 구문 분석되지 않습니다. @timestamp 필드를 기준으로 메시지를 정렬하여 순서를 변경할 수 없습니다.  

2. 컨테이너에서 분석에 사용할 수 있는 기본이 아닌 로그 목록에 로그 파일을 추가하십시오. 자세한 정보는 [컨테이너에서 기본이 아닌 로그 데이터 수집](logging_containers_other_logs.html#logging_containers_collect_data)을 참조하십시오. 

3. Kibana에서 로그를 분석하십시오. 자세한 정보는 [Kibana의 고급 로그 분석](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)을 참조하십시오.

    **참고:** 필드가 올바른 JSON으로 판별되면 구문 분석되고 여기에서 새 필드가 작성됩니다. Kibana에서 필터링하고 정렬하는 데 문자열 유형 필드 값만 사용할 수 있습니다.
    
    표시된 @timestamp 필드 값은 ElasticSearch에서 로그 항목을 수신했을 때의 시간소인에 해당합니다. 로그 항목이 컨테이너에서 생성되었을 때를 반영하는 시간소인이 메시지 필드의 일부로 표시됩니다.
    


