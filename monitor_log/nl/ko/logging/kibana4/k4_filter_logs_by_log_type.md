---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 로그 유형에 따라 로그 필터링
{:#k4_filter_logs_by_log_type}

로그 유형에 따라 {{site.data.keyword.Bluemix}} 로그를 보고 필터링하십시오.
{:shortdesc}

특정 로그 유형을 포함하는 항목을 검색하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

2. *필드 목록*에서 **type** 필드를 선택하십시오.

    예를 들어 다음 그림에서는 하나의 로그 유형(*syslog*)만 사용 가능합니다.
    
    ![필드 로그 유형을 표시하는 필터 목록](images/k4_filter_log_type_F1.jpg "필드 로그 유형을 표시하는 필터 목록")
   
3. 특정 로그 유형을 검색하는 필터를 추가하려면 분석하려는 로그 유형의 돋보기 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오.

    예를 들어, *syslog*의 로그 항목을 포함하는 필터를 추가하려면 *필드 목록* 섹션의 *syslog* 값에 사용 가능한 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 로그 유형 *syslog*의 항목을 포함하는 필터를 보여줍니다.

    ![syslog의 로그 유형 항목을 포함하는 필터](images/k4_filter_log_type_F2.jpg "syslog의 로그 유형 항목을 포함하는 필터")

    특정 로그 유형을 포함하지 않는 항목을 검색하는 필터를 추가하려면 값의 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "포함된 돋보기 단추")를 선택하십시오.

     예를 들어, *syslog*의 로그 항목을 제외하는 필터를 추가하려면 *필드 목록* 섹션의 *syslog* 값에 사용 가능한 돋보기 단추 ![제외 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "제외 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 로그 유형 *syslog*의 항목을 제외하는 필터를 보여줍니다.
     
     ![syslog의 로그 유형 항목을 제외하는 필터](images/k4_filter_log_type_F3.jpg "syslog의 로그 유형 항목을 제외하는 필터")



