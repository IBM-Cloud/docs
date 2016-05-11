---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty 앱 푸시 옵션
{: #options_for_pushing}

*마지막 업데이트 날짜: 2016년 3월 23일*

Bluemix에서 Liberty 서버의 동작은 Liberty 빌드팩을 통해 제어됩니다. 빌드팩은 애플리케이션의 특정 클래스에 맞는 완전한 런타임 환경을 제공할 수 있습니다. 클라우드 이식성을 높이고 개방형 클라우드 아키텍처를 향상시키는 데 있어 핵심 요소입니다. Liberty 빌드팩은 Java EE 7 및 OSGi 애플리케이션의 실행이 가능한 WebSphere Liberty 컨테이너를 제공합니다. 이는 Spring과 같은 유명한 프레임워크를 지원하며 IBM JRE를 포함합니다. WebSphere Liberty를 통해 클라우드에 적합한 애플리케이션을 신속하게 개발할 수 있습니다. Liberty 빌드팩은 하나의 Liberty 서버에 배치되는 여러 개의 애플리케이션을 지원합니다. Liberty 빌드팩이 Bluemix에 통합되는 과정에서 서비스 바인딩을 위한 환경 변수가 Liberty 서버에서 구성 변수로 표시되는지 확인합니다. 

Liberty 애플리케이션을 Bluemix에 배치하려면 다음 방법을 사용합니다.

* 독립형 애플리케이션 푸시
* 서버 디렉토리 푸시
* 패키지된 서버 푸시

중요: Liberty 빌드팩으로 애플리케이션을 배치하는 경우, 애플리케이션의 메모리 제한으로 최소 512M을 지정하십시오. 자세한 정보는 [메모리 한계 및 Liberty 빌드팩](memoryLimits.html)을 참조하십시오.

## 독립형 앱
{: #stand_alone_apps}

Bluemix에서 WAR 또는 EAR 파일과 같은 독립형 애플리케이션을 Liberty에 배치할 수 있습니다. 

독립형 애플리케이션을 배치하려면 WAR 또는 EAR 파일을 가리키는 -p 매개변수를 포함한 cf push 명령을 실행하십시오.
예: 

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

독립형 애플리케이션을 배치할 때 애플리케이션을 위한 기본 Liberty 구성이 제공됩니다. 기본 구성은 다음과 같은 Liberty 기능을 지원해 줍니다.

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

이 기능은 Java EE 7 Web Profile 기능에 해당합니다. JBP_CONFIG_LIBERTY 환경 변수를 설정하여 Liberty 기능의 다른 설정을 지정할 수 있습니다. 예를 들어, jsp-2.3 및 websocket-1.1 기능만 사용하려면 명령을 실행하고 애플리케이션을 다시 스테이징하십시오. 

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

참고: 최상의 결과를 얻으려면 JBP_CONFIG_LIBERTY 환경 변수로 Liberty 기능을 설정하거나 사용자 정의 server.xml 파일로 [서버 디렉토리](optionsForPushing.html#server_directory) 또는 [패키지된 서버](optionsForPushing.html#packaged_server)로서 애플리케이션을 배치하십시오. 이 환경 변수를 설정하면 애플리케이션이 필요한 기능만 사용하며 빌드팩의 기본 Liberty 기능 설정 변경사항의 영향을 받지 않도록 합니다. 기능 세트 외에도 추가 Liberty 구성을 제공해야 하는 경우에는 [서버 디렉토리](optionsForPushing.html#server_directory) 또는 [패키지된 서버](optionsForPushing.html#packaged_server) 옵션을 사용하여 애플리케이션을 배치하십시오. 

WAR 파일을 배치한 경우, 웹 애플리케이션은 임베디드 ibm-web-ext.xml 파일에 설정된 대로 컨텍스트 루트에서 액세스 가능합니다. ibm-web-ext.xml 파일이 존재하지 않거나 컨텍스트 루트를 지정하지 않는 경우에는 애플리케이션이 루트 컨텍스트에서 액세스 가능합니다. 예를 들면, 다음과 같습니다. 

```
    http://<yourappname>.mybluemix.net/
```
{: #codeblock}

EAR 파일을 배치했으면 EAR 배치 디스크립터에 정의된 컨텍스트 루트에서 임베디드 웹 애플리케이션에 액세스할 수 있습니다. 예를 들면, 다음과 같습니다. 

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

전체 기본 Liberty server.xml 구성 파일은 다음과 같습니다.
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

성능상 이유로 WAR 및 EAR 파일만 배치할 경우 [CDI 1.2 암시적 bean 아카이브 스캔](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html)이 기본적으로 사용하지 않도록 설정됩니다. JBP_CONFIG_LIBERTY 환경 변수를 사용하여 암시적 아카이브 아카이브 스캔을 사용하도록 설정할 수 있습니다.
예: 

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

중요: 환경 변수 변경사항을 적용하려면 다음과 같이 애플리케이션을 다시 스테이징해야 합니다.

```
    $ cf restage myapp
```
{: #codeblock}

## 서버 디렉토리
{: #server_directory}

경우에 따라 사용자 정의 Liberty 서버 구성을 애플리케이션에 제공해야 할 때가 있습니다. 이러한 사용자 정의 구성은 사용자가 WAR 또는 EAR 파일을 배치하고 기본 server.xml 파일에 애플리케이션이 요구하는 특정 설정이 없는 경우에 필요합니다. 

Liberty 프로파일을 워크스테이션에 설치했으며 이미 애플리케이션에서 Liberty 서버를 작성한 경우에는 해당 디렉토리의 컨텐츠를 Bluemix에 푸시할 수 있습니다.
예를 들어, Liberty 서버의 이름이 defaultServer이면 다음 명령을 실행하십시오.

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

Liberty 프로파일이 워크스테이션에 설치되어 있지 않으면 다음 단계에 따라 애플리케이션에 서버 디렉토리를 작성할 수 있습니다.

1. defaultServer 디렉토리를 작성합니다.
2. defaultServer 디렉토리에 apps 디렉토리를 작성합니다.
3. WAR 또는 EAR 파일을 defaultServer/apps 디렉토리에 복사합니다.
4. defaultServer 디렉토리에 다음 예제 컨텐츠를 포함한 server.xml 파일을 작성합니다. 또한 다음과 같아야 합니다.
  * 애플리케이션 요소의 location 또는 type 속성이 애플리케이션의 파일 이름과 유형에 일치하도록 업데이트해야 합니다.
  * 다이어그램에서 server.xml 파일은 최소 기능 세트를 표시합니다. 애플리케이션의 요구사항에 따라 기능 세트를 조정해야 할 수도 있습니다.

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id="defaultHttpEndpoint" host="*" httpPort="8080" />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

서버 디렉토리가 준비되면, Bluemix에 배치할 수 있습니다. 

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

참고: 서버 디렉토리의 일부로 배치되는 웹 애플리케이션은 [Liberty 프로파일에서 판별되는 컨텍스트 루트](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6)에서 액세스할 수 있습니다. 예: 

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## 패키지된 서버
{: #packaged_server}

패키지된 서버 파일을 Bluemix에 푸시할 수도 있습니다. 패키지된 서버 파일은 Liberty의 서버 패키지 명령을 사용하여 작성됩니다. 패키지된 서버 파일에는 애플리케이션과 구성 파일 외에 애플리케이션에 필요한 공유 자원 및 Liberty 사용자 기능이 포함되어 있습니다.

Liberty 서버를 패키징하려면 Liberty 설치 디렉토리에서 ./bin/server package 명령을 사용하십시오. 서버 이름을 지정하고 '––include=usr' 옵션을 포함하십시오.
예를 들어, Liberty 서버가 defaultServer이면 다음 명령을 실행하십시오.

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

이 명령은 서버 디렉토리에 serverName.zip 파일을 생성합니다. 그러면 사용자가 cf push 명령을 사용하여 해당 압축 파일을 Bluemix에 푸시할 수 있습니다.
예: 

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

참고: 패키지된 서버의 일부로 배치되는 웹 애플리케이션은 Liberty 프로파일에 따라 지정되는 컨텍스트 루트에서 액세스할 수 있습니다.

### server.xml 파일 수정
{: #modifications_of_serverxml}

패키지된 서버 또는 Liberty 서버 디렉토리를 푸시하면 Liberty 빌드팩이 사용자의 애플리케이션과 server.xml 파일을 검색합니다. 그런 다음 server.xml 파일을 다음과 같이 수정합니다.

* 파일 안에 httpEndpoint 요소가 정확히 한 개 있는지 확인합니다.
* httpEndpoint 요소의 httpPort 속성이 ${port} 시스템 변수를 가리키는지 확인합니다. 또한 빌드팩이 호스트 속성을 대체합니다.
* 로깅 요소의 logDirectory 속성이 시스템 로그 디렉토리를 가리키도록 설정합니다.
* runtime-vars.xml 파일이 논리적으로 server.xml 파일과 병합되어 있는지 확인합니다. 구체적으로, *&lt;include location="runtime-vars.xml" /&gt;* 행을 server.xml 파일에 추가합니다.

### 참조 가능한 변수
{: #referenceable_variables}

다음 변수는 runtime-vars.xml 파일에 정의되어 있고, 푸시된 server.xml 파일에서 참조됩니다. 모든 변수는 대소문자를 구분합니다. 

* ${port}: Liberty 서버가 수신 대기하고 있는 HTTP 포트입니다.
* ${vcap_console_port}: vcap 콘솔이 실행되고 있는 포트입니다(대개 ${port}와 같음).
* ${vcap_app_port}: app 서버가 수신 대기하는 포트입니다(대개 ${port}와 같음).
* ${vcap_console_ip}: vcap 콘솔의 IP 주소입니다(대개 Liberty 서버가 수신 대기하는 IP 주소임).
* ${application_name}: cf push 명령에 옵션을 사용하여 정의하는 애플리케이션의 이름입니다.
* ${application_version}: 이 애플리케이션 인스턴스의 버전이며, b687ea75-49f0-456e-b69d-e36e8a854caa와 같은 UUID 형식을 사용합니다. 새로운 코드 또는 변경된 애플리케이션 아티팩트가 포함된 애플리케이션을 연속으로 푸시될 때마다 이 변수가 변경됩니다.
* ${host}: 애플리케이션을 실행하고 있는 DEA의 IP 주소입니다(대개 ${vcap_console_ip}와 같음).
* ${application_uris}: 이 애플리케이션에 액세스하는 데 사용하는 JSON 스타일의 엔드포인트 배열입니다. 예: myapp.mydomain.com
* ${start}: 애플리케이션을 시작한 날짜 및 시간이며, 2013-08-22 10:10:18 -0400와 비슷한 형식을 사용합니다.

### 바인드된 서비스 정보 액세스
{: #accessing_info_of_bound_services}

서비스를 애플리케이션에 바인드하려는 경우, Cloud Foundry가 애플리케이션에 대해 설정하는 [VCAP_SERVICES 환경 변수](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES)에 연결 신임 정보와 같은 서비스 관련 정보가 포함됩니다. [자동으로 구성되는 서비스](autoConfig.html)의 경우, Liberty 빌드팩이 server.xml 파일에 서비스 바인딩 항목을 생성하거나 업데이트합니다. 서비스 바인딩 항목의 컨텐츠는 다음 형식 중 하나입니다.

* cloud.services.&lt;service-name&gt;.&lt;property&gt; 서비스의 이름, 유형, 플랜과 같은 정보를 설명합니다. 
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt; 서비스의 연결 정보를 설명합니다.

일반적인 정보 세트는 다음과 같습니다.
* name: 서비스의 이름입니다. 예: mysql-e3abd.
label: 작성된 서비스의 유형입니다. 예: mysql-5.5. 
* plan: 서비스 플랜이며, 해당 플랜의 고유 ID로 표시됩니다. 예: 100.
connection.name: 연결의 고유 ID이며, UUID 형식을 사용합니다. 예: d01af3a5fabeb4d45bb321fe114d652ee.
* connection.hostname: 서비스를 실행하는 서버의 호스트 이름입니다. 예: mysql-server.mydomain.com.
* connection.host: 서비스를 실행하고 있는 서버의 IP 주소입니다. 예: 9.37.193.2.
* connection.port: 서비스가 들어오는 연결을 수신 대기하는 포트입니다. 예: 3306,3307. 
* connection.user: 이 애플리케이션을 서비스에 인증하는 데 사용되는 사용자 이름입니다. 사용자 이름은 Cloud Foundry에서 자동 생성됩니다. 예: unHwANpjAG5wT.
* connection.username: connection.user에 대한 별명입니다.
* connection.password: 이 애플리케이션을 서비스에 인증하는 데 사용되는 비밀번호입니다. 비밀번호는 Cloud Foundry에서 자동 생성됩니다. 예: pvyCY0YzX9pu5.

Liberty 빌드팩을 통해 자동으로 구성되지 않는 바인드된 서비스의 경우, 애플리케이션에서 자체적으로 백엔드 자원의 액세스를 관리해야 합니다.

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
