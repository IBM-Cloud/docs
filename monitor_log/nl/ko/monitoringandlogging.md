{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#모니터링 및 로깅
{: #monitoringandlogging}

*마지막 업데이트 날짜: 2015년 12월 8일*

앱을 모니터링하고 로그를 검토하면서 애플리케이션 실행을 따라 가면 배치에 대해 더 잘 이해할 수 있습니다. 또한 문제를 찾아 이를 해결하는 데 드는 시간과 노력을 줄일 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix}} 애플리케이션은 넓게 배포되는 다중 인스턴스 애플리케이션으로, 애플리케이션의 실행과 이의 데이터를 다수의 서비스에서 공유할 수 있습니다. 이러한 복합 환경에서 앱을 모니터링하고 로그를 검토하는 것은 앱 관리에 중요합니다. 

{{site.data.keyword.Bluemix_notm}}에는 실행 중인 앱의 로그 파일을 생성하는 로깅 메커니즘이 기본 제공됩니다. 로그를 통해 사용자 앱에 대해 생성된 오류, 경고 및 정보 메시지를 확인할 수 있습니다. 또한 로그 메시지를 로그 파일에 기록하도록 앱을 구성할 수도 있습니다. 로그 형식 및 로그 보기 방법에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 앱 로깅](#logging_for_bluemix_apps)을 참조하십시오.

앱을 모니터링하면 앱 개발을 보고 제어할 수 있습니다. 모니터링을 사용하여 다음 태스크를 수행할 수 있습니다.

* 앱 인스턴스의 성능 정보를 수집 및 모니터링하고 이들이 작동 가능한지 확인합니다. 
* 잠재적 병목 현상 발견 또는 업그레이드가 필요한 시점 등과 같이 애플리케이션 운영에 대한 통찰력을 얻습니다. 
* 자원 사용량 및 비용을 예측합니다. 

{{site.data.keyword.Bluemix_notm}} 플랫폼에서 사용자의 배치를 안정적으로 운용하기 위해서는 문제점을 즉각 발견하여 원인을 효율적으로 판별하는 것이 좋습니다. 이를 위해서는 문제점 해결을 염두에 두고 앱을 개발하며 {{site.data.keyword.Bluemix_notm}}에 앱을 배치할 때 모니터링과 로깅을 위한 서비스나 도구를 사용하십시오. 

##Cloud Foundry에서 실행되는 앱 모니터링
{: #monitoring_bluemix_apps}

Cloud Foundry 인프라를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 앱을 실행하는 경우 작동 상태, 자원 사용량, 트래픽 메트릭 등 성능 정보를 받아보기를 원합니다. 이러한 성능 정보가 있으면 그에 맞게 의사 결정을 하거나 조치를 취할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} 앱을 모니터하려면 다음 방법 중 하나를 사용하십시오.

* {{site.data.keyword.Bluemix_notm}} 서비스. 모니터링 및 분석은 애플리케이션 성능을 모니터링할 때 사용할 수 있는 서비스를 제공합니다. 또한 이 서비스는 로그 분석과 같은 분석 기능도 제공합니다. 자세한 정보는 [Monitoring and Analytics](../services/monana/index.html)를
참조하십시오. 
* 써드파티 옵션. 예를 들어, [New Relic](http://newrelic.com/){:new_window}이 있습니다. 

##Cloud Foundry에서 실행되는 앱 로깅
{: #logging_for_bluemix_apps}

로그 파일은 Cloud Foundry 인프라를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 앱을 실행할 때 자동으로 작성됩니다. {{site.data.keyword.Bluemix_notm}} 대시보드 또는 명령행 인터페이스에서 로그를 볼 수 있습니다. 또한 관심있는 파트를 보기 위해 로그를 필터링할 수도 있습니다. 

###로그 형식
{: #log_format}

{{site.data.keyword.Bluemix_notm}} 애플리케이션에 대한 로그는 다음 패턴과 유사하게 고정 형식으로 표시됩니다. 

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

모든 로그 항목에는 네 개의 필드가 포함됩니다. 각 필드에 대한 간략한 설명은 다음 목록을 참조하십시오. 

<dl>
<dt><strong>시간소인</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>열: 1 - 27</p>
<p>로그 명령문의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다. </p>
</dd>

<dt><strong>컴포넌트</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>열: 29 - 40</p>
<p>로그를 생성하는 컴포넌트. 다음 목록에 모든 컴포넌트에 대한 정의가 제공됩니다. </p>

<dl>
<dt><strong>APP</strong></dt>
<dd>애플리케이션. 컴포넌트 APP 뒤에는 슬래시와 애플리케이션 인스턴스를 표시하는 숫자가 후속합니다. 0이 첫 번째 인스턴스인 경우 1이 두 번째가 되는 등입니다. </dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API</dd>

<dt><strong>DEA</strong></dt>
<dd>DEA(Droplet Execution Agent)</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator</dd>

<dt><strong>RTR</strong></dt>
<dd>라우터</dd>

<dt><strong>STG</strong></dt>
<dd>스테이징</dd>
</dl>
</dd>

<dt><strong>스트림</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>열: 42 - 44</p>
<p>로그 메시지가 기록되는 스트림. <samp class="ph codeph">OUT</samp>은 <samp class="ph codeph">stdout</samp> 스트림을 나타내고 <samp class="ph codeph">ERR</samp>은 <samp class="ph codeph">stderr</samp> 스트림을 나타냅니다. </p>
</dd>

<dt><strong>메시지</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>열: 46 - 행의 끝</p>
<p>컴포넌트에서 발행하는 메시지. 메시지는 컨텍스트에 따라 달라집니다.</p>
</dd>

</dl>

###로그 보기
{: #viewing_logs}

{{site.data.keyword.Bluemix_notm}} 대시보드 또는 명령행 인터페이스를 사용하여 로그를 볼 수 있습니다.

####{{site.data.keyword.Bluemix_notm}} 대시보드를 통해 로그 보기

**배치** 또는 **런타임** 로그를 확인하려면 다음 단계를 완료하십시오.
1. 앱의 타일을 클릭하십시오. 앱 세부사항 페이지가 표시됩니다.
2. 왼쪽 탐색줄에서 **로그**를 클릭하십시오.

####명령행 인터페이스를 통해 로그 보기

명령행 인터페이스를 통해 로그를 보려면 다음 옵션 중에서 선택하십시오. 

<ul>
<li>앱 배치 시 로그 추적
<p>**cf logs** 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}에 앱을 배치할 때 앱과 상호작용하는
시스템 컴포넌트 및 앱에서 로그를 표시합니다. cf 명령행 인터페이스에 다음 명령을 입력할 수 있습니다. cf 로그에 대한 자세한 정보는 [Log Types
and Their Messages in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}를 참조하십시오. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>가장 최신의 로그를 표시합니다. </dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>이 명령을 실행한 시점부터 생성된 로그를 표시합니다. </dd>
</dl>
<div class="note tip"><span class="tiptitle">팁:</span> 명령행 창에 <span class="keyword cmdname">cf push</span> 또는
<span class="keyword cmdname">cf start</span> 명령을 실행하는 경우, 다른 명령행 창에 <samp class="ph codeph">cf logs appname --recent</samp>를 입력하여
로그를 실시간으로 확인할 수 있습니다. </div>
</li>

<li>앱 배치 후 로그 보기
<p>애플리케이션 로깅이 사용되는 경우 런타임 시 앱에 문제가 발생하면 다음과 같은 애플리케이션 로그를 볼 수 있습니다. 애플리케이션 로그는 오류의 원인 판별에 도움이 됩니다. </p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>이 로그 파일은 디버깅을 위해 자세한 정보 이벤트를 기록합니다. 이 로그를 사용하여 빌드팩 실행 문제점을
해결할 수 있습니다. </p>
<p><span class="ph filepath">buildpack.log</span> 파일에 데이터를 생성하려면, 다음 명령을 입력하여 빌드팩 추적을 사용으로 설정해야 합니다.
   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>이 로그를 보려면 다음 명령을 입력하십시오.
<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>이 로그 파일은 스테이징 태스크의 주요 단계 후 메시지를 기록합니다. 이 로그를 사용하여 스테이징 문제점을
해결할 수 있습니다. </p>
<p>이 로그를 보려면 다음 명령을 입력하십시오.
<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**참고:** 애플리케이션 로깅 사용 방법에 대한 정보는 [런타임 오류 디버깅](../troubleshoot/debugging.html#debug_runtime)을 참조하십시오. 

###로그 필터링
{: #filtering_logs}

관심있는 로그를 보거나 보고 싶지 않은 컨텐츠를 제외하려면 cf 명령행 인터페이스에서 **cf logs** 명령을 필터링 옵션(예: **cut** 및 **grep**)과 함께 사용하십시오. 

* 전체적인 상세 로그 대신 일부분만 보려면 **cut** 옵션을 사용하십시오. 예를 들어, 컴포넌트 및 메시지 정보를 표시하려면 다음 명령을 사용하십시오.
```
cf logs appname --recent | cut -c 29-40,46- 
```

**grep** 옵션에 대한 자세한 정보를 보려면 cut --help를 입력하십시오. 
* 특정 키워드가 포함된 로그 항목을 표시하려면 **grep** 옵션을 사용하십시오. 예를 들어, [APP 키워드가 포함된 로그 항목을 표시하려면 다음 명령을 사용하십시오.
```
cf logs appname --recent | grep '\[App'
```
**grep** 옵션에 대한 자세한 정보를 보려면 `grep --help`를 입력하십시오. 

###써드파티 로깅 구성
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}}는 메모리에 제한된 양의 로그 정보를 보관합니다. 정보가 로깅되면
이전 정보는 새 정보로 바뀝니다.
로그 정보를 모두 보관하려면 써드파티 로그 관리 서비스에
로그를 저장할 수 있습니다. 

애플리케이션 및 시스템에서 써드파티 로그 관리 서비스로
로그를 스트림하려면 다음 단계를 수행하십시오.

1. 써드파티 로그 관리 서비스를 등록하십시오.
    
    Papertail, Splunk Storm, SumoLogic, Logentries 등
[syslog
프로토콜](http://tools.ietf.org/html/rfc5424){:new_window}을 지원하는 써드파티 로그 관리 서비스를 사용할 수 있습니다.
써드파티 로그 관리 서비스를 등록한 다음
{{site.data.keyword.Bluemix_notm}}에서 로그에 대한 대상을 제공하십시오.
구성을 완료한 후에는 일반적으로 서비스가 {{site.data.keyword.Bluemix_notm}}에서 로그에 대한 대상으로 syslog URL을 제공합니다. 써드파티 로그 관리 서비스를 구성하는 방법에 대한
자세한 정보는 [Configuring Selected Third-Party Log Management Services](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}를 참조하십시오. 

2. 사용자 제공 서비스 인스턴스를 작성하십시오.
	
	{{site.data.keyword.Bluemix_notm}}에서 써드파티 로그 관리 서비스로 로그를 스트림하려면
먼저 사용자 제공 서비스 인스턴스를 작성해야 합니다. 다음 명령을 사용하여 사용자 제공 서비스 인스턴스를 작성하십시오. 여기서, service_name은
사용자 제공 서비스 인스턴스의 이름이고 syslog_URL은 써드파티 로깅 서비스에서 가져온 URL입니다.
	
	```
	cf create-user-provided-service <service_name> -l <syslog_URL>
	```
	
3. 서비스 인스턴스를 애플리케이션에 바인딩하십시오.

	서비스 인스턴스를 애플리케이션에 바인딩하려면 다음 명령을 사용하십시오. 여기서, appname은 애플리케이션의 이름이고
service_name은 사용자 제공 서비스 인스턴스의 이름입니다.
	
	```
	cf bind-service appname <service_name>
	```
	
	그런 다음, 변경사항을 적용하기 위해 cf restage appname을 입력하여 애플리케이션을
다시 스테이징하라는 메시지가 표시됩니다. 로그가 생성되면 잠시 지연되었다가
써드파티 로그 관리 서비스에 유사한 메시지가 표시될 수 있습니다.


**참고:** 명령행 인터페이스에 표시된 로그는 syslog 형식이 아니며
써드파티 로그 관리 서비스에 표시된 메시지와 정확히 일치하지 않을 수 있습니다.
