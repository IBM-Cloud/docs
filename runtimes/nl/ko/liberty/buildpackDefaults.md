---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 빌드팩 기본값
{: #buildpack_defauts}

*마지막 업데이트 날짜: 2016년 3월 23일*

Liberty 빌드팩은 Bluemix에서 자주 업데이트됩니다. 각 릴리스에는 보안 수정사항 또는 기능 개선사항이 포함될 수 있습니다. 

빌드팩에는 WAR 또는 EAR 애플리케이션에 대한 Java 버전 또는 Liberty 기능 설정과 같은 설정에 대한 기본값이 있습니다. 일부 기본값은 빌드팩 릴리스 간에 변경될 수 있으며, 이는 애플리케이션에 부정적인 영향을 줄 수 있습니다. 애플리케이션이 빌드팩 기본값의 변경으로 인한 영향을 받지 않도록 하려면, 빌드팩 기본값의 의존을 피하도록 애플리케이션을 구성하는 단계를 수행하십시오. 

## Liberty 기능
{: #liberty_features}

WAR 또는 EAR 파일을 배치하는 경우, 빌드팩은 Liberty 기능의 기본 설정으로 애플리케이션에 대한 구성을 제공합니다. 드문 일이긴 하지만, Liberty 기능의 해당 기본 설정은 빌드팩 릴리스 간에 변경이 가능합니다. 기본 기능 설정을 변경하면 애플리케이션에 부정적인 영향을 줄 수 있습니다. 애플리케이션이 기능 기본값의 변경에 의해 영향을 받지 않도록 보장하는 옵션이 있습니다. 

* 애플리케이션에 대해 사용되는 기능의 목록을 명시적으로 지정하려면 JBP_CONFIG_LIBERTY 환경 변수를 설정하십시오. 자세한 정보는 [독립형 애플리케이션](optionsForPushing.html#stand_alone_apps)을 참조하십시오. 
* 애플리케이션을 [서버 디렉토리](optionsForPushing.html#server_directory) 또는 [패키지된 서버](optionsForPushing.html#packaged_server)로서 배치하십시오. 애플리케이션에서 필요한 정확한 기능 설정을 지정하려면 사용자 정의 server.xml 파일을 제공하십시오. 

서버 디렉토리 또는 패키지된 서버로서 배치된 애플리케이션은 Liberty 기능 기본값의 변경에 의해 영향을 받지 않습니다. 

## Java 버전
{: #java_version}

빌드팩은 애플리케이션의 기본 JRE를 제공합니다. JRE의 주 버전 또는 부 버전은 빌드팩 릴리스 간에 변경될 수 있습니다. JRE의 부 버전은 빈번히 업데이트 가능한 반면 주 버전은 좀처럼 업데이트되지 않습니다. JRE의 주 버전을 변경하면 애플리케이션에 부정적인 영향을 줄 수 있습니다. 

주 버전 변경사항에 의해 애플리케이션이 영향을 받지 않도록 보장하려면, [JRE 사용자 정의](customizingJRE.html)에 설명된 대로 적합한 JRE 버전으로 환경 변수를 설정하십시오. 최상의 결과를 얻으려면 애플리케이션에 대해 Java 8을 채택하십시오. 

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
