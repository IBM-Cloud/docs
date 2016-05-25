---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}}를 사용하여 클라우드 자원 보호
{: #protecting-resources}
{{site.data.keyword.amashort}} 서비스를 통해, 모바일 사용 OAuth 보안 및 모니터링으로 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 Java 기반 백엔드 애플리케이션 및 Node.js를 보호할 수 있습니다.
{:shortdesc}
## 권한 필터
{: #auth-filter}
{{site.data.keyword.amashort}} 서버 SDK에는 백엔드 애플리케이션을 보호하는 데 사용할 수 있는 권한 필터가 있습니다. 권한 필터는 수신 요청을 가로채기하여 권한 헤더가 있는지 유효성을 검증합니다. 권한 헤더가 없거나 올바르지 않은 경우 필터는 HTTP 401 오류와 함께 응답을 리턴합니다. {{site.data.keyword.amashort}} 클라이언트 SDK는 {{site.data.keyword.amashort}} 서버 SDK에서 리턴하는 HTTP 401 응답을 가로채는 방법을 알고 있으며 인증 플로우를 트리거합니다. 
## 권한 헤더
{: #auth-header}
수신 요청의 권한 헤더는 운반자, 액세스 토큰 및 ID 토큰 세 가지로 구성되며 공백으로 구분됩니다. `ID 토큰`이 선택사항인 반면 `액세스 토큰`은 필수 컴포넌트입니다. 

수신 권한 헤더는 각각의 권한 필터에서 처리합니다. 필터는 액세스 토큰 및 ID 토큰 서명, 만기 날짜 및 구조 무결성의 유효성을 검사합니다. 유효성 검사에 통과하면 보안 컨텍스트 오브젝트가 요청 오브젝트에 추가됩니다. 각 API를 사용하여 보안 컨텍스트에 대한 참조를 가져올 수 있습니다. 

보안 컨텍스트에는 제목, 사용자, 디바이스 및 다음 구조로 저장된 애플리케이션 정보가 포함되어 있습니다. ```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
* `imf.sub`: ID 토큰의 제목 또는 ID 토큰이 없는 경우 클라이언트의 고유 ID를 지정합니다. 
* `imf.user`: ID 토큰에서 추출된 사용자 ID를 지정합니다. ID 토큰이 없는 경우 이 필드는 공백 오브젝트를 유지합니다. 
* `imf.device`: ID 토큰에서 추출된 디바이스 ID를 지정합니다. ID 토큰이 없는 경우 이 필드는 공백 오브젝트를 유지합니다. 
* `imf.application`: ID 토큰에서 추출된 애플리케이션 ID를 지정합니다. ID 토큰이 없는 경우 이 필드는 공백 오브젝트를 유지합니다. 

## 다음 단계
{: #next-steps}
* [Node.js 자원 보호](protecting-resources-nodejs.html)
* [Liberty for Java&trade; 자원 보호](protecting-resources-java.html)
* [로컬 개발](protecting-resources-local.html)
