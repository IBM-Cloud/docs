---



copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"


---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Cloud Foundry(cf) 명령
{: #cf}

Cloud Foundry(cf) 명령행 인터페이스(CLI)는 앱 관리를 위한 명령 세트를 제공합니다. 다음 정보는 앱 관리를 위해 가장 공통적으로 사용되는 cf 명령을 나열하며, 해당 이름, 옵션, 사용법, 전제조건, 설명 및 예제가 포함됩니다. cf 명령과 연관된 도움말 정보를 모두 나열하려면 `cf help`를 사용하십시오. `cf command_name -h`를 사용하면 특정 명령에 대한 자세한 도움말 정보를 볼 수 있습니다.
{: shortdesc}

**참고**: 네트워크에서 cf 명령을 실행하는 호스트와 Cloud Foundry API 엔드포인트 사이에 HTTP 프록시 서버가 있으면 `HTTP_PROXY` 환경 변수를 설정하여 프록시 서버의 호스트 이름 또는 IP 주소를 지정해야 합니다. 세부사항은 [Using the cf CLI with an HTTP Proxy Server ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html){: new_window}를 참조하십시오.


## Cloud Foundry CLI 명령 색인
{: #CLIname_commands_index}

자주 사용되는 Cloud Foundry 명령을 참조하려면 다음 표의 색인을 사용하십시오.

<table summary="알파벳순으로 표시된 일반 Cloud Foundry 명령입니다. 명령에 대한 세부 정보를 제공하는 링크가 포함되어 있습니다.">
 <caption>표 1. 일반 Cloud Foundry 명령</caption>
 <thead>
 <th colspan="6">일반 Cloud Foundry 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](/docs/cli/reference/cfcommands/index.html#cf_api)</td>
 <td>[help](/docs/cli/reference/cfcommands/index.html#cf_help)</td>
 <td>[login](/docs/cli/reference/cfcommands/index.html#cf_login)</td>
 <td>[stacks](/docs/cli/reference/cfcommands/index.html#cf_stacks)</td>
 <td>[target](/docs/cli/reference/cfcommands/index.html#cf_target)</td>
 <td>[-v](/docs/cli/reference/cfcommands/index.html#cf_v)</td>
 </tr>
   </tbody>
 </table>


<table summary="알파벳순으로 표시된 앱, 영역 및 서비스 관리를 위한 명령입니다. 각 명령에는 명령에 대한 세부 정보를 제공하는 링크가 포함되어 있습니다.">
 <caption>표 2. 앱, 영역 및 서비스 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">앱, 영역 및 서비스 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](/docs/cli/reference/cfcommands/index.html#cf_apps)</td>
 <td>[bind-service](/docs/cli/reference/cfcommands/index.html#cf_bind-service)</td>
 <td>[create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)</td>
 <td>[create-space](/docs/cli/reference/cfcommands/index.html#cf_create-space)</td>
 <td>[delete](/docs/cli/reference/cfcommands/index.html#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](/docs/cli/reference/cfcommands/index.html#cf_delete-space)</td>
 <td>[events](/docs/cli/reference/cfcommands/index.html#cf_events)</td>
 <td>[logs](/docs/cli/reference/cfcommands/index.html#cf_logs)</td>
 <td>[marketplace](/docs/cli/reference/cfcommands/index.html#cf_marketplace)</td>
 <td>[push](/docs/cli/reference/cfcommands/index.html#cf_push)</td>
  </tr>
 <tr>
 <td>[scale](/docs/cli/reference/cfcommands/index.html#cf_scale)</td>
 <td>[services](/docs/cli/reference/cfcommands/index.html#cf_services)
 <td>[set-env](/docs/cli/reference/cfcommands/index.html#cf_set-env)</td>
 <td>[ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)</td>
 <td>[stop](/docs/cli/reference/cfcommands/index.html#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

이 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}의 API 엔드포인트에 대한 URL을 표시하거나 지정합니다.

```
cf api [BluemixServerURL] [--skip-ssl-validation] [--unset]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>BluemixServerURL(선택사항)</dt>
   <dd>{{site.data.keyword.Bluemix_notm}}에 연결할 때 지정해야 하는 Bluemix API 엔드포인트의 URL입니다. 일반적으로 이 URL은 `https://api.{DomainName}`입니다.
   현재 사용 중인 API 엔드포인트의 URL을 표시하려는 경우 cf api 명령에 이 매개변수를 지정할 필요가 없습니다.</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>SSL 유효성 검증 프로세스를 사용 안함으로 설정합니다. 이 매개변수를 사용할 경우 보안 문제가 발생할 수 있습니다. </dd>
   <dt>* --unset</dt>
   <dd>모든 API 엔드포인트에 대한 연결 정보를 제거합니다. </dd>
    </dl>

<strong>예제</strong>:

현재 API 엔드포인트를 확인합니다.
```
cf api
```
{: codeblock}

api.ng.bluemix.net의 모든 API 엔드포인트에 대한 연결을 제거합니다. 
```
cf api api.ng.bluemix.network --unset
```
{: codeblock}

api.ng.bluemix.network의 SSL 유효성 검증 프로세스를 사용하지 않습니다. 
```
cf api api.ng.bluemix.network --skip-ssl-validation
```
{: codeblock}


## cf apps
{: #cf_apps}

현재 영역에 배치된 모든 애플리케이션을 나열합니다. 각 애플리케이션의 상태도 표시됩니다. 

앱에 대해 하나의 인스턴스가 있는 것으로 가정할 때 cf 앱 명령 응답의 인스턴스 열에 앱이 실행 중이면 1/1이, 앱이 중단되었으면 0/1이 표시됩니다. 앱 인스턴스 상태를 알 수 없음을 의미하는 ?/1이 표시되면 앱 URL을 브라우저로 복사하여 앱의 응답 여부를 확인하거나 `cf logs appname` 명령으로 로그를 추적하여 앱이 로그 컨텐츠를 생성하는지 확인할 수 있습니다.

```
cf apps
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`


## cf bind-service
{: #cf_bind-service}

기존 서비스 인스턴스를 애플리케이션에 바인딩합니다. 

```
cf bind-service appname service_instance
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

   <dl>
   <dt>appname(필수)</dt>
   <dd>애플리케이션 이름입니다. </dd>
   <dt>service_instance(필수)</dt>
   <dd>기존 서비스 인스턴스의 이름입니다. </dd>
    </dl>

<strong>예제</strong>:

`my_dataworks`라는 서비스 인스턴스를 `my_app`이라는 앱으로 바인드합니다.
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

서비스 인스턴스를 작성합니다. 

```
cf create-service service_name service_plan service_instance
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

   <dl>
   <dt>service_name(필수)</dt>
   <dd>서비스 이름입니다. </dd>
   <dt>service_plan(필수)</dt>
   <dd>서비스 플랜의 이름입니다. </dd>
   <dt>service_instance(필수)</dt>
   <dd>작성할 새 서비스 인스턴스에 사용할 이름입니다. </dd>
    </dl>

<strong>예제</strong>:

`free` 플랜을 사용하여 {{site.data.keyword.dataworks_short}} 서비스의 인스턴스를 작성합니다. 
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

영역을 작성합니다. 

```
cf create-space space_name [-o] [-q]
```

<strong>전제조건</strong>: `cf api`, `cf login`

<strong>명령 옵션</strong>:

   <dl>
   <dt>space_name(필수)</dt>
   <dd>영역의 이름입니다. </dd>
   <dt>*-o*(선택사항)</dt>
   <dd>영역을 작성하려는 조직의 이름입니다. </dd>
   <dt>*-q*(선택사항)</dt>
   <dd>새로 작성된 영역에 지정되는 할당량입니다. 이 값을 지정하지 않으면 기본 할당량이 자동으로 지정됩니다.</dd>
    </dl>

<strong>예제</strong>:

new_space라는 영역을 작성합니다.
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

기존 애플리케이션을 삭제합니다. 

```
cf delete appname [-f] [-r]
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

   <dl>
   <dt>appname(필수)</dt>
   <dd>애플리케이션 이름입니다. </dd>
   <dt>*-f*(선택사항)</dt>
   <dd>애플리케이션을 확인 없이 강제로 삭제합니다. </dd>
   <dt>*-r*(선택사항)</dt>
   <dd>애플리케이션과 연관된 도메인 이름을 모두 삭제합니다. </dd>
    </dl>

<strong>예제</strong>:

`my_app`(확인 필수)이라는 애플리케이션을 삭제합니다.
```
cf delete my_app
```
{: codeblock}

확인할 필요 없이 `my_app`이라는 애플리케이션을 삭제합니다.
```
cf delete my_app -f
```
{: codeblock}

`my_app`이라는 애플리케이션 및 `my_app`과 연관된 모든 도메인 이름을 삭제합니다. 
```
cf delete my_app -r
```
{: codeblock}

확인할 필요 없이 `my_app`이라는 애플리케이션 및 `my_app`과 연관된 모든 도메인 이름을 삭제합니다. 
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

영역을 삭제합니다. 

```
cf delete-space space_name [-f]
```

<strong>전제조건</strong>: `cf api`, `cf login`

<strong>명령 옵션</strong>:

   <dl>
   <dt>space_name(필수)</dt>
   <dd>영역의 이름입니다. </dd>
   <dt>*-f*(선택사항)</dt>
   <dd>확인 없이 영역을 강제로 삭제합니다. </dd>
   *참고:* 영역을 삭제하면 되돌릴 수 없습니다.
</dl>

<strong>예제</strong>:

`my_app`(확인 필수)이라는 애플리케이션을 삭제합니다.
```
cf delete my_app
```
{: codeblock}

확인할 필요 없이 `my_app`이라는 애플리케이션을 삭제합니다.
```
cf delete my_app -f
```
{: codeblock}

`my_app`이라는 애플리케이션 및 `my_app`과 연관된 모든 도메인 이름을 삭제합니다. 
```
cf delete my_app -r
```
{: codeblock}

확인할 필요 없이 `my_app`이라는 애플리케이션 및 `my_app`과 연관된 모든 도메인 이름을 삭제합니다. 
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

애플리케이션과 관련된 런타임 이벤트를 표시합니다. 

```
cf events [appname]
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

   <dl>
   <dt>appname</dt>
   <dd>애플리케이션 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

`my_app`이라는 애플리케이션에 대한 이벤트를 표시합니다.
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

모든 cf 명령 또는 특정 cf 명령에 대한 도움말 정보를 표시합니다. 

```
cf help [command_name]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>command_name(선택사항)</dt>
   <dd>명령 이름입니다. </dd>
    </dl>

<strong>예제</strong>:

모든 cf 명령에 대한 도움말 정보를 표시합니다.
```
cf help
```
{: codeblock}

이벤트 명령에 대한 도움말 페이지를 표시합니다. 
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

{{site.data.keyword.Bluemix_notm}}에 로그인됩니다. 

**참고**: [연합 ID](/docs/admin/account.html#signup)로 로그인하는 경우 싱글 사인온(SSO) 매개변수를 사용하여 로그인해야 합니다. 

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

<dl>
<dt>*-a* https://api.{DomainName}(선택사항)</dt>
<dd>{{site.data.keyword.Bluemix_notm}} API 엔드포인트의 URL입니다. </dd>
<dt>*-u* user_name(선택사항)</dt>
<dd>사용자 이름입니다. </dd>
<dt>*-p* password(선택사항)</dt>
<dd>비밀번호입니다. </dd>
<dd>*중요:* 명령행 인터페이스에 *-p* 매개변수를 사용하여 비밀번호를 지정하는 경우, 이 비밀번호가 명령행 히스토리에 기록될 수 있습니다. 보안을 위해 -p 매개변수를 사용하여 비밀번호를 지정하지 말아야 합니다. 대신, 명령행 인터페이스의 지시에 따라 비밀번호를 입력하십시오.</dd>
<dt>*-sso*</dt>
<dd>연합된 ID로 로그인하는 경우 싱글 사인온 옵션(SSO)을 사용해야 합니다. IBM ID로 로그인하는 경우에는 필요하지 않습니다. 연합된 ID로 로그인하려고 시도하고 SSO 매개변수를 지정하지 않으면, 이를 포함하도록 프롬프트가 표시됩니다. SSO 매개변수를 사용하면 로그인 시 일회성 패스코드를 입력하도록 프롬프트가 표시됩니다.</dd>
<dt>*-o* organization_name</dt>
<dd>로그인하려는 조직의 이름입니다. </dd>
<dt>*-s* space_name</dt>
<dd>로그인하려는 영역의 이름입니다. </dd>
<dt>*--skip-ssl-validation*(선택사항)</dt>
<dd>SSL 유효성 검증 프로세스를 사용 안함으로 설정합니다. 이 매개변수를 사용할 경우 보안 문제가 발생할 수 있습니다. </dd>
</dl>

*참고:* 이 명령의 *-p* 매개변수에 비밀번호를 제공할 경우 비밀번호가 쉘 명령 히스토리 파일에 기록되며 로컬 운영 체제의 다른 사용자가 이를 볼 수 있습니다.

<strong>예제</strong>:

{{site.data.keyword.Bluemix_notm}}에 로그인하십시오.
```
cf login
```
{: codeblock}

`https://api.ng.bluemix.net`의 정의된 엔드포인트를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인합니다.
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

`https://api.ng.bluemix.net`의 정의된 엔드포인트, `user_name`의 사용자 이름 및 보안상의 이유로 지정되지 않은 비밀번호를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인합니다. 
```
cf login -a https://api.ng.bluemix.net -u user_name
```
{: codeblock}

`https://api.ng.bluemix.net`의 정의된 엔드포인트, `user_name`의 사용자 이름, 보안상의 이유로 지정되지 않은 비밀번호, `org_name`의 조직 이름 및 `space_name`의 영역 이름을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인합니다. 
```
cf login -a https://api.ng.bluemix.net -u user_name -o org_name -s space_name
```
{: codeblock}


## cf logs
{: #cf_logs}

애플리케이션의 STDOUT 및 STDERR 로그 스트림을 표시합니다. 

```
cf logs appname [--recent]
```
<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>*--recent*(선택사항)</dt>
<dd>최근 로그를 검색합니다. </dd>
</dl>

<strong>예제</strong>:

`my_app`이라는 애플리케이션에 대한 로그 스트림을 표시합니다.
```
cf logs my_app
```
{: codeblock}

`my_app`이라는 애플리케이션에 대한 최신 로그 스트림을 표시합니다.
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

Marketplace에서 사용 가능한 모든 서비스를 나열합니다. 이 명령을 통해 나열된 서비스가 {{site.data.keyword.Bluemix_notm}} 카탈로그에도 표시됩니다. 

```
cf marketplace
```
<strong>전제조건</strong>: `cf api`

<strong>명령 옵션</strong>: 없음

<strong>예제</strong>:

marketplace의 모든 서비스를 나열합니다. 
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

새 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하거나, {{site.data.keyword.Bluemix_notm}}에서 기존 애플리케이션을 업데이트합니다. 

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

<dl>
<dt>appname(필수)</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>*-b* buildpack_name(선택사항)</dt>
<dd>빌드팩 이름입니다. buildpack_name은 이름(예: liberty-for-java)별 사용자 정의 빌드팩이거나 Git URL(예: https://github.com/cloudfoundry/java-buildpack.git) 또는 분기나 태그가 포함된 Git URL(예: v3.3.0 태그의 경우 https://github.com/cloudfoundry/java-buildpack.git#v3.3.0)일 수 있습니다. </dd>
<dt>*-c* start_command(선택사항)</dt>
<dd>애플리케이션의 시작 명령입니다. 기본 시작 명령을 사용하려면 이 옵션에 대해 null 값을 지정하십시오. </dd>
<dt>*-f* manifest_path(선택사항)</dt>
<dd>Manifest 파일의 경로입니다. 기본 Manifest 파일은 애플리케이션의 루트 디렉토리 아래에 있는 manifest.yml입니다.</dd>
<dt>*-i* instance_number(선택사항)</dt>
<dd>인스턴스 수입니다. </dd>
<dt>*-k* disk_limit(선택사항)</dt>
<dd>애플리케이션에 대한 디스크 한계입니다. 가능한 값은 *256M*, *1024M* 또는 *1G*입니다.</dd>
<dt>*-m* memory_limit(선택사항)</dt>
<dd>애플리케이션에 대한 메모리 한계입니다. 가능한 값은 *256M*, *1024M* 또는 *1G*입니다.</dd>
<dt>*-n* host_name(선택사항)</dt>
<dd>애플리케이션의 호스트 이름입니다(예: *my-subdomain*). </dd>
<dt>*-p* app_path(선택사항)</dt>
<dd>애플리케이션 디렉토리 또는 애플리케이션 아카이브 파일의 경로입니다. </dd>
<dt>*-s* stack_name(선택사항)</dt>
<dd>앱을 실행하기 위한 스택입니다. 스택은 운영 체제를 포함하는 빌드별 파일 시스템입니다. {{site.data.keyword.Bluemix_notm}}에서 사용 가능한 스택을 보려면 `cf stacks`를 사용하십시오.</dd>
<dt>*-t* timeout(선택사항)</dt>
<dd>애플리케이션 시작에 걸리는 최대 시간(초)입니다. 다른 서버 측 제한시간이 이 값을 대체할 수 있습니다. </dd>
<dt>*--no-hostname*(선택사항)</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 시스템 도메인을 이 애플리케이션에 맵핑합니다. </dd>
<dt>*--no-manifest*(선택사항)</dt>
<dd>기본 Manifest 파일을 무시합니다. </dd>
<dt>*--no-route*(선택사항)</dt>
<dd>라우트를 이 애플리케이션에 맵핑하지 않습니다. </dd>
<dt>*--no-start*(선택사항)</dt>
<dd>애플리케이션이 배치된 후 애플리케이션을 시작하지 않습니다. </dd>
<dt>*--random-route*(선택사항)</dt>
<dd>애플리케이션에 대한 랜덤 라우트를 작성합니다. </dd>
</dl>

<strong>예제</strong>:

기본 시작 명령을 사용하여 `my_app`이라는 애플리케이션을 시작합니다.
```
cf push `my_app` -c null
```
{: codeblock}

옵션을 사용하여 `my_app`이라는 애플리케이션을 시작하여 `run.sh` 이라는 스크립트 파일을 실행합니다. 
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

애플리케이션에 대한 인스턴스 번호, 디스크 공간 한계 및 메모리 한계를 표시하거나 변경합니다. 

```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

<dl>
<dt>appname(필수)</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>*-i* instance_number(선택사항)</dt>
<dd>인스턴스 수입니다. </dd>
<dt>*-k* disk_limit(선택사항)</dt>
<dd>애플리케이션에 대한 디스크 한계입니다. 가능한 값은 `256M`, `1024M` 또는 `1G`입니다. </dd>
<dt>*-m* memory_limit(선택사항)</dt>
<dd>애플리케이션에 대한 메모리 한계입니다. 가능한 값은 `256M`, `1024M` 또는 `1G`입니다. </dd>
<dt>*-f*(선택사항)</dt>
<dd>프롬프트 없이 애플리케이션을 강제로 다시 시작합니다. </dd>
</dl>

<strong>예제</strong>:

`my_app`이라는 애플리케이션에 대한 인스턴스 번호, 디스크 공간 한계 및 메모리 한계를 표시합니다.
```
cf scale my_app
```
{: codeblock}

`my_app`이라는 앱에 대한 인스턴스 번호를 `1234`로, 디스크 영역 한계를 `1G`로, 메모리 한계를 `1G`로 수정하십시오.
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

현재 영역에서 사용 가능한 모든 서비스를 나열합니다. 

```
cf services
```
<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>: 없음

<strong>예제</strong>:

현재 영역의 모든 서비스를 나열합니다. 
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

애플리케이션에 대한 환경 변수를 설정합니다.

```
cf set-env appname var_name var_value
```
<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

<dl>
<dt>appname(필수)</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>var_name(필수)</dt>
<dd>환경 변수의 이름입니다. </dd>
<dt>var_value(필수)</dt>
<dd>환경 변수의 값입니다. </dd>
</dl>

<strong>예제</strong>:

`my_app`이라는 애플리케이션에 대한 `123`의 값을 사용하여 `variable_a`라는 환경 변수를 설정합니다. 
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

애플리케이션 컨테이너에 안전하게 액세스합니다. `cf ssh` 명령을 사용하면 대화식 SSH 세션을 설정하고, 리모트 명령을 실행하고, 파일을 전송하고, 특정 애플리케이션 컨테이너 인스턴스를 사용하여 포트 전달을 설정할 수 있습니다. 

```
cf ssh
```
<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

기본적으로, SSH 액세스는 Diego 애플리케이션에 대해 사용 가능하도록 설정되어 있습니다. `cf ssh-enabled` 명령을 사용하여 SSH 액세스가 사용 가능하도록 설정되어 있는지 확인하거나, 사용 안함으로 설정되어 있는 경우 `cf enable-ssh` 명령을 사용하여 액세스를 사용으로 설정할 수 있습니다.  

<strong>명령 옵션</strong>:

<dl>
<dt>appname</dt>
<dd>애플리케이션 이름입니다. </dd>
<dt>-c</dt>
<dd>실행할 원격 명령을 지정합니다. </dd>
<dt>-i</dt>
<dd>애플리케이션의 특정 인스턴스를 대상으로 합니다. 지정되지 않은 경우 애플리케이션의 첫 번째 인스턴스가 사용됩니다(인덱스가 0인 인스턴스). </dd>
<dt>-L</dt>
<dd>시스템의 출력 포트를 애플리케이션 VM의 입력 포트에 바인딩하도록 로컬 포트 전달을 사용으로 설정합니다.</dd>
<dt>-N</dt>
<dd>원격 명령을 실행하지 않습니다.</dd>
<dt>-t, -tt 또는 -T</dt>
<dd>터미널 라인 출력을 생성하지 않고 pseudo-tty 모드로 SSH 세션을 실행할 수 있습니다.<dd>
</dl>

<strong>예제</strong>:

`my_app` 애플리케이션을 실행하는 컨테이너 인스턴스로 대화식 SSH 세션을 시작합니다. 
```
$ cf ssh my_app
```
{: codeblock}

`my_app` 애플리케이션 컨테이너 인스턴스에서 단일 명령을 실행합니다. 
```
$ cf ssh my_app -c "ls -l"
```

`my_app` 애플리케이션 컨테이너 인스턴스에서 하나의 파일을 전송합니다. 
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

로컬 시스템의 7777 포트의 포트 전달을 `my_app` 애플리케이션 컨테이너 인스턴스의 8888 포트로 설정합니다. 
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

모든 스택을 나열합니다. 스택은 앱을 실행할 수 있는 운영 체제를 포함하여 미리 빌드된 파일 시스템입니다. 

```
cf stacks
```
<strong>전제조건</strong>: `cf api`, `cf login`

<strong>명령 옵션</strong>: 없음

<strong>예제</strong>:

모든 스택을 나열합니다. 
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

애플리케이션을 중지합니다.

```
cf stop appname
```
<strong>전제조건</strong>: `cf api`, `cf login`, `cf target`

<strong>명령 옵션</strong>:

<dl>
<dt>appname(필수)</dt>
<dd>애플리케이션 이름입니다. </dd>
</dl>

<strong>예제</strong>:

`my_app`이라는 애플리케이션을 중지합니다.
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

대상 조직 또는 영역을 설정하거나 확인합니다.

```
cf target [-o org_name] [-s space_name]
```
<strong>전제조건</strong>: `cf api`, `cf login`

<strong>명령 옵션</strong>:

<dl>
<dt>-o *org_name*(선택사항)</dt>
<dd>영역이 있는 조직의 이름입니다. </dd>
<dt>-s *space_name*(선택사항)</dt>
<dd>영역의 이름입니다. </dd>
</dl>

<strong>예제</strong>:

대상을 "my_org"라는 조직 및 "my_space"라는 영역 이름으로 설정합니다.
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

명령행 인터페이스의 버전을 표시합니다. 

```
cf -v
```
<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>: 없음

<strong>예제</strong>:

명령행 인터페이스의 버전을 표시합니다.
```
cf -v
```
{: codeblock}



# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [Cloud Foundry CLI 다운로드 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases)
{: new_window}
* [빠른 참조 카드 - cf 명령 ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html)
{: new_window}
