---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana로 고급 로그 분석
{:#analyzing_logs_Kibana}

{{site.data.keyword.Bluemix}}에서 오픈 소스 분석 및 시각화 플랫폼인 Kibana를 사용하여 데이터를 모니터링하고 검색하고 분석하고 다양한 그래프(예: 차트와 테이블)로 시각화할 수 있습니다. Kibana를 사용하여 고급 분석 태스크를 수행하십시오.
{:shortdesc}

다음 방법 중 하나로 Kibana를 실행할 수 있습니다.

* {{site.data.keyword.Bluemix_notm}}에서 다음을 수행할 수 있습니다.

    Kibana에서 특정 앱에 대한 컨텍스트로 특정 CF앱 로그를 시작할 수 있습니다.
    
    Kibana에서 특정 컨테이너에 대한 컨텍스트로 특정 Docker 컨테이너 로그를 시작할 수 있습니다. 
    
    CF 앱의 경우 Kibana에서 분석에 사용 가능한 데이터를 필터링하는 데 사용하는 조회를 통해 Cloud Foundry 애플리케이션의 로그 항목을 검색합니다. Kibana가 기본적으로 표시하는 로그 정보는 단일 Cloud Foundry 애플리케이션 및 모든 해당 인스턴스와 관련되어 있습니다. 
    
    컨테이너의 경우 Kibana에서 분석에 사용 가능한 데이터를 필터링하는 데 사용하는 조회를 통해 컨테이너의 모든 인스턴스에 대한 로그 항목을 검색합니다. Kibana가 기본적으로 표시하는 로그 정보는 단일 컨테이너나 컨테이너 그룹 및 모든 해당 인스턴스와 관련되어 있습니다. 
    
    자세한 정보는 [Bluemix 대시보드에서 Kibana 대시보드 시작](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)을 참조하십시오.

* 직접 브라우저 링크에서

    표시되는 데이터가 제공된 {{site.data.keyword.Bluemix_notm}} 영역 내의 서비스에서 로그를 집계하도록 Kibana를 시작할 수 있습니다.
    
    대시보드에 표시되는 데이터를 필터링하는 데 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역의 로그 항목을 검색합니다. Kibana에 표시되는 로그 정보에는 로그인한
    {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함됩니다. 
    
    자세한 정보는 [웹 브라우저에서 Kibana 대시보드 시작](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)을 참조하십시오.
    
    브라우저에서 Kibana를 시작할 때 Kibana 4 또는 Kibana 3으로 작업하도록 선택할 수 있습니다. **참고:** Kibana 3은 더 이상 사용되지 않습니다. Kibana 3을 사용하여 로그를 분석하는 데 대한 정보는 [Kibana 3에서 로그 분석(더 이상 사용되지 않음)](../logging_view_kibana3.html#analyzing_logs_Kibana3)을 참조하십시오.

<br>    

Kibana는 대화식으로 로그 데이터를 분석한 다음, 로그 데이터를 분석하고 고급 관리 태스크를 수행하는 데 사용할 수 있는 대시보드를 사용자 정의할 수 있는 브라우저 기반 인터페이스입니다. 

Kibana 페이지가 표시하는 데이터는 검색을 통해 제한됩니다. 기본 데이터 세트는 사전 구성된 색인 패턴으로 정의됩니다. 정보를 필터링하려면 새 검색 조회를 추가하고 기본 데이터 세트에 필터를 적용할 수 있습니다. 그런 다음 나중에 다시 사용하도록 검색을 저장할 수 있습니다. 

Kibana에는 로그를 분석하는 데 사용할 수 있는 다른 페이지가 포함되어 있습니다.

| Kibana 페이지 | 설명 |
|-------------|-------------|
| 검색 | 이 페이지를 사용하여 검색을 정의하고 테이블과 히스토그램을 통해 대화식으로 로그를 분석합니다. |
| 시각화 | 이 페이지를 사용하여 로그 데이터를 분석하고 결과를 비교하는 데 사용할 수 있는 그래프와 테이블 등의 시각화를 작성합니다.  |
| 대시보드 | 이 페이지를 사용하여 저장된 시각화와 검색의 콜렉션을 통해 로그를 분석합니다.  |

**참고:** 시각화 페이지 또는 대시보드 페이지를 통해 한 번에 하루 전체만 분석할 수 있습니다. 단, 7일 전까지 되돌아갈 수 있습니다. 로그 데이터는 기본적으로 7일 동안 저장됩니다. 

| Kibana 페이지 | 기간 정보 |
|-------------|-------------------------|
| 검색 | 최대 7일 동안의 데이터를 분석합니다. |
| 시각화 | 24시간 기간 동안의 데이터를 분석합니다. <br> 24시간을 경과하는 사용자 정의 기간 동안 로그 데이터를 필터링할 수 있습니다.  |
| 대시보드 | 24시간 기간 동안의 데이터를 분석합니다. <br> 24시간을 경과하는 사용자 정의 기간 동안 로그 데이터를 필터링할 수 있습니다.<br> 설정하는 시간 선택도구는 대시보드에 포함되는 모든 시각화에 적용됩니다. |


예를 들어, 다른 페이지를 통해 영역에 CF 앱 또는 컨테이너에 대한 정보를 표시하기 위해 Kibana를 사용하는 방법은 다음과 같습니다.

* 검색 페이지에서 새 검색 조회를 정의하고 조회당 필터를 적용할 수 있습니다. 로그 데이터는 테이블 및 히스토그램을 통해 표시됩니다. 이러한 시각화를 사용하여 대화식으로 데이터를 분석할 수 있습니다. 자세한 정보는 [Kibana에서 대화식으로 로그 분석](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)을 참조하십시오.

    로그 필드(예: message_type 및 instance_ID) 에서 필터를 구성하고 기간을 설정할 수 있습니다. 이러한 필터를 동적으로 사용 또는 사용하지 않게 설정할 수 있습니다. 사용으로 설정한 조회 및 필터링 기준을 충족하는 로그 항목이 테이블과 히스토그램에 표시됩니다. 자세한 정보는 [Kibana에서 로그 필터링](logging_kibana_filtering_logs.html#kibana_filtering_logs)을 참조하십시오.
    
* 시각화 페이지에서 새 검색 조회 및 시각화를 정의할 수 있습니다.

    데이터를 분석하기 위해 기존 검색 또는 새 검색을 기반으로 시각화를 작성할 수 있습니다. Kibana에는 정보를 분석하는 데 사용할 수 있는 테이블, 상태동향 및 히스토그램과 같은 여러 다른 유형의 시각화가 포함됩니다. 각 시각화의 목표는 서로 다릅니다. 일부 시각화는 하나 이상의 조회 결과를 제공하는 행으로 구성됩니다. 다른 시각화에서는 문서 또는 사용자 정의 정보를 표시합니다. 검색 조회가 업데이트되면 시각화의 데이터를 고치거나 변경할 수 있습니다. 웹 페이지에 시각화를 임베드하거나 공유할 수 있습니다. 자세한 정보는 [시각화를 사용하여 로그 분석](logging_kibana_visualizations.html#logging_kibana_visualizations)을 참조하십시오.

* 대시보드 페이지에서 여러 시각화 및 검색을 동시에 사용자 정의, 저장 및 공유할 수 있습니다. 

    대시보드에서 시각화를 추가하고 제거하고 다시 배열할 수 있습니다. 자세한 정보는 [대시보드를 통해 Kibana에서 로그 분석](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard)을 참조하십시오.
    
    Kibana 대시보드를 사용자 정의한 다음 시각화를 통해 데이터를 분석하고 나중에 재사용하기 위해 저장할 수 있습니다. 자세한 정보는 [Kibana 대시보드 저장](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard)을 참조하십시오.

Kibana에는 Kibana를 구성하고 검색, 시각화 및 대시보드를 저장, 삭제, 내보내기 및 가져오는 데 사용할 수 있는 *설정* 페이지도 있습니다.

자세한 정보는 [Kibana 사용자 안내서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}를 참조하십시오.

**참고:** Kibana 4와 Kibana 3이 지원됩니다. Kibana 3은 더 이상 사용되지 않습니다.


##  Bluemix 대시보드에서 Kibana 대시보드 시작
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

Kibana에 대한 자세한 정보는 [Kibana 사용자 안내서](https://www.elastic.co/guide/en/kibana/current/index.html)를 참조하십시오.

##  웹 브라우저에서 Kibana 대시보드 시작
{: #launch_Kibana_from_browser}

Kibana에 표시되는 데이터를 필터링하는 데 사용되는 조회는 {{site.data.keyword.Bluemix_notm}} 조직에서 영역의 로그 항목을 검색합니다. Kibana에 표시되는 로그 정보에는 로그인한
    {{site.data.keyword.Bluemix_notm}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함됩니다.

브라우저에서 Kibana를 시작하려면 다음 단계를 완료하십시오.

1. Kibana 사용자 인터페이스에 로그인하려면 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})을 여십시오. 

2. 로그를 분석하는 데 사용할 Kibana의 버전을 선택하십시오.
    * **Kibana 4** 탭을 선택하여 Kibana 4로 작업하십시오. 검색 페이지가 열립니다. 자세한 정보는 [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)를 참조하십시오.
    * **Kibana 3** 탭을 선택하여 Kibana 3으로 작업하십시오. 기본 Kibana 대시보드가 열립니다. Kibana 3 대시보드를 사용자 정의하는 데 대한 자세한 정보는 [이 블로그 게시물](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)을 참조하십시오.
     
        **참고:** Kibana 3은 더 이상 사용되지 않습니다.

    검색 페이지에서 로그 항목을 표시하지 않으면 시간 선택 도구를 조정하십시오. 자세한 정보는 [시간 필터 설정](logging_kibana_set_time_filter.html#set_time_filter)을 참조하십시오.

Kibana에 대한 자세한 정보는 [Kibana 사용자 안내서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}를 참조하십시오.

