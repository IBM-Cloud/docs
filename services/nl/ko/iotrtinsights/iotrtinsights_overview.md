---

copyright:
  years: 2015,2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.iotrtinsights_short}} 정보
{: #iotrtinsights_overview}
*마지막 업데이트 날짜: 2016년 2월 11일*

{{site.data.keyword.iotrtinsights_short}}는 IoT 디바이스 데이터의 컨텍스트화 및 모니터링을 실현하는 분석 작성 기능과 실시간 분석 엔진을 제공하고, 현재 상황을 빠르게 이해할 수 있게 하며, 발생하는 문제에 대한 응답과 의사결정 능력을 개선합니다.
{:shortdesc}

## {{site.data.keyword.iotrtinsights_full}}
{: #iotrtinsights_concept}
{{site.data.keyword.iotrtinsights_short}}는 단순 규칙 기반의 컴포지션 모델 및 확장 가능한 프레임워크를 통해 사용자가 IoT(Internet of Things) 데이터를 활용하고, 이러한 데이터를 마스터 자산 데이터와 결합하며, 상황에 맞게 현재 상태를 분석하고, 응답을 자동화하여 운영, 가용성, 서비스 레벨을 개선하도록 도와줍니다. 

{{site.data.keyword.iotrtinsights_short}}는 실시간 디바이스 데이터 피드를 위해 {{site.data.keyword.bluemix}} Internet of Things({{site.data.keyword.iot_short}}) 서비스에 연결합니다. 수신 데이터는 IBM Maximo&reg; Asset Management와 같은 자산 관리 시스템의 자산 마스터 데이터로 보강될 수 있는 가상 데이터 모델을 통해 해석됩니다. 

또한 주의가 필요한 상황을 식별하기 위해 사용자 정의 규칙이 실시간 스트리밍 데이터에 적용됩니다. 조치 엔진을 통해 사용자는 이메일 발송, IFTTT 레시피 트리거, Node-RED 워크플로우 실행 또는 다양한 웹 서비스 연결을 위한 웹훅 사용 등 발견된 상황에 대한 자동화된 응답을 정의할 수 있습니다.   

마지막으로, 실시간 데이터는 사용자의 IoT 디바이스에 대한 위치, 데이터, 메트릭, 경보를 한 눈에 볼 수 있는 구성이 가능한 대시보드에도 표시됩니다. 

![ {{site.data.keyword.iotrtinsights_short}} 아키텍처.](images/iota.svg "{{site.data.keyword.iotrtinsights_short}} 아키텍처")
