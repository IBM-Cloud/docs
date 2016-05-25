---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Liberty 및 Node.js 앱 관리
{: #app_management}

*마지막 업데이트 날짜: 2016년 3월 17일*

App Management는 {{site.data.keyword.Bluemix}}에서
Liberty 및 Node.js 애플리케이션에 사용할 수 있는 개발 및 디버깅 유틸리티 세트입니다.
{:shortdesc}

##App Management 유틸리티
{: #Utilities}

이 유틸리티는 Liberty 및 Node.js 모두에서 지원됩니다.

  1. *프록시*: 사용자 애플리케이션과 {{site.data.keyword.Bluemix_notm}} 사이에서 프록시로 작동하는 최소 애플리케이션 관리.

    사용 가능한 경우, 빌드팩이 사용자 애플리케이션의 런타임과 컨테이너 사이에 위치하는 프록시 에이전트를 시작합니다. *프록시* 유틸리티는 애플리케이션이 수신하는 모든 요청을 처리합니다. 요청 유형에 따라 앱 관리 조치를 수행하거나 사용자 애플리케이션에 요청을 전달합니다. *프록시*는 대다수의 기타 앱 관리 유틸리티에 대해 인에이블먼트를 허용합니다. *프록시*를 사용 가능하게 설정하면 애플리케이션이 충돌하는 경우에도 애플리케이션 컨테이너는 계속 활성 상태를 유지합니다. 또한 프록시 에이전트는 증분 파일 업데이트를 허용하여, Node.js 애플리케이션에서 "Live Edit" 모드를 사용할 수 있습니다. 
	
  2. *devconsole*: 다음 URL에서 액세스 가능한 개발 콘솔 유틸리티를 사용할 수 있게 합니다.
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```
	
    사용자는 개발 콘솔을 사용하여 자신의 애플리케이션을 다시 시작, 중지 또는 일시중단할 수 있습니다. 또한 shell 및 inspector 유틸리티를 사용하거나 이에 액세스할 수도 있습니다. 

    또한 devconsole 유틸리티는 *프록시*를 시작하지 않습니다.
	
  3. *hc*: Health Center 클라이언트가 사용자 애플리케이션을 모니터링할 수 있도록 하는 Health Center 에이전트입니다. 

    Health Center는 IBM 모니터링 및 진단 도구를 사용하여 Liberty 및 Node.js 애플리케이션의 성능을 분석할 수 있도록 지원합니다. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}}에서 Liberty Java 또는 Node.js 애플리케이션의 성능 분석 방법](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}을 참조하십시오. </p></li>
	
  4. *shell*: devconsole 유틸리티를 통해서나 다음 URL에 액세스하여 액세스할 수 있는 웹 기반 쉘을 사용할 수 있도록 합니다.
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```
	
    shell 유틸리티에 액세스하면 애플리케이션에 대한 쉘 액세스가 있는 터미널 창이 표시됩니다. 파일 편집, 메모리 사용량 점검 또는 진단 명령 실행 등 일반 쉘에서 지원되는 모든 작업을 수행할 수 있습니다. 
	
    또한 *shell* 유틸리티는 *프록시*를 시작하지 않습니다.

이 유틸리티는 Liberty에서만 지원됩니다.

  1. *debug*: Liberty 애플리케이션을 디버그 모드로 작동시키고, {{site.data.keyword.Bluemix_notm}}가 애플리케이션에 원격 디버깅 세션을 설정할 수 있도록 IBM Eclipse Tools와 같은 클라이언트를 사용 가능하게 합니다. 
  
   자세한 정보는 [원격 디버그](../manageapps/eclipsetools/eclipsetools.html#remotedebug)를 참조하십시오.
   
   또한 *debug* 유틸리티는 *프록시*를 시작하지 않습니다.
   
  2. *jmx*: 원격 JMX 클라이언트가 {{site.data.keyword.Bluemix_notm}} 사용자 신임 정보를 사용하여 애플리케이션을 관리할 수 있도록 JMX REST Connector를 사용 가능하게 설정합니다. 
  
  JMX 커넥터 구성에 대한 자세한 정보는 [Liberty 프로파일에 대한 보안 JMX 연결 구성](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}을 참조하십시오. 
  
  *jmx* 유틸리티는 프록시를 시작하지 않습니다.

이 유틸리티는 Node.js에서만 지원됩니다.

  1. *inspector*: *devconsole* 유틸리티를 통해서 또는 *https://myApp.mybluemix.net/bluemix-debug/inspector*에서 액세스 가능한 노드 검사기 디버거 인터페이스를 사용할 수 있도록 합니다. 
  
  검사기 프로세스는 애플리케이션 컨테이너에서 실행됩니다. 사용자 애플리케이션이 {{site.data.keyword.Bluemix_notm}}에서 실행되는 동안 CPU 사용량 프로파일을 작성하고 중단점을 추가하며 코드를 디버그하려면 이 유틸리티를 사용하십시오. 노드 검사기 모듈에 대한 자세한 정보는 odule, see [GitHub의 노드 검사기](https://github.com/node-inspector/node-inspector){:new_window}를 참조하십시오. 
  
  또한 *inspector* 유틸리티는 *프록시*를 시작하지 않습니다.
  
  2. *strongpm*: [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}에서 [StrongLoop 메트릭, 프로파일링 및 추적](https://strongloop.com/node-js/devops-tools/){:new_window} 등의 유틸리티를 사용하여 Node.js 애플리케이션을 분석할 수 있도록 합니다. 
    
  또한 *strongpm* 유틸리티는 *프록시*를 시작하지 않습니다.
  
  [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}에서 Node.js 애플리케이션을 구성하려면 다음 단계를 수행하십시오. 

    1. *strongpm* BlUEMIX_APP_MGMT_ENABLE 환경 변수를 구성하고 애플리케이션을 다시 스테이징하십시오.
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. Cloud Foundry 명령행에서, "-pm"이 애플리케이션 이름에 첨부되어 있는 라우트(예: <appname>-pm.mybluemix.net)를 애플리케이션에 추가하십시오. 
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. [StrongLoop npm 모듈](https://www.npmjs.com/package/strongloop){:new_window}을 로컬 워크스테이션에 설치하십시오. 
    
	```
    npm install -g strongloop
    ```
	
    4. [StrongLoop의 웹 사이트](https://strongloop.com/register/){:new_window}에서 계정을 작성하십시오. 
    5. 로컬 워크스테이션에서 Arc를 시작하고 작성한 계정을 사용하여 로그인하십시오. 
    
	```
    slc arc
    ```
	
    6. Arc 내의 프로세스 관리자로 이동하십시오. 포트를 80으로 하여 새로 작성한 라우트를 프로세스 관리자에 입력하십시오. 활성화 단추를 누르십시오. 자세한 정보는 [Arc 사용에 관한 상세 문서](https://docs.strongloop.com/display){:new_window}를 참조하십시오. 
	
  3. *trace*: 사용자 애플리케이션이 *log4js*, *ibmbluemix* 또는 *bunyan* 로깅 모듈을 사용하는 경우 동적으로 추적 레벨을 설정합니다. 
  
  **참고:** 지원되는 종속 버전은 다음과 같습니다.

    * log4js:(0.6.0 - 0.6.24)
    * bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  {{site.data.keyword.Bluemix_notm}} 웹 콘솔의 인스턴스 세부사항 페이지로 이동하고 **조치**를 선택하여 UI를 확인하십시오.

  *trace* 유틸리티는 *프록시*를 시작하지 않습니다.

##App Management를 구성하는 방법
{: #configure}

App Management 유틸리티를 사용하려면
*BLUEMIX_APP_MGMT_ENABLE* 환경 변수를 설정하고 애플리케이션을 다시 스테이징하십시오. "+"로 구분하여 여러 유틸리티를 사용으로 설정할 수 있습니다. 

예를 들어, devconsole 및 *shell* 유틸리티를 사용하려면 다음 명령을 실행하십시오.

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

환경 변수를 설정한 후 반드시 애플리케이션을 다시 스테이징하십시오. 

```
cf restage myApp
```

App Management 유틸리티를 사용자 애플리케이션에 설치하지 않으려면
*BLUEMIX_APP_MGMT_INSTALL* 환경 변수를 'false'로 설정하고 애플리케이션을 다시 스테이징하십시오. 

예:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

##제한사항
{: #restrictions}

* 앱 관리가 단일 인스턴스 애플리케이션만 지원합니다.
* 앱 관리를 사용하여 수행한 애플리케이션에 대한 변경은 임시적인 것으로, 이 모드를 종료하면 유실됩니다. 이 모드는 임시 개발 용도이며, 성능 상의 문제로 프로덕션 환경으로 사용하지는 않습니다. 
* 대부분의 앱 관리 유틸리티는 manifest.yml 파일(명령) 또는 CF CLI(-c)에서 시작 명령을 설정하는 경우 작동하지 않습니다. 이들 메소드는 빌드팩 대체이며 Node.js 애플리케이션을 시작하는 데에는 적합하지 않은 패턴입니다. 최상의 결과를 얻으려면 package.json 파일 또는 프로파일에서 시작 명령을 설정하십시오. 

##Eclipse 도구의 개발 모드
{: #devmode}

개발 모드는 애플리케이션이 클라우드에서 실행되는 동안 개발자가 애플리케이션에서 작업할 수 있도록 해주는 [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools)의 기능입니다.

개발자가 {{site.data.keyword.Bluemix_notm}}에서
애플리케이션 작업을 수행하는 경우 작업이 로컬 환경에서 이루어지므로 일반적인
개발 활동을 수행할 수 없다고 생각할 수 있습니다. Eclipse Tools를 통해 개발 모드를 사용하면
임시 보안 작업공간에서 작업하는 동시에 클라우드에서 작업할 수 있으므로
이 문제가 해결됩니다. 

개발 모드는 Liberty 및 Node.js 애플리케이션 모두에서 지원됩니다.
Liberty 또는 Node.js 애플리케이션에 대해 개발 모드가 사용되는 경우, 애플리케이션을 푸시할 필요 없이 증분 방식으로
애플리케이션 파일을 업데이트할 수 있습니다. 또한 애플리케이션에 대해 디버깅 세션을 설정할 수 있습니다. Liberty 애플리케이션의
개발 모드는 debug 및 jmx App Management 유틸리티를 사용하는 것과 같습니다. Node.js 애플리케이션의 경우에는 *devconsole*, *inspector* 및 *shell* 유틸리티를 사용하는 것과 같습니다.
