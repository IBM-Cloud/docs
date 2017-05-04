---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 웹 브라우저에서 Kibana 대시보드 시작
{: #launch_Kibana_from_browser}

{{site.data.keyword.Bluemix}} 영역의 로그 항목을 분석해야 하는 경우 브라우저에서 Kibana를 시작하십시오.
{:shortdesc}

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
