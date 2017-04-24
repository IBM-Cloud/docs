---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 필드 값의 특정 텍스트에 맞게 로그 필터링
{:#k4_filter_logs_spec_text}

필드 값에 특정 텍스트를 포함하는 항목을 보고 검색하십시오.
{:shortdesc}

**주의사항:** Elasticsearch 분석기를 통해 분석된 문자열 필드의 자유 텍스트 검색만 수행할 수 있습니다. 
    
Elasticsearch에서 문자열 필드의 값을 분석하면, 유니코드 컨소시엄에서 정의한 대로 단어 경계에 따라 텍스트를 분할하고 구두점을 제거하며 모든 단어를 소문자로 지정합니다.
    
필드 값에 특정 텍스트가 포함되는 항목을 검색하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별]((logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

2. 기본적으로 ElasticSearch에서 분석되는 필드를 식별하십시오.

    로그 데이터를 검색하고 필터링하는 데 사용할 수 있는 분석된 전체 필드 목록을 표시하려면 [필드 목록을 다시 로드](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields)하십시오. 그런 다음 검색 페이지에서 사용할 수 있는 *필드 목록*에서 다음 단계를 완료하십시오.
    
    1. 구성 아이콘 ![구성 아이콘](images/k4_configure_icon.jpg "구성 아이콘")을 클릭하십시오. 필드를 필터링할 수 있는 **선택한 필드** 섹션이 표시됩니다.

        ![특정 속성이 있는 필드를 보여주는 구성 섹션](images/k4_reset_filters.jpg "특정 속성이 있는 필드를 보여주는 구성 섹션")
    
    2. 분석된 필드를 식별하려면 **분석됨** 검색 필드에 대해 **예**를 선택하십시오.

        ![분석된 속성](images/k4_reset_filters_analyze_options.jpg "분석된 속성")
    
        분석된 필드 목록이 표시됩니다.
    
        ![분석된 필드 목록](images/k4_list_analyzed_fields.jpg "분석된 필드 목록")
        
         
    3. 자유 텍스트를 검색하려는 필드가 기본적으로 ElasticSearch에서 분석하는 필드인지 확인하십시오.
    
3. 필드를 분석하는 경우 필드 값의 일부로 해당 자유 텍스트를 포함하는 로그에서 항목을 검색하도록 조회를 수정하십시오.

    
**예**

{{site.data.keyword.Bluemix}} UI에서 CF(Cloud Foundry) 애플리케이션의 Kibana를 시작하고 메시지 ID *CWWKT0016I:*를 포함하는 특정 메시지를 찾으려면 자유 텍스트를 포함하도록 검색을 수정하십시오.
    
1. 로드된 검색 조회 및 검색 페이지에 표시된 데이터를 확인하십시오.
       
    ![기본 검색 조회](images/k4_filter_by_text_default_query.jpg "기본 검색 조회")
        
2. 메시지 ID *CWWKT0016I*를 검색하려면 검색 조회를 수정하고 **Enter**를 누르십시오.
    
    ```
	application_id:f52f6016-3aab-4b5c-aa2e-5493747cb978 AND message:"CWWKT0016I:" 
	```
        
    ![조회 수정](images/k4_filter_by_text_modify_query.jpg "조회 수정")
      
    
*CWWKT0016I* 텍스트가 *메시지* 필드의 값 일부인 CF 앱의 항목이 테이블에 표시됩니다.
    
![새 검색 보기](images/k4_filter_by_text_result_query.jpg "새 검색 보기")     	
        
 
 
