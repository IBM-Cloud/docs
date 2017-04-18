---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana 대시보드 내보내기 및 공유
<!-- for example, Uploading your data -->
{: #exporting_sharing_kibana_dash}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

대시보드 스키마를 JSON 파일로 내보내거나 로그 데이터의 사용자 정의된 Kibana 대시보드에 대한 URL을 공유하십시오.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Kibana에서는 대시보드를 JSON 파일로 내보내거나 대시보드의 URL을 공유하여 다른 이해 당사자(stakeholder)와 협업할 수 있습니다.

다음 태스크를 수행하여 Kibana 대시보드를 JSON 파일로 내보내십시오.

1. **저장** 아이콘 ![저장 아이콘](images/logging_save.jpg)을 클릭한 다음 **고급** **>** **스키마 내보내기**를 클릭하십시오.

    ![대시보드를 JSON 파일로 내보내기](images/logging_export_json.jpg)

2. JSON 파일의 의미 있는 이름을 선택한 다음 **저장**을 클릭하십시오. 이 JSON 파일을 사용하는 모든 사용자는 Kibana 대시보드에서 파일을 열 수 있습니다. 

다음 태스크를 수행하여 Kibana 대시보드에 대한 URL을 작성하고 공유하십시오.

1. Kibana 대시보드에서 **폴더**아이콘 ![폴더 아이콘](images/logging_folder.jpg)을 클릭하여 최근의 대시보드를 모두 나열하는 메뉴를 표시하십시오. 사용자가 이름으로 저장한 대시보드 외에 메뉴에는 *ALCH_TENANT_ID_application_id* 형식에 따라 이름이 지정되지 않은 대시보드가 나열됩니다. 

    ![대시보드 목록](images/logging_list_of_dashboards.jpg)

2. 공유할 대시보드에 대해 **공유** 아이콘 ![공유 아이콘](images/logging_create_url.jpg)을 클릭하십시오. 공유 가능한 URL이 작성되고 표시됩니다. 

    ![공유 가능한 URL 분할창](images/logging_shareable_link_popup.jpg)

    URL을 복사하여 다른 사용자와 대시보드를 공유하십시오. 대시보드로 돌아가려면 **닫기**를 클릭하십시오.
