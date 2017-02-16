---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 시작하기


{{site.data.keyword.openwhisk}}는 이벤트로 구동되는 분산형 컴퓨팅 서비스이며 Serverless 컴퓨팅 또는 FaaS(Function as a Service)라고도 합니다. {{site.data.keyword.openwhisk_short}}는 HTTP를 통한 웹 또는 모바일 앱에서의 직접 호출이나 이벤트에 응답하여 애플리케이션 로직을 실행합니다. Cloudant 같은 Bluemix 서비스와 외부 소스에서 이벤트를 제공할 수 있습니다. 개발자는 애플리케이션 로직 작성 및 On-Demand 실행이 수행되는 조치 작성에 집중할 수 있습니다. 조치 실행 비율은 항상 이벤트 비율과 일치하므로 스케일링, 복원성, 최적 활용도가 상속됩니다. 사용한 부분만 요금을 지불하며 서버를 관리할 필요가 없습니다. 또한 [소스 코드](https://github.com/openwhisk/openwhisk)를 얻어서 스스로 시스템을 실행할 수 있습니다.
{: shortdesc}

{{site.data.keyword.openwhisk_short}} 작동 방법에 대한 세부사항은 [{{site.data.keyword.openwhisk_short}} 정보](./openwhisk_about.html)를 참조하십시오.

브라우저 또는 CLI를 사용하여 {{site.data.keyword.openwhisk_short}} 애플리케이션을 개발할 수 있습니다.
둘 다 애플리케이션을 개발하는 데 유사한 기능을 제공하지만, CLI가 배치와 오퍼레이션을 더 효율적으로 제어합니다.


## 브라우저에서 개발
{: #openwhisk_start_editor}

[브라우저](https://console.{DomainName}/openwhisk/editor){: new_window}에서 {{site.data.keyword.openwhisk_short}}를 시도하여 조치를 작성하고, 트리거를 사용해 조치를 자동화하며, 퍼블릭 패키지를 탐색하십시오.
OpenWhisk 사용자 인터페이스 둘러보기를 보려면 [자세히 보기](https://console.{DomainName}/openwhisk/learn){: new_window} 페이지를 참조하십시오.

## {{site.data.keyword.openwhisk_short}} CLI 설정
{: #openwhisk_start_configure_cli}

{{site.data.keyword.openwhisk_short}} 명령행 인터페이스(CLI)를 사용하여 네임스페이스 및 권한 키를 설정할 수 있습니다.
[CLI 구성](https://new-console.{DomainName}/openwhisk/cli){: new_window}으로 이동하고 지시사항에 따라 이를 설치하십시오. 

### HTTPS 프록시를 사용하도록 CLI 구성
{: #openwhisk_configure_https_proxy_cli}

HTTPS 프록시를 사용하도록 CLI를 설정할 수 있습니다. HTTPS 프록시를 설정하려면 `HTTPS_PROXY`라는 환경 변수를
 작성해야 합니다. 이 변수는 `{PROXY IP}:{PROXY PORT}` 형식을 사용하여
HTTPS 프록시의 주소 및 해당 포트로 설정해야 합니다. 

CLI를 사용하여 {{site.data.keyword.openwhisk_short}}를 설정한 후 명령행에서 이를 시작할 수 있습니다. 

## {{site.data.keyword.openwhisk_short}} CLI 사용
{: #openwhisk_start_using_cli}

[환경을 구성한](https://new-console.{DomainName}/openwhisk/cli){: new_window} 후에 {{site.data.keyword.openwhisk_short}} CLI를 사용하기 시작하여 다음을 수행할 수 있습니다. 

* {{site.data.keyword.openwhisk_short}}에서 코드 스니펫 또는 조치를 실행합니다. [조치 작성 및 호출](./openwhisk_actions.html)을 참조하십시오.
* 조치가 이벤트에 응답할 수 있도록 트리거 및 규칙을 사용합니다. [트리거 및 규칙 작성](./openwhisk_triggers_rules.html)을 참조하십시오.
* 번들 조치를 패키지화하고 외부 이벤트 소스를 구성하는 방법을 학습합니다. [패키지 사용 및 작성](./openwhisk_packages.html)을 참조하십시오.
* 패키지 카탈로그를 탐색하여 [Cloudant 이벤트 소스](./openwhisk_catalog.html#openwhisk_catalog_cloudant) 등의 외부 서비스를 사용하여 애플리케이션을 강화합니다. [{{site.data.keyword.openwhisk_short}} 사용 가능 서비스 사용](./openwhisk_catalog.html)을 참조하십시오.


## iOS 앱에서 {{site.data.keyword.openwhisk_short}} 사용
{: #openwhisk_start_using_ios}

{{site.data.keyword.openwhisk_short}} iOS SDK를 사용하면 iOS 모바일 앱 또는 Apple Watch에서 {{site.data.keyword.openwhisk_short}}를 사용할 수 있습니다. 세부사항은 [iOS 문서](./openwhisk_mobile_sdk.html)를 참조하십시오. 

## {{site.data.keyword.openwhisk_short}}와 함께 REST API 사용
{: #openwhisk_start_using_restapi}

{{site.data.keyword.openwhisk_short}} 환경이 사용 가능하도록 설정된 후에 REST API 호출을 사용하여 웹 앱 및 모바일 앱과 함께 {{site.data.keyword.openwhisk_short}}를 사용할 수 있습니다.
조치, 활성화, 패키지, 규칙, 트리거 관련 API에 대한 세부사항은 [{{site.data.keyword.openwhisk_short}} API 문서](https://new-console.{DomainName}/apidocs/98)를 참조하십시오. 

## {{site.data.keyword.openwhisk_short}} Hello World 예
{: #openwhisk_start_hello_world}
{{site.data.keyword.openwhisk_short}}를 시작하려면 다음 JavaScript 코드 예를 시도하십시오.

```
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

이 예를 사용하려면 다음 단계에 따르십시오.

1. 코드를 파일에 저장하십시오. 예: *hello.js*.

2. {{site.data.keyword.openwhisk_short}} CLI 명령행에 다음 명령을 입력하여 조치를 작성하십시오.

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. 그런 다음 아래 명령을 입력하여 조치를 호출하십시오.

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    이 명령은 다음과 같이 출력됩니다.

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    이 명령은 다음과 같이 출력됩니다.

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

또한 {{site.data.keyword.openwhisk_short}}에서 이벤트 주도적인 기능을 사용하여 이벤트에 대한 응답으로 이 조치를 호출할 수 있습니다. [알람 서비스 예](./openwhisk_packages.html#openwhisk_packages_trigger)에 따라 정기 이벤트가 생성될 때마다 이벤트 소스가 `hello` 조치를 호출하도록 구성하십시오.


## 시스템 세부사항
{: #openwhisk_system_details}

다음 주제에서 {{site.data.keyword.openwhisk_short}}에 대한 추가 정보를 찾을 수 있습니다.

* [엔티티 이름](./openwhisk_reference.html#openwhisk_entities)
* [조치 시맨틱](./openwhisk_reference.html#openwhisk_semantics)
* [한계](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 관련 링크
{: #rellinks notoc}

## API 참조
{: #api}
* [REST API 문서](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 관련 링크
{: #general}
* [검색: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks의 {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
