---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 시작하기


{{site.data.keyword.openwhisk}}는 이벤트로 구동되는 분산형 컴퓨팅 서비스이며 Serverless 컴퓨팅 또는 FaaS(Function as a Service)라고도 합니다. {{site.data.keyword.openwhisk_short}}는 HTTP를 통한 웹 또는 모바일 앱에서의 직접 호출이나 이벤트에 응답하여 애플리케이션 로직을 실행합니다. Cloudant 같은 Bluemix 서비스와 외부 소스에서 이벤트를 제공할 수 있습니다. 개발자는 애플리케이션 로직 작성 및 On-Demand 실행이 수행되는 조치 작성에 집중할 수 있습니다. 새 패러다임의 이점은 서버를 명시적으로 프로비저닝하지 않고 Auto-Scaling에 대해 염려하지 않아도 되거나, 서버가 실행되지만 요청을 제공하지 않는 경우 고가용성, 업데이트, 유지보수 및 프로세서 시간에 대한 비용에 대해 걱정하지 않아도 된다는 점입니다.
HTTP 호출, 데이터베이스 스테이지 변경 또는 코드 실행을 트리거하는 다른 이벤트 유형이 있을 때마다 사용자 코드가 실행됩니다.
VM이 유용한 작업을 수행하는지 여부에 관계없이 VM 사용률에 대해 시간당이 아닌 밀리초 단위 실행 시간(반올림하여 100ms)을 기준으로 청구됩니다.
{: shortdesc}

이 프로그래밍 모델은 마이크로서비스, 모바일, IoT 및 기타 많은 앱에 적합합니다. 즉, 클러스터, 로드 밸런서, http 플러그인 등을 수동으로 구성하지 않고도 내재된 Auto-Scaling 및 로드 밸런싱을 바로 사용할 수 있습니다. {{site.data.keyword.openwhisk}}에서 실행하는 경우 IBM에서 모든 하드웨어, 네트워크 및 소프트웨어를 유지보수하므로 관리가 전혀 필요하지 않습니다. 실행할 코드를 제공하고 이 코드를 {{site.data.keyword.openwhisk}}에 전달하기만 하면 됩니다. 나머지는 그냥 이루어집니다. 서버리스(serverless) 프로그래밍 모델에 대한 소개는 [Martin Fowler의 블로그](https://martinfowler.com/articles/serverless.html)에서 볼 수 있습니다.

또한 [Apache OpenWHisk 소스 코드](https://github.com/openwhisk/openwhisk)를 가져와 시스템을 실행할 수도 있습니다.

{{site.data.keyword.openwhisk_short}} 작동 방법에 대한 세부사항은 [{{site.data.keyword.openwhisk_short}} 정보](./openwhisk_about.html)를 참조하십시오.

브라우저 또는 CLI를 사용하여 {{site.data.keyword.openwhisk_short}} 애플리케이션을 개발할 수 있습니다.
둘 다 애플리케이션을 개발하는 데 유사한 기능을 제공하지만, CLI가 배치와 오퍼레이션을 더 효율적으로 제어합니다.

## 브라우저에서 개발
{: #openwhisk_start_editor}

[브라우저](https://console.{DomainName}/openwhisk/editor){: new_window}에서 {{site.data.keyword.openwhisk_short}}를 시도하여 조치를 작성하고, 트리거를 사용해 조치를 자동화하며, 퍼블릭 패키지를 탐색하십시오.
OpenWhisk 사용자 인터페이스 둘러보기를 보려면 [자세히 보기](https://console.{DomainName}/openwhisk/learn){: new_window} 페이지를 참조하십시오.

## CLI를 사용하여 개발
{: #openwhisk_start_configure_cli}

{{site.data.keyword.openwhisk_short}} 명령행 인터페이스(CLI)를 사용하여 네임스페이스 및 권한 키를 설정할 수 있습니다.
[CLI 구성](https://new-console.{DomainName}/openwhisk/cli){: new_window}으로 이동하고 지시사항에 따라 이를 설치하십시오. 

## 개요
{: #openwhisk_start_overview}
- [OpenWhisk 작동 방식](./openwhisk_about.html)
- [서버리스(serverless) 애플리케이션에 대한 공통 유스 케이스](./openwhisk_use_cases.html)
- [OpenWhisk CLI 설정 및 사용](./openwhisk_cli.html)
- [iOS 앱에서 OpenWhisk 사용](./openwhisk_mobile_sdk.html)

## 프로그래밍 모델
{: #openwhisk_start_programming}
- [시스템 세부사항](./openwhisk_reference.html)
- [OpenWhisk 제공 서비스의 카탈로그](./openwhisk_catalog.html)
- [조치](./openwhisk_actions.html)
- [트리거 및 규칙](./openwhisk_triggers_rules.html)
- [피드](./openwhisk_feeds.html)
- [패키지](./openwhisk_packages.html)
- [어노테이션](./openwhisk_annotations.html)
- [웹 조치](./openwhisk_webactions.html)
- [API 게이트웨이](./openwhisk_apigateway.html)
- [엔티티 이름](./openwhisk_reference.html#openwhisk_entities)
- [조치 시맨틱](./openwhisk_reference.html#openwhisk_semantics)
- [한계](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}} Hello World 예
{: #openwhisk_start_hello_world}
{{site.data.keyword.openwhisk_short}}를 시작하려면 다음 JavaScript 코드 예를 시도하십시오.

```javascript
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

    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    이 명령은 다음과 같이 출력됩니다.

    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

또한 {{site.data.keyword.openwhisk_short}}에서 이벤트 주도적인 기능을 사용하여 이벤트에 대한 응답으로 이 조치를 호출할 수 있습니다. [알람 서비스 예](./openwhisk_packages.html#openwhisk_packages_trigger)에 따라 정기 이벤트가 생성될 때마다 이벤트 소스가 `hello` 조치를 호출하도록 구성하십시오.


## API 참조
{: #openwhisk_start_api notoc}
* [REST API 문서](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 관련 링크
{: #general notoc}
* [검색: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks의 {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
* [Apache {{site.data.keyword.openwhisk_short}} 프로젝트 웹 사이트](http://openwhisk.org){:new_window}
