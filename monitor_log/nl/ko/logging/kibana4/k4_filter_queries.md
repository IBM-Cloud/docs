---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 사용자 정의 검색 조회를 정의하여 로그 필터링
{:#k4_filter_queries}

검색 페이지의 검색 표시줄에서 Lucene 조회 언어를 사용하여 검색 조회를 정의하고 저장할 수 있습니다. 각 검색에 대해 필터를 적용하여 분석에 사용할 수 있는 항목을 세분화할 수 있습니다.
{:shortdesc}

사용자 정의 검색을 사용하여 로그를 필터링하려면 다음 태스크를 완료하십시오.

1. CF(Cloud Foundry) 앱 또는 컨테이너의 **로그** 탭에 액세스하십시오. 

    1. {{site.data.keyword.Bluemix}} 대시보드에서 앱 이름이나 컨테이너를 클릭하십시오.
    2. CF 애플리케이션의 경우 **로그** 탭을 클릭하십시오. 컨테이너의 경우 **모니터링 및 로그**를 클릭한 다음 **로깅** 탭을 선택하십시오.
    
    로그가 표시됩니다.

2. Kibana에 액세스하십시오. **고급 보기** ![고급 보기 링크](images/logging_advanced_view.jpg)를 클릭하십시오. Kibana 대시보드가 표시됩니다.

    Kibana에 액세스할 때 기본 검색이 적용됩니다. Kibana를 시작한 리소스의 인스턴스 목록에 대한 로그를 볼 수 있습니다. 해당 영역의 일부 또는 모든 {{site.data.keyword.Bluemix_notm}} 리소스에 대해 로그를 필터링할 수 있습니다.

Lucene의 경우 올바른 용어는 "키워드"가 아니라 "용어"입니다.

3. 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오. 그런 다음 항목을 필터링하도록 기본 조회를 수정하십시오.

    **참고:** Lucene 조회 언어를 사용하여 사용자 정의 조회를 정의하십시오. 자세한 정보는 [Apache Lucene - 조회 구문 분석기 구문 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}을 참조하십시오.
    
    {{site.data.keyword.Bluemix_notm}}에서 Kibana를 시작할 때 조회를 수정하고 여러 검색 기준을 정의하려면 논리 용어 **AND** 및 **OR**를 사용할 수 있습니다. 이 연산자는 대문자로 입력해야 합니다.    
    
    * 키워드 또는 키워드의 일부를 검색하려면 단어, 와일드카드 기호 \*를 차례로 입력하십시오(예: `Java*`). 
    * 특정 문구를 검색하려면 해당 문구를 큰따옴표 안에 입력하십시오(예: `"Java/1.8.0"`).
    * 복잡한 검색을 작성하기 위해 논리어 AND와 OR를 사용할 수 있습니다(예: `"Java/1.8.0" OR "Java/1.7.0"`).
    * 특정 필드 내에서 값을 검색하려면 *log_field_name:search_term* 양식으로 검색을 입력하십시오(예: `instance_id:"1"`).
    * 특정 로그 필드에 대한 값의 범위를 검색하려면 *log_field_name:[start_of_range TO end_of_range]* 양식으로 검색을 입력하십시오(예: `instance_id:["1" TO "2"]`).

     예를 들어, CF 앱의 경우 *0* 및 *1* 인스턴스의 항목만 나열하는 `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` 조회를 작성할 수 있습니다. 

4. 나중에 재사용할 수 있도록 조회를 저장하십시오. 자세한 정보는 [검색 저장](logging_kibana_filtering_logs.html#k4_save_search)을 참조하십시오. 

**참고:** 조회를 삭제해야 하는 경우 [검색 삭제](logging_kibana_filtering_logs.html#k4_delete_search)를 참조하십시오.



