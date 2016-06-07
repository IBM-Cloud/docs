---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cloud Foundry(cf) 명령

*마지막 업데이트 날짜: 2016년 1월 29일*

Cloud Foundry(cf) 명령을 사용하여 앱을 관리할 수 있습니다.
{:shortdesc}

다음 정보는 앱 관리에 가장 일반적으로 사용되는 cf 명령을 나열합니다. cf 명령과 도움말 정보를 모두 나열하려면 `cf help`를 사용하십시오. `cf command_name -h`를 사용하면 특정 명령에 대한 자세한 도움말 정보를 볼 수 있습니다.

*참고:* 네트워크에서 cf 명령을 실행하는 호스트와 Cloud Foundry API 엔드포인트 사이에 HTTP 프록시 서버가 있으면 `HTTP_PROXY` 환경 변수를 설정하여 프록시 서버의 호스트 이름 또는 IP 주소를 지정해야 합니다. 자세한 정보는 [HTTP 프록시 서버에 cf CLI 사용](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html)을 참조하십시오.

## cf api

{{site.data.keyword.Bluemix_notm}}API 엔드포인트의 URL을 지정하거나 표시합니다.
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>{{site.data.keyword.Bluemix_notm}}에 연결할 때 지정해야 하는 Bluemix API 엔드포인트의 URL입니다. 일반적으로 이 URL은 https://api.{DomainName}입니다.
현재 사용 중인 API 엔드포인트의 URL을 표시하려는 경우 cf api 명령에 이 매개변수를 지정할 필요가 없습니다.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>SSL 유효성 검증 프로세스를 사용 안함으로 설정합니다. 이 매개변수를 사용할 경우 보안 문제가 발생할 수 있습니다. </dd>
<dt>*--unset*</dt>
<dd>모든 API 엔드포인트에 대한 연결 정보를 제거합니다. </dd>
</dl>

## cf apps

현재 영역에 배치된 모든 애플리케이션을 나열합니다. 각 애플리케이션의 상태도 표시됩니다. 

앱에 대해 하나의 인스턴스가 있는 것으로 가정할 때 cf 앱 명령 응답의 인스턴스 열에 앱이 실행 중이면 1/1이, 앱이 중단되었으면 0/1이 표시됩니다. 앱 인스턴스 상태를 알 수 없음을 의미하는 ?/1이 표시되면 앱 URL을 브라우저로 복사하여 앱의 응답 여부를 확인하거나 `cf logs appname` 명령으로 로그를 추적하여 앱이 로그 컨텐츠를 생성하는지 확인할 수 있습니다.

## cf bind-service

기존 서비스 인스턴스를 애플리케이션에 바인딩합니다.
```
cf bind-service appname service_instance
```

예를 들어 현재 조직 및 영역에 `my_dataworks`라는 서비스 인스턴스가 있는 경우 `cf bind-service my_app my_dataworks`를 사용하여 이 서비스 인스턴스를 애플리케이션에 바인딩할 수 있습니다. 

<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>service_instance</dt>
<dd>기존 서비스 인스턴스의 이름입니다. </dd>
</dl>

## cf create-service

서비스 인스턴스를 작성합니다.
```
cf create-service service_name service_plan service_instance
```
예를 들어 `cf create-service DataWorks free my_dataworks`를 사용하여 무료 사용제가 있는 {{site.data.keyword.dataworks_short}} 서비스의 인스턴스를 작성할 수 있습니다. 

<dl>
<dt>service_name</dt>
<dd>서비스 이름입니다. </dd>
<dt>service_plan</dt>
<dd>서비스 플랜의 이름입니다. </dd>
<dt>service_instance</dt>
<dd>작성할 새 서비스 인스턴스에 사용할 이름입니다. </dd>
</dl>

## cf create-space

영역을 작성합니다.
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>영역의 이름입니다. </dd>
<dt>*-o*</dt>
<dd>영역을 작성하려는 조직의 이름입니다. </dd>
<dt>*-q*</dt>
<dd>새로 작성된 영역에 지정되는 할당량입니다. 이 값을 지정하지 않으면 기본 할당량이 자동으로 지정됩니다.</dd>
</dl>

## cf delete

기존 애플리케이션을 삭제합니다.
```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. <dd>
<dt>*-f*</dt>
<dd>애플리케이션을 확인 없이 강제로 삭제합니다. 이 매개변수는 선택적 매개변수입니다. </dd>
<dt>*-r*</dt>
<dd>애플리케이션과 연관된 도메인 이름을 모두 삭제합니다. 이 매개변수는 선택적 매개변수입니다. </dd>
</dl>

## cf delete-space

영역을 삭제합니다.
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>영역의 이름입니다. </dd>
<dt>*-f*</dt>
<dd>확인 없이 영역을 강제로 삭제합니다. 이 매개변수는 선택적 매개변수입니다. </dd>
*참고:* 영역을 삭제하면 되돌릴 수 없습니다.
</dl>

## cf events

애플리케이션과 관련된 런타임 이벤트를 표시합니다.
```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
</dl>

## cf help

모든 cf 명령 또는 특정 cf 명령(command_name 매개변수가 사용된 경우)에 대한 도움말 정보를 표시합니다.
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>명령 이름입니다. 특정 명령에 대한 도움말 정보를 원하는 경우 이 매개변수를 사용하면 됩니다. </dd>
<dd>이 매개변수를 지정하지 않으면 모든 cf 명령의 도움말 정보가 표시됩니다. </dd>
</dl>


## cf login

{{site.data.keyword.Bluemix_notm}}에 로그인됩니다.
```
cf login
```
cf login 명령을 실행할 때 다음 매개변수 중 하나 이상을 사용할 수 있습니다.
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>{{site.data.keyword.Bluemix_notm}} API 엔드포인트의 URL입니다. 이 매개변수는 선택적 매개변수입니다. </dd>
<dt>*-u* user_name</dt>
<dd>사용자 이름입니다. 이 매개변수는 선택적 매개변수입니다. </dd>
<dt>*-p*password</dt>
<dd>비밀번호입니다. </dd>
<dd>*중요:* 명령행 인터페이스에 *-p* 매개변수를 사용하여 비밀번호를 지정하는 경우, 이 비밀번호가 명령행 히스토리에 기록될 수 있습니다. 보안을 위해 -p 매개변수를 사용하여 비밀번호를 지정하지 말아야 합니다. 대신, 명령행 인터페이스의 지시에 따라 비밀번호를 입력하십시오.</dd>
<dt>*-o* organization_name</dt>
<dd>로그인하려는 조직의 이름입니다. </dd>
<dt>*-s* space_name</dt>
<dd>로그인하려는 영역의 이름입니다. </dd>
<dt>*--skip-ssl-validation*</dt>
<dd>SSL 유효성 검증 프로세스를 사용 안함으로 설정합니다. 이 매개변수를 사용할 경우 보안 문제가 발생할 수 있습니다. </dd>
</dl>

*참고:* 이 명령의 *-p* 매개변수에 비밀번호를 제공할 경우 비밀번호가 쉘 명령 히스토리 파일에 기록되며 로컬 운영 체제의 다른 사용자가 이를 볼 수 있습니다.


## cf logs

애플리케이션의 STDOUT 및 STDERR 로그 스트림을 표시합니다.
```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>*--recent*</dt>
<dd>최근 로그를 검색합니다. </dd>
</dl>

## cf marketplace

Marketplace에서 사용 가능한 모든 서비스를 나열합니다. 이 명령을 통해 나열된 서비스가 {{site.data.keyword.Bluemix_notm}} 카탈로그에도 표시됩니다.
```
cf marketplace
```

## cf push

새 애플리케이션을 Bluemix에 배치하거나, Bluemix에서 기존 애플리케이션을 업데이트합니다.
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>*-b* buildpack_name</dt>
<dd>빌드팩 이름입니다. buildpack_name은 이름 또는 Git URL로 된 사용자 정의 빌드팩일 수 있습니다(예: `my-buildpack` 또는 `https://github.com/heroku/heroku-buildpack-play.git`).</dd>
<dt>*-c* start_command</dt>
<dd>애플리케이션의 시작 명령입니다. 기본 시작 명령을 사용하려면 이 옵션에 대해 null 값을 지정하십시오. 예를 들어, 다음과 같습니다. </dd>
<dd>```
cf push appname -c null
```</dd>
<dd>이 옵션을 사용하여 스크립트 파일을 실행할 수도 있습니다. 예:
```
cf push appname -c “bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>Manifest 파일의 경로입니다. 기본 Manifest 파일은 애플리케이션의 루트 디렉토리 아래에 있는 manifest.yml입니다.</dd>
<dt>*-i* instance_number</dt>
<dd>인스턴스 수입니다. </dd>
<dt>*-k* disk_limit</dt>
<dd>애플리케이션에 대한 디스크 한계입니다(예: *256M*, *1024M* 또는 *1G*). </dd>
<dt>*-m* memory_limit</dt>
<dd>애플리케이션에 대한 메모리 한계입니다(예: *256M*, *1024M* 또는 *1G*). </dd>
<dt>*-n* host_name</dt>
<dd>애플리케이션의 호스트 이름입니다(예: *my-subdomain*). </dd>
<dt>*-p* app_path</dt>
<dd>애플리케이션 디렉토리 또는 애플리케이션 아카이브 파일의 경로입니다. </dd>
<dt>*-t* timeout</dt>
<dd>애플리케이션 시작에 걸리는 최대 시간(초)입니다. 다른 서버 측 제한시간이 이 값을 대체할 수 있습니다. </dd>
<dt>*-s* stackname</dt>
<dd>앱을 실행하기 위한 스택입니다. 스택은 운영 체제를 포함하는 빌드별 파일 시스템입니다. {{site.data.keyword.Bluemix_notm}}에서 사용 가능한 스택을 보려면 `cf stacks`를 사용하십시오.</dd>
<dt>*--no-hostname*</dt>
<dd>Bluemix 시스템 도메인을 이 애플리케이션에 맵핑합니다.</dd>
<dt>*--no-manifest*</dt>
<dd>기본 Manifest 파일을 무시합니다. </dd>
<dt>*--no-route*</dt>
<dd>라우트를 이 애플리케이션에 맵핑하지 않습니다. </dd>
<dt>*--no-start*</dt>
<dd>애플리케이션이 배치된 후 애플리케이션을 시작하지 않습니다. </dd>
<dt>*--random-route*</dt>
<dd>애플리케이션에 대한 랜덤 라우트를 작성합니다. </dd>
</dl>

## cf scale

애플리케이션에 대한 인스턴스 번호, 디스크 공간 한계 및 메모리 한계를 표시하거나 변경합니다.
```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>*-i* instance_number</dt>
<dd>인스턴스 수입니다. </dd>
<dt>*-k* disk_limit</dt>
<dd>애플리케이션에 대한 디스크 한계입니다(예: *256M*, *1024M* 또는 *1G*). </dd>
<dt>*-m* memory_limit</dt>
<dd>애플리케이션에 대한 메모리 한계입니다(예: *256M*, *1024M* 또는 *1G*). </dd>
<dt>*-f*</dt>
<dd>프롬프트 없이 애플리케이션을 강제로 다시 시작합니다. </dd>
</dl>

## cf services

현재 영역에서 사용 가능한 모든 서비스를 나열합니다.
```
cf services
```

## cf set-env

애플리케이션에 대한 환경 변수를 설정합니다.
```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>var_name</dt>
<dd>환경 변수의 이름입니다. </dd>
<dt>var_value</dt>
<dd>환경 변수의 값입니다. </dd>
</dl>

## cf stacks

모든 스택을 나열합니다. 스택은 앱을 실행할 수 있는 운영 체제를 포함하여 미리 빌드된 파일 시스템입니다.
```
cf stacks
```

## cf stop

애플리케이션을 중지합니다.
```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
</dl>

## cf -v

명령행 인터페이스의 버전을 표시합니다.
```
cf -v
```

# 관련 링크
{: #rellinks}
## 일반 
{: #general}
* [빠른 참조 카드 - cf 명령](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
