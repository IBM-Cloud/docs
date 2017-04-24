---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix 대시보드에서 Kibana 대시보드 시작
{: #launch_Kibana_from_bluemix}

{{site.data.keyword.Bluemix}} UI에서 Kibana를 시작하여 Cloud Foundry 애플리케이션 또는 Docker 컨테이너의 특정 로그를 확인하십시오.
{:shortdesc}

Kibana에 표시된 데이터를 필터링하는 데 사용되는 조회를 통해 Kibana를 시작할 {{site.data.keyword.Bluemix_notm}} CF 앱 또는 컨테이너의 로그 항목을 검색합니다. 

Kibana에서 Cloud Foundry 애플리케이션 또는 Docker 컨테이너의 로그를 보려면 다음 단계를 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 다음 {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱 이름 또는 컨테이너를 클릭하십시오. 
    
2. {{site.data.keyword.Bluemix_notm}} UI에서 로그 탭을 여십시오.

    * CF 앱의 경우 탐색줄에서 **로그**를 클릭하십시오. 
    * 컨테이너의 경우 탐색줄에서 **모니터링 및 로그**를 선택한 다음 **로깅** 탭을 클릭하십시오. 
    
     로그 탭이 열립니다. 
    
3. **고급 보기**를 클릭하십시오. **Kibana 4** 대시보드가 열립니다.

    기본적으로 **검색** 페이지는 기본 색인 패턴이 선택되고 시간 필터가 지난 30초로 설정되어 로드됩니다. 검색 조회는 CF 앱 또는 Docker 컨테이너의 모든 항목과 일치하도록 설정됩니다.

    검색 페이지에서 로그 항목을 표시하지 않으면 시간 선택 도구를 조정하십시오. 자세한 정보는 [시간 필터 설정](logging_kibana_set_time_filter.html#set_time_filter)을 참조하십시오.

Kibana에 대한 자세한 정보는 [Kibana 사용자 안내서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}를 참조하십시오.

