---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Liberty for Java 문제점 해결
{: #ts}


다음은 {{site.data.keyword.Bluemix_notm}}의 Liberty for Java 사용과 관련된 일반적인 문제점 해결 질문에 대한 답입니다.
{:shortdesc}

## 애플리케이션 연결 수락 실패
{: #health_check_timeout}


Liberty 애플리케이션 시작에 실패하고 “연결 수락에 실패함” 오류가 발생합니다. 예를 들면, 로그에 다음과 같은 오류가 표시됩니다.
{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698}
   2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

Bluemix는 애플리케이션이 정상적으로 시작되었는지 확인하기 위해 애플리케이션에 대한 상태 검사를 수행합니다. 상태 검사에서는 애플리케이션이 애플리케이션에 지정된 포트에서 청취 중인지 여부를 테스트합니다. 이 검사의 기본 제한시간은 60초이며 일부 애플리케이션은 시작하는 데 60초 넘게 걸릴 수 있습니다. 애플리케이션을 시작하는 데 오래 걸리는 이유는 여러 가지가 있습니다. 예를 들어, [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) 또는 [New Relic](/docs/runtimes/liberty/newRelic.html)과 같은 서비스를 바인딩하거나 [디버거를 사용](/docs/manageapps/app_mng.html#debug)하는 경우 시작 시간이 늘어납니다. 또한 애플리케이션에서 완료하는 데 시간이 오래 걸리는 초기화 단계를 수행할 수도 있습니다.
{: tsCauses}

먼저 로그를 조사하여 Liberty 애플리케이션 실패를 일으킨 명백한 오류가 있는지 확인하십시오. 명백한 오류를 찾을 수 없는 경우에는 다음을 시도하십시오.
{: tsResolve}

### **상태 검사 제한시간을 늘리십시오. **

* “cf push” 명령을 사용하여 애플리케이션을 배치할 경우 “-t” 옵션을 사용해 애플리케이션 시작 제한시간을 길게 지정하십시오. 예:

        $ cf push myApp -t 180
        {: #codeblock}

* manifest.yml 파일에서 상태 검사 제한시간을 지정할 수도 있습니다. 예:

        ---
           ...
           timeout: 180
        {: #codeblock}

### **appstate 기능을 사용 안함으로 설정하십시오. **

appstate 기능은 Bluemix 상태 검사 프로세스와 통합되어 Liberty 애플리케이션이 완전히 초기화되어야 HTTP 요청을 수신할 수 있도록 합니다. 애플리케이션이 완전히 초기화되면 appstate 기능이 적용되지 않습니다. 이 기능에는 일부 애플리케이션을 시작하는 데 시간이 오래 걸린다는 부작용이 있습니다. appstate 기능을 사용 안함으로 설정하려면 애플리케이션에서 다음 환경 특성을 설정하고 애플리케이션을 다시 스테이징하십시오. 

```
$ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **애플리케이션을 리팩토링하십시오. **

애플리케이션을 초기화하는 데 시간이 오래 걸리는 경우 애플리케이션을 리팩토링하여 지연 및/또는 비동기 초기화를 수행해야 합니다. 

### **“no-route” 옵션을 지정하여 배치하십시오.**

1. “--no-route” 옵션을 지정하여 애플리케이션을 배치하십시오. 그러면 포트 상태 검사를 사용하지 않습니다. 예:

        $ cf push myApp –no-route
        {: #codeblock}

2. 애플리케이션이 초기화되면 라우트를 애플리케이션에 맵핑하십시오. 예:

        $ cf map-route myApp mybluemix.net
        {: #codeblock}

## IBM 게이트웨이에서 SSL 오류 발생
{: #ssl_handshake_failure}


로그에 다음 오류가 표시되고 애플리케이션을 시작할 수 없습니다.
{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
    2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

Monitoring & Analytics 서비스가 Liberty 애플리케이션에 바인드되고 Liberty 애플리케이션이 Liberty ssl-1.0 기능을 구성하는 server.xml을 포함하는 패키지된 서버 또는 서버 디렉토리로 배치된 경우 오류가 생성될 수 있습니다. Monitoring & Analytics 서비스를 Liberty 애플리케이션에 바인드하면 런타임이 보안 연결을 통해 서비스에 연결합니다. 해당 보안 연결은 기본 SSL 설정을 사용해 설정됩니다. 기본 SSL 설정은 Liberty의 server.xml에서 지정되므로 구성된 신뢰 저장소에서 Monitoring & Analytics 서비스에 사용되는 인증서를 신뢰하지 않을 수 있습니다.
{: tsCauses}

다음 옵션 중 하나를 지정하여 JVM의 신뢰 저장소를 사용하도록 구성을 수정하십시오. 변경 후 애플리케이션을 다시 스테이징해야 합니다.
{: tsResolve}

### Liberty의 server.xml 업데이트

JVM의 cacerts 파일을 신뢰 저장소로 사용하도록 server.xml을 업데이트하십시오. 다음을 server.xml에 추가하십시오. 

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### 구성된 신뢰 저장소 업데이트

DigitCert ROOT CA를 신뢰하도록 구성된 신뢰 저장소를 수정하십시오.
  1. https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt에서 DigiCert Root CA를 다운로드하십시오.
  2. resources/security/key.jks를 신뢰 저장소로 사용할 경우 Java의 keytool 유틸리티를 사용하여 CA를 키로 가져오십시오.

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
            {: codeblock}
