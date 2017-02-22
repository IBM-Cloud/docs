---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Liberty 및 Node.js 앱 관리
{: #app_management}


App Management는 {{site.data.keyword.Bluemix}}에서 Liberty 및 Node.js 애플리케이션에 사용할 수 있는 개발 및 디버깅 유틸리티 세트입니다.
{:shortdesc}

## App Management 유틸리티
{: #Utilities}

### 이 유틸리티는 Liberty 및 Node.js 모두에서 지원됩니다.
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

*proxy*는 애플리케이션과 {{site.data.keyword.Bluemix_notm}} 간의 최소 애플리케이션 관리를 제공합니다.

사용 가능한 경우, 빌드팩이 사용자 애플리케이션의 런타임과 컨테이너 사이에 위치하는 프록시 에이전트를 시작합니다. *proxy* 유틸리티는 애플리케이션이 수신하는 모든 요청을 처리합니다. 요청 유형에 따라 앱 관리 조치를 수행하거나 사용자 애플리케이션에 요청을 전달합니다. *proxy*는 대다수의 기타 앱 관리 유틸리티의 인에이블먼트를 허용합니다. *proxy*를 사용 가능하게 설정하면 애플리케이션이 충돌하는 경우에도 애플리케이션 컨테이너는 계속 활성 상태를 유지합니다. 또한 프록시 에이전트는 증분 파일 업데이트를 허용하여, Node.js 애플리케이션에서 "Live Edit" 모드를 사용할 수 있습니다. 

#### noproxy
{: #noproxy}

다른 유틸리티 중 하나를 통해 *noproxy* 유틸리티가 자동으로 시작되는 경우 *proxy* 유틸리티를 사용 안함으로 설정합니다. Diego를 사용하면 Diego에서 애플리케이션에 직접 *ssh* 명령을 수행하고 포트 전달을 설정하는 기능을 제공하기 때문에 프록시가 필요하지 않습니다. 

*noproxy* 유틸리티만 Diego 셀에서 실행 중인 애플리케이션에 적용할 수 있습니다. 



#### devconsole
{: #devconsole}

사용자는 개발 콘솔 유틸리티(*devconsole*)를 사용하여 애플리케이션을 다시 시작, 중지 또는 일시중단할 수 있습니다. 또한 shell 및 inspector 유틸리티를 사용하거나 이에 액세스할 수도 있습니다. 다음 URL에서 액세스할 수 있습니다. 
```
  https://<yourappname>.mybluemix.net/bluemix-debug/manage
```

6.3.0 이상의 노드 버전의 경우, 개발 콘솔에서는 애플리케이션의 다시 시작 단추와 쉘 유틸리티에 대한 액세스 권한을 제공합니다. 자세한 정보는 *inspector* 토론을 참조하십시오.

*devconsole* 유틸리티는 또한 *proxy*를 시작합니다. 

#### hc
{: #hc}

(*hc*) Health Center 에이전트를 사용하면 Health Center 클라이언트에서 애플리케이션을 모니터링할 수 있습니다.

Health Center는 IBM 모니터링 및 진단 도구를 사용하여 Liberty 및 Node.js 애플리케이션의 성능을 분석할 수 있도록 지원합니다. 자세한 정보는 [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}} ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){: new_window}를 참조하십시오. </p></li>

*hc* 유틸리티는 또한 *proxy*를 시작합니다. 

*hc* 유틸리티를 *noproxy*와 함께 사용할 수 있습니다. *noproxy*와 함께 Health Center를 사용하려면, 먼저 `cf ssh` 명령을 사용하여 포트 전달을 설정하십시오. 예:

```
$ cf ssh -N -T -L 1883:127.0.0.1:1883 <appName>
```

다음으로, Health Center 클라이언트와 연결하려면 [MQTT 연결 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SS3KLZ/com.ibm.java.diagnostics.healthcenter.doc/topics/connectingtojvm.html){: new_window}을 사용하고 호스트를 `127.0.0.1`로, 포트를 `1883`으로 지정하십시오. 

#### shell
{: #shell}

*shell* 유틸리티는 웹 기반 쉘을 사용합니다. *devconsole* 유틸리티에서 액세스 가능하거나 다음 URL에 액세스하여 사용할 수 있습니다.

```
  https://<yourappname>.mybluemix.net/bluemix-debug/shell
```

*shell* 유틸리티에 액세스하면 애플리케이션에 대한 쉘 액세스가 있는 터미널 창이 표시됩니다. 파일 편집, 메모리 사용량 점검 또는 진단 명령 실행 등 일반 쉘에서 지원되는 모든 작업을 수행할 수 있습니다. 

*shell* 유틸리티는 또한 *proxy*를 시작합니다.

Diego에서 `cf ssh` 명령을 통해 대화식 쉘을 제공하므로 DEA에서 실행 중인 애플리케이션에는 *shell* 유틸리티만 유용합니다. 

### 이 유틸리티는 Liberty에서만 지원됩니다.
{: #liberty_utilities}

#### debug
{: #debug}

*debug* 유틸리티는 Liberty 애플리케이션을 디버그 모드로 전환시키며 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}와 같은 클라이언트에서 애플리케이션과 [원격 디버깅](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug) 세션을 설정 가능하게 합니다. 

*debug* 유틸리티는 또한 *proxy*를 시작합니다.

*debug* 유틸리티를 *noproxy*와 함께 사용할 수 있습니다. *noproxy*와 함께 디버거를 사용하려면, 먼저 `cf ssh` 명령을 사용하여 포트 전달을 설정하십시오. 예:

```
$ cf ssh -N -T -L 7777:127.0.0.1:7777 <appName>
```

다음으로, Eclipse에 연결하려면, "원격 Java 구성"을 사용하고 호스트를 `127.0.0.1`로, 포트를 `7777`로 지정하십시오. 

#### jmx
{: #jmx}

*jmx* 유틸리티는 원격 JMX 클라이언트가 {{site.data.keyword.Bluemix_notm}} 사용자 신임 정보를 사용하여 애플리케이션을 관리할 수 있도록 JMX REST Connector를 사용 가능하게 설정합니다. 

JMX 커넥터 구성에 대한 자세한 정보는 [Configuring secure JMX connection to the Liberty profile ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}을 참조하십시오. 

*jmx* 유틸리티는 프록시를 시작하지 않습니다.

#### localjmx
{: #localjmx}

*localjmx* 유틸리티는 [localConnector-1.0 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feature_localConnector-1.0.html){:new_window} Liberty 기능을 사용으로 설정합니다. 로컬 포트 전달과 결합하면 원격 JMX 클라이언트가 애플리케이션을 관리할 수 있는 대체 방법을 사용할 수 있습니다. 

*localjmx* 유틸리티만 Diego 셀에서 실행 중인 애플리케이션에 적용할 수 있습니다. *localjmx*를 사용하려면, 먼저 `cf ssh` 명령을 사용하여 포트 전달을 설정하십시오. 예:

```
$ cf ssh -N -T -L 5000:127.0.0.1:5000 <appName>
```

다음으로, JConsole과 연결하려면, "원격 프로세스"를 선택하고 `127.0.0.1:5000`을 지정하고 보안되지 않은 연결을 사용하십시오. 


### 이 유틸리티는 Node.js에서만 지원됩니다.
{: #node_utilities}

#### inspector
{: #inspector}

Node.js 버전이 6.3.0 미만인 경우 *inspector*는 노드 검사기 디버거 인터페이스를 사용으로 설정합니다. *inspector* 프로세스가 애플리케이션 컨테이너에서 실행됩니다. 사용자 애플리케이션이 {{site.data.keyword.Bluemix_notm}}에서 실행되는 동안 CPU 사용량 프로파일을 작성하고 중단점을 추가하며 코드를 디버그하려면 이 유틸리티를 사용하십시오. 노드 검사기 모듈에 대한 자세한 정보는 [node-inspector on GitHub ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/node-inspector/node-inspector){:new_window}를 참조하십시오. 

Node.js 버전이 6.3.0 이상인 경우 *inspector*는 [V8 Inspector Integration for Node.js ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}를 활용합니다. 

inspector 유틸리티는 기본적으로 *proxy*를 시작하지만, 원격으로 디버그하는 방법은 Node.js의 버전 및 *proxy*나 *noproxy*의 사용에 따라 달라집니다. 다음 표는 다양한 시나리오에서 원격 디버깅에 액세스하는 방법을 표시합니다. 

| | proxy | noproxy |
|---|---|---|
| < &nbsp; 6.3.0 | devconsole utility *at*<br/> https://myApp.mybluemix.net/bluemix-debug/inspector | http://127.0.0.1:8790
| >= 6.3.0 | chrome-devtools URL | chrome-devtools URL

*noproxy* 및 버전이 6.3.0 미만인 Node.js의 경우 로컬 포트 전달을 통해 URL에 액세스할 수 있습니다. 예:

```
$ cf ssh -N -T -L <localPort>:127.0.0.1:8790 <appName>
```

그런 다음 Chrome 웹 브라우저에서 http://127.0.0.1:8790을 브라우징하십시오. 다음과 같이 BLUEMIX_APP_MGMT_INSPECTOR 환경 변수를 설정하여 포트를 변경하십시오. 

```
$ cf set-env <appName> BLUEMIX_APP_MGMT_INSPECTOR='{port: 9790}'
```

Node.js 버전이 6.3.0 이상인 경우 Chrome DevTools를 앱에 연결하는 데 사용할 수 있는 URL이 포함된 로그 메시지를 찾을 수 있습니다. 로그 메시지는 다음과 유사합니다. 

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

로컬 포트 전달을 통해 URL에 대한 액세스를 사용으로 설정하십시오. 예:

```
$ cf ssh -N -T -L 9229:127.0.0.1:9229 <appName>
```

이 URL을 브라우징하려면 최신 버전의 Chrome 웹 브라우저가 필요합니다. 이 시나리오에서 프록시는 트래픽을 검사기로 라우팅하지 않습니다. 

#### trace
{: #trace}

*trace* 유틸리티를 사용하여 애플리케이션이 *log4js*, *ibmbluemix* 또는 *bunyan* 로깅 모듈을 사용하는 경우 추적 레벨을 동적으로 설정할 수 있습니다. 

**참고:** 지원되는 종속 버전은 다음과 같습니다.
* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)

{{site.data.keyword.Bluemix_notm}} 웹 콘솔의 인스턴스 세부사항 페이지로 이동하고 **조치**를 선택하여 UI를 확인하십시오.

"-b buildpack" 옵션을 사용하여 애플리케이션을 시작한 경우에는 *추적* 유틸리티를 사용할 수 없습니다.

*trace* 유틸리티는 *proxy*를 시작하지 않습니다.

##  App Management를 구성하는 방법
{: #configure}

App Management 유틸리티를 사용하려면 *BLUEMIX_APP_MGMT_ENABLE* 환경 변수를 설정하고 애플리케이션을 다시 스테이징하십시오. "+"로 구분하여 여러 유틸리티를 사용으로 설정할 수 있습니다. 

예를 들어, *devconsole* 및 *shell* 유틸리티를 사용하려면 다음 명령을 실행하십시오. 

```
$ cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

환경 변수를 설정한 후 애플리케이션을 다시 스테이징하십시오.

```
$ cf restage myApp
```

App Management 유틸리티를 사용자 애플리케이션에 설치하지 않으려면 *BLUEMIX_APP_MGMT_INSTALL* 환경 변수를 'false'로 설정하고 애플리케이션을 다시 스테이징하십시오. 

예:

```
$ cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
$ cf restage myApp
```

## 제한사항
{: #restrictions}

* 애플리케이션이 DEA 노드에서 실행 중인 경우 앱 관리는 단일 인스턴스 애플리케이션만 지원합니다. 
* 앱 관리를 사용하여 수행한 애플리케이션에 대한 변경은 임시적인 것으로, 이 모드를 종료하면 유실됩니다. 이 모드는 임시 개발 용도이며, 성능 상의 문제로 프로덕션 환경으로 사용하지는 않습니다. 
* 대부분의 앱 관리 유틸리티는 `manifest.yml` 파일(명령) 또는 CF CLI (-c)에서 시작 명령을 설정하는 경우 작동하지 않습니다. 이들 메소드는 빌드팩 대체이며 Node.js 애플리케이션을 시작하는 데에는 적합하지 않은 패턴입니다. 최상의 결과를 얻으려면 `package.json` 파일 또는 `Procfile`에서 시작 명령을 설정하십시오. 

## Eclipse 도구의 개발 모드
{: #devmode}

개발 모드는 애플리케이션이 클라우드에서 실행되는 동안 개발자가 애플리케이션에서 작업할 수 있도록 해주는 [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)의 기능입니다.

개발자가 {{site.data.keyword.Bluemix_notm}}에서 애플리케이션 작업을 수행하는 경우 작업이 로컬 환경에서 이루어지므로 일반적인 개발 활동을 수행할 수 없다고 생각할 수 있습니다. Eclipse Tools를 통해 개발 모드를 사용하면 임시 보안 작업공간에서 작업하는 동시에 클라우드에서 작업할 수 있으므로 이 문제가 해결됩니다. 

개발 모드는 Liberty 및 Node.js 애플리케이션 모두에서 지원됩니다. Liberty 또는 Node.js 애플리케이션에 대해 개발 모드가 사용되는 경우, 애플리케이션을 푸시할 필요 없이 증분 방식으로 애플리케이션 파일을 업데이트할 수 있습니다. 또한 애플리케이션에 대해 디버깅 세션을 설정할 수 있습니다. Liberty 애플리케이션의 개발 모드는 debug 및 jmx App Management 유틸리티를 사용하는 것과 같습니다. Node.js 애플리케이션의 경우에는 *devconsole*, *inspector* 및 *shell* 유틸리티를 사용하는 것과 같습니다.
