---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Kibana 대시보드로 이동
{: #k4_launch}

{{site.data.keyword.Bluemix}} UI에서 또는 웹 브라우저에서 직접 Kibana를 실행할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}}에서 Kibana를 실행하여 Kibana를 실행하는 리소스에 대한 컨텍스트에서 데이터를 보고 분석하십시오. 예를 들어, 특정 앱에 대한 컨텍스트에서 Kibana의 특정 CF 앱 로그를 실행하거나 특정 컨테이너에 대한 컨텍스트에서 Kibana의 특정 Docker 컨테이너 로그를 실행할 수 있습니다. 
    
제공된 {{site.data.keyword.Bluemix_notm}} 영역 내 서비스에서 수집된 로그 데이터를 보려면 직접 브라우저 링크에서 Kibana를 실행하십시오. 대시보드에 표시되는 데이터를 필터링하는 데 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역의 로그 항목을 검색합니다. Kibana에 표시되는 로그 정보에는 로그인한 {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함됩니다. 

Kibana에 대한 자세한 정보는 [Kibana 사용자 안내서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}를 참조하십시오.
    

##  Bluemix 대시보드에서 Kibana 대시보드로 이동
{: #launch_Kibana_from_bluemix}

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


##  웹 브라우저에서 Kibana 대시보드로 이동
{: #launch_Kibana_from_browser}

Kibana에 표시되는 데이터를 필터링하는 데 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역의 로그 항목을 검색합니다. Kibana에 표시되는 로그 정보에는 로그인한 {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함됩니다.

브라우저에서 Kibana를 시작하려면 다음 단계를 완료하십시오.

1. Kibana 사용자 인터페이스에 로그인하려면 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})을 여십시오. 

2. 로그를 분석하는 데 사용할 Kibana의 버전을 선택하십시오.
    * **Kibana 4** 탭을 선택하여 Kibana 4로 작업하십시오. 검색 페이지가 열립니다. 자세한 정보는 [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)를 참조하십시오.
    * **Kibana 3** 탭을 선택하여 Kibana 3으로 작업하십시오. 기본 Kibana 대시보드가 열립니다. Kibana 3을 사용하여 로그를 분석하는 데 대한 정보는 [Kibana 3에서 로그 분석(더 이상 사용되지 않음)](../logging_view_kibana3.html#analyzing_logs_Kibana3)을 참조하십시오. Kibana 3 대시보드 사용자 정의에 대한 자세한 정보는 [이 블로그 포스트 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)를 참조하십시오.
     
        **참고:** Kibana 3은 더 이상 사용되지 않습니다.

    검색 페이지에서 로그 항목을 표시하지 않으면 시간 선택 도구를 조정하십시오. 자세한 정보는 [시간 필터 설정](logging_kibana_set_time_filter.html#set_time_filter)을 참조하십시오.


