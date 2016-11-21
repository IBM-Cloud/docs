---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}} 서비스 시작하기
{: #autoscaling}
마지막 업데이트 날짜: 2016년 11월 02일
{: .last-updated}

{{site.data.keyword.Bluemix_notm}}에서 자동으로 애플리케이션 용량을 관리할 수 있습니다. {{site.data.keyword.autoscaling}} 서비스를 사용하여 애플리케이션의 컴퓨팅 성능을 자동으로 높이거나 낮출 수 있습니다. 애플리케이션 인스턴스의 수는 사용자가 정의한 {{site.data.keyword.autoscaling}} 정책에 따라 동적으로 조정됩니다.
{:shortdesc} 

## 목차
  * [{{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.autoscaling}} 서비스 사용](#as-service)
  * [{{site.data.keyword.autoscaling}} 서비스를 사용하여 Node.js 앱 구성](#node-asagent)
  * [RESTful API를 통한 {{site.data.keyword.autoscaling}} 서비스 관리](#RESTAPI)
  * [{{site.data.keyword.autoscaling}} CLI를 통한 {{site.data.keyword.autoscaling}} 서비스 관리](#CLI)
  * [{{site.data.keyword.autoscaling}} 서비스의 정책 필드](#policy_fields)
  * [오류 메시지](#err_msg)

## {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.autoscaling}} 서비스 사용
{: #as-service}

{{site.data.keyword.autoscaling}} 서비스를 사용하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 *서비스 또는 API 추가*를 클릭한 다음 서비스 카탈로그의 DevOps 섹션에서 {{site.data.keyword.autoscaling}} 서비스를 선택하십시오. {{site.data.keyword.autoscaling}} 서비스의 개요를 제공하는 새 창이 표시됩니다.
2. {{site.data.keyword.autoscaling}} 서비스를 바인딩할 애플리케이션을 선택하고 *작성*을 클릭하십시오. <br/>
*참고:* 애플리케이션에는 하나의 {{site.data.keyword.autoscaling}} 서비스만 바인드할 수 있습니다. 이 애플리케이션이 이미 다른 {{site.data.keyword.autoscaling}} 서비스에 바인드되어 있는 경우 이 단계에서 애플리케이션을 선택하지 마십시오. 그렇지 않으면, CWSCV2004E 오류가 발생합니다.<br/>애플리케이션 다시 스테이징 창이 표시됩니다.
3. 추가한 새 {{site.data.keyword.autoscaling}} 서비스를 사용하기 전에 애플리케이션 다시 스테이징 창에서 *다시 스테이징*을 클릭하여 애플리케이션을 다시 스테이징하십시오. <br/><ul><li>Liberty 애플리케이션의 경우, 애플리케이션을 다시 스테이징한 후 {{site.data.keyword.autoscaling}}이 자동으로 구성되어 사용할 준비가 됩니다.</li> <li>Node.js 애플리케이션의 경우, 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하기 전에 {{site.data.keyword.autoscaling}} 서비스를 사용으로 설정하도록 애플리케이션 코드를 업데이트해야 합니다. 세부사항은 [{{site.data.keyword.autoscaling}} 서비스를 사용하여 Node.js 앱 구성](index.html#node_asagent)을 참조하십시오.</ul><br/>
애플리케이션 다시 스테이징이 완료된 후 애플리케이션에 대한 {{site.data.keyword.autoscaling}} 서비스 구성을 시작할 수 있습니다.
4. 애플리케이션의 {{site.data.keyword.autoscaling}}을 구성하려면 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서 {{site.data.keyword.autoscaling}} 서비스가 바인드된 애플리케이션을 클릭하십시오.
5. 대시보드의 서비스 섹션에서 *Auto-Scaling* 아이콘을 클릭하십시오.
6. 완료하지 못한 경우 *{{site.data.keyword.autoscaling}} 정책 작성*을 클릭하여 애플리케이션에 대해 {{site.data.keyword.autoscaling}} 정책을 정의하십시오.

이제 {{site.data.keyword.autoscaling}} 정책을 구성하거나 메트릭 통계를 보거나 애플리케이션에 대한 스케일링 히스토리를 볼 수 있습니다.
<dl>
<dt>정책 구성</dt>
<dd>이 섹션은 특정 스케일링 활동을 트리거하는 조건을 지정하기 위해 스케일링 규칙을 작성하거나 편집하는 데 사용합니다.<ul>
<li> Liberty for Java™ 애플리케이션의 경우, 힙, 메모리, 응답 시간 및 처리량과 관련된 스케일링 규칙을 정의할 수 있습니다.  
<li> Node.js 애플리케이션의 경우, 힙, 메모리 및 처리량과 관련된 스케일링 규칙을 정의할 수 있습니다.
<li> Ruby 애플리케이션의 경우, 메모리와 관련된 스케일링 규칙을 정의할 수 있습니다. </ul>
*참고:* 둘 이상의 메트릭 유형에 여러 개의 스케일링 규칙을 정의할 수 있습니다. 그러나 {{site.data.keyword.autoscaling}} 서비스는 스케일링 정책 간의 충돌을 발견하지 않습니다. 스케일링 정책을 정의하는 경우, 여러 스케일링 규칙이 서로 충돌하지 않는지 확인해야 합니다. 그렇지 않으면, 애플리케이션이 스케일 축소했다가 1분 이내에 바로 스케일 확장하여 총 인스턴스 수의 변동이 클 수 있습니다.<br/><br/>
최대 시간과 여유 시간 동안 애플리케이션의 워크로드가 대폭 변경되는 경우, 서로 다른 기간에 각기 다른 스케일링 요구사항을 처리하도록 스케일링 스케줄을 작성합니다. 스케일 축소 및 스케일 확장 조치를 트리거하도록 동적 스케일링 규칙이 스케줄에 적용되는 동안 스케줄에 지정된 최소 인스턴스 수 매개변수를 사용하여 애플리케이션 인스턴스 수의 기준선을 정의하십시오. </dd>
<dt>메트릭 통계</dt>
<dd>애플리케이션 인스턴스에 대한 메트릭 통계를 표시합니다. 평균 통계를 확인하고 특정 인스턴스를 선택하여 해당 인스턴스의 통계를 확인할 수 있습니다. </dd>
<dt>스케일링 히스토리</dt>
<dd>애플리케이션의 스케일링 히스토리를 표시합니다.<ul>
<li> 지난 주: 지난 주의 스케일링 히스토리를 표시합니다.
<li> 지난 달: 지난 달의 스케일링 히스토리를 표시합니다.
<li> 사용자 정의 범위: 기간을 설정할 수 있습니다.</ul>
*참고:* 히스토리 레코드를 필터링하려면 스케일링 상태 또는 스케일 축소/확장을 선택하면 됩니다.</dd>
</dl>


## {{site.data.keyword.autoscaling}} 서비스를 사용하여 Node.js 앱 구성
{: #node-asagent}

서비스 프로비저닝 및 바인딩 단계 외에 Node.js 앱을 사용하여 {{site.data.keyword.autoscaling}} 서비스를 사용으로 설정하려면 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시하기 전에 다음 단계도 완료해야 합니다.

1. 다음 단계를 완료하여 package.json 파일을 업데이트하십시오. <ol><li>`blumix-autoscaling-agent`에 대한 종속 항목(예: `"bluemix-autoscaling-agent": "*"`)을 작성하십시오.<br/><li>(선택사항) 앱에 할당하는 메모리를 기반으로 `scripts` 섹션 내에 힙 한계를 설정하십시오(예: `"start": "node --max-old-space-size=600 app.js"`). <br/>*참고:* 힙 사용량을 기반으로 스케일링을 트리거하려면 `max-old-space-size`의 값을 설정하십시오. 애플리케이션을 시작할 때 값이 설정되어 있지 않으면 앱에 할당된 메모리 양과 관계없이 기본 Node.js 힙 한계인 1.4GB가 사용되며 이로 인해 적합하지 않은 자동 스케일링 의사결정이 내려질 수 있습니다.<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. 기본 파일을 업데이트하여 에이전트 선언 `var as_agent = require('bluemix-autoscaling-agent');`를 추가하십시오. 다음 코드 스니펫은 Auto-Scaling 에이전트 선언이 있는 전체 항목 js 파일을 표시합니다.<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## RESTful API를 통한 {{site.data.keyword.autoscaling}} 서비스 관리 
{: #RESTAPI}

{{site.data.keyword.autoscaling}} RESTful API는 Bluemix UI 외에 {{site.data.keyword.autoscaling}} 서비스를 관리하는 대체 방법을 제공하며 스케일링 데이터 검색 및 분석도 지원합니다. 이는 API를 사용하여 {{site.data.keyword.Bluemix_notm}} UI에서와 유사한 기능(예: 정책 작성 및 스케일링 히스토리 가져오기)을 제공합니다.

{{site.data.keyword.autoscaling}} RESTful API를 사용하여 {{site.data.keyword.autoscaling}} 서비스를 관리하려면 다음 전제조건을 완료하십시오. 이전 섹션에 지정된 대로 {{site.data.keyword.autoscaling}} 서비스를 애플리케이션과 바인드하고 `AccessToken`, {{site.data.keyword.autoscaling}} API 서버의 URL, 스케일을 축소하거나 확대하려는 애플리케이션의 `app_id`를 획득하십시오.

1. 보안 목적으로 {{site.data.keyword.autoscaling}} RESTful API의 각 요청 헤더에서 CloudFoundry UAA 프로시저를 통해 얻은 적절한 `AccessToken`을 `Authorization` 헤더에 제공하여 요청에 대한 필수 유효성 검증을 표시하십시오. 이 `AccessToken`을 준수하는 데 실패하면 401 권한 없음 응답이 발생합니다. Cloud Foundry 명령행 도구를 설치하고 {{site.data.keyword.Bluemix_notm}}에 로그인한 후 이 `AccessToken`을 가져올 수 있는 두 가지 방법이 있습니다.<ul><li>`cf oauth-token` 명령을 통해 이 토큰을 얻을 수 있습니다.
   
   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
“bearer”로 시작하는 리턴된 긴 문자열은 {{site.data.keyword.autoscaling}} RESTful API의 요청에서 사용할 수 있는 AccessToken입니다. “명령을 찾을 수 없음”과 같은 오류가 발생하면 Cloud Foundry 명령행 도구를 새 버전으로 업데이트할 수 있습니다.</li><li>홈 디렉토리에서 이 AccessToken을 찾을 수도 있습니다. 명령행 인터페이스에서 {{site.data.keyword.Bluemix_notm}}에 로그인하면 현재 로깅의 환경 정보 목록(예: 조직, 영역, 인증 엔드포인트 및 버전)이 포함되어 있는 `config.json`이라는 JSON 파일을 찾을 수 있는 `.cf` 폴더가 홈 폴더에 작성됩니다. 파일에서 다음과 같은 `AccessToken` 항목을 찾을 수 있습니다.
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
`config.json`의 `AccessToken`만 기간 동안 유효합니다. REST API 요청에 대해 401 권한 없음 응답이 발생하는 경우 명령행 인터페이스에서 다시 로그인하여 파일을 새로 고치고 새 `AcessToken`을 가져와야 할 수 있습니다. </li></ul>
 
2.  애플리케이션을 {{site.data.keyword.autoscaling}} 서비스와 바인드한 후 `VCAP_SERVICE` 환경 변수를 확인하여 {{site.data.keyword.autoscaling}} API 서버의 URL을 얻을 수 있습니다. `VCAP_SERVICE`에서 {{site.data.keyword.autoscaling}} 서비스 섹션을 찾을 수 있으며 `api_url`은 애플리케이션이 바인드된 API 서버의 URL입니다. {{site.data.keyword.autoscaling}} RESTful API 서비스에 연결하려면 이 API 서버 URL이 필요합니다.
   
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
`cf env APPNAME` 명령을 통해서도 이 URL을 찾을 수 있습니다.
   ```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   시스템 제공:
   {"VCAP_SERVICES": {
     "Auto-Scaling": [
      {
         "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  `VCAP_SERVICES` 환경 변수에서 `app_id`를 가져오거나 `cf app APPNAME --guid` 명령을 실행할 수 있습니다.

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

위의 전제조건을 모두 완료하면 이제 브라우저의 RestClient 추가 기능을 사용하거나 `curl`과 같은 일부 도구를 통해 REST API 요청을 작성할 수 있습니다. 

Firefox 또는 Chrome의 경우와 마찬가지로 REST Client 추가 기능을 사용하여 {{site.data.keyword.autoscaling}} API 서버에 대한 REST 요청을 트리거하여 명령을 실행할 수 있습니다. 해당 추가 기능에 REST API의 URL, 이 REST API에서 필요한 메소드 및 헤더, 본문 파트의 매개변수만 제공하면 됩니다. 각 API에 대한 세부사항은 [{{site.data.keyword.Bluemix_notm}}에 대한 IBM {{site.data.keyword.autoscaling}}의 Rest API](https://new-console.ng.bluemix.net/apidocs/48){:new_window}를 참조하십시오.

`curl`과 같은 도구를 사용하여 다음과 같이 스크립트 내에서 {{site.data.keyword.autoscaling}} 서비스를 관리할 수 있습니다.    
```
cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## {{site.data.keyword.autoscaling}} CLI를 통한 {{site.data.keyword.autoscaling}} 서비스 관리 
{: #CLI}

{{site.data.keyword.autoscaling}} CLI는 {{site.data.keyword.autoscaling}} RESTful API와 유사하지만 더 친숙한 방식으로 {{site.data.keyword.autoscaling}} 서비스를 구성할 수 있는 기능을 제공합니다. {{site.data.keyword.autoscaling}} CLI를 사용하는 경우 {{site.data.keyword.autoscaling}} RESTful API의 세부사항(예: `AccessToken` 및 API 서버의 URL)에 대해서는 주의할 필요가 없습니다. CLI가 제공하는 단계별 지시사항만 따르면 됩니다. {{site.data.keyword.autoscaling}} CLI를 설치하고 사용하는 방법에 대한 세부사항은 [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}를 참조하십시오.



## {{site.data.keyword.autoscaling}} 서비스의 정책 필드
{: #policy_fields}

| 필드 이름  | 설명 |
|-------------|----------------------|
|*허용되는 최대 인스턴스 개수* |	시작할 수 있는 애플리케이션 인스턴스의 최대 수입니다. 현재 애플리케이션 인스턴스 수가 이 값과 같으면 {{site.data.keyword.autoscaling}} 서비스는 애플리케이션의 스케일을 더 이상 확장하지 않습니다. 기본 최소 인스턴스 수는 시작할 수 있는 애플리케이션 인스턴스의 최소 수입니다. 인스턴스 수가 이 값과 같으면 {{site.data.keyword.autoscaling}} 서비스는 애플리케이션의 스케일을 더 이상 축소하지 않습니다.  |
| *메트릭 유형*	| 	지원되고 모니터링 가능한 메트릭 유형입니다. 자세한 정보는 표 2를 참조하십시오. |
| *스케일 확장* | 	스케일 확장 조치가 트리거될 때 스케일 확장 조치를 트리거하는 임계값 및 인스턴스 증가 개수를 지정합니다.  |
| *스케일 축소* |	스케일 축소 조치가 트리거될 때 스케일 축소 조치를 트리거하는 임계값 및 인스턴스 감소 개수를 지정합니다.  |
| *통계 기간* |	받은 메트릭 값이 유효하게 인식되는 과거 기간입니다. 시간소인이 이 기간에 속하는 경우에만 메트릭 값이 유효합니다. 통계 기간(Statistic Window) 매개변수는 초 단위를 사용합니다. |
| *위반 기간*	| 스케일링 조치가 트리거될 수 있는 과거 기간입니다. 수집된 메트릭 값이 상한 임계값보다 높거나 하한 임계값(지정된 시간보다 더 긴 값)보다 낮은 경우 스케일링 조치가 트리거됩니다. 위반 기간(Breach Duration) 매개변수는 초 단위를 사용합니다. |
| *스케일 축소의 쿨다운 기간* | 스케일 축소 조치가 발생한 후 스케일 축소 쿨다운 기간 매개변수에 지정된 기간 동안 다른 스케일링 요청이 무시됩니다. 이 매개변수는 초 단위를 사용합니다. |
| *스케일 확장 쿨다운 기간*	| 스케일 확장 조치가 발생한 후 스케일 확장 쿨다운 기간 매개변수에 지정된 기간 동안 다른 스케일링 요청이 무시됩니다. 이 매개변수는 초 단위를 사용합니다. |
| *시간대*	| 스케줄이 적용되는 시간대입니다. |
| *시작 시간*  |	순환 스케줄의 시작 시간입니다. |
| *종료 시간*    |	순환 스케줄의 종료 시간입니다.	|
| *반복 날짜*	|	순환 스케줄이 적용되는 요일입니다.  |
| *최소 인스턴스 개수* |	스케줄의 지정된 기간 동안 애플리케이션에 대해 시작할 수 있는 최소 인스턴스 수입니다. |
| *시작 날짜 및 시간* |	특정 날짜에 설정된 스케줄의 시작 날짜 및 시간입니다. |
| *종료 날짜 및 시간* |	특정 날짜에 설정된 스케줄의 종료 날짜 및 시간입니다.	|

표 1. 스케일링 정책의 정책 필드

| 메트릭 이름 | 설명 | 지원되는 애플리케이션 유형 |
|-------------|----------------------| ------------------- |
| *힙* |	힙 메모리의 이용률입니다.	| Liberty for Java, Node.js SDK |
| *메모리*   |	메모리의 이용률입니다.	|  모든 애플리케이션 유형 |
| *처리량* | 초당 처리되는 요청의 수입니다. | Liberty for Java, Node.js SDK |
| *응답 시간* |	처리된 요청의 응답 시간입니다.	| Liberty for Java |

표 2. 지원되는 메트릭 이름

*참고:* Auto-Scaling 메트릭 데이터를 수집하려면 Liberty 웹 컨테이너를 통해 HTTP/HTTPS 측정 요청이 처리되도록 애플리케이션이 Liberty 웹 앱으로 배치되어야 합니다.
예를 들어, "Main-Classs" 앱으로 Spring Boot 애플리케이션을 실행하는 경우 Liberty buildpack이 사용자를 위해 Java 환경만 제공하며 앱이 실제로는 Spring 임베디드 Tomcat 컨테이너에서 실행됩니다. 그러므로 메트릭 데이터가 Auto-Scaling 서비스로 수집되지 않습니다. Auto-Scaling 서비스에 대해 작업하려면 Liberty WAR 로 앱을 실행해야 합니다.

## 오류 메시지
{: #err_msg}
이 절에는 {{site.data.keyword.autoscaling}} 서비스를 통해 생성되는 경고 및 오류 메시지 목록이 표시됩니다.
 
### CWSCV2004E 다른 {{site.data.keyword.autoscaling}} 서비스가 이미 애플리케이션에 바인드되어 있습니다. 
**하나의 애플리케이션에는 하나의 {{site.data.keyword.autoscaling}} 서비스만 바인드할 수 있습니다. 이 오류는 이미 다른 {{site.data.keyword.autoscaling}} 서비스에 바인드된 애플리케이션에 {{site.data.keyword.autoscaling}} 서비스를 바인드하려는 경우 발생합니다.**

다른 {{site.data.keyword.autoscaling}} 서비스가 바인드되어 있지 않은 다른 애플리케이션을 선택하거나 대상 {{site.data.keyword.autoscaling}} 서비스를 이 애플리케이션에 바인드하십시오.
그 외 다른 경우에 이 오류가 발생하면 IBM 지원 센터에 문의하십시오.

### CWSCV6001E API 서버가 API에 대한 입력 JSON 문자열을 구문 분석할 수 없음: {0}
**입력 JSON 문자열을 구문 분석할 때 문제점이 발생합니다. **

API 문서에서 입력 JSON을 확인하고 오류를 정정하십시오. 

### CWSCV6002E API 서버가 API에 대한 출력 JSON 문자열을 구문 분석할 수 없음: {0}
**입력 JSON 문자열을 구문 분석할 때 문제점이 발생합니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6003E API에 대한 입력 JSON({1})에서 입력 JSON 문자열 형식 오류 발생({0})
**입력 JSON 문자열을 구문 분석할 때 형식 오류가 발견되었습니다. **

API 문서에서 입력 JSON을 확인하고 오류를 정정하십시오. 

### CWSCV6004E API에 대한 출력 JSON({1})에서 출력 JSON 문자열 형식 오류 발생({0})
**출력 JSON 문자열을 구문 분석할 때 형식 오류가 발견되었습니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6005E {0} 중에 내부 서버 오류 발생
**요청을 처리하는 중에 내부 서버 오류가 발생합니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6006E CloudFoundry API 호출 실패: {0}
**CloudFoundry API를 호출할 때 오류가 발생했습니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6007E 애플리케이션을 찾을 수 없음: {0}
**애플리케이션을 찾을 수 없습니다. **

자세한 내용은 애플리케이션 정보를 확인하십시오. 

### CWSCV6008E {0} 애플리케이션 정보 검색 중 다음 오류 발생: {1} 
**오류가 발생하여 애플리케이션 정보 검색에 실패했습니다. **

자세한 내용은 애플리케이션 정보를 확인하십시오. 

### CWSCV6009E {1} 앱에 대한 {0} 서비스를 찾을 수 없음
**이 애플리케이션에 대한 서비스를 찾을 수 없습니다. **

자세한 내용은 이 애플리케이션의 서비스 바인딩을 확인하십시오. 

### CWSCV6010E {0} 앱에 대한 정책을 찾을 수 없음
**이 애플리케이션에 대한 정책을 찾을 수 없습니다. **

자세한 내용은 애플리케이션 구성을 확인하십시오. 

### CWSCV6011E {0} 중 내부 인증 실패
**내부 인증에 실패했습니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 


# 관련 링크
{: #rellinks}

## 샘플
{: #samples}

* [튜토리얼: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## SDK
{: #sdk}

* [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}의 Rest API](https://new-console.{DomainName}/apidocs/48){:new_window}

## 일반
{: #general}

* [컨테이너 스케일링](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [가상 서버 스케일링](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [Node.js용 {{site.data.keyword.autoscaling}} 에이전트](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

