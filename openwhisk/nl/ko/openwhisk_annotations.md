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

# OpenWhisk 자산에 대한 어노테이션

OpenWhisk 조치, 트리거, 규칙 및 패키지(통틀어 자산이라고 함)에 `어노테이션`이 지정될 수 있습니다. 어노테이션은 이름을 정의하는 `key`와 값을 정의하는 `value`와 함께 매개변수와 같은 자산에 첨부됩니다. `--annotation` 또는 간단하게 `-a`를 통해 명령행 인터페이스(CLI)에서 설정하는 것이 좋습니다.
{: shortdesc}

Rationale: 어노테이션은 기본 자산 스키마를 변경하지 않고 시범용으로 허용하도록 OpenWhisk에 추가되었습니다. 이 문서를 작성할 때까지 허용되는 `어노테이션`을 의도적으로 정의하지 않았습니다. 하지만 어노테이션을 많이 사용하여 시맨틱 변경사항을 전달하기 시작할 때 문서화하기 시작해야 합니다.

날짜에 대한 어노테이션의 가장 일반적인 사용은 조치와 패키지 문서화입니다. OpenWhisk 카탈로그의 많은 패키지가 조치를 통해 제공된 기능, 패키지 바인딩 시간에 필요한 매개변수 및 호출-시간 매개변수, 매개변수가 "시크릿"(예: 비밀번호)인지의 여부에 대한 설명과 같은 어노테이션을 전달합니다. 필요에 따라(예: UI 통합 허용을 위해) 이러한 어노테이션을 개발합니다.

다음은 수정되지 않은 입력 인수(예: `function main(args) { return args }`)를 리턴하는 `echo` 조치에 대한 어노테이션의 샘플 세트입니다. 이 조치는 입력 매개변수를 예를 들어 시퀀스 또는 규칙의 일부로 로깅하는 데 유용합니다.

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

패키지 설명을 위해 사용한 어노테이션은 다음과 같습니다.

- `description`: 패키지에 대한 간단한 설명
- `parameters`: 패키지 범위에 있는 매개변수를 설명하는 배열(아래에 자세히 설명됨)

조치의 경우도 이와 유사합니다. 

- `description`: 조치에 대한 간단한 설명
- `parameters`: 조치 실행에 필요한 조치를 설명하는 배열
- `sampleInput`: 일반 값을 가진 입력 스키마를 표시하는 예
- `sampleOutput`: 출력 스키마(대개 `sampleInput`의 경우)를 표시하는 예

매개변수 설명을 위해 사용한 어노테이션은 다음과 같습니다.

- `name`: 매개변수 이름
- `description`: 매개변수에 대한 간단한 설명
- `doclink`: 매개변수에 대한 추가 문서 링크(예를 들어, OAuth 토큰에 유용함) 
- `required`: 필수 매개변수의 경우 true, 선택적 매개변수의 경우 false
- `bindTime`: 패키지가 바인드될 때 매개변수를 지정해야 하는 경우 true
- `type`: 매개변수 유형이며, `password`, `array` 중 하나(하지만 더 광범위하게 사용될 수도 있음)

어노테이션을 검사하지 *않습니다*. 따라서 두 조치를 하나의 시퀀스로 구성하는 것이 허용되는지를 나타내기 위해 어노테이션을 사용할 수 있을 때 예를 들어, 시스템은 이를 수행하지 않습니다.

## 웹 조치에 대한 어노테이션
{: #openwhisk_annotations_webactions}

최근에 새로운 기능을 사용하여 코어 API를 확장했습니다. 패키지 및 조치가 이러한 기능에 참여하도록 하기 위해 의미 있는 다음 새 어노테이션을 도입했습니다. 이러한 어노테이션을 적용하려면 명시적으로 `true`로 설정해야 합니다. `true`에서 `false`로 값을 변경하면 새 API에서 첨부된 자산이 제외됩니다. true로 설정하지 않으면 시스템에서 어노테이션이 의미가 없습니다. 어노테이션은 다음과 같습니다.

- `final`: 조치에만 적용됩니다. 이미 정의된 모든 조치 매개변수가 변경되지 않도록 설정합니다. 매개변수에 엔클로징 패키지 또는 조치 정의를 통해 정의된 값이 있으면 어노테이션을 전달하는 조치 매개변수를 호출-시간 매개변수로 대체할 수 없습니다.
- `web-export`: 조치에만 적용됩니다. 있는 경우 해당 조치를 인증 *없이* REST 호출에서 액세스 가능하도록 설정합니다. 이러한 [*웹 조치*](openwhisk_webactions.html)를 통해 예를 들어 브라우저에서 OpenWhisk 조치를 사용할 수 있으므로 해당 웹 조치를 호출합니다. 웹 조치의 *소유자*가 시스템에서 이 웹 조치를 실행하는 비용을 발생시킨다(예: 조치의 *소유자*가 활성화 레코드도 소유함)는 사실을 알아야 합니다.
- `require-whisk-auth`: 조치에 적용됩니다. 조치가 `web-export` 어노테이션을 전달하고 이 어노테이션이 `true`인 경우 라우트가 인증된 주제에서만 액세스 가능합니다. 웹 조치의 *소유자*가 시스템에서 이 웹 조치를 실행하는 비용을 발생시킨다(예: 조치의 *소유자*가 활성화 레코드도 소유함)는 사실을 알아야 합니다.
- `raw-http`: `web-export` 어노테이션이 있을 때 조치에만 적용됩니다. HTTP 요청 조회 및 본문 매개변수(있는 경우)는 예약 특성으로 조치에 전달됩니다.

