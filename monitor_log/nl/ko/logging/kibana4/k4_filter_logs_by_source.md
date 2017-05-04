---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 소스에 따라 CF 앱 로그 필터링
{:#k4_filter_logs_by_source}

Kibana 대시보드를 통해 소스 유형에 따라 Cloud Foundry 애플리케이션 로그를 보고 필터링하십시오.
{:shortdesc}

특정 로그 소스를 포함하는 항목을 검색하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

2. *필드 목록*에서 **source_id** 필드를 선택하십시오.

    ![source_id 필드를 보여주는 필터 목록](images/k4_filter_sourceid_F1.jpg "source_id 필드를 보여주는 필터 목록")     

3. 특정 source_id를 포함하는 항목을 검색하는 필터를 추가하려면 해당 값에 대해 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오.

    CF 앱에 사용 가능한 로그 소스 목록은 [CF 앱의 로그 소스](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)를 참조하십시오.

    예를 들어, CF 애플리케이션을 시작, 중지 또는 충돌하는 데 대한 로그 항목을 포함하는 필터를 추가하려면 *필드 목록* 섹션에 있는 *CELL* 값에 사용 가능한 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 source_id 값 *CELL*이 사용된 필터를 보여줍니다.
    
    ![필드 값을 포함하는 필터](images/k4_filter_sourceid_F2.jpg "필드 값을 포함하는 필터")

    특정 source_id를 포함하지 않는 항목을 검색하는 필터를 추가하려면 값의 돋보기 단추 ![제외 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "제외 모드의 돋보기 단추")를 선택하십시오.
    
    예를 들어, CF 애플리케이션을 시작, 중지 또는 충돌하는 데 대한 로그 항목을 제외하는 필터를 추가하려면 *필드 목록* 섹션에 있는 *CELL* 값에 사용 가능한 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 source_id 값 *CELL*의 항목을 제외하는 필터를 보여줍니다.

    ![필드 값을 제외하는 필터](images/k4_filter_sourceid_F3.jpg "필드 값을 제외하는 필터")




