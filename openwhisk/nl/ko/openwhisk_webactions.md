---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 웹 조치
{: #openwhisk_webactions}

웹 조치는 사용자가 웹 기반 애플리케이션을 빠르게 빌드할 수 있도록 어노테이션이 지정된 OpenWhisk 조치입니다. 이렇게 하면 OpenWhisk 인증 키 없이 웹 애플리케이션이 익명으로 액세스할 수 있는 백엔드 로직을 프로그래밍할 수 있습니다. 조치 개발자는 원하는 자신의 인증 및 권한(예: OAuth 플로우)을 구현해야 합니다.
{: shortdesc}

웹 조치 활성화는 조치를 작성한 사용자와 연관됩니다. 이 조치로 인해 조치 활성화 비용이 호출자에게서 조치 소유자로 넘어갑니다.

다음 JavaScript 조치 `hello.js`를 수행합니다.
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}  

값이 `true` 또는 `yes`인 CLI의 `--web` 플래그를 사용하여 `guest` 네임스페이스의 `demo` 패키지에 *웹 조치* `hello`를 작성할 수 있습니다.
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js --web true
```
{: pre}

값이 `true` 또는 `yes`인 `--web` 플래그를 사용하면 신임 정보가 없어도 REST 인터페이스를 통해 조치에 액세스할 수 있습니다. 다음과 같은 구조의 URL을 사용하여 웹 조치를 호출할 수 있습니다.
`https://{APIHOST}/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`. 조치의 완전한 이름은 세 가지 파트, 즉 네임스페이스, 패키지 이름 및 조치 이름으로 구성됩니다. 

*조치의 완전한 이름에는 해당 패키지 이름이 포함되어야 하며, 조치가 이름 지정된 패키지에 없는 경우 패키지 이름은 `default`입니다.*

예는 `guest/demo/hello`입니다. 웹 조치 API 경로는 API 키 없이 `curl` 또는 `wget`과 함께 사용될 수 있습니다. 이 경로는 브라우저에 직접 입력할 수도 있습니다.

웹 브라우저에서 [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane) 열기를 시도하십시오. 또는 `curl`을 통해 조치 호출을 시도하십시오.
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane
```
{: pre}

다음은 HTTP 경로 재지정을 수행하는 웹 조치 예입니다.

```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}    

또는 쿠키를 설정합니다.
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}  

또는 `image/png`를 리턴합니다.
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}  

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}  

It is important to be aware of the [응답 크기 한계](./openwhisk_reference.html)를 파악해야 합니다. 사전 정의된 시스템 한계를 초과하는 응답은 실패하기 때문입니다. 대형 오브젝트는 OpenWhisk를 통해 인라인으로 전송하면 안 되고 대신 예를 들어 오브젝트 저장소에 보류됩니다.

## 조치를 사용하여 HTTP 요청 처리
{: #openwhisk_webactions_http}

웹 조치가 아닌 OpenWhisk 조치에는 두 가지 인증이 모두 필요하며 JSON 오브젝트로 응답해야 합니다. 이와 반대로 웹 조치를 인증 없이 호출할 수 있으며 이 웹 조치를 사용하여 여러 유형의 *헤더*, *상태 코드* 및 *본문* 컨텐츠로 응답하는 HTTP 핸들러를 구현할 수 있습니다. 웹 조치가 여전히 JSON 오브젝트를 리턴해야 하지만, 해당 결과에 다음 중 하나 이상이 최상위 레벨 JSON 특성으로 포함되는 경우 OpenWhisk 시스템(즉, `제어기`)이 웹 조치를 다르게 처리합니다.

- `headers`: 키가 헤더-이름이고 값이 해당 헤더(기본값은 헤더 없음)의 문자열 값인 JSON 오브젝트입니다.
- `statusCode`: 올바른 HTTP 상태 코드입니다(기본값 200 OK).
- `body`: 일반 텍스트인 문자열 또는 base64 인코딩 문자열(바이너리 데이터의 경우)입니다.

요청/응답 종료 시 제어기가 조치 지정 헤더를 HTTP 클라이언트에 전달합니다. 이와 유사하게 제어기는 지정된 상태 코드(있는 경우)로 응답합니다. 마지막으로 본문은 응답 본문으로 전달됩니다. `컨텐츠-유형 헤더`가 조치 결과의 `헤더`에 선언되지 않는 한, 본문은 문자열인 것처럼 전달됩니다(그렇지 않으면 오류 발생). `컨텐츠-유형`이 정의되어 있으면 제어기는 응답이 바이너리 데이터인지 아니면 일반 텍스트인지를 판별하고 필요에 따라 base64 디코더를 사용하여 문자열을 디코딩합니다. 본문이 올바르게 디코딩되지 않으면 오류가 호출자에게 리턴됩니다.

*참고*: JSON 오브젝트 또는 배열은 바이너리 데이터로 처리되며 위의 예에 표시된 대로 base64로 인코딩되어야 합니다.

## HTTP 컨텍스트

호출 시 모든 웹 조치는 추가 HTTP 요청 세부사항을 조치 입력 인수에 대한 매개변수로 수신합니다. 다음과 같습니다.

- `__ow_method`(유형: 문자열). 요청의 HTTP 메소드.
- `__ow_headers`(유형: 문자열에 대한 맵 문자열): 요청 헤더.
- `__ow_path`(유형: 문자열): 요청의 불일치 경로(조치 확장을 이용한 후 일치 중단).
- `__ow_user`(유형: 문자열): OpenWhisk 인증 주제를 식별하는 네임스페이스
- `__ow_body`(유형: 문자열): 요청 본문 엔티티(컨텐츠가 바이너리인 경우 base64 인코딩 문자열, 바이너리가 아닌 경우 일반 문자열)
- `__ow_query`(유형: 문자열): 구문 분석되지 않은 문자열로서 요청의 조회 매개변수

요청은 위에서 이름 지정된 `__ow_` 매개변수를 대체할 수 없습니다. 대체하면 요청이 실패하며 400 잘못된 요청이라는 상태가 나타납니다.

`__ow_user`는 웹 조치가 [인증을 요구하도록 어노테이션이 지정된](./openwhisk_annotations.html#openwhisk_annotations_webactions) 경우에만 존재하며 웹 조치가 고유 권한 정책을 구현할 수 있도록 합니다. `__ow_query`는 웹 조치가 ["원시" HTTP 요청](#raw-http-handling)을 처리하도록 선택된 경우에만 사용 가능합니다. 이는 URI에서 구문 분석된 조회 매개변수가 포함된 문자열입니다(`&`으로 구분됨). `__ow_body` 특성은 "원시" HTTP 요청을 처리하거나 HTTP 요청 엔티티가 JSON 오브젝트 또는 양식 데이터가 아닌 경우에 존재합니다. 그렇지 않은 경우 웹 조치는 본문 매개변수가 조회 매개변수보다 우선하는(결국 조치 및 패키지 매개변수보다 우선하는) 조치 인수의 첫 번째 클래스 특성으로 조회 및 본문 매개변수를 수신합니다.

## 추가 기능

웹 조치는 다음과 같은 몇 가지 추가 기능을 가져옵니다.

- `컨텐츠 확장자`: 요청은 `.json`, `.html`, `.http`, `.svg` 또는 `.text` 중 하나로 원하는 컨텐츠 유형을 지정해야 합니다. 이는 URI의 조치 이름에 확장자를 추가하여 수행하므로, 조치 `/guest/demo/hello`가 예를 들어 HTTP 응답을 다시 수신하도록 `/guest/demo/hello.http`로 참조됩니다. 확장자가 발견되지 않으면 편의를 위해 `.http` 확장자를 가정합니다.
- `결과에서 필드 추정`: 조치 이름을 따르는 경로는 응답의 하나 이상의 레벨을 추정하는 데 사용됩니다. 예를 들어,  
`/guest/demo/hello.html/body`입니다. 이를 통해 사전 `{body: "..." }`를 리턴하는 조치가 `body` 특성을 추정하고 대신 해당 문자열 값을 직접 리턴합니다. 추정된 경로는 절대 경로 모델을 따릅니다(XPath에서와 같이).
- `입력인 조회 및 본문 매개변수`: 조치는 조회 매개변수 및 요청 본문의 매개변수를 수신합니다. 매개변수 병합을 위한 우선 순위는 패키지 매개변수, 조치 매개변수, 조회 매개변수, 본문 매개변수이며 겹치는 경우 각각 이전 값을 대체합니다. 예를 들어 `/guest/demo/hello.http?name=Jane`은 인수 `{name: "Jane"}`을 조치로 전달합니다.
- `양식 데이터`: 표준 `application/json` 외에 웹 조치는 데이터 `application/x-www-form-urlencoded data`에서 인코딩된 URL을 입력으로 수신할 수 있습니다.
- `여러 HTTP verb를 통한 활성화`: 웹 조치는 HTTP 메소드, 즉 `HEAD` 및 `OPTIONS` 뿐만 아니라 `GET`, `POST`, `PUT`, `PATCH` 또는 `DELETE` 중 하나를 통해 호출할 수 있습니다.
- `비JSON 본문 및 원시 HTTP 엔티티 처리`: 웹 조치는 JSON 오브젝트가 아닌 HTTP 요청 본문을 채택하고 불분명한 값과 같은 값(바이너리가 아닌 경우 일반 텍스트, 바이너리인 경우 base64 인코딩 문자열)을 항상 수신하도록 선택할 수 있습니다.

다음 예에는 웹 조치에서 이러한 기능을 사용하는 방법이 있습니다. 다음 본문을 포함한 `/guest/demo/hello` 조치를 고려하십시오.
```javascript
function main(params) { 
    return { response: params };
}
```

이 조치를 웹 조치로 호출하면 결과와 다른 경로를 추정하여 웹 조치의 응답을 변경할 수 있습니다.
예를 들어, 전체 오브젝트를 리턴하고 조치가 수신하는 인수를 확인하려면 다음을 수행하십시오.

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

조회 매개변수 포함:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

또는 양식 데이터:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

또는 JSON 오브젝트:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

이름(텍스트) 추정:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

편의를 위해 조회 매개변수, 양식 데이터 및 JSON 오브젝트 본문 엔티티가 모두 사전으로 처리되며 해당 값은 조치 입력 특성으로 직접 액세스 가능함을 위에서 볼 수 있습니다. 대신 HTTP 요청 엔티티를 직접적으로 처리하도록 선택한 웹 조치의 경우 또는 웹 조치가 JSON 오브젝트가 아닌 엔티티를 수신하는 경우는 해당하지 않습니다.

다음은 위에 표시된 동일한 예를 포함해 "텍스트" 컨텐츠-유형을 사용하는 예입니다.
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## 컨텐츠 확장
{: #openwhisk_webactions_extensions}

컨텐츠 확장자는 일반적으로 웹 조치를 호출할 때 필요합니다. 확장자가 없는 경우 `.http`를 기본값으로 가정합니다. `.json` 및 `.http` 확장자에는 추정 경로가 필요하지 않습니다. `.html`, `.svg` 및 `.text` 확장자에는 필요하지만 편의를 위해 기본 경로가 확장자 이름과 일치하는 것으로 가정합니다. 따라서 웹 조치를 호출하고 `.html` 응답을 수신하려면 조치가 최상위 레벨 특성 `html`이 포함된 JSON 오브젝트로 응답해야 합니다(또는 응답이 명시적으로 지정된 경로에 있어야 함). 즉, `/guest/demo/hello.html`은 `/guest/demo/hello.html/html`의 경우와 같이 `html` 특성의 명시적 추정에 해당합니다. 조치의 완전한 이름에는 해당 패키지 이름이 포함되어야 하며, 조치가 이름 지정된 패키지에 없는 경우 패키지 이름은 `default`입니다.


## 보호된 매개변수
{: #openwhisk_webactions_protected}

컨텐츠 확장자는 일반적으로 웹 조치를 호출할 때 필요합니다. 확장자가 없는 경우 `.http`를 기본값으로 가정합니다. `.json` 및 `.http` 확장자에는 추정 경로가 필요하지 않습니다. `.html`, `.svg` 및 `.text` 확장자에는 필요하지만 편의를 위해 기본 경로가 확장자 이름과 일치하는 것으로 가정합니다. 따라서 웹 조치를 호출하고 `.html` 응답을 수신하려면 조치가 최상위 레벨 특성 `html`이 포함된 JSON 오브젝트로 응답해야 합니다(또는 응답이 명시적으로 지정된 경로에 있어야 함). 즉, `/guest/demo/hello.html`은 `/guest/demo/hello.html/html`의 경우와 같이 `html` 특성의 명시적 추정에 해당합니다. 조치의 완전한 이름에는 해당 패키지 이름이 포함되어야 하며, 조치가 이름 지정된 패키지에 없는 경우 패키지 이름은 `default`입니다.


## 보호된 매개변수

조치 매개변수는 보호되고 불변으로 취급됩니다. 매개변수는 웹 조치를 사용할 때 자동으로 완료됩니다.

```
 wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --web true
```

이러한 변경 결과에서는 `name`이 `Jane`으로 바인드되고 마지막 어노테이션으로 인해 조회 또는 본문 매개변수로 대체될 수 없습니다. 이 경우 의도적인지 여부에 관계없이 이 값을 변경하려는 조회 또는 본문 매개변수에 대해 조치가 보호됩니다. 

## 웹 조치 사용 안함

웹 API(`https://openwhisk.ng.bluemix.net/api/v1/web/`)를 통해 웹 조치를 호출하지 않게 설정하려면 CLI로 조치를 업데이트하는 동안 `false` 또는 `no` 값을 `--web` 플래그에 전달하십시오.

```
 wsk action update /guest/demo/hello hello.js --web false
```
{: pre}

## 원시 HTTP 처리

웹 조치는 JSON 오브젝트를 조치 입력에 사용 가능한 첫 번째 클래스 특성으로 승격하지 않고 수신 HTTP 본문을 직접 해석하고 처리하도록 선택할 수 있습니다(예: `args.name` 대 `args.__ow_query` 구문 분석). 이는 `raw-http` [어노테이션](annotations.md)을 통해 수행됩니다. 동일한 예제 사용이 이전에 표시되었지만 이제 `name`을 HTTP 요청 본문의 조회 매개변수 및 JSON 값으로 수신하는 "원시" HTTP 웹 조치로 표시됩니다.
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
{
    "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

이 경우 JSON 컨텐츠는 바이너리 값으로 처리되므로 base64로 인코딩됩니다. 조치는 이 값을 base64 디코딩 및 JSON 구문 분석하여 JSON 오브젝트를 복구해야 합니다. OpenWhisk는 [Spray](https://github.com/spray/spray) 프레임워크를 사용하여 바이너리인 컨텐츠 유형과 일반 텍스트인 컨텐츠 유형을 [판별](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282)합니다.


### 원시 HTTP 처리 사용

원시 HTTP 웹 조치는 `원시`의 값을 사용하는 `--web` 플래그를 통해 사용됩니다.

```
 wsk action create /guest/demo/hello hello.js --web raw
```

### 원시 HTTP 처리 사용 안함

`false` 또는 `no` 값을 `--web` 플래그에 전달하여 원시 HTTP를 사용하지 않게 설정할 수 있습니다.

```
 wsk update create /guest/demo/hello hello.js --web false
```

### Base64에서 바이너리 본문 컨텐츠 디코딩

원시 HTTP 처리를 사용하면 요청 content-type이 바이너리일 때 `__ow_body` 컨텐츠가 Base64로 인코딩됩니다. 다음은 Node, Python 및 Swift에서 본문 컨텐츠를 디코딩하는 방법을 보여주는 함수입니다. 아래 표시된 메소드를 파일에 저장하고,
저장된 아티팩트를 활용하는 원시 HTTP 웹 조치를 작성한 다음, 웹 조치를 호출하기만 하면 됩니다.

#### Node

```javascript
  function main(args) {
       decoded = new Buffer(args.__ow_body, 'base64').toString('utf-8')
    return {body: decoded}
}
```
{: codeblock}

#### Python

```python
def main(args):
    try:
        decoded = args['__ow_body'].decode('base64').strip()
        return {"body": decoded}
    except:
        return {"body": "Could not decode body from Base64."}
```
{: codeblock}

#### Swift

```swift
extension String {
    func base64Decode() -> String? {
        guard let data = Data(base64Encoded: self) else {
            return nil
        }

        return String(data: data, encoding: .utf8)
    }
}

func main(args: [String:Any]) -> [String:Any] {
    if let body = args["__ow_body"] as? String {
        if let decoded = body.base64Decode() {
            return [ "body" : decoded ]
        }
    }

    return ["body": "Could not decode body from Base64."]
}
```
{: codeblock}

예를 들어, Node 함수를 `decode.js`로 저장하고 다음 명령을 실행하십시오.
```
 wsk action create decode decode.js --web raw
```
{: pre}
```
ok: created action decode
```
```
curl -k -H "content-type: application" -X POST -d "Decoded body" https:// openwhisk.ng.bluemix.net/api/v1/web/guest/default/decodeNode.json
```
{: pre}
```json
{
  "body": "Decoded body"
}
```

## 오류 처리
{: #openwhisk_webactions_errors}

OpenWhisk 조치가 실패하는 경우 서로 다른 두 가지 실패 모드가 있습니다. 첫 번째는 *애플리케이션 오류*로 알려져 있으며 발견된 예외와 비슷합니다. 즉, 조치가 최상위 레벨 `오류` 특성이 포함된 JSON 오브젝트를 리턴합니다. 두 번째는 조치가 크게 실패하고 응답을 생성하지 않는 경우에 발생하는 *개발자 오류*입니다(미발견 예외와 유사함). 웹 조치의 경우 제어기는 다음과 같이 애플리케이션 오류를 처리합니다.

- 지정된 경로 추정은 무시되고 대신 제어기가 `오류` 특성을 추정합니다.
- 제어기가 `오류` 특성 값에 조치 확장이 나타내는 컨텐츠 처리를 적용합니다.

개발자는 웹 조치를 사용하는 방법을 파악하고 이에 따라 오류 응답을 생성해야 합니다. 예를 들어, `.http` 확장자와 함께 사용되는 웹 조치는
HTTP 응답을 리턴해야 합니다(예: `{error: { statusCode: 400 }`). 이렇게 하지 못하면 확장을 통해 나타낸 컨텐츠-유형과 오류 응답의 조치 컨텐츠-유형 간에 불일치가 발생합니다. 시퀀스인 웹 조치를 특별히 고려해야 하므로 시퀀스를 구성하는 컴포넌트가 필요에 따라 적절한 오류를 생성할 수 있습니다.

