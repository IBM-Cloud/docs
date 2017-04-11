---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Bluemix에서 모니터링
{: #monitoring_bmx_ov}

{{site.data.keyword.Bluemix_notm}}는 기본적으로 CPU 사용량, 메모리 사용률 및 네트워크 I/O에 대한 성능 메트릭을 수집하고 표시합니다. 이러한 메트릭은 개별 클라우드 리소스의 성능에 대한 정보를 제공합니다. {{site.data.keyword.Bluemix_notm}} UI를 통해 클라우드 환경에서 이러한 리소스의 성능을 모니터링할 수 있습니다. 거의 실시간 데이터와 히스토리 데이터를 볼 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}}에서 모니터링 기능을 사용하여 사용자 환경 및 애플리케이션에서 키 메트릭을 자동으로 수집하고 측정할 수 있습니다. 메트릭 수집에 특수 인스트루먼테이션은 필요하지 않습니다. 예를 들어, 성능 메트릭에서 제공된 정보를 사용하여 클라우드에서 서비스가 실행되는 방식을 모니터링하고 병목 현상을 발견하고 SLA(Service Level Agreement)를 계속 확인할 수 있습니다. 서비스에 대한 성능 데이터를 분석하는 경우 리소스 병목 현상을 발생시키고 그 결과 클라이언트에 대한 서비스 SLA에 영향을 줄 수 있는 상황을 발견할 수 있습니다. 빠른 조치를 수행하여 비즈니스에 부정적인 영향을 줄 수 있는 상황을 방지할 수 있습니다.  

또한 추가 성능 메트릭을 구성하고 모니터링할 수 있습니다. {{site.data.keyword.Bluemix_notm}} 외부에서 이러한 메트릭을 시각화하고 분석할 수 있습니다. 예를 들어, {{site.data.keyword.containershort}}에서 앱을 실행하는 경우 Grafana를 사용하여 추가 메트릭을 모니터링할 수 있습니다. 성능 데이터를 시각화하고 분석하는 영역마다 또는 컨테이너 인스턴스마다 대시보드를 사용자 정의할 수 있습니다.

![{{site.data.keyword.Bluemix_notm}}에서 실행되는 컨테이너의 Grafana 모니터링 보기](images/monitoring_default_container_grafana_view.jpg)

{{site.data.keyword.Bluemix_notm}} 플랫폼 모니터링을 사용하여 다음을 수행할 수 있습니다.

* 잠재적 병목 현상 발견 또는 업그레이드가 필요한 시점 등과 같이 애플리케이션 운영에 대한 통찰력을 얻습니다. 
* 클라우드 플랫폼에서 향후 앱 요구사항을 계획하는 데 사용할 수 있는 상태동향을 정의합니다.

Cloud Foundry에서 실행되는 앱 모니터링에 대한 자세한 정보는 [Cloud Foundry에서 실행되는 앱 모니터링](monitoring_cf_apps.html#monitoring_bluemix_apps)을 참조하십시오.

{{site.data.keyword.containershort}}에서 모니터링에 대한 자세한 정보는 [{{site.data.keyword.containershort}}에서 모니터링](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor)을 참조하십시오.   

