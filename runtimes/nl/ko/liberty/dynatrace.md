---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace 사용
{: #using_dynatrace}

*마지막 업데이트 날짜: 2016년 4월 8일*

Dynatrace는 앱에 대한 모니터링을 제공하는 써드파티 서비스입니다. 

Dynatrace 서비스에서 제공하는 기능에 대한 자세한 정보는 [Dynatrace 애플리케이션 모니터링](http://www.dynatrace.com/en/products/application-monitoring.html)을 참조하십시오.

Liberty 앱에서 Dynatrace 서비스를 사용할 수 있는 경우 다음 프로세스 단계를 수행하십시오. 

1. Liberty 빌드팩에서 다운로드할 수 있도록 Dynatrace 에이전트 jar 파일을 획득하여 호스트하십시오. 
2. Liberty 앱에서 실행 중인 Dynatrace 에이전트가 통신할 수 있도록 Dynatrace 서버의 인스턴스를 설정하십시오. 
3. Liberty 앱이 Dynatrace 에이전트를 다운로드하고 Dynatrace 서버와 연결할 수 있도록 Liberty 앱을 구성하십시오. 

## Dynatrace 에이전트 호스트
{: #hosting_dynatrace_agent}
Dynatrace 에이전트는 웹 서버에 호스트되어야 하며, Liberty 빌드팩이 서버에서 에이전트 jar 파일을 다운로드할 수 있어야 합니다. 서버는 에이전트 jar 파일에 대한 세부사항을 지정하는 index.yml 파일로 구성되어야 합니다. Dynatrace 에이전트를 설정하려면 다음 단계를 완료하십시오. 
  1. Dynatrace 에이전트 jar를 다운로드하십시오. Dynatrace 에이전트 jar 다운로드에 대한 지시사항은 Dynatrace 커뮤니티 웹 사이트에서 [Dynatrace 서버 플랫폼 설치 프로그램](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace)을 참조하십시오. Bluemix에서 실행하기에 적절한 에이전트 jar 파일은 **dynatrace-agent-unix.jar** 버전 **6.3.0+**입니다.
  2. Liberty 빌드팩이 다운로드할 수 있는 위치에 에이전트 jar 파일이 호스트되도록 하십시오. 사용 가능한 서버 기능을 사용하여 Bluemix 자체에서 이 파일을 호스트하거나, 일부 공용 사용 가능 위치에서 호스트할 수 있습니다. 
     * 호스트 위치에서 index.yml 파일을 제공하는지 확인하십시오. index.yml 파일에는 에이전트 jar 파일의 버전 ID(뒤에 콜론이 붙음)와 에이전트 jar 위치의 완전한 URL로 구성된 항목이 포함되어야 합니다. 예:
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```
{: #codeblock}
     * URL의 끝에서 jar 파일의 이름은 **dynatrace-agent-version-unix.jar**이어야 합니다. 버전은 **6.3.0** 또는 **6.3.0_nnnn**이어야 합니다. 여기서, nnnn은 마이크로 버전 ID입니다. 이는 Dynatrace에서 사용하는 jar 파일 이름과 다를 수 있으므로 jar 파일의 이름을 바꾸어야 할 수도 있음을 참고하십시오.        
     * **dynatrace-agent-6.3.0-unix.jar** 파일은 index.yml 파일에 지정된 위치에 있어야 합니다. jar 파일과 index.yml 파일의 위치가 동일한 디렉토리일 수 있습니다. 

## Dynatrace 콜렉터 설정

다음으로 Dynatrace 에이전트에 액세스할 수 있는 Dynatrace 콜렉터를 설정해야 합니다. 또한 Dynatrace 콜렉터에 연결할 Dynatrace 에이전트에 대한 정보를 전달하는 사용자 제공 서비스를 작성해야 합니다. Dynatrace 컴포넌트 간의 관계에 대해 자세히 보려면 [Dynatrace 아키텍처](https://community.dynatrace.com/community/display/DOCDT63/Architecture)를 참조하십시오. 

  1. Dynatrace 콜렉터를 설정하십시오. 
    * Dynatrace 콜렉터 다운로드 및 설정에 대한 지시사항은 [Dynatrace 커뮤니티 웹 사이트](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace)를 참조하십시오. 
    * Bluemix의 앱에서 실행 중인 Dynatrace 에이전트에 액세스할 수 있는 위치에 콜렉터가 설치되었는지 확인하십시오. 
  2. 실행 중인 Dynatrace 콜렉터를 가리키는 사용자 제공 서비스를 작성하십시오. <b>참고</b> 사용자 제공 서비스의 이름에는 <b>dynatrace</b>가 포함되어야 합니다. 예를 들어 다음과 같은 명령을 사용하십시오.
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
```
{: #codeblock}
이 예에서 my-dynatrace-collector는 서비스에 지정된 이름이고, DynatraceCollectorIPaddress는 구성한 Dynatrace 콜렉터의 IP 주소이며, profile은 이 모니터되는 앱과 연관된 선택적 Dynatrace 프로파일 이름입니다. 기본 profile 값은 Monitoring입니다. 다음 예에서와 같이 선택적 매개변수를 지정할 수 있습니다.
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
```
{: #codeblock}
사용 가능한 옵션에 대한 자세한 정보는 Dynatrace 커뮤니티에서 [에이전트 구성의 에이전트 설정 섹션](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration)을 참조하십시오. 예를 들어 제외 옵션을 사용하면 Dynatrace에서 모니터되지 않도록 클래스를 제외시킬 수 있습니다. 사용자 제공 서비스 구성에 대한 자세한 정보는 [DynaTrace 에이전트 프레임워크](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md)를 참조하십시오. 
  3. Bluemix에 앱을 푸시한 후 앱에 작성한 사용자 제공 서비스를 바인드하십시오. 예를 들어 다음 명령을 사용하십시오.
```
    $ cf bs myApp my-dynatrace-service
```
**참고**: 서비스를 바인드한 후 애플리케이션을 다시 스테이징해야 합니다. 

## Liberty 앱 구성
{: #configuring_liberty_app}

이전에 설정한 에이전트 jar를 호스트하는 서버를 찾으려면 모니터할 Liberty 앱이 구성되어야 합니다. **JBP_CONFIG_DYNATRACEAGENT** 환경 변수를 사용하여 앱을 구성할 수 있습니다. **JBP_CONFIG_DYNATRACEAGENT** 환경 변수는 Dynatrace 에이전트를 다운로드할 소스 빌드팩을 알려줍니다. 이 환경 변수를 설정하려면 다음 단계를 완료하십시오. 
<ol>
   <li> **JBP_CONFIG_DYNATRACEAGENT** 변수에
*"repository_root: URL_of_server_hosting_index.yml"* 값을 설정하십시오. 예를 들어 애플리케이션을 푸시한 후 다음 명령을 실행하십시오.
```
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
```
{: #codeblock}
이 예에서 *my-dynatrace-agent-host.mybluemix.net*은 이전에 구성된 서버에 호스트된 index.yml 파일의 URL입니다. 
  </li>
  <li> 환경 변수를 설정한 후 앱을 다시 스테이징하십시오. Liberty 앱의 staging_task.log는 에이전트 호스트 서버에서 Dynatrace 에이전트를 다운로드했음을 알리는 메시지를 발행합니다. 예:
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: #codeblock}
</li>
<li>staging_task.log를 보려면 다음 명령을 실행하십시오.
```
    $ cf files myAppName logs/staging_task.log
```
{: #codeblock}
</li>
</ol>

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
