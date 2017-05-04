---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 메시지 유형에 따라 CF 앱 로그 필터링
{:#k4_filter_cf_logs_by_msg_type}

Kibana에서 메시지 유형에 따라 Cloud Foundry 로그를 보고 필터링할 수 있습니다.
{:shortdesc}


특정 메시지 유형을 포함하는 항목을 검색하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

2. *필드 목록*에서 **message_type** 필드를 선택하십시오.

    다음 그림은 CF 앱의 로그에 있는 *message_type* 필드의 값을 보여줍니다.
    
    ![message_type 필드를 보여주는 필터 목록](images/k4_filter_by_msg_type_f1.jpg "message_type 필드를 보여주는 필터 목록")     

3. 특정 *message_type*을 포함하는 항목을 검색하는 필터를 추가하려면 해당 값에 대해 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오.

    예를 들어, message_type 값이 *OUT*인 로그 항목을 포함하는 필터를 추가하려면 *필드 목록* 섹션의 *OUT* 값에 사용 가능한 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 message_type 값 *OUT*이 사용된 필터를 보여줍니다.
    
    ![필드 값을 포함하는 필터](images/k4_filter_by_msg_type_f2.jpg "필드 값을 포함하는 필터")

    특정 *message_type*을 포함하지 않는 항목을 검색하는 필터를 추가하려면 값의 돋보기 단추 ![제외 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "제외 모드의 돋보기 단추")를 선택하십시오.
    
    예를 들어, message_type *OUT*의 로그 항목을 제외하는 필터를 추가하려면 *필드 목록* 섹션의 *CELL* 값에 사용 가능한 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 message_type 값 *OUT*의 항목을 제외하는 필터를 보여줍니다.

    ![필드 값을 제외하는 필터](images/k4_filter_by_msg_type_f3.jpg "필드 값을 제외하는 필터")

