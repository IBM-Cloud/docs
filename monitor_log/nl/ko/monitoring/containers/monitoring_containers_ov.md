---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# IBM Bluemix 컨테이너 서비스 모니터링
{: #monitoring_bmx_containers_ov}

{{site.data.keyword.Bluemix}}에서는 컨테이너 내부에 에이전트를 설치하고 유지보수하지 않아도 컨테이너 외부에서 자동으로 컨테이너 메트릭이 수집됩니다.
{:shortdesc}

컨테이너 내 에이전트는 컨테이너를 신속하게 작성 및 영구 삭제할 수 있는 auto-scaling 그룹과 오래 실행되지 않는 경량의 클라우드 인스턴스에 비하면 상당한 오버헤드와 설정 시간이 필요할 수 있습니다.
이러한 대역 외 데이터 수집 접근 방식은 이러한 어려운 문제점을 해결하고 사용자들이 모니터링해야 하는 부담을 없앱니다.

호스트에서 실행 중인 프로세스를 통해 에이전트 없이 메트릭 모니터링을 수행합니다. 크롤러라고도 하는 이 프로세스는 기본적으로 모든 컨테이너에서 다음 메트릭을 계속 수집합니다.

* CPU
* 메모리
* 네트워크 정보

메트릭 데이터는 Graphite에서 수집되어 {{site.data.keyword.Bluemix_notm}} UI와 Grafana에서 표시됩니다. 

{{site.data.keyword.Bluemix_notm}} UI에서 Grafana를 시작하거나 브라우저에서 직접 시작할 수 있습니다. 자세한 정보는 [Grafana에서 메트릭 분석](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana)을 참조하십시오.

Docker 규약과 그룹 계정 정보는 데이터를 모니터링하는 콜렉션의 기본 메커니즘으로 사용됩니다. 

**메트릭 보존**

분당 최대 한 개의 데이터 점이 수집됩니다. 7일 내에 작성되지 않은 컨테이너 메트릭은 삭제됩니다. 
    
**메트릭 정렬**

데이터는 컨테이너 ID별로 표시되고 정렬됩니다.  

명령행에서 `cf ic ps` 명령을 실행하여 개인용 {{site.data.keyword.Bluemix_notm}} 이미지 레지스트리에서 컨테이너의 컨테이너 ID 목록을 볼 수 있습니다.

