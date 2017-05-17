---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana 3에서 로그 분석(더 이상 사용되지 않음)
{: #analyzing_logs_Kibana3}

{{site.data.keyword.Bluemix}}에서 오픈 소스 분석 및 시각화 플랫폼인 Kibana를 사용하여 데이터를 모니터링하고 검색하고 분석하고 다양한 그래프(예: 차트와 테이블)로 시각화할 수 있습니다. Kibana를 사용하여 고급 분석 태스크를 수행하십시오.
{:shortdesc}

다음 방법 중 하나로 Kibana를 실행할 수 있습니다.

* Cloud Foundary 앱 대시보드에서

    Kibana에서 특정 앱에 대한 컨텍스트로 특정 CF앱 로그를 시작할 수 있습니다.
    
    대시보드에 표시되는 데이터를 필터링하는 데 사용되는 조회는 Cloud Foundry 애플리케이션의 로그 항목을 검색합니다. Kibana 대시보드가 기본적으로 표시하는 로그 정보는 단일 Cloud Foundry 애플리케이션 및 모든 인스턴스와 관련되어 있습니다. 자세한 정보는 [Bluemix 대시보드에서 Kibana 대시보드 시작](logging_view_kibana3.html#launch_Kibana_from_bluemix)을 참조하십시오.

* 직접 브라우저 링크에서

    제공된 {{site.data.keyword.Bluemix}} 영역 내 서비스의 데이터를 집계하는 사용자 정의 Kibana 대시보드를 시작할 수 있습니다.
    
    대시보드에 표시되는 데이터를 필터링하는 데 사용되는 조회는 {{site.data.keyword.Bluemix}} 조직에서 영역의 로그 항목을 검색합니다. Kibana 대시보드가 표시하는 로그 정보에는 로그인한 {{site.data.keyword.Bluemix}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함됩니다. 자세한 정보는 [웹 브라우저에서 Kibana 대시보드 시작](logging_view_kibana3.html#launch_Kibana_from_browser)을 참조하십시오.
    
    또한 초기 조회를 변경하거나 제거하고 조회를 추가할 수 있습니다. 자세한 정보는 [Kibana에서 조회를 사용하여 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_query.html#logging_kibana_query)을 참조하십시오.


Kibana는 로그 데이터를 분석하고 고급 관리 태스크를 수행하는 데 사용할 수 있는 대시보드를 사용자 정의할 수 있는 브라우저 기반 인터페이스입니다. 

{{site.data.keyword.Bluemix}}에서 각 Cloud Foundry 앱에 그리고 조직의 각 영역에 사용 가능한 기본 Kibana 대시보드를 사용하여 데이터를 분석할 수 있습니다. 기본적으로 이러한 대시보드는 히스토그램 행 및 이벤트 행의 테이블이 포함된 패널을 통해 마지막 24시간 동안에 사용 가능한 모든 데이터를 표시합니다. 

기본 대시보드를 통해 표시되는 정보를 제한하기 위해 기본 대시보드에 조회 및 필터를 추가할 수 있습니다. 그런 다음 나중에 다시 사용할 대시보드를 저장할 수 있습니다. 

Kibana 대시보드에 표시되는 데이터는 조회를 통해 제어됩니다. 대시보드에 표시되는 정보를 수정하기 위해 조회를 변경하고 복수 조회를 추가한 다음 대시보드를 저장할 수 있습니다. 복수 대시보드를 동시에 사용자 정의하고 저장하고 공유할 수 있습니다. 이는 예를 들어 Kibana가 사용자 영역에 단일 앱에 대한 정보를 표시하는 방법입니다.

또한 로그 필드(예: message_type 및 instance_ID)에서 필터를 구성할 수 있습니다. 자세한 정보는 [Kibana 로그 형식](logging_view_kibana3.html#kibana_log_format_cf)을 참조하십시오. 이 필터를 동적으로 사용 또는 사용 안함으로 설정할 수 있습니다. 대시보드에 사용으로 설정한 조회 및 필터링 기준을 충족하는 로그 항목이 표시됩니다. 자세한 정보는 [Kibana 대시보드에서 데이터 필터링](logging_view_kibana3.html#filter_data_kibana_dashboard)을 참조하십시오.

데이터를 시각화하기 위해 패널을 구성할 수 있습니다. Kibana에는 정보를 분석하는 데 사용할 수 있는 테이블, 상태동향 및 히스토그램과 같은 여러 패널이 포함됩니다. 대시보드에서 패널을 추가하고 제거하고 다시 배열할 수 있습니다. 각 패널의 목적은 서로 다릅니다. 일부 패널은 하나 이상의 조회 결과를 제공하는 행으로 구성됩니다. 나머지 패널은 문서 또는 사용자 정의 정보를 표시합니다. 자세한 정보는 [Kibana 대시보드 사용자 정의](logging_view_kibana3.html#customize_kibana_dashboard)를 참조하십시오.

대시보드를 사용자 정의한 후 다음 조치 중 하나를 선택할 수 있습니다.

* 나중에 다시 사용할 대시보드를 저장할 수 있습니다. 자세한 정보는 [Kibana 대시보드 저장](logging_view_kibana3.html#save_Kibana_dashboard)을 참조하십시오.

* Kibana 대시보드에 대한 직접 링크를 내보내거나 다른 사용자와 공유할 수 있습니다. 자세한 정보는 [Kibana 대시보드 내보내기 및 공유](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash)를 참조하십시오.

* 웹 페이지에 대시보드를 임베드할 수 있습니다. 임베디드 대시보드를 보려는 사용자에게는 Kibana에 액세스할 수 있는 권한이 있어야 합니다.

자세한 정보는 [Kibana ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window} 문서를 참조하십시오.

**참고:** Kibana 4와 Kibana 3이 지원됩니다. Kibana 3은 더 이상 사용되지 않습니다.


##  Bluemix 대시보드에서 Kibana 대시보드 시작
{: #launch_Kibana_from_bluemix}

대시보드에 표시되는 데이터를 필터링하는 데 사용되는 조회는 Cloud Foundry 애플리케이션의 로그 항목을 검색합니다. Kibana 대시보드가 기본적으로 표시하는 로그 정보는 단일 Cloud Foundry 애플리케이션 및 모든 해당 인스턴스와 관련되어 있습니다.

Kibana에서 Cloud Foundry 애플리케이션의 로그를 보려면 다음 단계를 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 다음 {{site.data.keyword.Bluemix_notm}} **앱** 대시보드에서 앱 이름을 클릭하십시오.앱 세부사항 페이지가 열립니다.
    
2. 탐색줄에서 **로그**를 클릭하십시오. 로그 탭이 열립니다. 
    
3. **고급 보기**를 클릭하십시오. **Kibana 3** 대시보드가 열립니다.

로그가 표시되지 않는 경우 헤더에서 시간 선택도구를 조정하십시오. 

Kibana 대시보드 사용자 정의에 대한 자세한 정보는 [이 블로그 포스트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} 또는 [Kibana ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window} 문서를 참조하십시오.

##  웹 브라우저에서 Kibana 대시보드 시작
{: #launch_Kibana_from_browser}

대시보드에 표시되는 데이터를 필터링하는 데 사용되는 조회는 {{site.data.keyword.Bluemix}} 조직에서 영역의 로그 항목을 검색합니다. Kibana 대시보드에 표시되는 로그 정보에는 로그인한 {{site.data.keyword.Bluemix}} 조직의 영역 내에 배치된 모든 리소스에 대한 레코드가 포함됩니다.

브라우저에서 Kibana 대시보드를 열려면 다음 단계를 수행하십시오.

1. Kibana 사용자 인터페이스에 로그인하려면 [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName})을 여십시오. 

2. Kibana 3에 대한 작업을 수행하려면 **Kibana 3** 탭을 선택하십시오. Kibana 4에 대한 작업을 수행하려면 **Kibana 4** 탭을 선택하십시오. 기본 Kibana 대시보드가 열립니다. 

로그가 표시되지 않는 경우 헤더에서 시간 선택도구를 조정하십시오. 

Kibana 대시보드 사용자 정의에 대한 자세한 정보는 [이 블로그 포스트 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} 또는 [Kibana ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window} 문서를 참조하십시오.



## Kibana 대시보드에서 데이터 필터링
{: #filter_data_kibana_dashboard}

{{site.data.keyword.Bluemix}}에서 리소스마다 또는 {{site.data.keyword.Bluemix}} 영역에서 제공되는 기본 Kibana 대시보드를 사용하여 데이터를 분석할 수 있습니다. 기본적으로 이러한 대시보드는 마지막 24시간 동안 사용 가능한 데이터를 모두 표시합니다. 하지만 대시보드를 통해 표시되는 정보를 제한할 수 있습니다. 기본 대시보드에 조회 및 필터를 추가한 다음 나중에 사용하기 위해 저장할 수 있습니다.

대시보드에서 복수 조회 및 필터를 추가할 수 있습니다. 조회는 로그 항목의 서브세트를 정의합니다. 필터는 정보를 포함하거나 제외하여 데이터 선택사항을 세분화합니다. 

Cloud Foundry 앱의 경우 다음 목록에는 데이터 필터링 방법의 예가 간단하게 설명되어 있습니다.
* 핵심 용어를 포함한 로그 정보를 찾는 경우 해당 용어로 필터링하는 조회를 작성할 수 있습니다. Kibana를 사용하면 대시보드에서 시각적으로 조회를 비교할 수 있습니다. 자세한 정보는 [Kibana에서 조회를 사용하여 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_query.html#logging_kibana_query)을 참조하십시오.

* 특정 시간 범위 내에 정보를 찾는 경우 시간 범위 내에서 데이터를 필터링할 수 있습니다. 자세한 정보는 [Kibana에서 시간으로 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter)을 참조하십시오.

* 특정 인스턴스 ID에 대한 정보를 찾는 경우 인스턴스 ID로 데이터를 필터링할 수 있습니다. 자세한 정보는 [Kibana에서 인스턴스 ID로 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) 및 [Kibana에서 알려진 애플리케이션 ID로 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id)을 참조하십시오.

* 특정 컴포넌트에 대한 정보를 찾는 경우 컴포넌트(로그 유형)로 데이터를 필터링할 수 있습니다. 자세한 정보는 [Kibana에서 로그 유형으로 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter)을 참조하십시오.

* 오류 메시지와 같은 정보를 찾는 경우 메시지 유형으로 데이터를 필터링할 수 있습니다. 자세한 정보는 [Kibana에서 메시지 유형으로 Cloud Foundry 앱 로그 필터링](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter)을 참조하십시오.

## Kibana 대시보드 사용자 정의
{: #customize_kibana_dashboard}

데이터를 시각화하고 분석하기 위해 사용자 정의할 수 있는 여러 유형의 대시보드가 있습니다. 예를 들어, 다음과 같습니다.
* 단일 cf-app 대시보드: 이는 단일 Cloud Foundry 애플리케이션에 대한 정보가 표시된 대시보드입니다.  
* 다중 cf-app 대시보드: 동일한 {{site.data.keyword.Bluemix}} 영역에 배치된 모든 Cloud Foundry 애플리케이션에 대한 정보가 표시된 대시보드입니다. 

대시보드를 사용자 정의하는 경우 대시보드를 통해 표시할 로그 데이터의 서브세트를 선택하도록 조회와 필터를 구성할 수 있습니다.

데이터를 시각화하기 위해 패널을 구성할 수 있습니다. Kibana에는 정보를 분석하는 데 사용할 수 있는 테이블, 상태동향 및 히스토그램과 같은 여러 패널이 포함됩니다. 대시보드에서 패널을 추가하고 제거하고 다시 배열할 수 있습니다. 각 패널의 목적은 서로 다릅니다. 일부 패널은 하나 이상의 조회 결과를 제공하는 행으로 구성됩니다. 나머지 패널은 문서 또는 사용자 정의 정보를 표시합니다. 예를 들어, 데이터를 시각화하고 분석하기 위해 막대형 차트, 원형 차트 또는 테이블을 구성할 수 있습니다.  


## Kibana 대시보드 저장
{: #save_Kibana_dashboard}

Kibana 대시보드를 사용자 정의한 후 저장하려면 다음 단계를 수행하십시오.

1. 도구 모음에서 **저장** 아이콘을 클릭하십시오. 

2. 대시보드의 이름을 입력하십시오. 

    **참고:** 공백이 있는 이름의 대시보드는 저장되지 않습니다. 

3. 이름 필드 옆에 있는 **저장** 아이콘을 클릭하십시오. 



## Kibana 대시보드를 통해 로그 분석
{: #analyze_kibana_logs}

Kibana 대시보드를 사용자 정의한 후 해당 패널을 통해 데이터를 시각화하고 분석할 수 있습니다. 

정보를 검색하기 위해 조회를 고정시키거나 해제할 수 있습니다. 

* 대시보드에 조회를 고정시키면 검색이 자동으로 활성화됩니다.
* 대시보드에서 컨텐츠를 제거하기 위해 조회를 비활성화할 수 있습니다.

정보를 필터링하려면 필터를 사용 또는 사용 안함으로 설정할 수 있습니다. 

* 필터에서 **전환** 선택란 ![필터를 포함하는 전환 상자](images/logging_toggle_include_filter.jpg)을 선택하여 사용으로 설정할 수 있습니다.   
* 필터에서 **전환** 선택란 ![필터를 포함하는 전환 상자](images/logging_toggle_exclude_filter.jpg)을 선택 취소하여 사용 안함으로 설정할 수 있습니다. 

대시보드의 그래프와 차트에 데이터가 표시됩니다. 대시보드에 그래프와 차트를 사용하여 데이터를 모니터링할 수 있습니다. 

예를 들어, 단일 cf-app 대시보드의 경우 대시보드에 하나의 Cloud Foundry 애플리케이션에 대한 정보가 포함됩니다. 시각화하고 분석할 수 있는 데이터는 해당 앱으로 제한됩니다. 대시보드를 사용하여 앱의 모든 인스턴스에 대한 데이터를 분석할 수 있습니다. 인스턴스를 비교할 수 있습니다. 인스턴스 ID로 정보를 필터링할 수 있습니다. 

대시보드에 각 인스턴스 ID에 대한 조회를 정의하고 고정시킬 수 있습니다. 

![조회가 고정된 대시보드](images/logging_kibana_dash_activate_query.jpg)

그런 다음 대시보드에서 보려는 인스턴스 정보에 따라 개별 조회를 활성화하거나 비활성화할 수 있습니다. 

다음 그림은 활성화된 하나의 조회와 비활성화된 다른 조회를 표시합니다.

![조회가 고정된 대시보드](images/logging_kibana_dash_deactivate_query.jpg)

히스토그램에서 2개의 인스턴스를 비교하려는 경우 동일한 대시보드에서 두 개의 조회를 정의할 수 있습니다(각 인스턴스 ID에 하나씩). 조회에 별명 및 고유 색상을 제공하여 쉽게 식별할 수 있습니다. Kibana는 복수 조회를 논리 OR로 결합하여 처리합니다. 

다음 그림은 대시보드에 조회를 고정시키고 비활성화하기 위해 조회에 대한 별명 및 색상을 구성하도록 패널을 표시합니다.

![조회를 구성하는 대시보드 마법사](images/logging_kibana_query_def.jpg)



## Cloud Foundry 애플리케이션에 대한 Kibana 로그 형식
{: #kibana_log_format_cf}

각 로그 항목에 대한 다음 필드를 표시하도록 Kibana 대시보드를 구성할 수 있습니다.

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>로그된 이벤트의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다. </p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 리소스의 ID입니다.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>로그 문서의 고유 ID입니다.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>로그 항목의 색인입니다.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>로그 유형(예: <samp>syslog</samp>)입니다.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 애플리케이션의 이름입니다.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 애플리케이션의 고유 ID입니다.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>로그 데이터를 생성한 애플리케이션의 이름입니다.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>로그 데이터를 생성한 애플리케이션 인스턴스의 인스턴스 ID입니다.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>로그된 이벤트의 심각도입니다.</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>컴포넌트에서 발행하는 메시지. 메시지는 컨텍스트에 따라 달라집니다.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>로그 메시지가 기록되는 스트림. <samp class="ph codeph">OUT</samp>은 <samp class="ph codeph">stdout</samp> 스트림을 나타내고 <samp class="ph codeph">ERR</samp>은 <samp class="ph codeph">stderr</samp> 스트림을 나타냅니다. </p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 조직의 고유 ID입니다.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>앱이 스테이징된 {{site.data.keyword.Bluemix_notm}} 조직의 이름입니다.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>로그를 생성하는 컴포넌트. 다음 목록에서는 각 컴포넌트의 로그에 대해 설명합니다.</p>

<dl>
<dt><strong>API</strong></dt>
<dd>앱 상태 변경을 요청하는 API 호출에 대한 로그된 응답입니다.</dd>

<dt><strong>APP</strong></dt>
<dd>앱에서 로그된 응답입니다.</dd>

<dt><strong>CELL</strong></dt>
<dd>앱이 시작하거나 중지하거나 충돌할 때 표시되는 Diego 셀에서 로그된 응답입니다.</dd>

<dt><strong>LGR</strong></dt>
<dd>로깅 프로세스에 대한 문제점을 표시하는 lggregator에서 로그된 응답입니다.</dd>

<dt><strong>RTR</strong></dt>
<dd>HTTP 요청을 앱으로 라우트할 때 라우터에서 로그된 응답입니다.</dd>

<dt><strong>SSH</strong></dt>
<dd>사용자가 **cf ssh** 명령을 사용하여 앱 컨테이너에 액세스할 때 Diego 셀에서 로그된 응답입니다.</dd>

<dt><strong>STG</strong></dt>
<dd>앱이 스테이징되거나 다시 스테이징될 때 DEA(Droplet Execution Agent) 또는 Diego 셀에서 로그된 응답입니다.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>앱이 스테이징된 {{site.data.keyword.Bluemix_notm}} 영역의 이름입니다.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>로그된 이벤트의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다. </p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>로그 유형입니다(예: <samp>syslog</samp>).</p>
</dd>
</dl>




