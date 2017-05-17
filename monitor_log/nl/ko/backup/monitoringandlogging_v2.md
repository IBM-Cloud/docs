---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 모니터링 및 로깅
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}}는 앱과 서비스 빌드, 실행 및 관리를 위한 {{site.data.keyword.IBM_notm}}의 클라우드 컴퓨팅 플랫폼입니다. {{site.data.keyword.Bluemix_notm}}는 PaaS(Platform as a Service)를 IaaS(Infrastructure as a Service)와 결합합니다. 또한 {{site.data.keyword.Bluemix_notm}}에는 비즈니스 애플리케이션을 빠르게 빌드하기 위해 PaaS와 IaaS와 쉽게 통합할 수 있는 클라우드 서비스의 강력한 카탈로그가 있습니다. {{site.data.keyword.Bluemix_notm}}에는 플랫폼 전체의 통합 로깅 및 모니터링 서비스가 포함됩니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}}는 Cloud Foundry 및 {{site.data.keyword.containershort}}와 같은 여러 컴퓨팅 서비스에 로깅 및 모니터링 서비스를 제공합니다. 일반적으로 앱 개발 및 실행과 연관된 인프라를 빌드하고 유지보수하지 않고도 모든 컴퓨팅 런타임에서 애플리케이션을 개발하고 실행하고 관리할 수 있습니다. 

**참고:** 모니터링 및 로깅 기능은 미국 남부 지역 및 영국 지역에서 사용 가능합니다.

{{site.data.keyword.Bluemix_notm}}에서 모니터링 기능을 사용하여 사용자 환경 및 애플리케이션에서 키 메트릭을 자동으로 수집하고 측정할 수 있습니다. 메트릭 수집에 특수 인스트루먼테이션은 필요하지 않습니다. 예를 들어, 성능 메트릭에서 제공된 정보를 사용하여 클라우드에서 서비스가 실행되는 방식을 모니터링하고 병목 현상을 발견하고 SLA(Service Level Agreement)를 계속 확인할 수 있습니다. 예를 들어, 서비스에 대한 성능 데이터를 분석하는 경우 리소스 병목 현상을 발생시키고 그 결과 클라이언트에 대한 서비스 SLA에 영향을 줄 수 있는 상황을 발견할 수 있습니다. 빠른 조치를 수행하여 비즈니스에 부정적인 영향을 줄 수 있는 상황을 방지할 수 있습니다.  

{{site.data.keyword.Bluemix_notm}}에서 로깅 기능을 사용하여 클라우드 플랫폼의 동작 및 이 플랫폼에서 실행되는 리소스를 파악할 수 있습니다. 특수 인스트루먼테이션은 표준 출력 및 표준 오류 로그를 수집하는 데 필요합니다. 예를 들어, 로그를 사용하여 애플리케이션에 대한 감사 추적을 제공하고, 서비스에서 문제점을 발견하고, 취약점을 식별하고, 앱 배치와 런타임 동작의 문제점을 해결하고, 앱이 실행되는 인프라에서 문제점을 발견하고, 클라우드 플랫폼의 컴포넌트에서 앱을 추적하고, 서비스 SLA에 영향을 줄 수 있는 조치를 예방하는 데 사용할 수 있는 패턴을 발견할 수 있습니다.

## 컴퓨팅 인프라 리소스 모니터링
{: #monitoring_sl_ov}

모든 {{site.data.keyword.Bluemix_notm}} 서버에 항상 사용 가능한 쉽게 읽을 수 있는 보고서와 모니터링이 포함됩니다. 자세한 정보는 [인프라 모니터링 및 보고 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}를 참조하십시오.


## 컴퓨팅 서비스에 대한 {{site.data.keyword.Bluemix}}의 모니터링
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}}는 기본적으로 CPU 사용량, 메모리 사용률 및 네트워크 I/O에 대한 성능 메트릭을 수집하고 표시합니다. 이러한 메트릭은 개별 클라우드 리소스의 성능에 대한 정보를 제공합니다. {{site.data.keyword.Bluemix_notm}} UI를 통해 클라우드 환경에서 이러한 리소스의 성능을 모니터링할 수 있습니다. 거의 실시간 데이터와 히스토리 데이터를 볼 수 있습니다.
 

또한 추가 성능 메트릭을 구성하고 모니터링할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 외부에서 이러한 메트릭을 시각화하고 분석할 수 있습니다. 예를 들어, {{site.data.keyword.containershort}}에서 앱을 실행하는 경우 Grafana를 사용하여 추가 메트릭을 모니터링할 수 있습니다. 성능 데이터를 시각화하고 분석하는 영역마다 또는 컨테이너 인스턴스마다 대시보드를 사용자 정의할 수 있습니다.

![{{site.data.keyword.Bluemix_notm}}에서 실행 중인 컨테이너의 Grafana 모니터링 보기](images/monitoring_default_container_grafana_view.jpg)

{{site.data.keyword.Bluemix_notm}} 플랫폼 모니터링을 사용하여 다음을 수행할 수 있습니다.

* 잠재적 병목 현상 발견 또는 업그레이드가 필요한 시점 등과 같이 애플리케이션 운영에 대한 통찰력을 얻습니다. 
* 클라우드 플랫폼에서 향후 앱 요구사항을 계획하는 데 사용할 수 있는 상태동향을 정의합니다.

Cloud Foundry에서 실행되는 앱 모니터링에 대한 자세한 정보는 [Cloud Foundry에서 실행되는 앱 모니터링](monitoring_cf_apps.html#monitoring_bluemix_apps)을 참조하십시오.

{{site.data.keyword.containershort}}에서 모니터링에 대한 자세한 정보는 [{{site.data.keyword.containershort}}에서 모니터링](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)을 참조하십시오.   

## {{site.data.keyword.Bluemix}}에서 로깅
{: #logging_bmx_ov}

{{site.data.keyword.Bluemix_notm}} 로깅 기능은 플랫폼에 통합되며 데이터 콜렉션이 클라우드 리소스에서 자동으로 사용됩니다. {{site.data.keyword.Bluemix_notm}}는 기본적으로 앱, 앱 런타임 및 해당 앱이 실행되는 컴퓨팅 런타임에 대한 로그를 수집하고 표시합니다.
 

클라우드에서 앱을 실행할 때 로그에 액세스하기 위해 앱이 실행되는 인프라에 SSH 또는 FTP로 접속할 수 없습니다(예: 앱이 Cloud Foundry에서 실행되는 경우). 반면에 {{site.data.keyword.Bluemix_notm}}에서 사용 가능한 다른 컴퓨팅 런타임인 {{site.data.keyword.containershort}}에서 앱을 실행할 수 있으며, 이 경우 SSH로 접속하여 로그에 액세스할 수 있습니다. 컴퓨팅 런타임에 관계없이 로그에 대한 액세스는 중요하며 {{site.data.keyword.Bluemix_notm}}는 공통 경험을 제공하여 클라우드 플랫폼에서 로그를 시각화하고 분석합니다.

{{site.data.keyword.Bluemix_notm}}는 Cloud Foundry 플랫폼 및 Cloud Foundry 애플리케이션에서 생성된 로그 데이터를 기록합니다. 로그에서 앱에 대해 생성된 오류, 경고 및 정보 메시지를 볼 수 있습니다. Cloud Foundry에 로깅에 대한 자세한 정보는 [{{site.data.keyword.Bluemix}}의 Cloud Foundry 앱에 대한 로깅](logging_cf_apps.html#logging_bluemix_cf_apps)을 참조하십시오.

{{site.data.keyword.Bluemix_notm}}는 {{site.data.keyword.containershort}}에서 생성된 로그 데이터를 기록합니다. {{site.data.keyword.containershort}}에 로깅에 대한 자세한 정보는 [{{site.data.keyword.containershort}}에 로깅](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs)을 참조하십시오.   


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


