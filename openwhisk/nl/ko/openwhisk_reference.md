---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 시스템 세부사항
{: #openwhisk_reference}
*마지막 업데이트 날짜: 2016년 4월 14일*

다음 절에서는 {{site.data.keyword.openwhisk}}에 대한 세부사항을 제공합니다.
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 엔티티
{: #openwhisk_entities}

### 네임스페이스 및 패키지

{{site.data.keyword.openwhisk_short}} 조치, 트리거 및 규칙은 네임스페이스에 속하며 선택적으로 패키지에 속합니다.

패키지는 조치와 피드를 포함할 수 있습니다. 패키지는 다른 패키지를 포함할 수 없으므로 패키지 중첩이 허용되지 않습니다. 또한 엔티티는 패키지에 포함될 필요가 없습니다.

Bluemix에서 조직+영역 쌍은 {{site.data.keyword.openwhisk_short}} 네임스페이스에 해당됩니다. 예를 들어, `BobsOrg` 조직 및 `dev` 영역은 {{site.data.keyword.openwhisk_short}} 네임스페이스 `/BobsOrg_dev`에 해당됩니다.

자격이 부여되면 자신의 네임스페이스를 작성할 수 있습니다. `/whisk.system` 네임스페이스는 {{site.data.keyword.openwhisk_short}} 시스템과 함께 분배되는 엔티티를 위해 예약되어 있습니다.


### 완전한 이름

엔티티의 완전한 이름은 `/namespaceName[/packageName]/entityName`입니다. 네임스페이스, 패키지 및 엔티티를 구분하기 위해
`/`가 사용됩니다. 또한 네임스페이스에 `/` 접두부가 사용되어야 합니다.

네임스페이스가 사용자의 *기본 네임스페이스*인 경우, 편의상 쓰지 않을 수 있습니다.

예를 들어, 기본 네임스페이스가 `/myOrg`인 사용자를 고려해 보십시오. 다음은
수많은 엔티티 및 별명의 완전한 이름 예입니다.

| 완전한 이름 | 별명 | 네임스페이스 | 패키지 | 이름 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` | - | `filter` |

다른 위치에서 {{site.data.keyword.openwhisk_short}} CLI를 사용할 때 이 명명 체계를 사용할 것입니다.

### 엔티티 이름

조치, 트리거, 규칙, 패키지 및 네임스페이스를 포함하여 모든 엔티티의 이름은 다음 형식을 따르는 일련의 문자입니다.

* 첫 번째 문자는 영숫자 문자, 숫자 또는 밑줄이어야 합니다.
* 후속 문자는 영숫자, 숫자, 공백 또는 다음 중 하나일 수 있습니다. `_`, `@`, `.`, `-`.
* 마지막 문자는 공백이 될 수 없습니다.

더 정확하게 말해서, 이름이 다음 정규식(Java 메타문자 구문)과 일치해야 합니다. `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## 조치 시맨틱
{: #openwhisk_semantics}

다음 절에서는 {{site.data.keyword.openwhisk_short}} 조치에 대한 세부사항을 설명합니다.

### Stateless

조치 구현이 Stateless이거나 *idempotent*여야 합니다. 시스템이 이 특성을 적용하지 않으며 조치에 의해 유지보수되는 상태가 호출 전체에 걸쳐 사용될 수 있다는 보장도 없습니다.

또한 조치의 다중 인스턴스화가 존재할 수 있으며 각 인스턴스화에 자신의 상태가 있을 수 있습니다. 조치 호출이 이러한 인스턴스화 중 하나에 디스패치될 수 있습니다.

### 입력 및 출력 호출

조치에 대한 입력 및 출력은 키-값 쌍의 사전입니다. 키는 문자열이며 값은 유효한 JSON 값입니다.

### 조치 호출 순서 지정
{: #openwhisk_ordering}

조치의 호출은 순서가 지정되어 있지 않습니다. 사용자가 명령행 또는 REST API에서 조치를 두 번 호출하면 두 번째 호출이 첫 번째 호출보다 먼저 실행될 수 있습니다. 조치에 부작용이 있으면 어떤 순서도로 관찰될 수 있습니다.

또한 조치가 원자적으로 실행된다는 보장이 없습니다. 두 조치가 동시에 실행되어 부작용이 인터리브될 수 있습니다. 모든 동시성 부작용은 구현에 따라 다릅니다.

### 최대 한 번 시맨틱
{: #openwhisk_atmostonce}

시스템에서는 조치의 최대 일회 호출을 지원합니다.

호출 요청이 수신되면 시스템이 요청을 기록하고 활성화를 신속히 처리합니다.

시스템은 호출이 수신되었음을 확인하기 위해 활성화 ID(비블로킹 호출의 경우)를 리턴합니다. (네트워크 연결 끊김 등의 이유로) 이 응답이 없는 경우에도 호출이 수신되었을 수 있습니다.

시스템이 조치를 한 번 호출하려고 시도하면 다음 네 가지 결과 중 하나가 발생합니다.
- *성공*: 조치 호출이 성공적으로 완료됩니다.
- *애플리케이션 오류*: 조치 호출이 성공했으나 인수의 전제조건이 충족되지 않는 등의 이유로 의도적으로 인스턴스에 대한 오류 값이 리턴되었습니다.
- *조치 개발자 오류*: 조치가 호출되었으나 비정상적으로 완료되었습니다. 예를 들어, 조치가 예외를 발견하지 않았거나 구문 오류가 있습니다.
- *whisk 내부 오류*: 시스템이 조치를 호출하지 못했습니다.
결과는 다음 절에서 문서화된 대로 활성화 레코드의 `status` 필드에 기록됩니다.

성공적으로 수신되고 사용자에게 청구될 수 있는 모든 호출은 결과적으로 활성화 레코드를 갖게 됩니다.


## 활성화 레코드
{: #openwhisk_ref_activation}

각 조치 호출 및 트리거 실행으로 인해 활성화 레코드가 생성됩니다.

활성화 레코드에는 다음 필드가 포함됩니다.

- *activationId*: 활성화 ID입니다.
- *시작* 및 *종료*: 활성화의 시작 및 종료를 기록하는 시간소인입니다. 값은 [UNIX 시간 형식](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)으로 표시됩니다.
- *네임스페이스* 및 `이름`: 엔티티의 네임스페이스 및 이름입니다.
- *로그*: 활성화 동안 조치에 의해 생성된 로그가 있는 문자열의 배열입니다. 각 배열 요소는 조치에 의한 stdout 또는 stderr에 대한 행 출력에 해당되며 로그 출력의 시간 및 스트림을 포함합니다. 구조는 다음과 같습니다. ```TIMESTAMP STREAM: LOG_OUTPUT```.
- *응답*: `success`, `status` 및 `result` 키를 정의하는 사전입니다.
  - *상태*: "성공", "애플리케이션 오류", "조치 개발자 오류", "whisk 내부 오류" 값 중 하나일 수 있는 활성화 결과입니다.
  - *성공*: 상태가 `"success"`인 경우에만 `true`입니다.
- *결과*: 활성화 결과를 포함하는 사전입니다. 활성화가 성공적이면 조치에 의해 리턴된 값이 포함됩니다. 활성화가 실패이면 `result`가 `error` 키를 포함하며 일반적으로 실패에 대한 설명이 있습니다.


## JavaScript 조치
{: #openwhisk_ref_javascript}

### 함수 프로토타입

{{site.data.keyword.openwhisk_short}} JavaScript 조치는 Node.js 런타임에서 실행되며 현재 버전은 0.12.9입니다.

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


### 동기 및 비동기 동작

JavaScript 함수가 리턴 후에도 콜백 짝수에서 계속 실행되는 것이 일반적입니다. 이를 수용하기 위해 JavaScript 조치의 활성화가 *동기* 또는 *비동기*가 될 수 있습니다.

다음 조건 중 하나 아래에서 기본 함수가 종료되면 JavaScript 조치의 활성화가 **동기**입니다.

- ```return``` 명령문을 실행하지 않고 기본 함수가 종료됩니다.
- 임의의 값 *except* ```whisk.async()```를 리턴하는 ```return`` 명령문을 실행하여 기본 함수가 종료됩니다.

다음은 동기 조치의 두 가지 예입니다.

```
// a synchronous action
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indicates normal completion
  } else if (params.payload == 2) {
    return whisk.error();   // indicates abnormal completion
  }
}
```
{: codeblock}

```return whisk.async();```를 호출하여 기본 함수가 종료되면 JavaScript 조치의 활성화가 **비동기**입니다. 이 경우, 시스템은 조치가 다음 중 하나를 실행할 때까지 조치가 여전히 실행 중이라고 가정합니다.
- ```return whisk.done();```
- ```return whisk.error();```

다음은 비동기적으로 실행되는 조치의 예입니다.

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

조치가 일부 입력에서는 동기적으로, 다른 입력에서는 비동기적으로 실행될 수 있습니다. 다음은 그에 대한 예입니다.

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // asynchronous activation
      }  else {
         return whisk.done();   // synchronous activation
      }
  }
```
{: codeblock}

- 이 경우, `main` 함수가 `whisk.async()`를 리턴해야 합니다. 활성화 결과가 사용 가능한 경우에는 `whisk.done()` 함수가 JSON 오브젝트로서 전달된 결과와 함께 호출되어야 합니다. 이를 *비동기* 활성화라고 합니다.

활성화가 동기인지 비동기인지에 상관없이 조치의 호출이 블로킹 또는 비블로킹일 수 있습니다.

### 추가 SDK 메소드

`whisk.invoke()` 함수는 또 다른 조치를 호출합니다. 이 경우, 다음 매개변수를 정의하는 사전을 인수로 사용합니다.

- *name*: 호출할 조치의 완전한 이름입니다.
- *parameters*: 호출된 조치에 대한 입력을 나타내는 JSON 오브젝트입니다. 생략하는 경우, 기본값은 비어 있는 오브젝트입니다.
- *apiKey*: 조치를 호출할 때 사용할 권한 키입니다.
기본값은 `whisk.getAuthKey()`입니다. 
- *blocking*: 조치가 블로킹 또는 비블로킹 모드로 호출되어야 하는지 나타냅니다. 기본값은 비블로킹 호출을 나타내는 `false`입니다.
- *next*: 호출이 완료될 때 실행되는 선택적 콜백 함수입니다.

`next`에 대한 시그니처는 `function(error, activation)`입니다. 여기서, 

- `error`는 호출이 성공하면 `false`이며 실패하면 진리치이며 일반적으로 오류를 설명하는 문자열입니다.
- 오류가 발생하면 실패 모드에 따라 `activation`이 정의되지 않을 수 있습니다.
- 정의되면 `activation`이 다음 필드가 있는 사전입니다.
  - *activationId*: 활성화 ID입니다.
  - *결과*: 조치가 블로킹 모드에서 호출되면 조치의 결과가 JSON 오브젝트이며 그렇지 않으면 `undefined`입니다.

`whisk.trigger()` 함수가 트리거를 실행합니다. 이 경우, 다음 매개변수가 있는 JSON 오브젝트를 인수로 사용합니다.

- *name*: 호출할 트리거의 완전한 이름입니다.
- *parameters*: 트리거에 대한 입력을 나타내는 JSON 오브젝트입니다. 생략하는 경우, 기본값은 비어 있는 오브젝트입니다.
- *apiKey*: 트리거를 실행할 때 사용할 권한 키입니다. 기본값은 `whisk.getAuthKey()`입니다.
- *next*: 실행이 완료될 때 실행되는 선택적 콜백입니다.

`next`에 대한 시그니처는 `function(error, activation)`입니다. 여기서, 

- `error`는 실행이 성공하면 `false`이며 실패하면 진리치이며 일반적으로 오류를 설명하는 문자열입니다.
- 오류가 발생하면 실패 모드에 따라 `activation`이 정의되지 않을 수 있습니다.
- 정의되면 `activation`이 활성화 ID를 포함하는 `activationId` 필드가 있는 사전입니다.

`whisk.getAuthKey()` 함수가 조치가 실행되는 권한 키를 리턴합니다. 일반적으로 이 함수는 `whisk.invoke()` 및 `whisk.trigger()` 함수에 의해 내재적으로 사용되므로 직접 호출할 필요가 없습니다.

### 런타임 환경
{: #openwhisk_ref_runtime_environment}

JavaScript 조치는 조치에 의해 사용 가능한 다음 패키지와 함께 Node.js 버전 0.12.9 환경에서 실행됩니다.

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- jade
- log4js
- merge
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- request
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Docker 조치
{: #openwhisk_ref_docker}

Docker 조치는 Docker 컨테이너 내의 사용자 제공 2진을 실행합니다. 2진은 Ubuntu 14.04 LTD를 기반으로 하는 Docker 이미지에서 실행되므로 2진이 이 배포와 호환 가능해야 합니다.

조치 입력 "payload" 매개변수는 위치 인수로 2진 프로그램에 전달되고 프로그램 실행의 표준 출력은 "result" 매개변수로 리턴됩니다.

Docker 스켈레톤은 {{site.data.keyword.openwhisk_short}}-호환 가능 Docker 이미지를 구현하는 편리한 방법입니다. `wsk sdk install docker` CLI 명령을 사용하여 스켈레톤을 설치할 수 있습니다.

기본 2진 프로그램은 `dockerSkeleton/client/clientApp` 파일에 복사되어야 합니다. 모든 동반 파일 또는 라이브러리는 `dockerSkeleton/client` 디렉토리에 상주할 수 있습니다.

또한 `dockerSkeleton/Dockerfile`을 수정하여 모든 컴파일 단계 또는 종속 항목을 포함시킬 수 있습니다. 예를 들어, 조치가 Python 스크립트이면 Python을 설치할 수 있습니다.


## 시스템 한계
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}}에는 조치가 사용할 수 있는 메모리 양, 시간당 허용되는 조치 호출 수 등을 포함하여 시스템 한계가 있습니다. 다음은 기본 한계를 표시하는 표입니다.

| 한계 | 설명 | 구성 가능 | 단위 | 기본값 |
| ----- | ----------- | ------------ | -----| ------- |
| 제한시간 | 컨테이너가 N밀리초를 초과하여 실행되도록 허용되지 않음 | 조치당 |  밀리초 | 60000 |
| 메모리 | 컨테이너에 N MB의 메모리를 초과하여 할당되도록 허용되지 않음 | 조치당 | MB | 256 |
| 동시 | 네임스페이스당 N 동시 활성화를 초과하여 허용되지 않음 | 네임스페이스당 | 수 | 100 |
| minuteRate | 분당 이를 초과하여 조치를 호출할 수 없음 | 사용자당 | 수 | 120 |
| hourRate | 시간당 이를 초과하여 조치를 호출할 수 없음 | 사용자당 | 수 | 3600 |

### 조치당 제한시간(ms)(기본값: 60초)
* 제한시간 한계 N은 [100ms..300000ms] 범위이며 조치당 밀리초 단위로 설정됩니다.
* 사용자가 조치를 작성할 때 한계를 변경할 수 있습니다.
* N밀리초를 초과하여 실행되는 컨테이너는 종료됩니다.

### 조치 메모리(MB)당(기본값: 256MB)
* 메모리 한계 M은 [128MB..512MB] 범위이며 조치당 MB 단위로 설정됩니다.
* 사용자가 조치를 작성할 때 한계를 변경할 수 있습니다.
* 컨테이너에 한계보다 더 많은 메모리가 할당될 수 없습니다.

### 네임스페이스당 #동시 호출(#)(기본값: 100)
* 네임스페이스에 대해 동시에 처리되는 활성화의 수가 100을 초과할 수 없습니다.
* 기본 한계는 consul kvstore의 whisk에 의해 정적으로 구성될 수 있습니다.
* 현재 사용자가 한계를 변경할 수 없습니다.


### 분/시간당 호출(#)(고정됨: 120/3600)
* 비율 한계 N은 120/3600으로 설정되어 1분/시간 창에서 조치 호출의 수를 제한합니다.
* 사용자가 조치를 작성할 때 한계를 변경할 수 없습니다.
* 이 한계를 초과하는 호출은 TOO_MANY_REQUESTS에 해당되는 오류 코드를 수신합니다.
