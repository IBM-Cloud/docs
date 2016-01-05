
{:shortdesc: .shortdesc}

# VCAP 서비스

*마지막 업데이트 날짜: 2015년 11월 9일*


VCAP_SERVICES 환경 변수는 {{site.data.keyword.Bluemix_notm}}의
서비스 인스턴스와 상호작용하는 데 사용할 수 있는 정보가 포함된 JSON
오브젝트입니다.
{:shortdesc}


## VCAP_SERVICES 환경 변수의 값 검색
{:retrieving}

VCAP_SERVICES 환경 변수는 {{site.data.keyword.Bluemix_notm}}의
서비스 인스턴스와 상호작용하는 데 사용할 수 있는 정보가 포함된 JSON
오브젝트입니다. 이러한 정보로는 서비스 인스턴스 이름, 신임 정보 및 서비스 인스턴스의 연결 URL 등이
있습니다. 애플리케이션이 {{site.data.keyword.Bluemix_notm}}의 서비스 인스턴스에 바인딩된 경우 이러한 값이 VCAP_SERVICES 환경 변수에 채워집니다.

VCAP_SERVICES 환경 변수의 값은 서비스 인스턴스를 애플리케이션에 바인딩한 경우에만 사용할 수 있습니다. 애플리케이션 환경 변수는 WebSocket 콘솔 드라이버를
사용하여 확인할 수 있습니다. 다음 예는 WebSocket 콘솔 드라이버를 사용하여 Node.js
애플리케이션의 환경 변수를 확인하는 방법을 보여줍니다.

먼저 다음 명령을 실행하여 Node.js 애플리케이션을 다시 푸시하십시오.
```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp
```
다음으로, 다음 URL을 입력하십시오.
```
https://yourapp.{APPDomain}/bash.sh
```
표시되는 페이지에서 선택 표시를 클릭하여 도구에 연결한 다음 env 명령을 실행하여 애플리케이션의 환경 변수를 확인하십시오. cf-debug-tools에 대한 자세한 정보는 [Debug Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools)를 참조하십시오.


## Bluemix 인프라 계층 보기
{:viewinfra}


{{site.data.keyword.Bluemix_notm}}는 관리할 필요가 없도록
운영 체제 및 인프라 계층을 추상화하고 숨깁니다. 그러나 때때로 사용자 앱의 운영 체제와 미들웨어에 대한 정보가 필요할 수 있습니다.

cf stacks 명령을 실행하여 앱을 배치할 사용 가능한 스택 또는 루트 파일 시스템을 표시할 수 있습니다. cf push 명령에 *-s* 옵션과 *stack_name*을 사용하여 스택을 지정할 수도 있습니다. 여기서 stack_name은 루트 파일 시스템(예: `lucid64` 또는 `cflinuxfs2`)입니다.
```
cf push appName -s stack_name
```
`cf buildpacks` 명령을 사용하여 앱을 실행할 런타임으로 사용 가능한 미들웨어 컴포넌트(예: WebSphere Liberty 프로파일 및 SDK for Node.js)를 표시할 수 있습니다. 또한 다음 명령을 사용하여 앱의 런타임 환경을 지정할 수 있습니다.
```
cf push appName -b buildpackname
```
