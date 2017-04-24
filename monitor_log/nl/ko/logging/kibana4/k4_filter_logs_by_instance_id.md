---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 인스턴스 ID에 따라 로그 필터링
{:#k4_filter_logs_by_instance_id}

인스턴스 ID에 따라 {{site.data.keyword.Bluemix}} 로그를 보고 필터링하십시오.
{:shortdesc}

Kibana 대시보드에서 인스턴스 ID에 따라 로그를 보고 필터링하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

2. *필드 목록*에서 다음 필드 중 하나를 선택하여 특정 인스턴스 ID를 검색하십시오.

    * **instance_ID**: 이 필드에서는 Cloud Foundry 애플리케이션의 로그에서 사용할 수 있는 여러 다른 인스턴스 ID를 나열합니다. 
    * **instance**: 이 필드에서는 컨테이너 그룹용 모든 인스턴스의 여러 다른 GUID를 나열합니다. 

    예를 들어, 다음 그림은 CF 앱의 여러 다른 인스턴스 값을 보여줍니다.
    
    ![instance_id 필드를 보여주는 필터 목록](images/k4_filter_instanceid_f1.jpg "instance_id 필드를 보여주는 필터 목록")
   
3. 특정 로그 유형을 검색하는 필터를 추가하려면 분석하려는 로그 유형의 돋보기 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오.

   예를 들어, CF 앱 인스턴스 *2*의 항목을 포함하는 필터를 추가하려면 필드 목록 섹션의 값 *2*에 사용 가능한 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오. 다음 그림은 인스턴스 *2*의 항목을 포함하는 필터를 보여줍니다.
    
    ![인스턴스 2의 instance_id 항목을 포함하는 필터](images/k4_filter_instanceid_f2.jpg "인스턴스 2의 instance_id 항목을 포함하는 필터")

    특정 인스턴스 ID를 포함하지 않는 항목을 검색하는 필터를 추가하려면 값의 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "포함된 돋보기 단추")를 선택하십시오.

     예를 들어 CF 앱 인스턴스 *2*의 항목을 제외하는 필터를 추가하려면 필드 목록 섹션의 값 *2*에 사용 가능한 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "포함된 돋보기 단추")를 선택하십시오. 다음 그림은 인스턴스 *2*의 항목을 제외하는 필터를 보여줍니다.
     
      ![인스턴스 2의 instance_id 항목을 제외하는 필터](images/k4_filter_instanceid_f3.jpg "인스턴스 2의 instance_id 항목을 제외하는 필터")

