---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Kibana에서 로그 유형으로 Cloud Foundry 앱 로그 필터링
{: #logging_kibana_component_filter}

Kibana 대시보드에서 {{site.data.keyword.Bluemix_notm}} 애플리케이션 로그를 보고 컴포넌트(로그 유형)로 필터링하십시오. Cloud Foundry 앱의 **로그** 탭에서 Kibana 대시보드에 액세스할 수 있습니다.
{:shortdesc}

다음 태스크를 수행하여 Kibana 대시보드에서 Cloud Foundry 앱 로그를 보고 로그 유형으로 필터링하십시오.

1. Cloud Foundry 앱의 **로그** 탭에 액세스하십시오. 

    1. {{site.data.keyword.Bluemix_notm}} **앱** 대시보드에서 앱 이름을 클릭하십시오.
    2. **로그** 탭을 클릭하십시오. 
    
    앱에 대한 로그가 표시됩니다.

2. 앱의 Kibana 대시보드에 액세스하십시오. **고급 보기**(![고급 보기 링크](images/logging_advanced_view.jpg "고급 보기 링크"))를 클릭하십시오. Kibana 대시보드가 표시됩니다.

3. **모든 이벤트** 창에서 오른쪽 화살표 아이콘을 클릭하여 모든 필드를 표시하십시오. 

    ![오른쪽 화살표가 있는 모든 이벤트 창 아이콘](images/logging_all_events_no_fields.jpg "오른쪽 화살표가 있는 모든 이벤트 창 아이콘")

4. **필드** 분할창에서 **source_id**를 선택하여 **모든 이벤트** 창에 각 로그 항목을 생성한 컴포넌트를 표시하십시오.

    ![source_id 필드가 선택된 모든 이벤트 창](images/logging_component.png "source_id 필드가 선택된 모든 이벤트 창")

5. **모든 이벤트** 창에서 로그 이벤트 행을 클릭하여 해당 이벤트의 세부사항을 표시하십시오. 필터링할 source_id가 표시된 이벤트를 선택하십시오.

    ![선택된 로그 이벤트에 대한 세부사항을 표시하는 모든 이벤트 창](images/logging_component_add_filter.png "선택된 로그 이벤트에 대한 세부사항을 표시하는 모든 이벤트 창")

6. 컴포넌트(로그 유형)에 대한 정보를 포함하거나 제외하는 필터를 추가하십시오. 

    * 컴포넌트 값을 포함하는 필터를 추가하려면 테이블의 source_id 행에서 **돋보기** ![돋보기 아이콘](images/logging_magnifying_glass.jpg "돋보기 아이콘") 아이콘을 클릭하십시오. 

        ![source_id 필드에 대한 필터 조건](images/logging_component_filter.png "source_id 필드에 대한 필터 조건") 

    * 컴포넌트 값을 제외하는 필터를 추가하려면 테이블의 source_id 행에 **제외** ![제외 아이콘](images/logging_exclusion_icon.png "제외 아이콘") 아이콘을 클릭하십시오. 
    
         ![source_id 필드를 제외하는 필터 조건](images/logging_component_add_exclusion_filter.png "source_id 필드를 제외하는 필터 조건") 
     
     새 필터 조건이 Kibana 대시보드에 추가됩니다.

7. 선택적으로, 이전 단계를 반복하고 각 컴포넌트에 필터를 추가할 수 있습니다. 전체 컴포넌트 목록은 [로그 형식](../logging_view_kibana3.html#kibana_log_format_cf)을 참조하십시오.

    다음 이미지에는 여러 컴포넌트에 대한 다중 필터가 있는 대시보드가 표시됩니다.
    
    ![source_id 필드의 여러 필터 조건](images/logging_component_multiple_filters.png "source_id 필드의 여러 필터 조건")

8. 대시보드를 저장하십시오. 

    필터 추가 및 대시보드 사용자 정의를 완료한 후 **저장** 아이콘(![저장 아이콘](images/logging_save.jpg "저장 아이콘"))을 클릭하고 대시보드의 이름을 입력하십시오. 
      
    **참고:** 공백이 있는 이름의 대시보드는 저장되지 않습니다. 공백이 없는 이름을 입력하고 **저장** 아이콘을 클릭하십시오.
    
    ![대시보드 이름 저장 ](images/logging_save_dashboard.jpg "대시보드 이름 저장")

컴포넌트(로그 유형)로 로그 항목을 필터링하는 대시보드를 작성했습니다. **폴더** 아이콘(![폴더 아이콘](images/logging_folder.jpg "폴더 아이콘"))을 클릭하고 이름으로 대시보드를 선택하여 언제든 저장된 대시보드를 로드할 수 있습니다.


