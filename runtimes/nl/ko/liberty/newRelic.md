---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# New Relic 사용
{: #new_relic}

*마지막 업데이트 날짜: 2016년 3월 23일*

New Relic은 애플리케이션에 모니터링 메트릭을 제공하는 써드파티 서비스입니다. New Relic 서비스의 혜택에 대한 자세한 정보는 [New Relic](http://newrelic.com/java)을 참조하십시오.

이 [Java 에이전트 매뉴얼 설치 문서](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation)에 따라 New Relic 서비스를 사용하여 모니터하는 Java 애플리케이션 일반적으로 New Relic 에이전트 및 계정 라이센스 키와 번들로 제공되고 관련 내용이 구성되어 있어야 합니다. IBM Bluemix 환경에서 New Relic 라이센스 계약과 계정은 IBM Bluemix에서 서비스 인스턴스를 작성하여 얻을 수 있습니다. 그런 다음 Java 애플리케이션을 New Relic 서비스 인스턴스에 바인드하고, Liberty 빌드팩에서 New Relic 서비스를 통해 모니터링할 애플리케이션을 자동 구성합니다.
구체적으로, 빌드팩은 다음을 수행합니다.

* 애플리케이션과 New Relic 에이전트를 함께 제공합니다.
* VCAP_APPLICATION 및 VCAP_SERVICES 애플리케이션 환경 변수에서 애플리케이션 이름과 라이센스 키를 확인합니다.
* New Relic 에이전트에 필요한 특성 및 구성 템플리트를 구성합니다.

애플리케이션용 Liberty 빌드팩에서 생성되는 샘플 구성을 참조하십시오.

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## New Relic 서비스 추가
{: #add_new_relic}

IBM Bluemix에서 New Relic을 통해 기존 Java 애플리케이션을 모니터링하려면 다음 단계를 따르십시오. 
1. IBM Bluemix에서 New Relic 서비스 인스턴스를 작성하십시오.
```
    $ cf create-service newrelic standard mynewrelic
```
{: #codeblock}

2. New Relic 서비스를 사용하여 애플리케이션을 IBM Bluemix에 배치하십시오. 다음 샘플 애플리케이션
Manifest를 참조하십시오.
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. 애플리케이션의 IBM Bluemix 대시보드에서 애플리케이션의 New Relic 대시보드에 바로 액세스하십시오. 

### 사용자 제공 New Relic 서비스 추가
{: #add_user_provided_new_relic}

New Relic 계정과 라이센스 키가 이미 있으면 "사용자 제공 서비스"를 사용하여 기존의 New Relic 서비스를 애플리케이션에 바인드할 수 있습니다. 

1. 기존의 라이센스 키를 사용하여 사용자 제공 서비스 인스턴스를 작성하십시오. 예를 들어, 기존의 라이센스 키가 1234567이면 CF CLI를 사용하여 "사용자 제공 서비스를 작성"하고 다음과 같이 프롬프트되면 라이센스 키 1234567을 제공합니다.
```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. 사용자 제공 New Relic 서비스 인스턴스를 사용하여 애플리케이션을 IBM Bluemix에 배치하십시오. 다음은
사용자 제공 New Relic 서비스 인스턴스를 사용하는
샘플 애플리케이션 Manifest입니다.
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. New Relic 대시보드에 액세스하여 애플리케이션 메트릭을 확인하십시오.

New Relic 서비스의 자동 구성은 빌드팩 프레임워크를 통해 제공되는 컨테이너 관리 서비스이므로 다른 서비스의 자동 구성과 다릅니다. 프레임워크를 통해 제공된다는 점에서, 이 서비스의 자동 구성은 다음 3가지 측면에서 다른 서비스들과 차이가 납니다. 
* 옵트 아웃이 옵션이 아닙니다.
* 서비스 통합에 New Relic의 에이전트인 Java 에이전트가 사용됩니다. 따라서, server.xml 파일의 클라우드 변수가 아니라 Java 옵션을 통해 구성됩니다. 
* 구성에 VCAP_SERVICES 및 VCAP_APPLICATION이 사용됩니다.

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
