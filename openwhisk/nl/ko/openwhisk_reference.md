---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 시스템 세부사항
{: #openwhisk_reference}


다음 절에서는 {{site.data.keyword.openwhisk}}에 대한 세부사항을 제공합니다.
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 엔티티
{: #openwhisk_entities}

### 네임스페이스 및 패키지
{: #openwhisk_entities_namespaces}

{{site.data.keyword.openwhisk_short}} 조치, 트리거 및 규칙은 네임스페이스에 속하며 선택적으로 패키지에 속합니다.

패키지는 조치와 피드를 포함할 수 있습니다. 패키지는 다른 패키지를 포함할 수 없으므로 패키지 중첩이 허용되지 않습니다. 또한 엔티티는 패키지에 포함될 필요가 없습니다.

Bluemix에서 조직+영역 쌍은 {{site.data.keyword.openwhisk_short}} 네임스페이스에 해당됩니다. 예를 들어, `BobsOrg` 조직 및 `dev` 영역은 {{site.data.keyword.openwhisk_short}} 네임스페이스 `/BobsOrg_dev`에 해당됩니다.

자격이 부여되면 자신의 네임스페이스를 작성할 수 있습니다. `/whisk.system` 네임스페이스는 {{site.data.keyword.openwhisk_short}} 시스템과 함께 분배되는 엔티티를 위해 예약되어 있습니다.


### 완전한 이름
{: #openwhisk_entities_fullyqual}

엔티티의 완전한 이름은 `/namespaceName[/packageName]/entityName`입니다. 네임스페이스, 패키지 및 엔티티를 구분하기 위해
`/`가 사용됩니다. 또한 네임스페이스에 `/` 접두부가 사용되어야 합니다. 

네임스페이스가 사용자의 *기본 네임스페이스*인 경우 편의상 쓰지 않을 수 있습니다. 

예를 들어, 기본 네임스페이스가 `/myOrg`인 사용자를 고려해 보십시오. 여러 엔티티와 별명의 완전한 이름 예는 다음과 같습니다. 

| 완전한 이름 | 별명 | 네임스페이스 | 패키지 | 이름 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

다른 위치에서 {{site.data.keyword.openwhisk_short}} CLI를 사용할 때 이 명명 체계를 사용할 것입니다.

### 엔티티 이름
{: #openwhisk_entities_names}

조치, 트리거, 규칙, 패키지, 네임스페이스를 포함하여 모든 엔티티의 이름은 다음과 같은 형식을 따르는 일련의 문자입니다. 

* 첫 번째 문자는 영숫자 문자 또는 밑줄이어야 합니다. 
* 후속 문자는 영숫자, 공백 또는 다음 중 하나일 수 있습니다. `_`, `@`, `.`, `-`.
* 마지막 문자는 공백이 될 수 없습니다.

더 정확하게 말해서 이름은 다음 정규식(Java 메타문자 구문으로 표현)과 일치해야 합니다. `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`. 


## 조치 시맨틱
{: #openwhisk_semantics}

다음 절에서는 {{site.data.keyword.openwhisk_short}} 조치에 대한 세부사항을 설명합니다.

### Statelessness
{: #openwhisk_semantics_stateless}

조치 구현이 Stateless이거나 *idempotent*여야 합니다. 시스템이 이 특성을 적용하지 않으며 조치에 의해 유지보수되는 상태가 호출 전체에 걸쳐 사용될 수 있다는 보장도 없습니다.

또한 조치의 다중 인스턴스화가 존재할 수 있으며 각 인스턴스화에 자신의 상태가 있을 수 있습니다. 조치 호출이 이러한 인스턴스화 중 하나에 디스패치될 수 있습니다.

### 호출 입력 및 출력
{: #openwhisk_semantics_invocationio}

조치에 대한 입력 및 출력은 키-값 쌍의 사전입니다. 키는 문자열이며 값은 유효한 JSON 값입니다.

### 조치 호출 순서 지정
{: #openwhisk_ordering}

조치의 호출은 순서가 지정되어 있지 않습니다. 사용자가 명령행 또는 REST API에서 조치를 두 번 호출하면 두 번째 호출이 첫 번째 호출보다 먼저 실행될 수 있습니다. 조치에 부작용이 있으면 어떤 순서도로 관찰될 수 있습니다.

또한 조치가 원자적으로 실행된다는 보장이 없습니다. 두 조치가 동시에 실행되어 부작용이 인터리브될 수 있습니다. OpenWhisk는 부작용과 관련하여 특정 동시 일관성 모델을 보장하지 않습니다. 모든 동시성 부작용은 구현에 따라 다릅니다. 

### 조치 실행 보증
{: #openwhisk_atmostonce}

호출 요청이 수신되면 시스템이 요청을 기록하고 활성화를 디스패치합니다. 

시스템은 호출이 수신되었음을 확인하기 위해 활성화 ID(비블로킹 호출의 경우)를 리턴합니다.
HTTP 응답을 수신하기 전에 개입하는 네트워크 장애 또는 다른 실패가 있는 경우
{{site.data.keyword.openwhisk_short}}에서 요청을 수신하고 처리했을 가능성이 있습니다. 

시스템이 조치를 한 번 호출하려고 시도하면 다음 네 가지 결과 중 하나가 발생합니다.
- *성공*: 조치 호출이 성공적으로 완료됩니다.
- *애플리케이션 오류*: 조치 호출이 성공했으나 인수의 전제조건이 충족되지 않는 등의 이유로 의도적으로 인스턴스에 대한 오류 값이 리턴되었습니다.
- *조치 개발자 오류*: 조치가 호출되었으나 비정상적으로 완료되었습니다. 예를 들어, 조치가 예외를 발견하지 않았거나 구문 오류가 있습니다.
- *whisk 내부 오류*: 시스템이 조치를 호출하지 못했습니다.
결과는 다음 절에서 문서화된 대로 활성화 레코드의 `status` 필드에 기록됩니다.

성공적으로 수신되고 사용자에게 청구될 수 있는 모든 호출은 결과적으로 활성화 레코드를 갖게 됩니다.

*조치 개발자 오류*가 발생한 경우, 조치가 부분적으로 실행되어 가시적인 부작용이 발생했을 수
있습니다. 그러한 부작용이 실제로 발생했는지 여부를 확인하고 필요한 경우 재시도 로직을 실행하는 것은 사용자의
책임입니다. 또한 특정 *whisk 내부 오류*는 조치 실행이 시작되었지만 조치가 완료를 등록하기 전에 시스템이
실패했음을 나타냅니다. 

## 활성화 레코드
{: #openwhisk_ref_activation}

각 조치 호출 및 트리거 실행으로 인해 활성화 레코드가 생성됩니다.

활성화 레코드에는 다음 필드가 포함됩니다.

- *activationId*: 활성화 ID입니다.
- *시작* 및 *종료*: 활성화의 시작 및 종료를 기록하는 시간소인입니다. 값은 [UNIX 시간 형식](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)으로 표시됩니다.
- *네임스페이스* 및 `name`: 엔티티의 네임스페이스 및 이름입니다.
- *로그*: 활성화하는 동안 조치로 인해 생성된 로그가 있는 문자열의 배열입니다. 각 배열 요소는 조치에 따라 `stdout` 또는 `stderr`로 출력된 행에 해당하며 로그 출력의 시간과 스트림을 포함합니다. 구조는 다음과 같습니다. `TIMESTAMP STREAM: LOG_OUTPUT`.
- *응답*: `success` 키, `status` 키, `result` 키를 정의하는 사전입니다.
  - *상태*: "성공", "애플리케이션 오류", "조치 개발자 오류", "whisk 내부 오류" 값 중 하나일 수 있는 활성화 결과입니다.
  - *성공*: 상태가 `"success"`인 경우에만 `true`입니다.
- *결과*: 활성화 결과를 포함하는 사전입니다. 활성화에 성공한 경우 조치에서 리턴된 값이 포함됩니다. 활성화에 실패한 경우에는 `result`에 `error` 키가 포함되며 일반적으로 실패에 대한 설명이 있습니다. 


## JavaScript 조치
{: #openwhisk_ref_javascript}

### 함수 프로토타입
{: #openwhisk_ref_javascript_fnproto}

{{site.data.keyword.openwhisk_short}} JavaScript 조치는 Node.js 런타임에서 실행됩니다.

JavaScript로 작성된 조치는 단일 파일로 구성되어야 합니다. 파일에는 다중 함수가 포함될 수 있으나 편의상 `main`이라 불리는 함수가 반드시 존재해야 하며 조치가 호출될 때 호출되는 함수여야 합니다. 예를 들어, 다음은 다중 함수가 있는 조치의 예입니다.

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

조치 입력 매개변수가 JSON 오브젝트 매개변수로 `main` 함수에 전달됩니다. 성공적인 활성화의 결과 또한 JSON 오브젝트이나 다음 절에서 설명하는 대로 조치가 동기 또는 비동기인지에 따라 다르게 리턴될 수 있습니다.


### 동기 및 비동기 작동
{: #openwhisk_ref_javascript_synchasynch}

일반적으로 JavaScript 함수는 리턴 후에도 콜백 함수에서 계속 실행됩니다. 이를 수용하기 위해 JavaScript 조치의 활성화가 *동기* 또는 *비동기*가 될 수 있습니다.

다음 조건 중 하나 아래에서 기본 함수가 종료되면 JavaScript 조치의 활성화가 **동기**입니다.

- 기본 함수가 `return` 명령문을 실행하지 않고 종료합니다.
- 기본 함수가 Promise를 *제외한* 모든 값을 리턴하는 `return` 명령문을 실행하여 종료합니다. 

다음은 동기 조치의 예제입니다. 

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

JavaScript 조치의 활성화는 기본 함수가 Promise를 리턴하여 존재하는 경우 **비동기**입니다. 이 경우 시스템은 Promise가 이행되거나 거부될 때까지 조치가 여전히 실행 중이라고 가정합니다.
새 Promise 오브젝트를 인스턴스화하고 이를 콜백 함수에 전달하여 시작하십시오. 콜백에는 resolve와 reject라는 두 개의 인수가 사용되며 이는 둘 다 함수입니다. 모든 비동기 코드는 해당 콜백 안에 들어갑니다. 


다음은 resolve 함수를 호출하여 Promise를 이행하는 방법의 예제입니다. 

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

다음은 reject 함수를 호출하여 Promise를 거부하는 방법의 예제입니다. 

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

조치가 일부 입력에서는 동기로, 다른 입력에서는 비동기로 실행될 수 있습니다. 예를 들면, 다음과 같습니다. 

```
  function main(params) {
      if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
                  resolve({ done: true });
                }, 100);
             })
      }  else {
         // synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

활성화가 동기인지 또는 비동기인지 여부에 상관없이 조치의 호출은 블로킹이거나 비블로킹입니다. 

### JavaScript 글로벌 Whisk 오브젝트는 더 이상 사용되지 않음

글로벌 오브젝트 `whisk`는 현재 더 이상 사용되지 않습니다. 대체 메소드를 사용하려면 nodejs 조치를 마이그레이션하십시오.
`whisk.invoke()` 및 `whisk.trigger()` 함수의 경우 클라이언트 라이브러리 [openwhisk](https://www.npmjs.com/package/openwhisk)를 사용할 수 있습니다.
`whisk.getAuthKey()`의 경우 환경 변수 `__OW_API_KEY`의 API 키 값을 가져올 수 있습니다.
`whisk.error()`의 경우 거부된 Promise(즉, Promise.reject)를 리턴할 수 있습니다. 

### JavaScript 런타임 환경
{: #openwhisk_ref_javascript_environments}

JavaScript 조치는 기본적으로 Node.js 버전 6.9.1 환경에서 실행됩니다. 또한 6.9.1 환경은 조치를 작성하거나 업데이트할 때 `--kind` 플래그에 'nodejs:6' 값이 명시적으로 지정된 경우 조치에 사용됩니다.
다음 패키지를 Node.js 6.9.1 환경에서 사용할 수 있습니다. 

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.0.0
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.9.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0

조치를 작성하거나 업데이트할 때 `--kind` 플래그에 'nodejs' 값이 명시적으로 지정된 경우 Node.js 버전 0.12.17 환경이 조치에 사용됩니다.
다음 패키지를 Node.js 0.12.17 환경에서 사용할 수 있습니다. 

**참고**: Node.js 버전 0.12.x는 더 이상 사용되지 않으므로, 모든 Node.js 조치를 마이그레이션하여 Node.js 버전 6.x를 사용하십시오.

- apn v1.7.4
- async v1.5.2
- btoa v1.1.2
- cheerio v0.20.0
- cloudant v1.4.1
- commander v2.7.0
- consul v0.18.1
- cookie-parser v1.3.4
- cradle v0.6.7
- errorhandler v1.3.5
- gm v1.20.0
- jade v1.9.2
- log4js v0.6.38
- merge v1.2.0
- moment v2.8.1
- mustache v2.1.3
- nano v5.10.0
- node-uuid v1.4.2
- oauth2-server v2.4.0
- openwhisk v3.0.0
- process v0.11.0
- request v2.79.0
- rimraf v2.5.1
- semver v4.3.6
- serve-favicon v2.2.0
- socket.io v1.3.5
- socket.io-client v1.3.5
- superagent v1.3.0
- swagger-tools v0.8.7
- tmp v0.0.28
- watson-developer-cloud v1.4.1
- when v3.7.3
- ws v1.1.0
- xml2js v0.4.15
- xmlhttprequest v1.7.0
- yauzl v2.3.1

## Python 조치

Python 조치는 Python 2.7.12를 사용하여 기본적으로 실행됩니다.
표준 Python 라이브러리뿐만 아니라 다음 패키지도 Python 조치에서 사용 가능합니다. 

- attrs v16.1.0
- beautifulsoup4 v4.5.1
- cffi v1.7.0
- click v6.6
- cryptography v1.5
- cssselect v0.9.2
- enum34 v1.1.6
- flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.10
- httplib2 v0.9.2
- idna v2.1
- ipaddress v1.0.16
- itsdangerous v0.24
- jinja2 v2.8
- lxml v3.6.4
- markupsafe v0.23
- parsel v1.0.3
- pyasn1 v0.1.9
- pyasn1-modules v0.0.8
- pycparser v2.14
- pydispatcher v2.0.5
- pyopenssl v16.1.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- twisted v16.4.0
- w3lib v1.15.0
- werkzeug v0.11.10
- zope.interface v4.3.1

## Docker 조치
{: #openwhisk_ref_docker}

Docker 조치는 Docker 컨테이너 내의 사용자 제공 2진을 실행합니다. 2진은 [python:2.7.12-alpine](https://hub.docker.com/r/library/python)을 기반으로 하는 Docker 이미지에서 실행되므로 2진은 이 배포판과 호환 가능해야 합니다. 

Docker 스켈레톤은 OpenWhisk 호환 가능 Docker 이미지를 빌드하는 편리한 방법입니다. `wsk sdk install docker` CLI 명령을 사용하여 스켈레톤을 설치할 수 있습니다.

기본 2진 프로그램은 컨테이너 내부(`/action/exec`)에 있어야 합니다. 실행 파일은 `stdin`을 통해 입력 인수를 수신하고 `stdout`를 통해 결과를 리턴해야 합니다.

`dockerSkeleton`에 포함된 `Dockerfile`을 수정하여 모든 컴파일 단계 또는 종속 항목을 포함시킬 수 있습니다. 

## REST API
{: #openwhisk_ref_restapi}

REST API를 통해 시스템의 모든 기능을 사용할 수 있습니다. 조치, 트리거, 규칙, 패키지, 활성화 및 네임스페이스에 대해 콜렉션 및 엔티티 엔드포인트가 있습니다. 

다음은 콜렉션 엔드포인트입니다. 

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations`

`openwhisk.`<span class="keyword" data-hd-keyref="DomainName">DomainName</span>은 OpenWhisk API 호스트 이름입니다(예: openwhisk.ng.bluemix.net, 172.17.0.1 등).

`{namespace}`의 경우 `_` 문자를 사용하여 사용자의 *기본 네임스페이스*(즉,
이메일 주소)를 지정할 수 있습니다. 

콜렉션 엔드포인트에서 GET 요청을 수행하여 콜렉션에서 엔티티의 목록을 페치할 수 있습니다. 

각 엔티티 유형마다 엔티티 엔드포인트가 있습니다. 

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations/{activationName}`


네임스페이스 엔드포인트와 활성화 엔드포인트는 GET 요청만 지원합니다. 조치 엔드포인트, 트리거 엔드포인트, 규칙 엔드포인트, 패키지 엔드포인트는 GET, PUT, DELETE 요청을 지원합니다. 조치, 트리거, 규칙의 엔드포인트는 POST 요청도 지원하며 이 요청은 조치와 트리거를 호출하고 규칙을 사용 또는 사용 안함으로 설정하는 데 사용됩니다. 세부사항은 [API 참조](https://new-console.{DomainName}/apidocs/98)를 참조하십시오. 

모든 API는 HTTP 기본 인증으로 보호됩니다. 기본 인증 신임 정보는 `~/.wskprops` 파일의 `AUTH` 특성에 있으며 콜론으로 구분됩니다. [CLI 구성 단계](./index.html#openwhisk_start_configure_cli)에서 이 신임 정보를 검색할 수도 있습니다. 

다음은 cURL 명령을 사용하여 `whisk.system` 네임스페이스에서 모든 패키지의 목록을 가져오는 예제입니다. 

```
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}
```
[
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

OpenWhisk API는 웹 클라이언트에서 요청-응답 호출을 지원합니다. OpenWhisk는 교차-원본 리소스 공유 헤더가 포함된 `OPTIONS` 요청에 응답합니다. 현재 모든 원본이 허용되며(즉, 액세스-제어-허용-원본이 "`*`"임) 액세스-제어-허용-헤더가 권한과 컨텐츠-유형을 산출합니다. 

**주의:** 현재 OpenWhisk에서는 계정마다 하나의 키만 지원하므로 단순 시범을 넘어 CORS를 사용하지 않는 것이 좋습니다. 사용자의 키는 클라이언트 측 코드에 임베드되어 공용으로 표시되어야 합니다. 사용 시 주의하십시오. 

## 시스템 한계
{: #openwhisk_syslimits}

### 조치
{{site.data.keyword.openwhisk_short}}에는 조치가 사용할 수 있는 메모리 양, 분당 허용되는 조치 호출 수 등을 포함하여 시스템 한계가 있습니다.  

다음 표에서는 조치에 대한 기본 한계를 나열합니다. 

| 한계 | 설명 | 구성 가능 | 단위 | 기본값 |
| ----- | ----------- | ------------ | -----| ------- |
| 제한시간 | 컨테이너가 N밀리초를 초과하여 실행되도록 허용되지 않음 | 조치당 |  밀리초 | 60000 |
| 메모리 | 컨테이너에 N MB의 메모리를 초과하여 할당되도록 허용되지 않음 | 조치당 | MB | 256 |
| 로그 | 컨테이너는 stdout에 N MB를 초과하여 쓸 수 없음 | 조치당 | MB | 10 |
| 동시 | 실행 중이거나 실행을 위해 큐에 보관된 네임스페이스당 N개 이하의 활성화 | 네임스페이스당 | 수 | 1000 |
| minuteRate | 분당 이를 초과하여 조치를 호출할 수 없음 | 사용자당 | 수 | 5000 |
| codeSize | 조치 코드의 최대 크기 | 구성할 수 없음, 조치당 한계 | MB | 48 |
| 매개변수 | 첨부할 수 있는 최대 매개변수 크기 | 구성할 수 없음, 조치/패키지/트리거당 한계 | MB | 1 |

### 조치당 제한시간(ms)(기본값: 60초)
{: #openwhisk_syslimits_timeout}
* 제한시간 한계 N은 [100ms..300000ms] 범위이며 조치당 밀리초 단위로 설정됩니다.
* 사용자가 조치를 작성할 때 한계를 변경할 수 있습니다.
* N밀리초를 초과하여 실행되는 컨테이너는 종료됩니다.

### 조치 메모리(MB)당(기본값: 256MB)
{: #openwhisk_syslimits_memory}
* 메모리 한계 M은 [128MB..512MB] 범위이며 조치당 MB 단위로 설정됩니다.
* 사용자가 조치를 작성할 때 한계를 변경할 수 있습니다.
* 컨테이너에 한계보다 더 많은 메모리가 할당될 수 없습니다.

### 조치 로그당(MB)(기본값: 10MB)
{: #openwhisk_syslimits_logs}
* 로그 한계 N은 [0MB..10MB] 범위이며 조치당 설정됩니다. 
* 사용자가 조치를 작성하거나 업데이트할 때 한계를 변경할 수 있습니다. 
* 설정된 한계를 초과하는 로그는 잘리고 활성화의 마지막 출력으로 경고가 추가되어 활성화가 설정된 로그 한계를 초과했음을 표시합니다. 

### 조치 아티팩트당(MB)(고정값: 48MB)
{: #openwhisk_syslimits_artifact}
* 조치의 최대 코드 크기는 48MB입니다.
* JavaScript 조치에서 종속 항목을 포함하여 모든 소스 코드를 단일 번들된 파일로 연결하는 데 도구를 사용하도록 권장합니다.

### 활성화 페이로드 크기당(MB)(고정값: 1MB)
{: #openwhisk_syslimits_activationsize}
* 최대 POST 컨텐츠 크기와 조치 호출 또는 트리거 실행을 위해 전달되는 매개변수를 더하면 1MB입니다.

### 네임스페이스 동시 호출당(기본값: 1000)
{: #openwhisk_syslimits_concur}
* 네임스페이스에 대해 실행 중이거나 실행을 위해 큐에 보관된 활성화의 수가 1000을 초과할 수 없습니다.
* 기본 한계는 consul kvstore의 whisk에 의해 정적으로 구성될 수 있습니다.
* 현재 사용자가 한계를 변경할 수 없습니다.

### 분당 호출 수(고정값: 5000)
{: #openwhisk_syslimits_invocations}
* 비율 한계 N은 5000으로 설정되어 1분 창에서 조치 호출의 수를 제한합니다.
* 사용자가 조치를 작성할 때 한계를 변경할 수 없습니다.
* 이 한계를 초과하는 CLI 또는 API 호출은 HTTP 상태 코드 `429: TOO MANY REQUESTS`에 해당하는 오류 코드를 수신합니다.

### 매개변수의 크기(고정값: 1MB)
{: #openwhisk_syslimits_parameters}
* 조치/패키지/트리거의 작성 또는 업데이트에서 매개변수의 크기 한계는 1MB입니다.
* 사용자는 한계를 변경할 수 없습니다. 
* 매개변수가 너무 큰 엔티티는 작성 또는 업데이트 시 거부됩니다. 

### Docker 조치 오픈 파일 상한당(고정값: 64:64)
{: #openwhisk_syslimits_openulimit}
* 최대 오픈 파일 수는 64입니다(하드 한계와 소프트 한계 둘 다에 적용됨).
* docker run 명령에서는 `--ulimit nofile=64:64` 인수를 사용합니다.
* 오픈 파일의 상한에 대한 자세한 정보는 [docker run](https://docs.docker.com/engine/reference/commandline/run) 문서를 참조하십시오.

### Docker 조치 프로세스 상한당(고정값: 512:512)
{: #openwhisk_syslimits_proculimit}
* 사용자가 사용할 수 있는 최대 프로세스 수는 512입니다(하드 한계와 소프트 한계 둘 다에 적용됨).
* docker run 명령에서는 `--ulimit nproc=512:512` 인수를 사용합니다.
* 최대 프로세스 수의 상한에 대한 자세한 정보는 [docker run](https://docs.docker.com/engine/reference/commandline/run) 문서를 참조하십시오. 

### 트리거

트리거는 아래 표에 설명된 대로 분당 실행률에 따라 달라집니다. 

| 한계 | 설명 | 구성 가능 | 단위 | 기본값 |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | 사용자는 분당 이 수를 초과하여 트리거를 실행할 수 없음 | 사용자당 | 수 | 5000 |

### 분당 트리거 수(고정값: 5000)
{: #openwhisk_syslimits_triggerratelimit}
* 비율 한계 N은 5000으로 설정되어 1분 창에서 실행될 수 있는 트리거 수를 제한합니다.
* 사용자는 트리거를 작성할 때 이 한계를 변경할 수 없습니다.
* 이 한계를 초과하는 CLI 또는 API 호출은 HTTP 상태 코드 `429: TOO MANY REQUESTS`에 해당하는 오류 코드를 수신합니다.
