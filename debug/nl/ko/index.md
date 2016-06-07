---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# 디버깅
{: #debugging}

*마지막 업데이트 날짜: 2016년 3월 3일*

{{site.data.keyword.Bluemix}}에서 문제점이
발견된 경우 로그 파일을 확인하여 문제점을 조사하고 오류를 디버그할 수 있습니다.
{:shortdesc}

로그는 작업이 성공적으로 실행되었는지 또는 실패하였는지 등의 정보를 제공합니다.
또한 문제점을 디버그하고 문제점의 원인을 판별하는 데 사용할 수 있는 관련 정보도 제공합니다. 

로그 형식은 고정되어 있습니다. 상세 로그의 경우 로그를 필터링하거나 외부 로깅 호스트를 사용하여 로그를 저장하고 처리할 수 있습니다. 로그 형식, 로그 보기 및 필터링, 외부 로깅 구성에 대한 자세한 정보는 [Cloud Foundry에서 실행되는 앱 로깅](../monitor_log/monitoringandlogging.html#logging_for_bluemix_apps){: new_window}을 참조하십시오.


## 스테이징 오류 디버깅
{: #debugging-staging-errors}
{{site.data.keyword.Bluemix_notm}}에서 애플리케이션을
스테이징할 때 문제점이 발견될 수 있습니다. 앱을 스테이징할 수 없는 경우, 로그를 검토하여 오류 원인을 확인하고 문제점을 복구할 수 있습니다.

앱이 {{site.data.keyword.Bluemix_notm}}에서 실패하는 원인을 파악하려면 앱이 {{site.data.keyword.Bluemix_notm}}에
배치되고 실행되는 방식을 알고 있어야 합니다. 자세한 정보는 [애플리케이션
배치](../manageapps/depapps.html#appdeploy){: new_window}를 참조하십시오. 

다음 프로시저는 `cf logs` 명령을 사용하여 스테이징 오류를
디버그하는 방법을 보여줍니다. 다음 단계를 수행하기 전에 cf 명령행 인터페이스를 설치했는지
확인하십시오. cf 명령행 인터페이스 설치에 대한 자세한 정보는
[ cf 명령행 인터페이스 설치](../starters/install_cli.html){: new_window}를
참조하십시오.

  1. cf 명령행 인터페이스에 다음 코드를 입력하여 {{site.data.keyword.Bluemix_notm}}에 연결하십시오.
```
	 cf api https://api.ng.bluemix.net
	 ```
	 
  2. `cf login`을 입력하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 
  
  3. `cf logs appname --recent`를 입력하여 최근 로그를 검색하십시오. 자세한 로그를 필터링하려면 `grep` 옵션을 사용하십시오. 예를 들어 다음 코드를 입력하여 [STG] 로그만 표시할 수 있습니다.
```
	cf logs appname --recent | grep '\[STG\]'
	```
  4. 로그에 첫 번째로 표시되는 오류를 확인하십시오. 
  
IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 플러그인을 사용하여 애플리케이션을 배치하는 경우 Eclipse 도구의 **콘솔** 탭에서 cf logs 출력과 유사한 로그를 확인할 수 있습니다. 별도의 Eclipse 창을 열어 애플리케이션을 배치할 때 `로그`를 추적할 수도 있습니다. 

`cf logs` 명령 이외에도, {{site.data.keyword.Bluemix_notm}}에서 Monitoring and Analytics 서비스를 사용하여 로그 세부사항을 수집할 수도 있습니다. 또한 Monitoring and Analytics 서비스는 애플리케이션의 성능, 상태 및 가용성을 모니터링하며, Node.js 및 Liberty 런타임 애플리케이션에 대한 로그 분석을 제공합니다.   

### Node.js 애플리케이션에 대한 스테이징 오류 디버깅

다음 예에서는 `cf logs appname --recent`를 입력하면 표시되는 로그를 보여줍니다. 이 예에서는 Node.js 애플리케이션에서 스테이징 오류가 발생했다고 간주합니다.
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


로그의 첫 번째 오류는 스테이징 실패 이유를 보여줍니다. 이 예에서 첫 번째 오류는 스테이징 단계 중 DEA 컴포넌트에서 제공하는 출력입니다.
```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3
```
{: screen}


Node.js 애플리케이션의 경우 DEA에서는 `package.json` 파일의 정보를 사용하여 모듈을 다운로드합니다. 이 오류에서 모듈에 대해 발생한 오류를 확인할 수 있습니다. 따라서 `package.json` 파일의 18번째 행을 검토해야 합니다.  

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


17행의 끝에 쉼표가 있으므로, 18행에는 키-값 쌍이
필요합니다. 이 문제점을 해결하려면 쉼표를 제거하십시오. 

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## 런타임 오류 디버깅
{: #debugging-runtime-errors}
런타임 시 애플리케이션에서 문제점이 발견된 경우 애플리케이션 로그를
사용하면 오류의 원인을 정확히 찾아내고 해당 문제점에서 복구할 수 있습니다.  

특히, stdout 및 stderr에 대한 로깅을 사용하도록 설정할 수 있습니다.
{{site.data.keyword.Bluemix_notm}} 기본 제공
빌드팩을 사용하여 배치된 애플리케이션에 대해 로그 파일을 구성하는 자세한 방법은
다음 목록을 참조하십시오. 

  * Liberty for Java™ 애플리케이션의 경우, [Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}를 참조하십시오.
  * Node.js 애플리케이션의 경우, [How to log
in node.js](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}를 참조하십시오.  
  * PHP 애플리케이션의 경우, [error_log](http://php.net/manual/en/function.error-log.php){: new_window}를
참조하십시오. 
  * Python 애플리케이션의 경우, [Logging
HOWTO](https://docs.python.org/2/howto/logging.html){: new_window}를 참조하십시오. 
  * Ruby on Rails 애플리케이션의 경우, [The
Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}를 참조하십시오. 
  * Ruby Sinatra 애플리케이션의 경우, [Logging](http://www.sinatrarb.com/intro.html#Logging){: new_window}을
참조하십시오. 
  
cf 명령행 인터페이스에 `cf logs appname --recent`를 입력하면 가장 최근의 로그만 표시됩니다. 이전에 발생한 오류에 대한 로그를 보려면 모든 로그를
가져와서 오류를 검색해야 합니다. 애플리케이션의 모든 로그를 가져오려면 다음 방법 중 하나를
사용하십시오. 
<dl> 
<dt><strong>{{site.data.keyword.Bluemix_notm}} Monitoring and Analytics Service</strong></dt> 
<dd>Monitoring and Analytics Service의 통합 로그 파일 검색 및 분석 기능을 사용하면 오류를 신속하게 식별할 수 있습니다. 자세한 정보는 <a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Monitoring and Analytics</a>를
참조하십시오. </dd> 
<dt><strong>타사 써드파티 도구</strong></dt> 
<dd>애플리케이션에서 로그를 수집하여 외부 로그 호스트로 내보낼 수 있습니다. 자세한 정보는 <a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">외부 로깅 구성</a>을 참조하십시오.</dd> 
<dt><strong>로그를 수집 및 내보내는 스크립트</strong></dt> 
<dd>로그를 자동으로 수집하여 외부 파일로 내보내는 스크립트를 사용하려면 컴퓨터에서
{{site.data.keyword.Bluemix_notm}} 서버에
연결해야 합니다. 또한 컴퓨터에 로그를 다운로드할 수 있는 충분한 공간이 있어야 합니다.
자세한 정보는 <a href="../support/index.html#collecting-diagnostic-information" target="_blank">진단 정보 수집</a>을
참조하십시오. </dd>
</dl>

이전에는 기본적으로 **파일** > **로그**의 {{site.data.keyword.Bluemix_notm}} 대시보드에 있는 애플리케이션 보기를 통해 `stdout.log` 및 `stderr.log` 파일에 액세스할 수 있었습니다. 그러나 {{site.data.keyword.Bluemix_notm}}에서
호스팅하는 Cloud Foundry의 현재 버전에서는 애플리케이션 로깅을 사용할 수 없습니다.
**파일** > **로그**의 {{site.data.keyword.Bluemix_notm}} 대시보드를 통해 stdout 및 stderr 애플리케이션 로깅에 계속 액세스할 수 있도록 하려면 사용 중인 런타임에 따라 {{site.data.keyword.Bluemix_notm}} 파일 시스템의 다른 파일로 로깅 경로를 재지정하면 됩니다. 

  * Liberty for Java 애플리케이션의 경우, stdout 및 stderr로 경로 지정된 출력이 이미 로그 디렉토리의 `messages.log` 파일에 포함되어 있습니다. 각각 SystemOut 및 SystemErr로 시작하는 항목을 찾으십시오. 
  * Node.js 애플리케이션의 경우, 로그 디렉토리의 파일에 명시적으로 기록하도록 console.log 함수를 대체할 수 있습니다.
  * PHP 애플리케이션의 경우, error_log 함수를 사용하여 로그 디렉토리의 파일에
기록할 수 있습니다. 
  * Python 애플리케이션의 경우, 다음과 같이 로거가 로그 디렉토리의 파일에
기록하도록 할 수 있습니다. logging.basicConfig(filename='../../logs/example.log',level=logging.DEBUG)
  * Ruby 애플리케이션의 경우, 로거가 로그 디렉토리의 파일에
기록하도록 할 수 있습니다. 
 

# 관련 링크
{: #rellinks}

## 일반
{: #general}

  * [DEA(Droplet Execution Agent)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [IBM Monitoring and Analytics for Bluemix 서비스 시작하기](../services/monana/index.html#gettingstartedtemplate){: new_window}
  * [Bluemix의 작동 방식](../public/index.html#howwork){: new_window}
  * [cf 명령 도구 설치](../starters/install_cli.html){: new_window}
  * [로그 보기](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}
  
  
 














