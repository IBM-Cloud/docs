---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud IAM(Identity and Access Management)
{: #iam_overview}

IBM Cloud IAM에서는 사용자와 서비스 ID 및 리소스에 대한 해당 ID의 액세스 권한을 관리하는 안전한 방법을 제공합니다. 관리할 권한이 부여된 액세스 옵션에 따라 계정 또는 조직 전체의 사용자를 보고 관리할 수 있습니다. 사용자 초대 및 사용자와 지정된 역할, 사용자가 액세스할 수 있는 계정, 조직 또는 둘 다를 관리하는 작업을 포함하여 사용자의 모든 작업을 수행할 수 있습니다. 계정 소유자는 현재 계정에서의 역할에 상관없이 사용자가 모두 구성원으로 있는 액세스 옵션을 관리할 수 있습니다.

ID 관리에는 다음이 포함됩니다.
 * 사용자 관리 
   * 사용자 정보 작성, 삭제, 업데이트
   * API 키 관리
   * 토큰 작성, 새로 고치기 및 교환
   * 사용자 ID 인증
 * 서비스 ID 관리
   * 사용자 정보 작성, 삭제, 업데이트
   * API 키 관리
   * 토큰 작성, 새로 고치기 및 교환
   * 서비스 ID 인증
   
   
액세스 관리에는 다음이 포함됩니다.
 * 정책 관리
   * 정책 작성, 삭제 및 업데이트
 * 리소스에 대한 액세스 권한 결정
 
## ID 개요
{: #identity}

클라우드 IAM 토큰 서비스는 IBM 클라우드의 인증 서비스이고 [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [JWT 프로파일](https://tools.ietf.org/html/rfc7523) 및 [JWKS](https://tools.ietf.org/html/rfc7517)를 통해 지정된 개방형 표준을 기반으로 빌드합니다.

토큰 서비스에서는 중점을 두는 사항 중 하나는 IBM Cloud Platform 개발자, 운영자 및 관리자의 인증입니다. 이 인증에서는 토큰 서비스가 사용자를 인증하기 위해 IBM ID 시스템에 연결하고, 전용 및 로컬 환경에서 고객이 선택한 인증 시스템(예: LDAP)에 연결할 수 있습니다. 

IAM 토큰을 검색하려면 `password`와 같은 표준 OAuth 2.0 권한 부여 유형을 사용할 수 있습니다. 예를 들어 다음과 같습니다.
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=password&username=<IBMid>&password=<IBMid password>
       [&ims_account=<ims account>][&bss_account=<bss account>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

OAuth 2.0의 확장기능으로서 토큰 계정을 고유하게 만들 계정 정보를 제공해야 합니다. CloudFoundry API 또는 IMS API와 상호 작용하는 `UAA` 또는 `IMS` 토큰을 가져오기 위해 여러 다른 응답 유형도 나열할 수 있습니다.

클라우드 IAM 토큰 서비스를 사용하면 사용자의 API 키를 작성, 업데이트, 삭제 및 사용할 수 있습니다. 이러한 API 키는 API 호출 또는 Bluemix 콘솔을 사용하여 작성할 수 있습니다. API 키를 활용하기 위해 어댑터에서 다음과 같은 확장 권한 부여 유형을 사용할 수 있습니다.
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

결과 토큰은 비밀번호 부여 또는 UI 로그인을 사용하여 검색된 토큰과 같이 사용할 수 있습니다.

또한 클라우드 IAM 토큰 서비스를 사용하면 UI를 통해 대화식으로 로그인할 수 있습니다. 이 기능은 OAuth 2.0 권한 부여 유형 `authorization_code`를 사용하여 구현되며 `OAuth Dance`라고도 합니다. 인증 단계 중에 여러 웹 브라우저의 경로가 재지정되기 때문입니다.

토큰 서비스에서 중점을 두는 또 다른 기능은 서비스 ID와 서비스 ID의 API 키를 제공하는 것입니다. 서비스 ID는 "기능 ID" 또는 "애플리케이션 ID"와 비슷하고, 사용자를 표시하는 것이 아니라 서비스에 대해 인증하는 데 사용합니다.

서비스 ID를 작성하여 Bluemix 계정, CloudFoundry 조직 또는 CloudFoundry 영역과 같은 범위에 바인딩할 수 있습니다. 이 바인딩은 서비스 ID를 보관할 컨테이너를 제공하기 위해 수행됩니다. 이 컨테이너는 서비스 ID를 업데이트하고 삭제할 사용자와 해당 서비스 ID에 연관된 API 키를 작성, 업데이트, 읽기 및 삭제하는 사용자도 정의합니다. 서비스 ID는 사용자에 관련되지 않습니다.

서비스 ID 사용 방법을 더 잘 이해하려면 API를 데모하는 [데모 애플리케이션](https://iam.ng.bluemix.net/demo)을 사용해 볼 수 있습니다.

## 액세스 관리 개요
{: #access_management}

IAM은 [NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf) 발행물에
영감을 받은 조건이 있는 속성 기반 액세스 제어(ABAC) 시스템입니다.  

IAM에서는 속성 조합을 사용하여 리소스에 대한 액세스 권한을 결정합니다. IAM 정책에는 역할, 사용자/서비스 ID 속성, 리소스 속성 및 조건에 적용된 규칙이 있습니다. 따라서 사용자와 서비스 ID의 액세스 권한을 정의하는 유연하고 강력한 방법을 사용할 수 있습니다.

예를 들어, 가상 머신 VM123에는 다음 속성이 포함될 수 있습니다. 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
이러한 리소스 속성의 조합을 사용하여 정책을 작성하는 데 사용할 수 있습니다.

자세한 예제는 [IAM 정책 예제](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples)를 참조하십시오.

ABAC는 사전 정의된 역할이 사용자에게 지정되는 역할 기반 액세스 제어(RBAC)와 다릅니다. 이러한 사전 정의된 역할에는 특정 권한이 있으며, 이 역할의 사용자는 해당 역할로 정의된 모든 권한이 있습니다. 
 
예를 들어, 가상 머신 `관리자` 역할이 있습니다. 이 역할은 가상 머신 리소스에 대해 모든 관리자 유형 권한이 있음을 의미합니다. 

ABAC는 단순하게 다음과 같이 생각해 볼 수 있습니다.

1. 사용자, 리소스, 컨텍스트 및 조치가 있습니다.
1. 사용자, 리소스, 컨텍스트 및 조치의 각 인스턴스에는 고유 ID가 있습니다.
1. 각 인스턴스에는 속성이 제공됩니다.
   기본적으로 "권한 부여 관점에서 인스턴스에 해당하는 사항"을 나타냅니다.
   예를 들어 다음과 같습니다.
   1. 사용자는 Pisces이고 1960년에 태어났습니다.
   1. 리소스는 야구 팀 선수 명단입니다.
   1. 컨텍스트는 동부 시간으로 오전 9시부터 오후 5시까지입니다.
   1. 조치는 "업데이트 가능"입니다.
1. 리소스에 대해 조치를 수행하는 사용자에 대해 권한이 부여된 속성 세트를 판별하기 위해 정책을 작성합니다.
1. 사용자가 리소스에 대해 조치를 수행하기 위해 요청하면 요청이 허용되는지 확인하기 위해 정책을 확인합니다.

다음 이미지는 권한 순서의 자세한 보기를 표시합니다.

![권한 부여 순서](auth_sequence.png)

## 서비스의 액세스 제어 설정
{: #setup_access_mgmt}

{{site.data.keyword.Bluemix_notm}}에 서비스를 온보딩하는 작업은 클라우드 IAM으로 서비스를 온보딩하는 것과는 다른 작업 세트입니다. 기술적으로 {{site.data.keyword.Bluemix_notm}} 및 클라우드 IAM을 사용하여 독립적으로 임의 순서에 따라 온보딩할 수 있습니다. 클라우드 IAM 팀이 {{site.data.keyword.Bluemix_notm}} 서비스 온보딩 팀과 협업하므로 온보딩 프로세스의 {{site.data.keyword.Bluemix_notm}} 서비스에는 클라우드 IAM 온보딩도 포함됩니다.

서비스의 액세스 제어를 설정하려면 온보딩 프로세스의 일부로 다음 단계를 사용해야 합니다.

### 1단계: 이 http 요청을 통해 서비스 ID를 작성합니다.
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Curl 명령:
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

다음은 `curl` 명령에서 사용된 `서비스 ID`와 `서비스 crn` 값을 자세히 설명합니다.
  
#### 서비스 ID 
  
서비스 ID 이름은 서비스의 crns에 표시되는 서비스 이름과 같을 수 있습니다.
  
서비스 ID는 계정, 조직 또는 영역에 바인딩되어야 합니다. 이 바인딩을 통해 서비스 ID를 관리할 수 있는 사용자를 결정합니다. 예를 들어 서비스 ID가 바인딩된 관리자가 업데이트하거나 삭제할 수 있습니다. 사용자가 ID를 바인딩하는 계정, 조직 및 영역에 대한 액세스 권한이 {{site.data.keyword.Bluemix_notm}} 토큰에 있어야 합니다. 계정에 바인딩하려면 `boundTo` crn은 다음과 같아야 합니다. 

`crn:v1:::<service name>::a/<account id>:::` 
  
조직의 경우 다음과 같아야 합니다.
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
영역의 경우 다음과 같아야 합니다.
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
지정된 `boundTo` 값은 서비스 ID가 액세스할 수 있는 리소스에 영향을 미치지 않습니다. 
  
IAM 액세스 정책에 따라 서비스 ID가 액세스할 수 있는 리소스를 제어합니다. 서비스 ID가 IBM 조직에 바인딩되어 있어도 서비스 ID에서 해당 조직 외부의 리소스에 액세스하도록 허용하는 IAM 정책을 작성할 수 있습니다. IAM으로 온보딩할 때 IAM 팀이 작성하는 첫 번째 액세스 정책을 통해 서비스 ID가 서비스에서 소유한 리소스의 정책을 작성할 수 있습니다.

이 API와 관련 API에 대한 자세한 정보는 [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/)를 참조하십시오.

#### 서비스 crn

`boundTo` crn의 service-name은 서비스의 crn에 표시되는 서비스 이름과 일치해야 합니다.
  
이러한 필드를 완료하는 데 대한 도움말은 [CRN 스펙](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md)을 참조하십시오.

응답에서 서비스 ID와 서비스 ID crn인 메타데이터->uuid 및 메타데이터>crn을 저장하십시오.


### 2단계: [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters)에서 AccessControl Squad에 문의하십시오. 
서비스 ID에 서비스 리소스의 정책을 관리하는 관리자 역할이 부여되었습니다.

다음 형식을 사용하십시오.
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```
{: codeblock}

### 3 단계: 서비스 ID에서 api-key를 작성해야 합니다. 다음 http 요청을 사용하십시오.
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
{: codeblock}

Curl 명령: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo`는 서비스 ID의 crn이어야 합니다(1단계의 응답에서 저장된 필드 메타데이터->crn). 이름과 설명은 임의로 지정할 수 있습니다.

응답에서 엔티티->apiKey를 저장하십시오.

이 API와 관련 API에 대한 자세한 정보는 [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey)를 참조하십시오.

### 4단계: 서비스 ID API 키의 액세스 토큰을 가져옵니다. 

권한이 설정된 경우 서비스에서 서비스 리소스에 대한 PAP 및 PDP 요청을 수행할 수 있습니다.

3단계의 엔티티 **apiKey** 필드를 사용하십시오. 이 필드는 API 키 값입니다(apikey_value).

  * 그런 다음 API 키 값으로 토큰을 가져오십시오(반드시 이스케이프 문자 사용).

    Curl 명령:
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

결과에서 **access_token** 필드를 사용합니다. 이 필드는 api-key 토큰입니다(서비스 ID용). 이전에 표시된 curl 명령에서 사용된 경우 **access_token**은 URL 인코딩이어야 합니다.


### 5단계: 서비스 이름의 가능한 서비스 조치 목록을 등록합니다.

  a. 서비스 조치를 IAM 시스템 정의 역할에 맵핑합니다. 이 맵핑은 나중에 서비스 등록 중에 사용됩니다.

  * IAM 시스템 정의 역할의 목록은 다음 요청을 수행하여 찾을 수 있습니다.
  
Curl 명령:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**참고:** 서비스 등록 페이로드에서 IAM 시스템 정의 역할의 *crn 버전*을 사용하십시오.

다음은 서비스 조치를 역할에 맵핑하는 예입니다.

  <table>
    <tr>
      <th>API 엔드포인트</th>
      <th>서비스 조치</th>
      <th>IAM 시스템 정의 역할</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>관리자</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>뷰어, 편집자, 관리자</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>편집자, 관리자</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>관리자</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>편집자, 관리자</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>편집자, 관리자</td>
    </tr>
  </table>

  b. 다음 명령행을 사용하여 `PAP`에 서비스를 등록하십시오.
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
{: codeblock}
  
[서비스 조치 형식](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format)에
지정된 대로 조치를 정의해야 합니다.
  
예를 들어 표준 형식을 사용할 때 다음과 같습니다.

  `<service-name>.<component>.<verb>`
  
  이전 예에서 조치 `key-protect.keys.decode` 사용 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### 6단계: 5단계의 세부사항에 따라 등록된 서비스를 확인합니다.

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### 7단계(선택사항): 5단계에서 등록된 서비스를 삭제합니다.

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### 8단계: PDP로 권한을 확인하기 위해 PEP SDK를 사용하도록 서비스를 구성합니다. 해당 SDK 언어를 선택합니다.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## 용어
{: #terminology}

### ID 용어

* IBM ID(ibmid) - IBM 클라우드, IBM 애플리케이션, 커뮤니티 및 지원에 액세스하기 위해 IBM에서 제공하고 호스팅하는 ID입니다.
* 사용자 ID(User Id) - 실제 사용자를 나타내는 ID입니다.
* 서비스 ID(Service Id) - 기술 사용자, 시스템, 애플리케이션 또는 서비스를 나타내는 ID입니다. 기술 사용자도 나타내는 "기능 ID" 또는 "애플리케이션 ID"와 비슷하지만, "사용자 ID" 엔티티 유형을 사용합니다. 
* OAuth 2.0 - 대상 서비스에 신임 정보를 제공하지 않고 애플리케이션과 API에 대한 액세스 권한을 부여하는 개방형 표준입니다. OAuth는 인증 정보를 포함하는 데도 사용됩니다.
* OpenID Connect - 인증된 사용자에 대한 정보를 제공하는 데 중점을 둔 OAuth 2.0을 기반으로 빌드된 개방형 표준입니다.
* 클라이언트 ID(Client Id) - OAuth 2.0 준수 엔드포인트와 상호작용하는 애플리케이션이 인증하려면 본인확인정보 클라이언트 ID / 본인확인정보 쌍이 필요합니다. 클라이언트 ID를 가져오려면 애플리케이션을 토큰 서비스에 등록해야 합니다.
* 토큰 엔드포인트(Token endpoint) - 클라이언트에서 사용자 이름 또는 비밀번호, 권한 부여 또는 새로 고치기 토큰과 같은 ID 정보를 제공하여 하나 이상의 토큰을 확보하기 위해 사용합니다.
* 권한 엔드포인트(Authorization endpoint) - 클라이언트에서 UI를 통해 토큰 서비스에 대해 사용자를 인증하는 데 사용합니다.
* 토큰(Token) - 애플리케이션이 ID의 인증 및/또는 권한을 검색하는 데 사용할 수 있는 불투명하거나 투명한 문자열입니다.
* 액세스 토큰(Access token) - 이 토큰은 API에 ID 정보로 전송될 수 있습니다. 여기에는 ID 정보가 들어 있으며 짧은 시간 동안만 유효합니다.
* 새로 고치기 토큰(Refresh token) - 이 토큰은 인증을 요청한 클라이언트에만 저장됩니다. 액세스 토큰이 만기되면 새 액세스 토큰을 가져오는 데 사용됩니다(즉, 액세스 토큰 새로 고치기). 새로 고치기 토큰은 장기가 유지되므로 액세스 토큰 자체를 새로 고치기 위한 경우가 아니면 클라이언트 시스템을 떠나지 않아야 합니다.
* ID 쿠키(Identity cookie) - IBM 클라우드 토큰 서비스에 로그인할 때 ID를 포함하는 쿠키가 브라우저에 발행됩니다. 이 쿠키가 있으며 올바른 경우 로그인하기 위해 다시 인증을 확인하지 않습니다. IBM 클라우드 토큰 서비스에서 로그아웃하거나 브라우저를 닫으면 24시간 후에 만기됩니다.
* JSON 웹 토큰(JSON Web Token) - 액세스 토큰을 나타내는 JSON 기반 표준(RFC 7519)입니다. 액세스 토큰의 컨텐츠는 투명합니다(즉, 쉽게 읽을 수 있음). 해당 토큰의 원본 증명을 확인할 수 있도록 JWT 기반 토큰은 일반적으로 서명됩니다.
* 공개 키(Public Key) - JSON 웹 토큰의 서명을 유효성 검증하는 데 사용할 수 있습니다. 비대칭 암호화를 사용하는 경우 클라이언트가 사용하도록 공개 키를 안전하게 공개할 수 있습니다.
* 개인 키(Private Key) - JSON 웹 토큰의 서명을 작성하는 데 사용할 수 있습니다. 이 키는 비밀로 유지해야 합니다. 그렇지 않으면 다른 사용자가 올바른 액세스 토큰을 작성할 수 있습니다.
* realmid - 다른 사용자 레지스트리와 사용자를 구분하는 ID입니다. 현재 사용된 값은 IBM ID 시스템에서 인증한 사용자의 경우 "IBM ID"이고 토큰 서비스에서 인증한 서비스 ID의 경우에는 "iam"입니다.
* ID(identifier) - 절대 변경되지 않고 한 사용자 레지스트리에서 사용자를 고유하게 식별하는 ID입니다(`realmid` 매개변수로 표시). <realmid>-<identifier>를 조합하면 항상 고유하게 식별할 수 있는 사용자가 생성되어야 합니다. IBM ID의 경우 IBM 고유 ID 'IUI'가 사용됩니다.             
* 주체(subject) - ID의 사용자 이름입니다. 이메일 주소와 같은 양식인 경우가 많습니다. IBM ID의 경우, 이는 ID의 IBM ID입니다.
* 사용자 정의 클레임(Custom claims) - JSON 웹 토큰 내부의 추가적인 비표준 정보입니다.

### 액세스 관리 용어

* 정책 관리 지점(PAP, Policy Administration Point) - 액세스 권한 정책을 관리하는 지점입니다.
* 정책 의사결정 지점(PDP, Policy Decision Point) - 액세스 의사결정을 실행하기 전에 권한 부여 정책에 대한 액세스 요청을 평가하는 지점입니다.
* 정책 시행 지점(PEP, Policy Enforcement Point) - 리소스에 대한 사용자의 액세스 요청을 인터셉트하고, 액세스 의사결정을 얻기 위해 PDP에 의사결정을 요청하고(즉, 리소스에 대한 액세스가 승인되거나 거부됨), 받은 의사결정에 대해 조치를 수행하는 지점입니다.
* 정책 정보 지점(PIP, Policy Information Point) - 속성 값의 소스로 작동하는 시스템 엔티티(즉, 리소스, 주체, 환경)입니다.
* 정책 검색 지점(PRP, Policy Retrieval Point) - XACML 액세스 권한 정책이 저장된 지점입니다(일반적으로 데이터베이스 또는 파일 시스템).
* 주체(subject) - 리소스 및 주체 권한 쌍에 있는 "인물(who)"(사용자 또는 그룹)입니다. 리소스는 주체가 액세스할 수 있는 리소스입니다.
* 역할(role) - 특정 태스크를 수행할 수 있는 사용자, 사용자 그룹, 시스템, 서비스 또는 애플리케이션에 지정할 수 있는 권한의 콜렉션입니다.
* 리소스(resource) - 조직, 영역, 데이터베이스 또는 테이블과 같이 조치를 수행할 수 있는 실제 또는 논리 오브젝트입니다.
* 조건(conditions) - "True", "False" 또는 "Indeterminate"로 평가되는 함수입니다.
* 조치(actions) - 애플리케이션이 이벤트의 결과로 오브젝트나 리소스에서 수행하는 정의된 태스크입니다.
* 정책(policy) - 규칙 세트, 규칙 결합 알고리즘의 ID 및 (선택사항) 의무나 권고 사항 세트입니다. 정책 세트의 컴포넌트일 수 있습니다.

## 시스템 정의 역할
{: #system_defined_roles}

IBM 클라우드 역할은 조치의 콜렉션을 나타내고 이러한 조치는 IAM 사용 서비스를 통해 제공합니다.

조치를 역할로 그룹화하면 최소한의 시스템 정의 역할 세트를 사용하여 서비스나 리소스의 조치를 지원하는 유연성이 제공됩니다. 예를 들어, VM, 스토리지 및 네트워킹의 `관리자`가 필요하면 이 세 가지 모두의 `관리자` 역할을 사용하지만 정책의 대상만 변경할 수 있습니다. VM의 `관리자`, 스토리지의 `관리자` 및 네트워킹의 `관리자`.

*IBM 클라우드 IAM에서 수행하지 않는 사항*: 기타 액세스 관리 시스템에서 사용하는 대안을 사용하여 리소스를 역할로 빌드합니다. 이 접근 방식을 사용하면 시스템에 도입된
모든 리소스 유형의 역할 이름이 의도치 않게 새로 작성됩니다. 예를 들어,
이 접근 방식을 사용하면 VM, 스토리지 및 네트워크 리소스의 관리를 다루기 위해
`VMAdministrator` 역할, `StorageAdministrator` 역할
및 `NetworkAdministrator` 역할이 필요합니다.


다음 테이블에서는 IBM 시스템 정의 역할과 이 역할에 맵핑된 조치의 예제를 보여줍니다.

|IBM 클라우드 역할 이름| 설명 | 예제 조치|
|:-----------------|:-----------------|:-----------------|
|뷰어|상태를 변경하지 않는 조치(예: 읽기 전용)| <ul><li>디바이스 나열</li><li>스토리지 오브젝트 읽기</li><li>조회 실행</li><li>검색 실행</li></ul>|
|편집자|상태를 수정하고 하위 리소스를 작성/삭제할 수 있는 조치|<ul><li>vm 작성</li><li>vm 삭제</li><li>스토리지 접속</li><li>다시 부팅</li><li>시작/중지</li><li>이름 바꾸기</li></ul>|
|운영자|리소스를 구성하고 조작하는 데 필요한 조치|<ul><li>구성 업데이트</li><li>vm 시작/중지</li><li>로그 보기</li><li>백업/복원</li></ul>|
|관리자|액세스 제어를 관리하는 기능을 포함하는 모든 조치|<ul><li>사용자 초대</li><li>vm 작성</li>사용자 액세스 정책 업데이트</li><li>디바이스 나열</li><li>vm 작성</li><li>vm 삭제</li><li>스토리지 접속</li><li>다시 부팅</li><li>시작/중지</li><li>이름 바꾸기</li><li>백업/복원</li></ul>|
|청구 관리자|청구 관리와 관련된 조치|<ul><li>신용 카드 업데이트</li><li>송장 나열</li><li>송장 다운로드</li></ul>|

다음에 있는 PAP 마이크로 서비스에서 최신 시스템 정의
역할 목록을 조회할 수 있습니다.

Curl 명령: 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## 서비스 조치 형식
{: #action_format}

조치는 다음 두 형식 중 하나로 정의해야 합니다.
  
* 표준:

    `<service-name>.<component>.<verb>`
* 액세스 제어 인터셉트 위치: 

    `<METHOD> /<api_route>`
  
### 표준
대부분의 서비스에서 IAM PDP를 직접 호출하고 표준 조치 형식을 지원하도록 소스 코드를 수정할 수 있습니다.  
 
 이 형식은 세 파트를 모두 포함해야 하며, 영숫자이거나 공백이 없고 '-' 이외의 특수 문자여야 합니다.

`<service-name>.<component>.<verb>`

여기서, 
* service-name - CRN service-name 필드에 정의된 서비스 이름입니다.
* component - 서비스의 리소스 또는 하위 리소스입니다.
* verb - 서비스 이름 컴포넌트의 지원 조치를 정의하는 Verb입니다. 
  
예를 들어 `key-protect.keys.decode`입니다. 
* service-name = key-protect
* component = keys
* verb = decode

### REST API 액세스 제어 인터셉트 위치
{: intercept_point}

경우에 따라 REST API 요청은 액세스 제어 인터셉트 위치로 사용되는 게이트웨이를 통해 경로가 지정됩니다. IAM PDP는 실제 REST API 서비스를 호출하기 전에 인터셉트 위치에서 직접 호출됩니다. REST API 요청을 처리하는 서비스에서 IAM PDP를 호출하지 않습니다.

인터셉트 위치는 REST API 라우트와 요청을 보낼 엔드포인트에 대해서만 알고 있습니다. 자세한 정보는 [액세스 제어 인터셉트 위치 고려사항](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview)을 참조하십시오.


 이 형식에는 [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt)로 지정된 URL의 파트 및 지원 안전 문자가 모두 포함되어야 합니다.
 
 
`<METHOD> /<api_route>`
  
여기서,
* METHOD - REST API 메소드입니다. 
* api_route - REST API의 URI입니다.

예: `GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# 랩 서비스 ID 및 API 키

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


