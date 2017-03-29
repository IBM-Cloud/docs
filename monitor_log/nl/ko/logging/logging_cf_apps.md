---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix에서 Cloud Foundry 앱에 대한 로깅
{: #logging_bluemix_cf_apps}

{{site.data.keyword.Bluemix}}에서 {{site.data.keyword.Bluemix}} 대시보드, Kibana 및 명령행 인터페이스를 통해 로그를 보고 필터링하고 분석할 수 있습니다. 또한 로그 레코드를 외부 로그 관리 도구로 스트리밍할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}}의 Cloud Foundry와 같은 클라우드 PaaS(Platform as a Service)에서 앱을 실행하는 경우 로그에 액세스하기 위해 앱이 실행되는 인프라에 SSH 또는 FTP로 접속할 수 없습니다. 클라우드 제공자가 플랫폼을 제어합니다. {{site.data.keyword.Bluemix_notm}}에서 실행되는 Cloud Foundry 앱은 Loggerator 컴포넌트를 사용하여 Cloud Foundry 인프라의 내부에서 로그 레코드를 전달합니다. Loggregator는 자동으로 STDOUT 및 STDERR 데이터를 선택합니다. {{site.data.keyword.Bluemix}} 대시보드, Kibana 및 명령행 인터페이스를 통해 이러한 로그를 시각화하고 분석할 수 있습니다.

다음 그림은 {{site.data.keyword.Bluemix_notm}}에서 Cloud Foundry 앱 로깅에 대한 상위 레벨 보기를 표시합니다.

![CF 앱에 대한 상위 레벨 컴포넌트 개요](images/logging_cf_apps_ov.jpg)
 
Cloud Foundry 인프라를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 앱을 실행하는 경우 Cloud Foundry 앱 로깅이 자동으로 사용됩니다. Cloud Foundry 런타임 로그를 보려면 STDOUT 및 STDERR에 로그를 기록해야 합니다. 자세한 정보는 [CF 앱을 통한 런타임 애플리케이션 로깅](cfapps/logging_writing_to_log_from_cf_app.html#logging_writing_to_log_from_cf_app)을 참조하십시오.

다음 방법 중 하나를 선택하여 Cloud Foundry 애플리케이션의 로그를 분석할 수 있습니다.

* {{site.data.keyword.Bluemix_notm}}에서 로그를 분석하고 애플리케이션의 최근 활동을 보십시오.
    
    {{site.data.keyword.Bluemix}}에서 각 Cloud Foundry 애플리케이션에서 사용 가능한 **로그** 탭을 통해 로그를 보고 필터링하고 분석할 수 있습니다. 자세한 정보는 [Bluemix 대시보드에서 CF 앱 로그 분석](logging_view_dashboard.html#analyzing_logs_bmx_ui)을 참조하십시오.
    
* Kibana에서 로그를 분석하여 고급 분석 태스크를 수행하십시오.
    
    {{site.data.keyword.Bluemix}}에서 Kibana, 즉 오픈 소스 분석과 시각화 플랫폼을 사용하여 데이터를 모니터링하고 검색하고 분석하고 다양한 그래프(예: 차트와 테이블)로 시각화할 수 있습니다. 자세한 정보는 [Kibana에서 로그 분석](logging_view_kibana3.html#analyzing_logs_Kibana)을 참조하십시오.

* CLI를 통해 로그를 분석하여 명령을 통해 프로그래밍 방식으로 로그를 관리하십시오.
    
    {{site.data.keyword.Bluemix}}에서 **cf logs** 명령을 사용하여 명령행 인터페이스를 통해 로그를 보고 필터링하고 분석할 수 있습니다. 자세한 정보는 [명령행 인터페이스를 통해 Cloud Foundry 앱 로그 분석](logging_view_cli.html#analyzing_logs_cli)을 참조하십시오.

{{site.data.keyword.Bluemix_notm}}는 제한된 양의 로그 정보를 보관합니다. 정보가 로깅되면 이전 정보는 새 정보로 바뀝니다. 감사 또는 다른 용도로 로그 정보의 일부 또는 모두 보관해야 하는 조직 또는 산업 정책을 따라야 하는 경우 써드파티 로그 관리 서비스 또는 기타 호스트와 같은 외부 로그 호스트로 로그를 스트리밍할 수 있습니다. 자세한 정보는 [외부 로그 호스트 구성](logging_view_external.html#viewing_logs_external)을 참조하십시오.



