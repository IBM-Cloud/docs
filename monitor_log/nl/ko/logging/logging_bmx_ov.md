---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-29"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix에서 로깅
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix}} 로깅 기능은 플랫폼에 통합되며 데이터 콜렉션이 클라우드 리소스에서 자동으로 사용됩니다. {{site.data.keyword.Bluemix_notm}}는 기본적으로 앱, 앱 런타임 및 해당 앱이 실행되는 컴퓨팅 런타임에 대한 로그를 수집하고 표시합니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}}에서 로깅 기능을 사용하여 클라우드 플랫폼의 동작 및 이 플랫폼에서 실행되는 리소스를 파악할 수 있습니다. 특수 인스트루먼테이션은 표준 출력 및 표준 오류 로그를 수집하는 데 필요합니다. 예를 들어, 로그를 사용하여 애플리케이션에 대한 감사 추적을 제공하고, 서비스에서 문제점을 발견하고, 취약점을 식별하고, 앱 배치와 런타임 동작의 문제점을 해결하고, 앱이 실행되는 인프라에서 문제점을 발견하고, 클라우드 플랫폼의 컴포넌트에서 앱을 추적하고, 서비스 SLA에 영향을 줄 수 있는 조치를 예방하는 데 사용할 수 있는 패턴을 발견할 수 있습니다.

클라우드에서 앱을 실행할 때 로그에 액세스하기 위해 앱이 실행되는 인프라에 SSH 또는 FTP로 접속할 수 없습니다(예: 앱이 Cloud Foundry에서 실행되는 경우). 반면에 {{site.data.keyword.Bluemix_notm}}에서 사용 가능한 다른 컴퓨팅 런타임인 {{site.data.keyword.containershort}}에서 앱을 실행할 수 있으며, 이 경우 SSH로 접속하여 로그에 액세스할 수 있습니다. 컴퓨팅 런타임에 관계없이 로그에 대한 액세스는 중요하며 {{site.data.keyword.Bluemix_notm}}는 공통 경험을 제공하여 클라우드 플랫폼에서 로그를 시각화하고 분석합니다.

{{site.data.keyword.Bluemix_notm}}가 제공하는 로깅 기능을 사용하여 다음을 수행할 수 있습니다.

* 클라우드 리소스 및 리소스 수행과 실행 방법을 파악합니다.
* 조치가 필요한 시나리오를 식별하는 데 도움이 되는 동향을 정의합니다.
* 예를 들어, 감사에 사용할 수 있는 앱에 대한 데이터 추적을 정의합니다.
* 앱에서 문제를 찾고 복구하는 데 필요한 시간과 노력을 줄입니다. 
* 클라우드 플랫폼에서 앱의 배치를 모니터링합니다.
* 서비스 또는 앱이 중단되거나 충돌할 때 이를 발견합니다.
* 애플리케이션 실행 및 데이터 플로우를 따릅니다.
* 앱에서 취약점을 식별합니다.
* 인프라에서 문제점을 발견합니다.
* 앱 런타임에서 문제점을 발견합니다.

## CF 앱에 대한 로깅
{: #logging_bmx_ov_cf}

{{site.data.keyword.Bluemix_notm}}는 Cloud Foundry 플랫폼 및 Cloud Foundry 애플리케이션에서 생성된 로그 데이터를 기록합니다. 로그에서 앱에 대해 생성된 오류, 경고 및 정보 메시지를 볼 수 있습니다. Cloud Foundry에서 로깅에 대한 자세한 정보는 [Bluemix에서 Cloud Foundry 앱에 대해 로깅](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps)을 참조하십시오.

## 컨테이너에 대한 로깅
{: #logging_bmx_ov_containers}

{{site.data.keyword.Bluemix_notm}}는 {{site.data.keyword.containershort}}에서 생성된 로그 데이터를 기록합니다. {{site.data.keyword.containershort}}의 로깅에 대한 자세한 정보는 [IBM Bluemix 컨테이너 서비스의 로깅](containers/logging_containers_ov.html#logging_containers_ov)을 참조하십시오.  

**참고:** {{site.data.keyword.IBM}} 관리 클라우드 인프라에 배치된 Docker 컨테이너의 {{site.data.keyword.Bluemix_notm}}에서 컨테이너 로그를 분석할 수 있습니다.

## Bluemix의 로그 분석
{: #logging_bmx_ov_ui}

{{site.data.keyword.Bluemix_notm}}에서 앱에 대한 최근 로그를 보거나 실시간으로 로그를 추적할 수 있습니다.

* UI를 통해 로그를 보고 필터링하고 분석할 수 있습니다. 자세한 정보는 [Bluemix 콘솔에서 로그 분석](logging_view_dashboard.html#analyzing_logs_bmx_ui)을 참조하십시오.

* 로그를 프로그래밍 방식으로 관리하기 위해 명령행을 사용하여 로그를 보고 필터링하고 분석할 수 있습니다. 자세한 정보는 [CLI에서 로그 분석](logging_view_cli.html#analyzing_logs_cli)을 참조하십시오.

## Kibana로 고급 로그 분석
{: #logging_bmx_ov_kibana}

{{site.data.keyword.Bluemix_notm}}에서 오픈 소스 분석 및 시각화 플랫폼인 Kibana를 사용하여 데이터를 모니터링하고 검색하고 분석하고 다양한 그래프(예: 차트와 테이블)로 시각화할 수 있습니다. 자세한 정보는 [Kibana의 고급 로그 분석](kibana4/analyzing_logs_Kibana.html#analyzing_logs_Kibana)을 참조하십시오.


