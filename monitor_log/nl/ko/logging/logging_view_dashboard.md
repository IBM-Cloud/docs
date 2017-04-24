---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix 콘솔에서 로그 분석
{: #analyzing_logs_bmx_ui}

{{site.data.keyword.Bluemix}}에서 각 Cloud Foundry 앱 또는 Docker 컨테이너에 사용 가능한 로그 탭을 통해 로그를 보고 필터링하고 분석할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 퍼블릭에서는 통합 로깅 기능을 제공합니다. 예를 들어, CF(Cloud Foundry)에서 애플리케이션을 실행하는 경우 애플리케이션과 상호작용하는 시스템 컴포넌트의 로그 데이터, 애플리케이션에 대한 로그 데이터 및 stdout과 stderr를 사용하는 경우 애플리케이션 내 로그 데이터를 캡처합니다.


분석 및 로그 보존용 로그 데이터 사용 가능성에 대한 다음 정보를 고려하십시오.

* {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 로그 데이터는 기본적으로 7일 동안 저장됩니다.  
* 하루에 최대 1GB의 데이터를 저장할 수 있습니다. 
* 기본적으로 {{site.data.keyword.Bluemix_notm}} 콘솔에서 분석에 사용 가능한 로그에는 지난 24시간 동안의 데이터가 포함됩니다.

**팁:** 지난 24시간 이전의 사용자 정의 기간 동안 데이터를 분석하려면 [Kibana를 사용한 고급 로그 분석](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)을 참조하십시오. 

##  Cloud Foundry 앱의 로그 시작
{: #launch_logs_tab_bmx_ui_cf}

Cloud Foundry 앱의 배치 또는 런타임 로그를 보려면 다음 단계를 수행하십시오.

1. 앱 대시보드에서 Cloud Foundry 앱의 이름을 클릭하십시오. 
    
2. 앱 세부사항 페이지에서 **로그**를 클릭하십시오.
    
    **로그** 탭에서 앱에 대한 최신 로그를 보거나 실시간으로 추적 로그를 볼 수 있습니다. 또한 컴포넌트(로그 유형), 앱 인스턴스 ID 및 오류로 로그를 필터링할 수 있습니다.
    

##  Docker 컨테이너의 로그 시작
{: #launch_logs_tab_bmx_ui_containers}

Docker 컨테이너의 배치 또는 런타임 로그를 보려면 다음 단계를 수행하십시오.

1. 앱 대시보드에서 단일 컨테이너 또는 컨테이너 그룹을 클릭하십시오. 
    
2. 앱 세부사항 페이지에서 **모니터링 및 로그**를 클릭하십시오.

3. **로깅** 탭을 선택하십시오. 
    
    **로깅** 탭에서 컨테이너의 최신 로그를 보거나 실시간으로 추적 로그를 볼 수 있습니다. 

## CF 앱 로그의 로그 형식
{: #log_format_cf}

{{site.data.keyword.Bluemix_notm}} Cloud Foundry 앱의 로그는 다음 패턴과 유사하게 고정 형식으로 표시됩니다. 

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>/<var class="keyword varname">message</var>/<var class="keyword varname">timestamp</var></code>

각 로그 항목에는 다음 필드가 포함됩니다.

| 필드  | 설명 |
|-------|-------------|
| 시간소인 | 로그 명령문의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다.  |
| 컴포넌트 | 로그를 생성하는 컴포넌트입니다. 여러 다른 컴포넌트 목록은 [CF 앱의 로그 소스](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)를 참조하십시오. <br> 각 컴포넌트 유형 다음에는 슬래시와 애플리케이션 인스턴스를 표시하는 숫자가 옵니다. 0은 첫 번째 인스턴스에 할당된 숫자이고 1은 두 번째 인스턴스에 할당된 숫자이며 이와 같이 계속됩니다.  |
| 메시지 | 컴포넌트에서 발행하는 메시지. 메시지는 컨텍스트에 따라 달라집니다. |



## 컨테이너 로그의 로그 형식
{: #log_format_containers}

컨테이너의 로그는 다음 패턴과 유사하게 고정 형식으로 표시됩니다. 

<code><var class="keyword varname">timestamp</var>/<var class="keyword varname">machine</var>/<var class="keyword varname">message</var>  </code>

각 로그 항목에는 다음 필드가 포함됩니다.

| 필드  | 설명 |
|-------|-------------|
| 날짜/시간 | 로그 명령문의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다.  |
| 시스템 | 컨테이너가 실행 중인 호스트 이름입니다. |
| 메시지 | 발행된 메시지입니다. 메시지는 컨텍스트에 따라 달라집니다. |


