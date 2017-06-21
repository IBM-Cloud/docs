---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}(bx) 명령
{: #bluemix_cli}

버전: 0.5.2

{{site.data.keyword.Bluemix_notm}} 명령행 인터페이스(CLI)는 사용자가 {{site.data.keyword.Bluemix_notm}}와 상호작용할 수 있도록 네임스페이스별로 그룹화된 명령 세트를 제공합니다. 일부 {{site.data.keyword.Bluemix_notm}} 명령은 기존 cf 명령의 랩퍼이며, 나머지는 {{site.data.keyword.Bluemix_notm}} 사용자에 대해 확장 기능을 제공합니다. 다음 정보에서는 {{site.data.keyword.Bluemix_notm}} CLI에서 지원하는 명령을 나열하며, 해당 이름, 옵션, 사용법, 전제조건, 설명 및 예제가 포함됩니다.
{:shortdesc}

**참고:** *전제조건*에는 명령을 사용하기 전에 필요한 조치가 설명되어 있습니다. 전제조건 조치가 없는 명령은 **없음**으로 표시됩니다. 그 밖의 경우에는 전제조건으로 다음과 같은 조치 중 하나 이상을 수행해야 할 수 있습니다.

<dl>
<dt>엔드포인트</dt>
<dd>명령을 사용하기 전에 <code>bluemix api</code>를 통해 API 엔드포인트를 설정해야 합니다.</dd>
<dt>로그인</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix login</code> 명령을 사용하여 로그인해야 합니다. 연합 ID로 로그인한 경우에는 '--sso' 옵션을 사용하여 일회성 패스코드로 인증하거나 '--apikey'를 사용하여  API 키로 인증하십시오. {{site.data.keyword.Bluemix_notm}} 콘솔 **관리** &gt; **보안** &gt; **Bluemix API 키**로 이동하여 API 키를 작성하십시오.
</dd>
<dt>대상</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix target</code> 명령을 사용하여 조직과 영역을 설정해야 합니다.</dd>
<dt>Docker</dt>
<dd>이 명령을 실행하려면 Docker CLI(docker)가 설치되어 있어야 합니다.</dd>
</dl>

## Bluemix 명령 색인
{: #bx_commands_index}

자주 사용되는 Bluemix 명령을 참조하려면 다음 표의 색인을 사용하십시오.

**참고:** Bluemix 명령의 short 형식을 사용할 수 있습니다. 예를 들어, `bx api`는 `bluemix api`의 단축형입니다. 



<table summary="일반 Bluemix 명령.">
 <caption>표 1. 일반 Bluemix 명령</caption>
 <thead>
 <th colspan="5">일반 Bluemix 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help
](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api
](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout
](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target
](bx_cli.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](bx_cli.html#bluemix_info) </td>
 <td>[bluemix regions](bx_cli.html#bluemix_regions) </td>
 <td>[bluemix config](bx_cli.html#bluemix_config)</td>
 <td>[bluemix curl](bx_cli.html#bluemix_curl)</td>
 <td>[bluemix update](bx_cli.html#bluemix_update)</td>
 </tr>
 </tbody>
 </table>

<table summary="계정, 조직, 영역, 역할 및 API 키를 관리하는 데 사용할 수 있는 bluemix 명령입니다.">
<caption>표 2. 계정, 조직, 영역, 역할 및 API 키 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">계정, 조직, 영역, 역할 및 API 키 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](bx_cli.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](bx_cli.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](bx_cli.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](bx_cli.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](bx_cli.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](bx_cli.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](bx_cli.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](bx_cli.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](bx_cli.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](bx_cli.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](bx_cli.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam org-users](bx_cli.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-user-add](bx_cli.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](bx_cli.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-roles](bx_cli.html#bluemix_iam_org_roles)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-role-set](bx_cli.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](bx_cli.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](bx_cli.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-roles](bx_cli.html#bluemix_iam_space_roles)</td>
 <td>[bluemix iam space-role-set](bx_cli.html#bluemix_iam_space_role_set)</td>
</tr>
 <tr>
 <td>[bluemix iam space-role-unset](bx_cli.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix iam accounts](bx_cli.html#bluemix_iam_accounts)</td>
 <td>[bluemix iam org-account](bx_cli.html#bluemix_iam_org_account)</td>
 <td>[bluemix iam account-users
](bx_cli.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](bx_cli.html#bluemix_iam_account_users_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam account-user-invite](bx_cli.html#bluemix_iam_account_user_invite)</td>
  <td>[bluemix iam account-user-reinvite](bx_cli.html#bluemix_iam_account_user_reinvite)</td>
  <td>[bluemix iam api-keys](bx_cli.html#bluemix_iam_api_keys)</td>
  <td>[bluemix iam api-key-create](bx_cli.html#bluemix_iam_api_key_create)</td>
  <td>[bluemix iam api-key-delete](bx_cli.html#bluemix_iam_api_key_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam api-key-update](bx_cli.html#bluemix_iam_api_key_update)</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
 </tr>
 </tbody>
 </table>

<table summary="cf 앱 및 앱 관련 도메인, 라우트와 인증서를 관리하는 데 사용할 수 있는 bluemix 명령입니다.">
<caption>표 3. cf 앱 및 앱 관련 도메인, 라우트 및 인증서 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">cf 앱 및 앱 관련 도메인, 라우트 및 인증서 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](bx_cli.html#bluemix_app_push)</td>
 <td>[bluemix app list](bx_cli.html#bluemix_app_list)</td>
 <td>[bluemix app show](bx_cli.html#bluemix_app_show)</td>
 <td>[bluemix app delete](bx_cli.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](bx_cli.html#bluemix_app_rename)</td>
 </tr>
 <tr>
 <td>[bluemix app start](bx_cli.html#bluemix_app_start)</td>
 <td>[bluemix app stop](bx_cli.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](bx_cli.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](bx_cli.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](bx_cli.html#bluemix_app_instance_restart)</td>
 </tr>
 <tr>
 <td>[bluemix app events](bx_cli.html#bluemix_app_events)</td>
 <td>[bluemix app files](bx_cli.html#bluemix_app_files)</td>
 <td>[bluemix app logs](bx_cli.html#bluemix_app_logs)</td>
 <td>[bluemix app env](bx_cli.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](bx_cli.html#bluemix_app_env_set)</td>
 </tr>
 <tr>
 <td>[bluemix app env-unset](bx_cli.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](bx_cli.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack-show](bx_cli.html#bluemix_app_stack_show)</td>
 <td>[bluemix app manifest-create](bx_cli.html#bluemix_app_manifest_create)</td>
 <td>[bluemix app domain-cert](bx_cli.html#bluemix_app_domain_cert)</td>
 </tr>
 <tr>
  <td>[bluemix app domain-cert-add](bx_cli.html#bluemix_app_domain_cert_add)</td>
  <td>[bluemix app domain-cert-remove](bx_cli.html#bluemix_app_domain_cert_remove)</td>
  <td>[bluemix app domains](bx_cli.html#bluemix_app_domains)</td>
  <td>[bluemix app domain-create](bx_cli.html#bluemix_app_domain_create)</td>
  <td>[bluemix app domain-delete](bx_cli.html#bluemix_app_domain_delete)</td>
 </tr>
 <tr>
  <td>[bluemix app shared-domain-create](bx_cli.html#bluemix_app_shared_domain_create)</td>
  <td>[bluemix app shared-domain-delete](bx_cli.html#bluemix_app_shared_domain_delete)</td>
  <td>[bluemix app routes](bx_cli.html#bluemix_app_routes)</td>
  <td>[bluemix app route-check](bx_cli.html#bluemix_app_route_check)</td>
  <td>[bluemix app route-map](bx_cli.html#bluemix_app_route_map)</td>
 </tr>
 <tr>
  <td>[bluemix app route-unmap](bx_cli.html#bluemix_app_route_unmap)</td>
  <td>[bluemix app route-create](bx_cli.html#bluemix_app_route_create)</td>
  <td>[bluemix app route-delete](bx_cli.html#bluemix_app_route_delete)</td>
  <td>[bluemix app orphaned-routes-delete](bx_cli.html#bluemix_app_orphaned_routes_delete)</td>
  <td></td>
 </tr>
  </tbody>
 </table>

<table summary="Bluemix 서비스 관리에 사용 가능한 Bluemix 명령">
 <caption>표 4. Bluemix 서비스 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">Bluemix 서비스 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](bx_cli.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](bx_cli.html#bluemix_service_list)</td>
 <td>[bluemix service show](bx_cli.html#bluemix_service_show)</td>
 <td>[bluemix service create](bx_cli.html#bluemix_service_create)</td>
 <td>[bluemix service update](bx_cli.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](bx_cli.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](bx_cli.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](bx_cli.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](bx_cli.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](bx_cli.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](bx_cli.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](bx_cli.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](bx_cli.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](bx_cli.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](bx_cli.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>

<table summary="Bluemix 카탈로그, 플러그인, 청구 및 보안 설정을 관리하는 데 사용할 수 있는 Bluemix 명령.">
 <caption>표 5. Bluemix 카탈로그, 플러그인, 청구 및 보안 설정 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">Bluemix 카탈로그, 플러그인, 청구 및 보안 설정 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos
](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list
](bx_cli.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](bx_cli.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](bx_cli.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix plugin update](bx_cli.html#bluemix_plugin_update)</td>
 <td>[bluemix billing account-usage](bx_cli.html#bluemix_billing_account_usage)</td>
 <td>[bluemix billing org-usage](bx_cli.html#bluemix_billing_org_usage)</td>
 <td>[bluemix billing orgs-usage-summary](bx_cli.html#bluemix_billing_orgs_usage_summary)</td>
 <td></td>
 </tr>
 </tbody>
 </table>
 
## bluemix help
{: #bluemix_help}
첫 번째 레벨 기본 제공 명령 및 지원되는 {{site.data.keyword.Bluemix_notm}} CLI 네임스페이스에 대한 일반 도움말 또는 특정 기본 제공 명령 또는 네임스페이스의 도움말을 표시합니다. 

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>COMMAND|NAMESPACE(선택사항)</dt>
   <dd>해당 도움말이 표시되는 명령 또는 네임스페이스입니다. 값을 지정하지 않으면 {{site.data.keyword.Bluemix_notm}} CLI의 일반 도움말이 표시됩니다.</dd>
   </dl>



<strong>예제</strong>:

{{site.data.keyword.Bluemix_notm}} CLI의 일반 도움말을 표시합니다.

```
bluemix help
```

`info` 명령의 도움말을 표시합니다.

```
bluemix help info
```



## bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}} API 엔드포인트를 설정하거나 확인합니다. 

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:
   <dl>
   <dt>API_ENDPOINT(선택사항)</dt>
   <dd>대상으로 지정된 API 엔드포인트입니다(예: `https://api.chinabluemix.net`). *API_ENDPOINT* 및 `--unset` 옵션 중 하나를 지정하지 않으면 현재 API 엔드포인트가 표시됩니다. </dd>
   <dt>--unset(선택사항)</dt>
   <dd>API 엔드포인트 설정을 제거합니다.</dd>
   <dt>--skip-ssl-validation(선택사항)</dt>
   <dd>HTTP 요청의 SSL 유효성 검증을 무시합니다.</dd>
   </dl>
<strong>예제</strong>:

API 엔드포인트를 api.chinabluemix.net으로 설정합니다.

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

현재 API 엔드포인트를 확인합니다.

```
bluemix api
```

API 엔드포인트를 설정 해제합니다.

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

사용자가 로그인됩니다.  

```
bluemix login [OPTIONS...]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:
<dl>
  <dt>-a <i>API_ENDPOINT</i>(선택사항)</dt>
  <dd> API 엔드포인트(예: api.ng.bluemix.net)</dd>
  <dt> --apikey <i>API_KEY 또는 @API_KEY_FILE_PATH</i>
  <dd> API 키 컨텐츠 또는 @로 표시되는 API 키 파일의 경로</dd>
  <dt> --sso(선택사항) </dt>
  <dd> 로그인에 일회성 패스코드 사용</dd>
  <dt> -u <i>USERNAME</i>(선택사항)</dt>
  <dd> Username</dd>
  <dt> -p <i>PASSWORD</i>(선택사항)</dt>
  <dd> 비밀번호</dd>
  <dt> -c <i>ACCOUNT_ID</i>(선택사항) </dt>
  <dd> 대상 계정의 ID</dd>
  <dt> -o <i>ORG_NAME</i>(선택사항)</dt>
  <dd> 대상 조직의 이름</dd>
  <dt> -s <i>SPACE_NAME</i>(선택사항)</dt>
  <dd> 대상 영역의 이름</dd>
  <dt> --skip-ssl-validation(선택사항)</dt>
  <dd> HTTP 요청의 SSL 유효성 검증을 무시합니다. 이 옵션은 권장되지 않습니다.</dd>
</dl>

<strong>예제</strong>:

대화식 로그인:

```
bluemix login
```

사용자 이름과 비밀번호로 로그인하고 대상 계정, 조직 및 영역을 설정하십시오.

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

일회성 패스코드로 로그인하고 대상 계정, 조직 및 영역을 설정하십시오.

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

API 키로 로그인하고 대상을 설정하십시오.

* API 키에 계정이 연관되어 있음

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* API에 계정이 연관되어 있지 않음

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>참고:</strong> API 키에 계정이 연관되어 있는 경우 다른 계정으로 전환이 허용되지 않습니다.


## bluemix logout
{: #bluemix_logout}

사용자가 로그아웃됩니다. 

```
bluemix logout
```

<strong>전제조건</strong>: 없음


## bluemix target
{: #bluemix_target}


대상 계정, 지역, 조직 또는 영역을 설정하거나 보십시오.

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>-c <i>ACCOUNT_ID</i>(선택사항) </dt>
   <dd>대상으로 지정된 계정의 ID입니다.</dd>
   <dt>-r <i>REGION</i>(선택사항)</dt>
   <dd>전환할 지역입니다.</dd>
   <dt>-o <i>ORG_NAME</i>(선택사항)</dt>
   <dd>대상으로 지정된 조직의 이름입니다. </dd>
   <dt>-s <i>SPACE_NAME</i>(선택사항)</dt>
   <dd>대상으로 지정된 영역의 이름입니다. </dd>
   </dl>
옵션이 지정되지 않은 경우, 현재 계정, 영역, 조직 및 영역이 표시됩니다.

<strong>예제</strong>:

현재 계정, 조직 및 영역 설정

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

새 지역으로 전환

```
bluemix target -r eu-gb
```

현재 계정, 지역, 조직 및 영역 보기:

```
bluemix target
```


## bluemix info
{: #bluemix_info}

현재 지역, 클라우드 제어기 버전, 로그인과 교환 액세스 토큰의 엔드포인트 같은 유용한 엔드포인트 등 기본 {{site.data.keyword.Bluemix_notm}} 정보를 확인합니다.

```
bluemix info
```

<strong>전제조건</strong>:  엔드포인트


## bluemix config
{: #bluemix_config}


구성 파일에 기본값을 작성합니다.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>HTTP 요청의 제한시간 값입니다. 기본값은 60초입니다.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>터미널 또는 지정된 파일에 대한 HTTP 요청을 추적합니다. </dd>
   <dt>--color true|false</dt>
   <dd>색상 출력을 사용하거나 사용하지 않습니다. 색상 출력은 기본적으로 사용됩니다. </dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>기본 로케일을 설정합니다. LOCALE이 <i>CLEAR</i>이면 이전 로케일이 삭제됩니다. </dd>
   <dt>--check-version true|false</dt>
   <dd>CLI 버전 확인을 사용하거나 사용하지 않습니다. </dd>
   </dl>

이들 옵션 중에서 한 번에 하나만 지정할 수 있습니다. 

<strong>예제</strong>:

HTTP 요청 제한시간을 30초로 설정합니다.

```
bluemix config --http-timeout 30
```

HTTP 요청에 대한 추적 출력을 사용하도록 설정합니다.

```
bluemix config --trace true
```

지정된 파일 */home/usera/my_trace*에 대한 HTTP 요청 추적: 

```
bluemix config --trace /home/usera/my_trace
```

색상 출력을 사용하지 않도록 설정합니다.

```
bluemix config --color false
```

로케일을 zh_Hans로 설정합니다.

```
bluemix config --locale zh_Hans
```

로케일 설정을 지웁니다.

```
bluemix config --locale CLEAR
```


## bluemix curl
{: #bluemix_curl}

원시 HTTP 요청을 {{site.data.keyword.Bluemix_notm}}에 실행합니다. *Content-Type*은 기본적으로 *application/json*으로 설정됩니다. 이 명령은 {{site.data.keyword.Bluemix_notm}} 다중 클라우드 제어 프록시에 요청을 전송합니다. 지원되는 경로는 [CloudFoundry API 문서 ](http://apidocs.cloudfoundry.org/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg)의 API 경로 정의를 참조하십시오. 

```
bluemix curl PATH [OPTIONS...]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt><i>PATH</i>(필수)</dt>
   <dd>리소스의 URL 경로입니다. 예: /v2/apps.</dd>
   <dt><i>OPTIONS</i>(선택사항)</dt>
   <dd>`bluemix curl` 명령에서 지원하는 옵션은 `cf curl` 명령에 대한 옵션과 동일합니다. </dd>
   </dl>

<strong>예제</strong>:

현재 계정의 모든 조직에 대한 정보를 봅니다.

```
bluemix curl /v2/organizations
```

## bluemix update
{: #bluemix_update}

최신 버전으로 CLI 업데이트

```
bluemix update
```

<strong>전제조건</strong>: 없음

## bluemix regions
{: #bluemix_regions}

{{site.data.keyword.Bluemix_notm}}의 모든 지역에 대한 정보를 확인합니다.

```
bluemix regions
```

<strong>전제조건</strong>:  엔드포인트


## bluemix iam orgs
{: #bluemix_iam_orgs}

모든 조직 나열

```
bluemix iam orgs [-r REGION] [--guid]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>-r <i>REGION</i>(선택사항)</dt>
   <dd>조직 정보가 표시되는 대상 지역입니다. 'all'로 설정되면 모든 지역의 모든 조직이 나열됩니다.</dd>
   <dt>--guid(선택사항)</dt>
   <dd>조직의 GUID를 표시합니다. </dd>
   </dl>

<strong>예제</strong>:

지역: `us-south`의 모든 조직을 GUID를 표시하여 나열합니다. 

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

지정된 조직의 정보를 표시합니다.

```
bluemix iam org ORG_NAME [--guid]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>ORG_NAME(필수)</dt>
   <dd>조직의 이름입니다. </dd>
   <dt>--guid(선택사항)</dt>
   <dd>조직의 GUID를 표시합니다. </dd>
   </dl>

<strong>예제</strong>:

조직 `IBM`의 정보를 GUID를 표시하여 보여줍니다. 

```
bluemix iam org IBM --guid
```


## bluemix iam org-create
{: #bluemix_iam_org_create}

새 조직을 작성합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam org-create ORG_NAME
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>ORG_NAME(필수)</dt>
   <dd>작성 중인 조직의 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

이름이 `IBM`인 조직을 작성합니다. 

```
bluemix iam org-create IBM
```

## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

현재 지역의 조직을 다른 지역으로 복제합니다.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>ORG_NAME(필수)</dt>
   <dd>복제할 기존 조직의 이름입니다. </dd>
   <dt>REGION_NAME(필수)</dt>
   <dd>복제된 조직을 호스팅하는 지역의 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

`myorg` 조직을 `eu-gb` 지역에 복제합니다.

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

조직의 이름을 변경합니다. 이 조작은 조직 관리자만 수행할 수 있습니다.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>OLD_ORG_NAME(필수)</dt>
   <dd>이름이 변경될 조직의 이전 이름입니다.</dd>
   <dt>NEW_ORG_NAME(필수)</dt>
   <dd>이름이 변경될 대상 조직의 새 이름입니다. </dd>
   </dl>

## bluemix iam org-delete
{: #bluemix_iam_org_delete}

현재 지역에서 지정된 조직을 삭제합니다.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>ORG_NAME(필수)</dt>
   <dd>삭제되는 기존 조직의 이름입니다.</dd>
   <dt>-f(선택사항)</dt>
   <dd>확인 없이 강제 삭제합니다. </dd>
   <dt>--all(선택사항)</dt>
   <dd>모든 지역의 조직을 삭제합니다. </dd>
   </dl>


## bluemix iam spaces
{: #bluemix_iam_spaces}

이 명령은 `cf spaces` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space
{: #bluemix_iam_space}

이 명령은 `cf space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-create
{: #bluemix_iam_space_create}

이 명령은 `cf create-space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


이 명령은 `cf rename-space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


이 명령은 `cf delete-space` 명령과 기능 및 옵션이 동일합니다.

## bluemix iam org-users
{: #bluemix_iam_org_users}

역할별로 지정된 조직의 사용자를 표시합니다.

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
<dt>ORG_NAME(필수)</dt>
<dd>조직의 이름입니다. </dd>
<dt>-a(선택사항)</dt>
<dd>지정된 조직의 모든 사용자를 나열하지만, 역할별로 그룹화하지는 않습니다. </dd>
</dl>

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

조직에 사용자를 추가합니다(조직 관리자 필요).

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

조직에서 사용자를 제거합니다(조직 관리자 또는 사용자 자신만).

```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>명령 옵션</strong>:
<dl>
<dt>--force, -f</dt>
<dd>확인 없이 강제 삭제합니다. </dd>
</dl>

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

현재 사용자의 모든 조직 역할 가져오기

```
bluemix iam org-roles
```

<strong>전제조건</strong>: 엔드포인트, 로그인

## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

사용자에게 조직 역할을 지정합니다. 이 조작은 조직 관리자만 수행할 수 있습니다.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
  <dl>
   <dt>USER_NAME(필수)</dt>
   <dd>지정되는 사용자의 이름입니다. </dd>
   <dt>ORG_NAME(필수)</dt>
   <dd>이 사용자가 지정되는 조직의 이름입니다. </dd>
   <dt>ORG_ROLE(필수)</dt>
   <dd>이 사용자가 지정되는 조직 역할의 이름입니다. 예를 들어, 다음과 같습니다.
   <ul>
   <li>OrgManager: 이 역할은 사용자를 초대 및 관리하고, 플랜을 선택 및 변경하며, 지출 한계를 설정할 수 있습니다.</li>
   <li>BillingManager: 이 역할은 청구 계정 및 결제 정보를 작성하고 관리할 수 있습니다. </li>
   <li>OrgAuditor: 이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다. </li>
   </ul>
   </dd>
  </dl>

<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직에 `OrgManager` 역할로 지정합니다.

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

사용자로부터 조직 역할을 제거합니다. 이 조작은 조직 관리자만 수행할 수 있습니다.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>USER_NAME(필수)</dt>
   <dd>제거되는 사용자의 이름입니다. </dd>
   <dt>ORG_NAME(필수)</dt>
   <dd>이 사용자가 제거되는 조직의 이름입니다. </dd>
   <dt>ORG_ROLE(필수)</dt>
   <dd>이 사용자가 제거되는 조직 역할의 이름입니다. 예를 들어, 다음과 같습니다.
   <ul>
   <li>OrgManager: 이 역할은 사용자를 초대 및 관리하고, 플랜을 선택 및 변경하며, 지출 한계를 설정할 수 있습니다.</li>
   <li>BillingManager: 이 역할은 청구 계정 및 결제 정보를 작성하고 관리할 수 있습니다. </li>
   <li>OrgAuditor: 이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다. </li>
   </ul>
   </dd>
    </dl>

<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직에서 `OrgManager` 역할로 제거합니다.

```
bluemix iam org-role-unset Mary IBM OrgManager
```

## bluemix iam space-users
{: #bluemix_iam_space_users}

역할별로 지정된 영역의 사용자를 표시합니다.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>ORG_NAME(필수)</dt>
   <dd>조직의 이름입니다. </dd>
   <dt>SPACE_NAME(필수)</dt>
   <dd>영역의 이름입니다. </dd>
   </dl>


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

사용자에게 영역 역할을 지정합니다. 이 조작은 영역 관리자만 수행할 수 있습니다.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:

   <dl>
   <dt>USER_NAME(필수)</dt>
   <dd>지정되는 사용자의 이름입니다. </dd>
   <dt>ORG_NAME(필수)</dt>
   <dd>이 사용자가 지정되는 조직의 이름입니다. </dd>
   <dt>SPACE_NAME(필수)</dt>
   <dd>이 사용자가 지정되는 영역의 이름입니다. </dd>
   <dt>SPACE_ROLE(필수)</dt>
   <dd>이 사용자가 지정되는 영역 역할의 이름입니다. 예를 들어, 다음과 같습니다.
   <ul>
   <li>SpaceManager: 이 역할은 사용자를 초대 및 관리하고 제공된 영역에 대한 기능을 사용할 수 있습니다. </li>
   <li>SpaceDeveloper: 이 역할은 앱 및 서비스를 작성 및 관리하며 로그 및 보고서를 볼 수 있습니다. </li>
   <li>SpaceAuditor: 이 역할은 영역에 대한 설정 및 로그, 보고서를 볼 수 있습니다. </li>
   </ul></dd>
    </dl>

<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직 및 `Cloud` 영역에 `SpaceManager` 역할로 지정합니다.

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

사용자로부터 영역 역할을 제거합니다. 이 조작은 영역 관리자만 수행할 수 있습니다.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:

   <dl>
   <dt>USER_NAME(필수)</dt>
   <dd>제거되는 사용자의 이름입니다. </dd>
   <dt>ORG_NAME(필수)</dt>
   <dd>이 사용자가 제거되는 조직의 이름입니다. </dd>
   <dt>SPACE_NAME(필수)</dt>
   <dd>이 사용자가 제거되는 영역의 이름입니다. </dd>
   <dt>SPACE_ROLE(필수)</dt>
   <dd>이 사용자가 제거되는 영역 역할의 이름입니다. 예를 들어, 다음과 같습니다.
   <ul>
   <li>SpaceManager: 이 역할은 사용자를 초대 및 관리하고 제공된 영역에 대한 기능을 사용할 수 있습니다. </li>
   <li>SpaceDeveloper: 이 역할은 앱 및 서비스를 작성 및 관리하며 로그 및 보고서를 볼 수 있습니다. </li>
   <li>SpaceAuditor: 이 역할은 영역에 대한 설정 및 로그, 보고서를 볼 수 있습니다. </li>
   </ul></dd>
    </dl>


<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직 및 `Cloud` 영역에서 `SpaceManager` 역할로 제거합니다.

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```

## bluemix iam accounts
{: #bluemix_iam_accounts}

현재 사용자의 모든 계정 나열

```
bluemix iam accounts
```

<strong>전제조건</strong>: 엔드포인트, 로그인


## bluemix iam org-account
{: #bluemix_iam_org_account}

지정된 조직의 계정 표시(조직 사용자 필요)

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
  <dt>--guid(선택사항)</dt>
  <dd>계정 ID만 표시</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

계정과 연관된 사용자를 표시합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

현재 계정에서 사용자 삭제(계정 소유자만)

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
<dt>USERNAME(필수)</dt>
<dd>사용자 이름</dd>
<dt>--force, -f(선택사항)</dt>
<dd>확인 없이 강제 삭제합니다. </dd>
</dl>

## bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}

조직 및 영역 역할이 이미 설정된 계정으로 사용자를 초대합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
   <dt>USER_NAME(필수)</dt>
   <dd>초대되는 사용자의 이름입니다. </dd>
   <dt>ORG_NAME(필수)</dt>
   <dd>이 사용자가 초대되는 조직의 이름입니다. </dd>
   <dt>ORG_ROLE(필수)</dt>
   <dd>이 사용자가 초대되는 조직 역할의 이름입니다. 예를 들어, 다음과 같습니다.
   <ul>
  <li>OrgManager: 이 역할은 사용자를 초대 및 관리하고, 플랜을 선택 및 변경하며, 지출 한계를 설정할 수 있습니다.</li>
  <li>BillingManager: 이 역할은 청구 계정 및 결제 정보를 작성하고 관리할 수 있습니다. </li>
  <li>OrgAuditor: 이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다. </li>
  </ul> </dd>
   <dt>SPACE_NAME(필수)</dt>
   <dd>이 사용자가 초대되는 영역의 이름입니다. </dd>
   <dt>SPACE_ROLE(필수)</dt>
   <dd>이 사용자가 초대되는 영역의 이름입니다. 이 사용자가 초대되는 영역 역할의 이름입니다. 예를 들어, 다음과 같습니다.
   <ul>
<li>SpaceManager: 이 역할은 사용자를 초대 및 관리하고 제공된 영역에 대한 기능을 사용할 수 있습니다. </li>
<li>SpaceDeveloper: 이 역할은 앱 및 서비스를 작성 및 관리하며 로그 및 보고서를 볼 수 있습니다. </li>
<li>SpaceAuditor: 이 역할은 영역에 대한 설정 및 로그, 보고서를 볼 수 있습니다. </li>
</ul>
</dd>
</dl>

<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직에 `OrgManager` 역할로 초대하고 `Cloud` 영역에 `SpaceAuditor` 역할로 초대합니다.

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

사용자에게 초대를 다시 보냅니다(조직 관리자 또는 계정 소유자 필요).

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

모든 Bluemix 플랫폼 API 키 나열

```
bluemix iam api-keys
```

<strong>전제조건</strong>: 엔드포인트, 로그인

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

새 Bluemix 플랫폼 API 키 작성

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
<dt>NAME(필수)</dt>
<dd>작성할 API 키의 이름입니다.</dd>
<dt>-d <i>DESCRIPTION</i>(선택사항)</dt>
<dd>API 키에 대한 설명</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>지정된 파일에 API 키 정보를 저장합니다. 설정하지 않으면 JSON 컨텐츠가 표시됩니다.</dd>
</dl>

<strong>예제</strong>:

API 키 작성 및 파일에 저장

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

Bluemix 플랫폼 API 키 업데이트

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
<dt>NAME(필수)</dt>
<dd>업데이트할 API 키의 이전 이름.</dd>
<dt>-n <i>NAME</i>(선택사항)</dt>
<dd>API 키의 새 이름</dd>
<dt>-d <i>DESCRIPTION</i>(선택사항)</dt>
<dd>API 키의 새 설명</dd>
</dl>

<strong>예제</strong>:

API 키의 설명 업데이트:

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

Bluemix 플랫폼 API 키 삭제

```
bluemix iam api-key-delete NAME [-f]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
<dt>NAME(필수)</dt>
<dd>삭제할 API 키의 이름입니다.</dd>
<dt>-f(선택사항)</dt>
<dd>확인 없이 강제 삭제합니다. </dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

이 명령은 `cf push` 명령과 기능 및 옵션이 동일합니다.


## bluemix app list
{: #bluemix_app_list}

이 명령은 `cf apps` 명령과 기능 및 옵션이 동일합니다.


## bluemix app show
{: #bluemix_app_show}

이 명령은 `cf app` 명령과 기능 및 옵션이 동일합니다.


## bluemix app delete
{: #bluemix_app_delete}

이 명령은 `cf delete` 명령과 기능 및 옵션이 동일합니다.


## bluemix app rename
{: #bluemix_app_rename}

이 명령은 `cf rename` 명령과 기능 및 옵션이 동일합니다.


## bluemix app start
{: #bluemix_app_start}

이 명령은 `cf start` 명령과 기능 및 옵션이 동일합니다.


## bluemix app stop
{: #bluemix_app_stop}

이 명령은 `cf stop` 명령과 기능 및 옵션이 동일합니다.


## bluemix app restart
{: #bluemix_app_restart}

이 명령은 `cf restart` 명령과 기능 및 옵션이 동일합니다.


## bluemix app restage
{: #bluemix_app_restage}


이 명령은 `cf restage` 명령과 기능 및 옵션이 동일합니다.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


이 명령은 `cf restart-app-instance` 명령과 기능 및 옵션이 동일합니다.


## bluemix app events
{: #bluemix_app_events}

이 명령은 `cf events` 명령과 기능 및 옵션이 동일합니다.


## bluemix app files
{: #bluemix_app_files}

이 명령은 `cf files` 명령과 기능 및 옵션이 동일합니다.


## bluemix app logs
{: #bluemix_app_logs}

이 명령은 `cf logs` 명령과 기능 및 옵션이 동일합니다.


## bluemix app env
{: #bluemix_app_env}

이 명령은 `cf env` 명령과 기능 및 옵션이 동일합니다.


## bluemix app env-set
{: #bluemix_app_env_set}

이 명령은 `cf set-env` 명령과 기능 및 옵션이 동일합니다.


## bluemix app env-unset
{: #bluemix_app_env_unset}

이 명령은 `cf unset-env` 명령과 기능 및 옵션이 동일합니다.


## bluemix app stacks
{: #bluemix_app_stacks}

이 명령은 `cf stacks` 명령과 기능 및 옵션이 동일합니다.


## bluemix app stack-show
{: #bluemix_app_stack_show}

이 명령은 `cf stack` 명령과 기능 및 옵션이 동일합니다.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

이 명령은 `cf create-app-manifest` 명령과 기능 및 옵션이 동일합니다.

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

도메인의 인증서 정보를 나열합니다.

```
bluemix app domain-cert DOMAIN_NAME
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
<dl>
<dt>DOMAIN_NAME(필수)</dt>
<dd>인증서를 호스팅하는 도메인입니다. </dd>
</dl>


<strong>예제</strong>:

`ibmcxo-eventconnect.com` 도메인의 인증서 정보를 봅니다.

```
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

현재 조직의 지정된 도메인에 인증서를 추가합니다.

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:
   <dl>
   <dt>DOMAIN(필수)</dt>
   <dd>인증서가 추가되는 도메인입니다. </dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i>(필수)</dt>
   <dd>개인 키 파일 경로입니다. </dd>
   <dt>-c <i>CERT_FILE</i>(필수)</dt>
   <dd>인증서 파일 경로입니다. </dd>
   <dt>-p <i>PASSWORD</i>(선택사항)</dt>
   <dd>인증서의 비밀번호입니다. </dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i>(선택사항)</dt>
   <dd>중간 인증서 파일 경로입니다. </dd>
   <dt>-t <i>TRUST_STORE_FILE</i>(선택사항)</dt>
   <dd>신뢰 저장소 파일입니다.</dd>
   </dl>


<strong>예제</strong>:

인증서를 도메인 `ibmcxo-eventconnect.com`에 추가합니다.

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

현재 조직의 지정된 도메인에서 인증서를 제거합니다.

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>DOMAIN(필수)</dt>
   <dd>인증서가 제거되는 도메인입니다. </dd>
   <dt>-f(선택사항)</dt>
   <dd>확인 없이 강제 삭제합니다. </dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

이 명령은 `cf domains` 명령과 기능 및 옵션이 동일합니다.


## bluemix app domain-create
{: #bluemix_app_domain_create}

이 명령은 `cf create-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

이 명령은 `cf delete-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

이 명령은 `cf create-shared-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

이 명령은 `cf delete-shared-domain` 명령과 기능 및 옵션이 동일합니다.

## bluemix app routes
{: #bluemix_app_routes}

이 명령은 `cf routes` 명령과 기능 및 옵션이 동일합니다.


## bluemix app route-check
{: #bluemix_app_route_check}

이 명령은 `cf check-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix app route-map
{: #bluemix_app_route_map}

지정된 도메인과 호스트 이름이 있는 기존의 cf 애플리케이션 또는 컨테이너 그룹에 라우트를 맵핑합니다.

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME(필수)</dt>
   <dd>라우트로 맵핑되는 cf 애플리케이션 또는 컨테이너 그룹의 이름입니다. </dd>
   <dt>DOMAIN(필수)</dt>
   <dd>라우트의 도메인입니다. 예: mychinabluemix.net 또는 chinabluemix.net. </dd>
   <dt>-n <i>HOST_NAME</i>(선택사항)</dt>
   <dd>라우트의 호스트 이름입니다. 값을 제공하지 않으면 호스트 이름이 기본적으로 앱 이름 또는 컨테이너 그룹 이름으로 설정됩니다.</dd>
   </dl>

<strong>예제</strong>:

라우트를 지정된 도메인이 있는 `my-app`으로 맵핑합니다.

```
bluemix app route-map my-app mychinabluemix.net
```

라우트를 지정된 도메인과 호스트 이름이 있는 'my-container-group'으로 맵핑합니다.

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

기존의 cf 애플리케이션이나 컨테이너 그룹과 지정된 라우트의 맵핑을 해제합니다.

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME(필수)</dt>
   <dd>cf 애플리케이션 또는 컨테이너 그룹의 이름입니다. </dd>
   <dt>DOMAIN(필수)</dt>
   <dd>라우트의 도메인입니다(예: mychinabluemix.net 또는 chinabluemix.net).</dd>
   <dt>-n <i>HOST_NAME</i>(선택사항)</dt>
   <dd>라우트의 호스트 이름입니다. 값을 제공하지 않으면 호스트 이름이 기본적으로 앱 이름 또는 컨테이너 그룹 이름으로 설정됩니다.</dd>
   </dl>

<strong>예제</strong>:

`my-app`에서 `my-app.mychinabluemix.net`을 맵핑 해제합니다.

```
bluemix app route-unmap my-app mychianbluemix.net
```

`my-container-group`에서 `abc.chinabluexmix.net`을 맵핑 해제합니다.

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

이 명령은 `cf create-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix app route-delete
{: #bluemix_app_route_delete}

이 명령은 `cf delete-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

이 명령은 `cf delete-orphaned-routes` 명령과 기능 및 옵션이 동일합니다.


## bluemix app domains
{: #bluemix_app_domains}

이 명령은 `cf domains` 명령과 기능 및 옵션이 동일합니다.


## bluemix app domain-create
{: #bluemix_app_domain_create}

이 명령은 `cf create-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

이 명령은 `cf delete-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

이 명령은 `cf create-shared-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

이 명령은 `cf delete-shared-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix service offerings
{: #bluemix_service_offerings}


이 명령은 `cf marketplace` 명령과 기능 및 옵션이 동일합니다.


## bluemix service list
{: #bluemix_service_list}

이 명령은 `cf services` 명령과 기능 및 옵션이 동일합니다.


## bluemix service show
{: #bluemix_service_show}

이 명령은 `cf service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service create
{: #bluemix_service_create}

이 명령은 `cf create-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service update
{: #bluemix_service_update}

이 명령은 `cf update-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service delete
{: #bluemix_service_delete}

이 명령은 `cf delete-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service rename
{: #bluemix_service_rename}

이 명령은 `cf rename-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service bind
{: #bluemix_service_bind}

이 명령은 `cf bind-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service unbind
{: #bluemix_service_unbind}

이 명령은 `cf unbind-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service key-create
{: #bluemix_service_key_create}

이 명령은 `cf create-service-key` 명령과 기능 및 옵션이 동일합니다.


## bluemix service key-delete
{: #bluemix_service_key_delete}

이 명령은 `cf delete-service-key` 명령과 기능 및 옵션이 동일합니다.


## bluemix service keys
{: #bluemix_service_keys}

이 명령은 `cf service-keys` 명령과 기능 및 옵션이 동일합니다.


## bluemix service key-show
{: #bluemix_service_key_show}

이 명령은 `cf service-key` 명령과 기능 및 옵션이 동일합니다.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

이 명령은 `cf create-user-provided-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

이 명령은 `cf update-user-provided-service` 명령과 기능 및 옵션이 동일합니다.


## bluemix catalog templates
{: #bluemix_catalog_templates}

Bluemix에서 표준 유형 템플리트를 확인합니다.

```
bluemix catalog templates [-d]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:

   <dl>
   <dt>-d(선택사항)</dt>
   <dd><i>-d</i> 옵션을 지정하면 각 템플리트의 설명도 표시됩니다. 그렇지 않으면 각 템플리트의 ID와 이름만 표시됩니다.</dd>
   </dl>


## bluemix catalog template
{: #bluemix_catalog_template}

지정된 표준 유형 템플리트의 자세한 정보를 봅니다.

```
bluemix catalog template TEMPLATE_ID
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>TEMPLATE_ID(필수)</dt>
   <dd>표준 유형 템플리트의 ID입니다. <i>bluemix 템플리트</i>를 사용하여 모든 템플리트의 ID를 볼 수 있습니다. </dd>
   </dl>


<strong>예제</strong>:

`mobileBackendStarter` 템플리트의 세부사항을 봅니다.

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

특정 URL 및 설명이 있는 지정된 템플리트를 기반으로 하는 cf 애플리케이션을 작성합니다. 기본적으로 새 앱이 자동으로 시작됩니다. 

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:
   <dl>
   <dt>TEMPLATE_ID(필수)</dt>
   <dd>애플리케이션을 작성할 때 이의 기반이 되는 템플리트입니다. 모든 템플리트의 ID를 보려면 <i>bluemix templates</i>를 사용하십시오.</dd>
   <dt>CF_APP_NAME(필수)</dt>
   <dd>작성되는 cf 애플리케이션의 이름입니다. </dd>
   <dt>-u <i>URL</i>(선택사항)</dt>
   <dd>애플리케이션의 라우트입니다. 지정하지 않으면, 앱 이름과 기본 도메인에 따라 Bluemix가 자동으로 라우트를 설정합니다. </dd>
   <dt>-d <i>DESCRIPTION</i>(선택사항)</dt>
   <dd>애플리케이션에 대한 설명입니다. </dd>
   <dt>--no-start(선택사항)</dt>
   <dd>애플리케이션을 작성한 후에 이를 자동으로 시작하지 않습니다. 값을 지정하지 않으면 애플리케이션이 작성 후 자동으로 시작됩니다. </dd>
   </dl>


<strong>예제</strong>:

`javaHelloWorld` 템플리트를 기반으로 cf 애플리케이션 `my-app`을 작성합니다.

```
bluemix catalog template-run javaHelloWorld my-app
```

라우트가 `myrubyapp.chinabluemix.net`이고 설명이 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`인 `rubyHelloWorld` 템플리트를 기반으로 `my-ruby-app` 애플리케이션을 작성합니다.

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

자동 시작 없이 `pythonHelloWorld` 템플리트를 기반으로 `my-python-app` 애플리케이션을 작성합니다.

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

계정의 월별 사용량 및 비용을 표시하십시오.

```
bluemix billing account-usage [-d YYYY-MM] [--json]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:

<dl>
  <dt>-d MONTH_DATE(선택사항)</dt>
  <dd>YYYY-MM 형식을 사용하여 월 및 날짜 지정에 대한 데이터를 표시하십시오. 지정되지 않으면 현재 월의 사용량이 표시됩니다.</dd>
  <dt>--json(선택사항)</dt>
  <dd>JSON 형식으로 사용량 결과를 표시하십시오.</dd>
</dl>

<strong>예제</strong>:

2016-06의 내 계정 사용량 및 비용 보고서 표시:

```
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

조직의 월별 사용량 세부사항을 표시하십시오. 이 오퍼레이션은 조직의 청구 관리자만 완료할 수 있습니다.

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:

<dl>
  <dt>ORG_NAME(필수)</dt>
  <dd>조직의 이름입니다.</dd>
  <dt>-d MONTH_DATE(선택사항)</dt>
  <dd>YYYY-MM 형식을 사용하여 지정된 월 및 날짜에 대한 데이터를 표시하십시오. 지정되지 않으면 현재 월의 사용량이 표시됩니다.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>조직을 호스트하는 지역의 이름입니다. 'all'로 설정되면 모든 지역의 조직 사용량이 표시됩니다.</dd>
  <dt>--json(선택사항)</dt>
  <dd>JSON 형식으로 사용량 결과를 표시하십시오.</dd>
</dl>



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

내 계정에서 조직에 대한 월별 사용량 요약을 표시하십시오.

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:

<dl>
  <dt>-d MONTH_DATE(선택사항)</dt>
  <dd>YYYY-MM 형식을 사용하여 지정된 월 및 날짜에 대한 데이터를 표시하십시오. 지정되지 않으면 현재 월의 사용량이 표시됩니다.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>조직을 호스트하는 지역의 이름입니다. 'all'로 설정되면 모든 지역에 있는 조직의 사용량 요약이 표시됩니다.</dd>
  <dt>--json(선택사항)</dt>
  <dd>JSON 형식으로 사용량 결과를 표시하십시오.</dd>
</dl>


## bluemix plugin repos
{: #bluemix_plugin_repos}

{{site.data.keyword.Bluemix_notm}} CLI에 등록된 모든 플러그인 저장소를 나열합니다.

```
bluemix plugin repos
```

<strong>전제조건</strong>: 없음


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

새 플러그인 저장소를 {{site.data.keyword.Bluemix_notm}} CLI에 추가합니다.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>REPO_NAME(필수)</dt>
   <dd>추가되는 저장소의 이름입니다. 각 저장소의 고유 이름을 정의할 수 있습니다.</dd>
   <dt>REPO_URL(필수)</dt>
   <dd>추가되는 저장소의 URL입니다. 저장소 URL에는 프로토콜이 포함되어 있어야 합니다(예: plugins.ng.bluemix.net이 아닌 http://plugins.ng.bluemix.net). http://plugins.ng.bluemix.net 이것이 Bluemix CLI의 공식 플러그인 저장소입니다. </dd>
    </dl>


<strong>예제</strong>:

Bluemix CLI의 공식 플러그인 저장소를 `bluemix-repo`로 추가합니다.

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

{{site.data.keyword.Bluemix_notm}} CLI에서 플러그인 저장소를 제거합니다.

```
bluemix plugin repo-remove REPO_NAME
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:
   <dl>
   <dt>REPO_NAME(필수)</dt>
   <dd>제거되는 저장소의 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

{{site.data.keyword.Bluemix_notm}} CLI에서 `bluemix-repo` 저장소를 제거합니다.

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

모든 추가된 저장소 또는 특정 저장소에서 사용 가능한 모든 플러그인을 나열합니다.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i>(선택사항)</dt>
   <dd>지정된 저장소의 플러그인만 나열합니다. </dd>
   </dl>

<strong>예제</strong>:

모든 추가된 저장소의 플러그인을 나열합니다.

```
bluemix plugin repo-plugins
```

`bluemix-repo` 저장소의 모든 플러그인을 나열합니다.

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

{{site.data.keyword.Bluemix_notm}} CLI에 설치된 모든 플러그인을 나열합니다.

```
bluemix plugin list
```

<strong>전제조건</strong>: 없음


## bluemix plugin install
{: #bluemix_plugin_install}

지정된 경로 또는 저장소에서 {{site.data.keyword.Bluemix_notm}} CLI에 특정 버전의 플러그인을 설치합니다.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME(필수)</dt>
   <dd>-r <i>REPO_NAME</i>을 지정하지 않으면 지정된 로컬 경로 또는 원격 URL에서 플러그인이 설치됩니다. </dd>
   <dt>-r <i>REPO_NAME</i>(선택사항)</dt>
   <dd>플러그인 바이너리가 있는 저장소의 이름입니다. </dd>
   <dt>-v <i>VERSION</i>(선택사항)</dt>
   <dd>설치되는 플러그인의 버전입니다. 값을 지정하지 않으면 최신 버전의 플러그인이 설치됩니다. 이 옵션은 저장소에서 플러그인을 설치하는 경우에만 유효합니다.</dd>
    </dl>

<strong>예제</strong>:

로컬 파일에서 플러그인을 설치합니다.

```
bluemix plugin install /downloads/new_plugin
```

원격 URL에서 플러그인을 설치합니다.

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

`bluemix-repo` 저장소에서 최신 버전의 `IBM-Containers` 플러그인을 설치합니다.

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
`bluemix-repo` 저장소에서 버전 `0.5.800`인 `IBM-Containers` 플러그인을 설치합니다.

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```

## bluemix plugin update
{: #bluemix_plugin_update}

저장소에서 플러그인 업그레이드

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:
<dl>
 <dt>-r REPO_NAME(필수)</dt>
 <dd>플러그인 바이너리가 있는 저장소의 이름입니다. </dd>
 <dt><i>PLUGIN_NAME</i>(선택사항)</dt>
 <dd>지정하지 않으면 지정된 저장소에서 업데이트에 사용 가능한 모든 플러그인이 선택을 위해 나열됩니다.</dd>
 <dt>-v <i>VERSION</i>(선택사항)</dt>
 <dd>업데이트할 플러그인의 버전입니다. 제공하지 않은 경우, 최신 사용 가능 버전으로 플러그인을 업데이트하십시오.</dd>
</dl>

<strong>예제</strong>:

플러그인 저장소 "My-Repo"에서 사용 가능한 모든 업그레이드 확인:

```
bluemix plugin update -r My-Repo
```

저장소 "My-Repo"의 플러그인 "plugin-echo"를 최신 상태로 업그레이드:

```
bluemix plugin update -r My-Repo plugin-echo
```

저장소 "My-Repo"의 플러그인 "plugin-echo"를 버전 "1.0.1"로 업데이트:

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

{{site.data.keyword.Bluemix_notm}} CLI에서 지정된 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:

   <dl>
   <dt>PLUGIN_NAME(필수)</dt>
   <dd>설치 제거되는 플러그인의 이름입니다. </dd>
    </dl>

<strong>예제</strong>:

이전에 설치한 `IBM-Containers` 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall IBM-Containers
```
