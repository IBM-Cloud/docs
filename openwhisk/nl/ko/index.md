---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 시작하기
*마지막 업데이트 날짜: 2016년 2월 17일*

{{site.data.keyword.openwhisk}}는 이벤트 주도적인 분배된 계산 서비스입니다. {{site.data.keyword.openwhisk_short}}는 HTTP를 통한 웹 또는 모바일 앱의 직접 호출 또는 이벤트에 응답하여 애플리케이션 로직을 실행합니다. 이벤트는 Cloudant와 같은 Bluemix 서비스 및 외부 소스에서 제공될 수 있습니다. 개발자는 애플리케이션 로직 작성 및 On-Demand 실행이 수행되는 조치 작성에 집중할 수 있습니다. 조치 실행 비율은 항상 이벤트 비율과 일치하므로 결과적으로 스케일링, 복원성 및 최적 활용도가 상속됩니다. 사용한 부분만 요금을 지불하며 서버를 관리할 필요가 없습니다. 또한 [소스 코드](https://github.com/openwhisk/openwhisk)를 얻어서 스스로 시스템을 실행할 수 있습니다.
{: shortdesc}

{{site.data.keyword.openwhisk_short}} 작동 방법에 대한 세부사항은 [{{site.data.keyword.openwhisk_short}} 정보](./openwhisk_about.html)를 참조하십시오.

## {{site.data.keyword.openwhisk_short}} 설정
{{site.data.keyword.openwhisk_short}} 명령행 인터페이스(CLI)를 사용하여 네임스페이스 및 권한 키를 설정할 수 있습니다. [CLI 구성](https://console.{DomainName}/openwhisk/cli){: new_window}으로 이동하여 안내에 따라 설치하십시오. CLI를 사용하려면 시스템에 Python 2.7이 설치되어 있어야 합니다.

CLI를 사용하여 {{site.data.keyword.openwhisk_short}}가 설정된 후에 명령행 또는 REST API를 사용하여 이를 시작할 수 있습니다.

## {{site.data.keyword.openwhisk_short}} CLI 사용
환경을 구성한 후에 {{site.data.keyword.openwhisk_short}} CLI를 사용하여 다음을 수행할 수 있습니다.

* {{site.data.keyword.openwhisk_short}}에서 코드 스니펫 또는 조치를 실행합니다. [조치 작성 및 호출](./openwhisk_actions.html)을 참조하십시오.
* 조치가 이벤트에 응답할 수 있도록 트리거 및 규칙을 사용합니다. [트리거 및 규칙 작성](./openwhisk_triggers_rules.html)을 참조하십시오.
* 번들 조치를 패키지화하고 외부 이벤트 소스를 구성하는 방법을 학습합니다. [패키지 사용 및 작성](./openwhisk_packages.html)을 참조하십시오.
* 패키지 카탈로그를 탐색하여 [Cloudant 이벤트 소스](./openwhisk_catalog.html#openwhisk_catalog_cloudant) 등의 외부 서비스를 사용하여 애플리케이션을 강화합니다. [{{site.data.keyword.openwhisk_short}} 사용 가능 서비스 사용](./openwhisk_catalog.html)을 참조하십시오.


## iOS 앱에서 {{site.data.keyword.openwhisk_short}} 사용
{{site.data.keyword.openwhisk_short}} iOS SDK를 사용하면 iOS 모바일 앱 또는 Apple Watch에서 {{site.data.keyword.openwhisk_short}}를 사용할 수 있습니다. 세부사항은 [iOS 문서](./openwhisk_mobile_sdk.html)를 참조하십시오.

## {{site.data.keyword.openwhisk_short}}와 함께 REST API 사용
{{site.data.keyword.openwhisk_short}} 환경이 사용 가능하도록 설정된 후에 REST API 호출을 사용하여 웹 앱 및 모바일 앱과 함께 {{site.data.keyword.openwhisk_short}}를 사용할 수 있습니다. 조치, 활성화, 패키지, 규칙 및 트리거에 관한 API에 대한 세부사항은 [{{site.data.keyword.openwhisk_short}} API 문서](https://new-console.{DomainName}/apidocs/98)를 참조하십시오.

## {{site.data.keyword.openwhisk_short}} Hello World 예
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

다음 주제에서 {{site.data.keyword.openwhisk_short}}에 대한 추가 정보를 찾을 수 있습니다.

* [엔티티 이름](./openwhisk_reference.html#openwhisk_entities)
* [조치 시맨틱](./openwhisk_reference.html#openwhisk_semantics)
* [한계](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 관련 링크
## api
* [REST API 문서](https://new-console.{DomainName}/apidocs/98){:new_window}

## 일반
* [검색: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks의 {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
