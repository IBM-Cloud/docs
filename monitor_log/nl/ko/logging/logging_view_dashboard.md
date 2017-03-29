---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix 대시보드에서 CF 앱 로그 분석
{: #analyzing_logs_bmx_ui}

{{site.data.keyword.Bluemix}}에서 각 Cloud Foundry 애플리케이션에서 사용 가능한 **로그** 탭을 통해 로그를 보고 필터링하고 분석할 수 있습니다. {{site.data.keyword.Bluemix}} 대시보드를 사용하여 애플리케이션의 최근 활동을 보십시오.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 퍼블릭은 통합 로깅 서비스를 제공합니다. Cloud Foundry에서 애플리케이션을 실행하는 경우 로깅 서비스가 애플리케이션과 상호작용하는 시스템 컴포넌트의 로그 데이터, 애플리케이션에 대한 로그 데이터 및 stdout과 stderr를 사용하는 경우 애플리케이션 내 로그 데이터를 캡처합니다.

{{site.data.keyword.Bluemix_notm}} 애플리케이션에 대한 로그는 다음 패턴과 유사하게 고정 형식으로 표시됩니다. 

<code><var class="keyword varname">Component</var>/<var class="keyword varname">instanceID</var>     <var class="keyword varname">message</var>     <var class="keyword varname">timestamp</var></code>
   
로그 형식에 대한 자세한 정보는 [Cloud Foundry 앱 로그의 로그 형식](logging_view_dashboard.html#log_format_cf)을 참조하십시오.

**참고:** {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 로그 데이터는 기본적으로 7일 동안 저장됩니다. 하루에 최대 1GB의 데이터를 검색할 수 있습니다.



##  Bluemix 로그 탭 시작
{: #launch_logs_tab_bmx_ui}

Cloud Foundry 애플리케이션의 배치 또는 런타임 로그를 보려면 다음 단계를 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}}에 로그인한 다음 {{site.data.keyword.Bluemix_notm}} **앱** 대시보드에서 앱 이름을 클릭하십시오. 

    앱 세부사항 페이지가 표시됩니다.
    
2. 탐색줄에서 **로그**를 클릭하십시오.

    로그 탭이 열립니다. 
    
    **로그** 탭에서 앱에 대한 최신 로그를 보거나 실시간으로 추적 로그를 볼 수 있습니다. 또한 컴포넌트(로그 유형), 앱 인스턴스 ID 및 오류로 로그를 필터링할 수 있습니다.



## Cloud Foundry 앱 로그의 로그 형식
{: #log_format_cf}

모든 로그 항목에는 다음 필드가 포함됩니다.

<dl>
<dt><strong>시간소인</strong></dt>
<dd>
<p>로그 명령문의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다. </p>
</dd>

<dt><strong>컴포넌트</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>로그를 생성하는 컴포넌트입니다. </p>
<p>각 컴포넌트 유형 다음에는 슬래시와 애플리케이션 인스턴스를 표시하는 숫자가 옵니다. 0은 첫 번째 인스턴스에 할당된 숫자이고 1은 두 번째 인스턴스에 할당된 숫자이며 이와 같이 계속됩니다. 대시보드에서 하나의 앱 인스턴스만 볼 수 있도록 필터링할 수 있습니다.</p>
<p>다음 목록에는 여러 유형의 컴포넌트가 간단하게 설명되어 있습니다.</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: LGR 컴포넌트는 Cloud Foundry 내부의 로그를 전달하는 Cloud Foundry Loggregator에 대한 정보를 제공합니다.</dd>

<dt><strong>RTR</strong></dt>
<dd>라우터: RTR 컴포넌트는 애플리케이션에 대한 HTTP 요청 정보를 제공합니다.</dd>

<dt><strong>STG</strong></dt>
<dd>스테이징: STG 컴포넌트는 애플리케이션을 스테이징하거나 다시 스테이징하는 방법에 대한 정보를 제공합니다.</dd>

<dt><strong>APP</strong></dt>
<dd>애플리케이션: APP 컴포넌트는 애플리케이션의 로그를 제공합니다. 이는 코드의 stderr 및 stdout이 표시되는 위치입니다.
</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API: API 컴포넌트는 애플리케이션의 스테이지를 변경하는 사용자 요청의 원인이 되는 내부 조치에 대한 정보를 제공합니다.</dd>

<dt><strong>DEA</strong></dt>
<dd>DEA(Droplet Execution Agent): DEA 컴포넌트는 애플리케이션의 시작, 중지 또는 충돌에 대한 정보를 제공합니다.
<p>이 컴포넌트는 애플리케이션이 DEA를 기반으로 하는 Cloud Foundry 아키텍처에 배치된 경우에만 사용 가능합니다.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego 셀: CELL 컴포넌트는 애플리케이션 시작, 중지 또는 충돌에 대한 정보를 제공합니다.
<p>이 컴포넌트는 애플리케이션이 Diego를 기반으로 하는 Cloud Foundry 아키텍처에 배치된 경우에만 사용 가능합니다.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: SSH 컴포넌트는 **cf ssh** 명령을 사용하여 사용자가 애플리케이션에 액세스할 때마다 정보를 제공합니다.
<p>이 컴포넌트는 애플리케이션이 Diego를 기반으로 하는 Cloud Foundry 아키텍처에 배치된 경우에만 사용 가능합니다.</p></dd>

</dl>
</dd>

<dt><strong>메시지</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>컴포넌트에서 발행하는 메시지. 메시지는 컨텍스트에 따라 달라집니다.</p>
</dd>
</dl>

다음 그림은 DEA(Droplet Execution Agent)를 기반으로 하는 Cloud Foundry 아키텍처의 여러 컴포넌트(로그 유형)를 표시합니다.
![DEA 아키텍처의 로그 유형.](images/logging_F1.png "DEA(Droplet Execution Agent)를 기반으로 하는 Cloud Foundry 아키텍처의 컴포넌트.")



