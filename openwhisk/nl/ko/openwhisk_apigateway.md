---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API Gateway를 통해 조치 노출(시범)
{: #openwhisk_apigateway}

{{site.data.keyword.openwhisk}}에서 **POST** 메소드를 통해서만 HTTP 요청을 사용하는 [REST API](./openwhisk_reference.html#openwhisk_ref_restapi)를 통해 조치를 호출할 수 있습니다.
이는 조치를 호출하도록 허용할 뿐만 아니라 마스터 키인 OpenWhisk 권한 부여 API 키를
사용하여 HTTP 클라이언트가 요청을 작성해야 하며, 추가 조치를 삭제하거나 작성할 수도 있습니다.
{: shortdesc}

이 시범 기능을 통해 조치의 권한 부여 API 키 없이, POST 메소드 외에 HTTP 메소드를 사용하여 조치를 호출할 수 있습니다. 

OpenWhisk API Gateway를 통해 OpenWhisk 조치를 노출하려면 CLI를 사용하십시오.  

## OpenWhisk CLI 구성
{: #openwhisk_apigateway_cli}
이 시범 기능은 각 네임스페이스에 현재 연관된 고유 인증 키가 있는 새로운 OpenWhisk 인증 모델에 대해서만 작동합니다.
특정 네임스페이스에 대한 인증 키 설정 방법에 대해서는 [CLI 구성](https://console.ng.bluemix.net/openwhisk/cli)의 지시사항을 따르십시오. 

## OpenWhisk 조치 노출
{: #openwhisk_apigateway_hello}

OpenWhisk를 사용하여 이미 사전 설치되어 있는 단순 조치를 노출시키십시오. 

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
**GET** HTTP 메소드를 통해 `echo` 조치를 노출시키는 새 URL이 생성됩니다.

HTTP 요청을 URL로 전송하여 이를 시도해 보십시오. 
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
`echo` 조치가 호출되며 전송된 매개변수를 포함하는 JSON 문자열을 다시 리턴합니다.
```
{
  "marco":"polo"
}
```
{: screen}

단순 조회 매개변수 또는 요청 본문을 통해 매개변수를 조치에 전달할 수 있습니다. 

### 여러 조치 노출
{: #openwhisk_apigateway_actions}

친구들을 위한 독서 클럽에 대해 조치 세트를 노출하기 원한다고 가정해 봅시다.
독서 클럽에 대한 백엔드를 구현하기 위한 일련의 조치가 있습니다. 

| 조치 | http 메소드 | 설명 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 책 세부사항 가져오기  |
| postBooks   | POST | 책 추가 |
| putBooks    | PUT | 책 세부사항 업데이트 |
| deleteBooks | DELETE | 책 삭제 |

해당 HTTP URL 기본 경로로 `/club`을 사용하고 해당 리소스로 `books`를 사용하여 `Book Club`이라는 독서 클럽에 대한 API를 작성해 보십시오. 
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

기본 경로 `/club`을 사용하여 노출된 첫 번째 조치가 `Book Club`이라는 이름의 API 레이블을 얻으며 `/club` 아래에 노출된 다른 모든 조치는 `Book Club`과 연관됩니다. 

방금 노출시킨 조치를 모두 나열해 보십시오. 

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

이제 HTTP **POST**를 사용하여 새 책 `JavaScript: The Good Parts`를 추가해 보십시오. 
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

HTTP **GET**을 통한 `getBooks` 조치를 사용하여 책 목록을 가져오도록 하십시오. 
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 구성 내보내기
입력으로 파일을 사용하여 API를 다시 작성하려면 기본으로 사용할 수 있는 파일에 `Book Club`이라는 API를 내보내십시오.  
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

먼저 공통 기본 경로 아래의 노출된 모든 URL을 삭제하여 Swagger 파일을 테스트해 보십시오.
기본 경로 `/club` 또는 API 이름 레이블 `"Book Club"`을 사용하여 노출된 URL을 모두 삭제할 수 있습니다. 
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

이제 `club-swagger.json` 파일을 사용하여 `Book Club`이라는 이름의 API를 복원해 보십시오. 
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

API가 다시 작성되었는지 확인할 수 있습니다. 
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **참고**: 이 기능은 현재 시범 오퍼링으로 시도해 본 후 피드백을 제공하도록 사용자에게 우선 기회를 제공합니다. 다음 피드백이 이미 수신되었습니다. 
  - CORS(Cross-Origin Resource Sharing)에 대한 HTTP 액세스 제어를 사용자 정의할 기능이 없습니다. 현재 생성된 API 응답 헤더는 모든 HTTP 동사 또는 원본(즉, *)을 허용하도록 구성되어 있습니다. 다음 헤더가 항상 리턴됩니다. 
    - Access-Control-Allow-Origin: *
    - Access-Control-Allow-Headers: Authorization, Content-Type
    - Access-Control-Allow-Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - 요청 및 응답에 대해 `application/json` 컨텐츠 유형만 지원됩니다. 
  - OpenWhisk 조치에서 응답을 제어할 프로그래밍 방법은 없습니다. 
  - 모든 OpenWhisk 조치는 공용 액세스를 통해 노출되며 사용자 정의 API 키를 구성할 기능이 없습니다. 
  - 경로 매개변수는 지원되지 않으며 조회 매개변수 및 요청 본문만 지원됩니다. 
  - API가 API 이름 없이 작성되는 경우 이름이 기본 경로가 되며 이를 변경할 수 없습니다. 
  - 입력 파일을 통해 API를 재작성하는 경우 API를 우선 삭제해야 합니다. 
  - API를 내보낼 때 OpenWhisk API 키가 포함되는 경우 이 정보가 중요하며 사용 가능한 템플리트는 없습니다. 
