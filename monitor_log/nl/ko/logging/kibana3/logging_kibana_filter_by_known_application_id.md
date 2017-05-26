---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana에서 알려진 애플리케이션 ID로 Cloud Foundry 앱 로그 필터링
{: #logging_kibana_known_application_id}

Cloud Foundry 앱의 애플리케이션 ID를 알고 있는 경우 Kibana 대시보드에서 신속하게 로그를 보고 앱의 애플리케이션 ID(application_id)로 필터링할 수 있습니다. Cloud Foundry 앱의 **로그** 탭에서 Kibana 대시보드에 액세스할 수 있습니다.
{:shortdesc}


다음 태스크를 수행하여 Kibana 대시보드에서 Cloud Foundry 앱 로그를 보고 알려진 애플리케이션 ID로 필터링하십시오.

1. Cloud Foundry 앱의 **로그** 탭에 액세스하십시오. 

    1. {{site.data.keyword.Bluemix_notm}} **앱** 대시보드에서 앱 이름을 클릭하십시오.
    2. **로그** 탭을 클릭하십시오. 
    
    앱에 대한 로그가 표시됩니다.

2. 앱의 Kibana 대시보드에 액세스하십시오. **고급 보기**(![고급 보기 링크](images/logging_advanced_view.jpg "고급 보기 링크"))를 클릭하십시오. Kibana 대시보드가 표시됩니다.

3. Kibana 대시보드에서 **폴더** 아이콘(![폴더 아이콘](images/logging_folder.jpg "폴더 아이콘"))을 클릭하여 최신 대시보드를 모두 나열하는 메뉴를 표시하십시오.  

    **참고:** 이름으로 저장한 대시보드 외에 메뉴에는 *ALCH_TENANT_ID_application_id* 형식으로 이름이 지정되지 않은 대시보드가 나열됩니다. 

    ![대시보드 목록](images/logging_list_of_dashboards.jpg "대시보드 목록")

4. 알려진 application_id가 포함된 이름의 대시보드를 선택하십시오. 

    대시보드는 application_id에 대해 필터링된 정보를 로드하고 표시합니다.

5. 선택적으로 필터 섹션에 필드(예: **instance_id**)를 추가하여 인스턴스 ID로 레코드 필터링을 사용 또는 사용 안함으로 설정할 수 있습니다. 
  
    1. **모든 이벤트** 창에서 로그 이벤트 행을 클릭하여 해당 이벤트의 세부사항을 표시하십시오. 
	
        ![선택된 로그 이벤트에 대한 세부사항을 표시하는 모든 이벤트 창](images/logging_selected_log_event.jpg "선택된 로그 이벤트에 대한 세부사항을 표시하는 모든 이벤트 창")
	
    2. 필터링할 필드 값이 표시된 이벤트를 선택하십시오.
	
    3. 필터를 추가하십시오.
    
        특정 필드 값에 대한 정보가 포함된 필터를 추가하려면 **돋보기** ![돋보기 아이콘](images/logging_magnifying_glass.jpg "돋보기 아이콘") 아이콘을 클릭하십시오. 
	
        특정 필드 값에 대한 정보를 제외하는 필터를 추가하려면 필터링할 필드가 포함된 테이블의 행에서 **제외** ![제외 아이콘](images/logging_exclusion_icon.png "제외 아이콘") 아이콘을 클릭하십시오.  

        새 필터 조건이 Kibana 대시보드에 추가됩니다.
	
	    ![instance_id 필드에 대한 필터 조건](images/logging_instance_id_filter.jpg "instance_id 필드에 대한 필터 조건")
	
6. 인식 가능한 이름으로 이 대시보드를 저장하십시오. 

    **저장** 아이콘(![저장 아이콘](images/logging_save.jpg "저장 아이콘"))을 클릭하고 대시보드의 이름을 입력하십시오. 

    **참고:** 공백이 있는 이름의 대시보드는 저장되지 않습니다. 공백이 없는 이름을 입력하고 **저장** 아이콘을 클릭하십시오.

    ![대시보드 이름 저장](images/logging_save_dashboard.jpg "대시보드 이름 저장").


애플리케이션 ID 및 인스턴스 ID로 로그 항목을 필터링하는 대시보드를 작성했습니다. **폴더** 아이콘(![폴더 아이콘](images/logging_folder.jpg "폴더 아이콘"))을 클릭하고 이름으로 대시보드를 선택하여 언제든 저장된 대시보드를 로드할 수 있습니다.
