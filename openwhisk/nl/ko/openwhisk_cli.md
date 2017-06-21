---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} CLI

{{site.data.keyword.openwhisk_short}}는 시스템의 모든 측면을 완전히 관리할 수 있는 강력한 명령행 인터페이스를 제공합니다.

## {{site.data.keyword.openwhisk_short}} CLI 설정 

{{site.data.keyword.openwhisk_short}} 명령행 인터페이스(CLI)를 사용하여 네임스페이스 및 권한 키를 설정할 수 있습니다.
[CLI 구성](https://console.{DomainName}/openwhisk/cli)으로 이동하고 지시사항에 따라 이를 설치하십시오. 

CLI를 사용하기 위해 구성할 두 가지 필수 특성은 다음과 같습니다.

1. 사용할 {{site.data.keyword.openwhisk_short}} 배치의 **API 호스트**(이름 또는 IP 주소).
2. {{site.data.keyword.openwhisk_short}} API에 대한 액세스 권한을 부여하는 **권한 키**(사용자 이름 및 비밀번호).

다음 명령을 실행하여 API 호스트를 설정하십시오.

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

권한 키를 알고 있는 경우 이 키를 사용하도록 CLI를 구성할 수 있습니다. 

다음 명령을 실행하여 권한 키를 설정하십시오.

```
wsk property set --auth <authorization_key>
```
{: pre}

**팁:** OpenWhisk CLI는 기본적으로 `~/.wskprops`에 설정된 특성을 저장합니다. 이 파일 위치는 `WSK_CONFIG_FILE` 환경 변수를 설정하여 변경 가능합니다. 

CLI 설정을 확인하려면 [조치 작성 및 실행](./index.html#openwhisk_start_hello_world)을 시도하십시오.

## {{site.data.keyword.openwhisk_short}} CLI 사용

환경을 구성한 후 {{site.data.keyword.openwhisk_short}} CLI를 사용하여 다음을 수행할 수 있습니다.

* {{site.data.keyword.openwhisk_short}}에서 코드 스니펫 또는 조치를 실행합니다. [조치 작성 및 호출](./openwhisk_actions.html)을 참조하십시오.
* 조치가 이벤트에 응답할 수 있도록 트리거 및 규칙을 사용합니다. [트리거 및 규칙 작성](./openwhisk_triggers_rules.html)을 참조하십시오.
* 번들 조치를 패키지화하고 외부 이벤트 소스를 구성하는 방법을 학습합니다. [패키지 사용 및 작성](./openwhisk_packages.html)을 참조하십시오.
* 패키지 카탈로그를 탐색하여 [Cloudant 이벤트 소스](./openwhisk_cloudant.html) 등의 외부 서비스를 사용하여 애플리케이션을 강화합니다. [OpenWhisk 사용 서비스 사용](./openwhisk_catalog.html)을 참조하십시오.

## HTTPS 프록시를 사용하도록 CLI 구성

HTTPS 프록시를 사용하도록 CLI를 설정할 수 있습니다. HTTPS 프록시를 설정하려면 환경 변수 `HTTPS_PROXY`를 작성해야 합니다. 이 변수는 `{PROXY IP}:{PROXY PORT}` 형식을 사용하여
HTTPS 프록시의 주소 및 해당 포트로 설정해야 합니다. 
