---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 바인드된 서비스의 자동 구성
{: #auto_config}

*마지막 업데이트 날짜: 2016년 3월 31일*

다양한 서비스를 Liberty 애플리케이션에 바인드할 수 있습니다. 개발자에게 필요한 기능에 따라 서비스는 컨테이너 관리형, 애플리케이션 관리형 또는 두 형태 모두로 제공됩니다.

애플리케이션 관리형 서비스는 Liberty의 지원 없이 애플리케이션에서 전적으로 관리하는 서비스입니다. 일반적으로 VCAP_SERVICES를 읽어 바인드된 서비스에 대한 정보를 가져오고 서비스에 직접 액세스합니다. 필요한 모든 클라이언트 액세스 코드가 제공됩니다. Liberty 기능 또는 server.xml 파일 구성에 종속되지 않습니다. 이 유형의 서비스에는 Liberty 빌드팩 자동 구성이 적용되지 않습니다. 

컨테이너 관리 서비스는 Liberty 런타임에서 관리하는 서비스입니다. 경우에 따라 애플리케이션이 JNDI에서 바인드된 서비스를 찾을 때도 있고, 서비스가 Liberty 자체에 바로 사용되는 때도 있습니다. Liberty 빌드팩은 VCAP_SERVICES를 읽어 바인드된 서비스에 대한 정보를 가져옵니다. 각 컨테이너 관리 서비스에 대해 빌드팩은 다음 세 가지 기능을 수행합니다.

* 바인딩된 서비스의 [클라우드 변수](optionsForPushing.html#accessing_info_of_bound_services)를 생성합니다.
* Liberty 기능과 바인드된 서비스에 액세스하는 데 필요한 클라이언트 액세스 코드를 설치합니다. 
* 서비스에 필요한 server.xml 파일 스탠자를 생성하거나 업데이트합니다. 

이 프로세스를 자동 구성이라고 합니다.
Liberty 빌드팩은 다음 서비스 유형에 대해 자동 구성을 제공합니다. 

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab 
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

이미 설명했듯이, 일부 서비스는 애플리케이션 관리형 또는 컨테이너 관리형으로 이용할 수 있습니다. Mongo와 SQLDB가 이러한 서비스의 일례입니다. 기본적으로, Liberty 빌드팩에서는 이 서비스가 컨테이너 관리형이고 서비스를 자동으로 구성한다고 가정합니다. 애플리케이션이 서비스를 관리하게 하려면 services_autoconfig_excludes 환경 변수를 설정하여 서비스에 대한 자동 구성을 옵트 아웃합니다. 자세한 정보는 [서비스 자동 구성 옵트 아웃](autoConfig.html#opting_out)을 참조하십시오.

## Liberty 기능 및 클라이언트 액세스 코드 설치
{: #installation_of_liberty_features}

컨테이너 관리 서비스에 바인드하는 경우, 서비스가 server.xml 파일의 featureManager 스탠자에 Liberty 기능을 구성해야 할 수 있습니다. Liberty 빌드팩은 featureManager 스탠자를 업데이트하고 필요한 지원 2진을 설치합니다. 서비스에 클라이언트 드라이버 jar이 필요하면 설치된 Liberty의 알려진 위치에 jar이 다운로드됩니다. 

자세한 정보는 바인드된 서비스 유형과 관련된 문서를 참조하십시오.

## server.xml 구성 스탠자 생성 또는 업데이트
{: #generating_or_updating_serverxml}

독립형 애플리케이션을 푸시하면 Liberty 빌드팩에서 Liberty [Liberty 애플리케이션 푸시 옵션](optionsForPushing.html#options_for_pushing)에 설명된 대로 server.xml 스탠자를 Bluemix에 생성합니다. 독립형 애플리케이션을 푸시하고 컨테이너 관리 서비스에 바인드하면 Liberty 빌드팩에서 바인드된 서비스에 필요한 server.xml 스탠자를 생성합니다. 

server.xml 파일을 제공하고 컨테이너 관리 서비스에 바인드하면 Liberty 빌드팩은 다음을 수행합니다.

* 제공된 server.xml 파일에 바인드된 서비스의 구성 스탠자가 없는 경우 바인드된 서비스에 대한 구성을 생성합니다. 
* 제공된 server.xml 파일에 바인드된 서비스의 구성 스탠자가 있는 경우 바인드된 서비스에 대한 구성을 업데이트합니다.

자세한 정보는 바인드된 서비스 유형과 관련된 문서를 참조하십시오.

## 서비스 자동 구성 옵트 아웃
{: #opting_out}

Liberty 빌드팩을 통해 바인드된 서비스를 자동으로 구성하지 않으려는 경우가 있습니다. 다음 시나리오를 고려하십시오. 

* 내 애플리케이션이 MongoDB를 사용하지만, 애플리케이션에서 데이터베이스 연결을 직접 관리하게 하고 싶습니다. 애플리케이션에 필요한 클라이언트 드라이버 jar이 들어 있습니다. Liberty 빌드팩을 통해 Mongo 서비스가 자동으로 구성되는 것을 원하지 않습니다.
* server.xml 파일을 제공하고, 독립형이 아닌 데이터 소스 구성이 필요하므로 SQLDB 인스턴스에 대한 구성 스탠자를 제공했습니다. Liberty 빌드팩을 통해 내 server.xml 파일이 업데이트되는 것을 원하지 않지만, 올바른 지원 소프트웨어가 설치되어 있는지 확인하기 위해 Liberty 빌드팩이 계속 필요합니다. 

자동 서비스 구성을 옵트 아웃하려면 services_autoconfig_excludes 환경 변수를 사용하십시오. 이 환경 변수를 manifest.yml에 포함하거나 cf 클라이언트를 사용하여 설정합니다. 

서비스 자동 구성은 서비스 유형별로 옵트 아웃합니다. 완전히 옵트 아웃하거나(Mongo 시나리오) server.xml 파일 구성 업데이트만 옵트 아웃하도록(SQLDB 시나리오) 선택할 수 있습니다. services_autoconfig_excludes 환경 변수에 지정하는 값은 아래 표시된 대로 문자열입니다. 

* 문자열에는 하나 이상의 서비스에 대한 옵트 아웃 명세가 포함됩니다.
* 특정 서비스의 옵트 아웃 명세는 service_type=option입니다. 여기서, 
  * service_type은 VCAP_SERVICES에 표시된 서비스의 레이블입니다. 
  * 옵션은 all 또는 config입니다.
* 문자열에 두 개 이상 서비스에 대한 옵트 아웃 명세가 포함되어 있는 경우, 공백 문자 하나를 사용해 개별 옵트 아웃 명세를 구분해야 합니다. 

좀 더 공식적으로 표현하자면, 문자열의 문법은 다음과 같습니다. 

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: #codeblock}

**중요**: 사용자가 지정한 서비스 유형이 VCAP_SERVICES 환경 변수에 표시된 서비스 레이블과 일치해야 합니다. 공백은 허용되지 않습니다.
**중요**: <service_type_specification>에 공백을 사용할 수 없습니다. 단, 여러 개의 <service_type_specification> 인스턴스를 구분하는 목적으로만 유일하게 공백을 사용할 수 있습니다.

위의 Mongo 시나리오에서처럼 서비스에 대한 자동 구성 조치를 모두 옵트 아웃하려면 "all" 옵션을 사용하십시오. 위의 SQLDB 시나리오에서처럼 구성 업데이트 조치만 옵트 아웃하려면 "config" 옵션을 사용하십시오. 

다음은 Mongo 및 SQLDB 시나리오에서 manifest.yml 파일에 지정된 샘플 옵트 아웃 명세입니다. 

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

다음은 명령 인터페이스를 사용하여 애플리케이션 myapp에 services_autoconfig_excludes 환경 변수를 설정하는 방법의 예입니다. 

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
