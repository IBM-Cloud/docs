---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API 게이트웨이
{: #openwhisk_apigateway}

OpenWhisk 조치에서는 API Management를 통해 관리하는 것이 이로울 수 있습니다.

API 게이트웨이는 [웹 조치](webactions.md)에 대한 프록시로 작동하고 HTTP 메소드 라우팅, 클라이언트 ID/시크릿, 비율 제한, CORS, API 사용 및 응답 로그 보기 및 API 공유 정책 정의를 포함한 추가 기능을 제공합니다.
API 게이트웨이 기능에 대한 자세한 정보는 [API Management 문서](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)에서 확인할 수 있습니다.

## 브라우저를 사용하여 OpenWhisk 웹 조치에서 API를 작성하십시오.

API 게이트웨이를 사용하면 OpenWhisk 조치를 API로 표시할 수 있습니다. API를 정의한 후 보안 및 비율 제한 정책을 적용하고 API 사용 및 응답 로그를 보고 API 공유 정책을 정의할 수 있습니다.
OpenWhisk 대시보드에서 [API 탭](https://console.ng.bluemix.net/openwhisk/apimanagement)을 클릭하십시오.


## CLI를 사용하여 OpenWhisk 웹 조치에서 API 작성

### OpenWhisk CLI 구성

apihost `wsk property set --apihost openwhisk.ng.bluemix.net`을 사용하여 OpenWhisk CLI를 구성하십시오.
`wsk api`를 사용하려면 CLI 구성 파일 `~/.wskprops`에 Bluemix 액세스 토큰이 있어야 합니다.
액세스 토큰을 가져오려면 CLI 명령 `wsk bluemix login`을 사용하십시오. 명령에 대한 자세한 정보를 보려면 `wsk bluemix login -h`를 실행하십시오.

**참고:** 명령 오류에 싱글 사인온(sso)이 필요한 경우 현재 지원되지 않습니다. 임시 해결책으로 `cf login`을 사용하여 Cloud Foundry CLI로 로그인한 다음 홈 디렉토리 구성 파일 `~/.cf/config.json`의 액세스 토큰을 `~/.wskprops` 파일에 특성 `APIGW_ACCESS_TOKEN="value of AccessToken`으로 복사하십시오. 액세스 토큰 문자열을 복사할 때 접두부 `Bearer`를 제거하십시오.

**참고:** `wsk api-experimental`을 사용하여 작성한 API는 계속 짧은 기간 동안 작동하지만 웹 조치로 API 마이그레이션을 시작하고 새 CLI 명령 `wsk api`를 사용하여 기존 apis를 재구성해야 합니다.

### CLI를 사용하여 첫 번째 API 작성

1. 다음 컨텐츠를 사용하여 JavaScript 파일을 작성하십시오. 이 예에서 파일 이름은 'hello.js'입니다.
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. 다음 JavaScript 함수에서 웹 조치를 작성하십시오. 이 예에서 조치를 'hello'라고 합니다. 플래그 `--web true`를 추가해야 합니다.
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. 기본 경로 `/hello`, 경로 `/world` 및 응답 유형이 `json`인 메소드 `get`으로 API를 작성하십시오.
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
  새 URL은 **GET** HTTP 메소드를 통해 `hello` 조치를 표시하여 생성됩니다.
  
4. HTTP 요청을 URL로 전송하여 이를 시도해 보십시오. 
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
{
    "payload": "Hello world OpenWhisk"
  }
  ```
  웹 조치 `hello`가 호출되었으며 조회 매개변수를 통해 보낸 매개변수 `name`이 포함된 JSON 오브젝트를 다시 리턴했습니다. 단순 조회 매개변수를 통해 또는 요청 본문을 통해 매개변수를 조치에 전달할 수 있습니다. 웹 조치를 사용하면 OpenWhisk 권한 부여 API 키 없이 공용 방식으로 조치를 호출할 수 있습니다.
  
### HTTP 응답에 대한 전체 제어
  
  `--response-type` 플래그는 API 게이트웨이로 프록시 지정할 웹 조치의 대상 URL을 제어합니다. `--response-type json`을 위와 같이 사용하면 JSON 형식의 전체 조치 결과가 리턴되고 컨텐츠-유형 헤더가 사용자가 쉽게 시작할 수 있게 하는 `application/json`으로 자동 설정됩니다. 
  
  시작하면 `statusCode`, `headers`와 같은 HTTP 응답 특성을 완전히 제어할 수 있으며 `body`에 서로 다른 컨텐츠 유형을 리턴할 수 있습니다. `--response-type http`를 사용하여 이를 수행할 수 있으며, 이렇게 하면 `http` 확장자로 웹 조치의 대상 URL이 구성됩니다.

  조치 코드를 변경하여 `http` 확장자를 가진 웹 조치 리턴을 따르거나 HTTP 응답에 맞게 형식화되도록 결과를 변환하는 새 조치에 해당 결과를 전달하여 조치를 시퀀스에 포함하도록 선택할 수 있습니다. [웹 조치](webactions.md) 문서에서 응답 유형과 웹 조치 확장자에 대해 자세히 볼 수 있습니다.

  JSON 특성 `body`, `statusCode` 및 `headers`를 리턴하여 `hello.js`의 코드를 변경하십시오.
  ```javascript
  function main({name:name='Serverless API'}) {
      return { 
    body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  본문을 문자열이 아닌 `base64`로 인코딩하여 리턴해야 합니다.
  
  수정된 결과로 조치 업데이트
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  API를 `--response-type http`로 업데이트
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  업데이트된 API 호출
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
{
    "payload": "Hello world Serverless API"
  }
  ```
  이제 API를 완전히 제어할 수 있으므로 HTML 리턴과 같이 컨텐츠를 제어하거나 찾을 수 없음(404), 권한 없음(401) 또는 내부 오류(500)와 같은 내용에 대한 상태 코드를 설정할 수 있습니다.

### 여러 웹 조치 표시

친구들을 위한 독서 클럽에 대해 조치 세트를 노출하기 원한다고 가정해 봅시다.
독서 클럽에 대한 백엔드를 구현하기 위한 일련의 조치가 있습니다. 

| 조치 | HTTP 메소드(HTTP method) | 설명 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 책 세부사항 가져오기  |
| postBooks   | POST | 책 추가 |
| putBooks    | PUT | 책 세부사항 업데이트 |
| deleteBooks | DELETE | 책 삭제 |

해당 HTTP URL 기본 경로로 `/club`을 사용하고 해당 리소스로 `books`를 사용하여 `Book Club`이라는 독서 클럽에 대한 API를 작성해 보십시오. 
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

기본 경로 `/club`을 사용하여 노출된 첫 번째 조치가 `Book Club`이라는 이름의 API 레이블을 얻으며 `/club` 아래에 노출된 다른 모든 조치는 `Book Club`과 연관됩니다. 

방금 노출시킨 조치를 모두 나열해 보십시오. 

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

이제 HTTP **POST**를 사용하여 새 책 `JavaScript: The Good Parts`를 추가해 보십시오. 
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

HTTP **GET**을 통한 `getBooks` 조치를 사용하여 책 목록을 가져오도록 하십시오. 
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 구성 내보내기
입력으로 파일을 사용하여 API를 다시 작성하려면 기본으로 사용할 수 있는 파일에 `Book Club`이라는 API를 내보내십시오.  
```
wsk api get "Book Club" > club-swagger.json
```

먼저 공통 기본 경로 아래의 노출된 모든 URL을 삭제하여 Swagger 파일을 테스트해 보십시오.
기본 경로 `/club` 또는 API 이름 레이블 `"Book Club"`을 사용하여 노출된 URL을 모두 삭제할 수 있습니다. 
```
wsk api delete /club
```
```
ok: deleted API /club
```
### 구성 변경

OpenWhisk 대시보드에서 구성을 편집할 수 있습니다. [API 탭](https://console.ng.bluemix.net/openwhisk/apimanagement)을 클릭하여 보안, 비율 제한 및 기타 기능을 설정하십시오.

### 구성 가져오기

이제 `club-swagger.json` 파일을 사용하여 `Book Club`이라는 이름의 API를 복원해 보십시오. 
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

API가 다시 작성되었는지 확인할 수 있습니다. 
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
