---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Bluemix에서 JConsole을 사용하여 Liberty 모니터링
{: #jconsole}

*마지막 업데이트 날짜: 2016년 3월 23일*

## JConsole을 사용하여 Bluemix Liberty 런타임을 모니터하는 단계는 다음과 같습니다. 
{: #steps_to_monitor}

1. 올바른 server.xml을 포함한 서버 패키지 안에서 앱을 푸시합니다. 
2. 명령행에서 올바른 시스템 특성을 사용하여 JConsole 앱을 시작합니다. 
3. 적절한 원격 프로세스 URI, 사용자 이름 및 비밀번호를 JConsole에 제공합니다.

### 서버 패키지 푸시
{: #push_server_package}

하나의 인스턴스로 제한되는 애플리케이션을 포함한 서버 패키지를 푸시합니다. server.xml 파일에 `monitor-1.0` 및 `restConnector-1.0` 기능이 포함되어 있어야 합니다. basicRegistry 요소와 administrator-role 요소도 있어야 합니다.
```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * 참고: Liberty에서 제공되는 securityUtility 도구를 사용하여 비밀번호가 인코딩되어야 합니다.

### JConsole 앱 시작
{: #start_jconsole_app}

JConsole은 Java 설치에 포함되어 있습니다. JConsole 앱을 시작하려면 &lt;java-home&gt;/bin으로 이동하여 다음 명령을 실행하십시오.
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

Java trustStore를 구성하려면 추가 매개변수를 전달해야 할 수 있습니다. 대부분의 경우에 다음 매개변수가 작동되어야 합니다.
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### 연결 완료
{: #start_jconsole_app}
  * 원격 프로세스 필드에 다음 URL을 채우십시오. 
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  또한 Username 및 Password 필드에 administrator-role 역할 사용자와 server.xml 파일에서 구한 비밀번호를 입력하십시오. 
  * 연결을 클릭하십시오.

연결에 성공하면 JConsole이 모니터링을 시작합니다.

연결에 실패하면 문제점을 진단하는 데 도움이 되는 로그를 생성할 수 있습니다. 먼저, ** -J-Djava.util.logging.config.file=c:/tmp/logging.properties**를 jconsole 명령에 추가하여 클라이언트 측 추적을 수집합니다.
다음은 샘플 로깅 특성 파일입니다.
```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
```
{: #codeblock}

<b>&dash;J&dash;Djavax.net.debug=ssl</b>을 jconsole 명령에 추가할 수도 있습니다. 이렇게 하면 SSL 진단 추적이 별도의 JConsole 출력 창에 생성됩니다. 마지막으로 server.xml 파일에 다음을 추가하여 서버측에 추적을 사용으로 설정할 수 있습니다.
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
