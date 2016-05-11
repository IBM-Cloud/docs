---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}}(bx) 명령
{: #bluemix_cli}

*마지막 업데이트 날짜: 2016년 4월 15일*

{{site.data.keyword.Bluemix_notm}} 명령행 인터페이스(CLI)는 사용자가 {{site.data.keyword.Bluemix_notm}}와 상호작용할 수 있도록 네임스페이스별로 그룹화된 명령 세트를 제공합니다. 일부 {{site.data.keyword.Bluemix_notm}} 명령은 기존 cf 명령의 랩퍼이며 나머지 일부는 {{site.data.keyword.Bluemix_notm}} 사용자에게 확장 기능을 제공합니다. 뒤이어 나오는 정보는 {{site.data.keyword.Bluemix_notm}} CLI에서 지원되는 모든 명령과 각 명령의 이름, 옵션, 사용법, 전제조건, 설명, 예제 등을 제공합니다. 옵션, 사용법, 전제조건, 설명과 예를 포함하는 모든 명령을 나열합니다.
{:shortdesc}
 
**참고:** *전제조건*에는 명령을 사용하기 전에 필요한 조치가 설명되어 있습니다. 전제조건 조치가 없는 명령은 **없음**으로 표시됩니다. 그 밖의 경우에는 전제조건으로 다음과 같은 조치 중 하나 이상을 수행해야 할 수 있습니다.
<dl>
<dt>엔드포인트</dt>
<dd>명령을 사용하기 전에 <code>bluemix api</code>를 통해 API 엔드포인트를 설정해야 합니다.</dd>
<dt>로그인</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix login</code> 명령을 사용하여 로그인해야 합니다.</dd>
<dt>대상</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix target</code> 명령을 사용하여 조직과 영역을 설정해야 합니다.</dd>
<dt>Docker</dt>
<dd>이 명령을 실행하려면 Docker CLI(docker)가 설치되어 있어야 합니다.</dd>
</dl>

다음 {{site.data.keyword.Bluemix_notm}} 명령을 사용할 수 있습니다.

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix 로그인](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
첫 번째 레벨 기본 제공 명령 및 지원되는 {{site.data.keyword.Bluemix_notm}} CLI 네임스페이스에 대한 일반 도움말 또는 특정 기본 제공 명령 또는 네임스페이스의 도움말을 표시합니다. 

```
bluemix help [COMMAND|NAMESPACE]
```

**전제조건**: 없음

**명령 옵션**:

*COMMAND*|*NAMESPACE* (선택사항): 도움말이 표시되는 명령 또는 네임스페이스입니다. 값을 지정하지 않으면 {{site.data.keyword.Bluemix_notm}} CLI의 일반 도움말이 표시됩니다.

**예제**:

{{site.data.keyword.Bluemix_notm}} CLI의 일반 도움말을 표시합니다.

```
bluemix help
```

`info` 명령의 도움말을 표시합니다.

```
bluemix help info
```

`ic` 네임스페이스의 도움말을 표시합니다.

```
bluemix help ic
```

또는 

```
bluemix ic help
```

`ic` 네임스페이스 아래에 있는 `group-create` 명령의 도움말을 표시합니다. 

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}} API 엔드포인트를 설정하거나 확인합니다. 이 명령은 `cf api` 명령을 랩핑 처리합니다. 

```
bluemix api [API_ENDPOINT][--unset]
```

**전제조건**: 없음

**명령 옵션**:

*API_ENDPOINT* (선택사항): 대상으로 하는 API 엔드포인트입니다(예: https://api.ng.bluemix.net). *API_ENDPOINT* 및 `--unset` 옵션 중 하나를 지정하지 않으면 현재 API 엔드포인트가 표시됩니다. 

`--unset` (선택사항): API 엔드포인트 설정을 제거합니다.

**예제**:

API 엔드포인트를 api.ng.bluemix.net으로 설정합니다.

```
bluemix api api.ng.bluemix.net
```

현재 API 엔드포인트를 확인합니다.

```
bluemix api
```

API 엔드포인트를 설정 해제합니다.

```
bluemix api --unset
```


## bluemix 로그인
{: #bluemix_login}

사용자가 로그인됩니다. 이 명령은 `cf login` 명령을 랩핑 처리합니다. 명령 옵션이 `cf login` 명령 옵션과 동일합니다. 

```
bluemix login [OPTIONS...]
```

**전제조건**: 엔드포인트

**명령 옵션**:
`login` 명령에 지원되는 옵션에 대한 자세한 정보는 `cf login` 명령 사용법 정보에서 애플리케이션 관리를 위한 cf 명령을 참조하십시오.


## bluemix logout
{: #bluemix_logout}

사용자가 로그아웃됩니다. 이 명령은 `cf logout` 명령을 랩핑 처리합니다. 

```
bluemix logout
```

**전제조건**: 없음


## bluemix target
{: #bluemix_target}


대상 조직 또는 영역을 설정하거나 확인합니다. 이 명령은 `cf target` 명령을 랩핑 처리합니다. 

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

-o *ORG_NAME* (선택사항): 대상으로 지정할 조직의 이름입니다.

-s *SPACE_NAME* (선택사항): 대상으로 지정할 영역의 이름입니다.

-o *ORG_NAME*과 -s *SPACE_NAME*을 둘 다 지정하지 않으면 현재 조직 및 영역이 표시됩니다.

**예제**:

현재 조직을 `MyOrg`로, 영역을 `MySpace`로 설정합니다.

```
bluemix target -o MyOrg -s MySpace
```

현재 조직과 영역을 확인합니다.

```
bluemix target
```


## bluemix info
{: #bluemix_info}

현재 지역, 클라우드 제어기 버전, 로그인과 교환 액세스 토큰의 엔드포인트 같은 유용한 엔드포인트 등 기본 {{site.data.keyword.Bluemix_notm}} 정보를 확인합니다.

```
bluemix info
```

**전제조건**:  엔드포인트


## bluemix config
{: #bluemix_config}


구성 파일에 기본값을 작성합니다.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**전제조건**: 없음

**명령 옵션**:

--http-timeout *TIMEOUT_IN_SECONDS*:  HTTP 요청의 제한시간 값입니다. 기본값은 60초입니다.

--trace true|false|*path/to/file*:  터미널 또는 지정된 파일에 대한 HTTP 요청을 추적합니다. 

--color true|false:  색상 출력의 사용 여부를 설정합니다. 색상 출력은 기본적으로 사용됩니다. 

--locale *LOCALE*:  기본 로케일을 설정합니다. LOCALE이 *CLEAR*이면 이전 로케일이 삭제됩니다.

이들 옵션 중에서 한 번에 하나만 지정할 수 있습니다. 

**예제**:

HTTP 요청 제한시간을 30초로 설정합니다.

```
bluemix config --http-timeout 30
```

HTTP 요청에 대한 추적 출력을 사용하도록 설정합니다.

```
bluemix config --trace true
```

지정된 파일 */home/usera/my_trace*에 대한 HTTP 요청을 추적합니다.

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


## bluemix list
{: #bluemix_list}

현재 영역의 모든 cf 애플리케이션, 컨테이너, 컨테이너 그룹 및 VM 그룹을 나열합니다.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

apps  (선택사항):  애플리케이션 정보만 표시합니다.

containers  (선택사항):  컨테이너 정보만 표시합니다.

container-groups  (선택사항):  컨테이너 그룹 정보만 표시합니다.

vm-groups  (선택사항):  VM 그룹 정보만 표시합니다.

`apps`, `containers`, `container-groups` 또는 `vm-groups` 중에서 한 번에 하나만 지정할 수 있습니다. 지정한 항목이 없으면 cf 앱, 컨테이너, 컨테이너 그룹 및 VM 그룹이 모두 나열됩니다.

**예제**:

모든 cf 애플리케이션을 나열합니다.

```
bluemix list apps
```

모든 컨테이너 인스턴스를 나열합니다.

```
bluemix list containers
```

앱, 컨테이너, 컨테이너 그룹 및 VM 그룹을 모두 나열합니다.

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

cf 애플리케이션 또는 컨테이너 그룹을 지정된 인스턴스 개수, 디스크 할당량 및 메모리 크기로 스케일 축소하거나 스케일 확장합니다.

**참고:** 컨테이너 그룹을 스케일링하는 경우 인스턴스 번호만 지정할 수 있습니다. 옵션을 지정하지 않은 경우, 이 명령은 컨테이너 그룹의 현재 인스턴스 수와 cf 애플리케이션의 디스크 할당량 및 메모리 크기도 나열합니다. 

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (필수):  스케일링할 cf 애플리케이션 또는 컨테이너 그룹의 이름입니다.

-i *INSTANCE_COUNT*  (선택사항):  스케일링할 cf 애플리케이션 또는 컨테이너 그룹의 새 인스턴스 번호입니다. 이 옵션은 스케일링할 컨테이너 그룹에만 유효한 옵션입니다.

-k *DISK_QUOTA* (선택사항):  cf 애플리케이션의 새 디스크 할당량입니다. 컨테이너 그룹을 스케일링하는 데는 유효하지 않습니다.

-m *MEMORY_SIZE* (선택사항):  cf 애플리케이션의 새 메모리 크기입니다. 컨테이너 그룹을 스케일링하는 데는 유효하지 않습니다.

**예제**:

`my-container-group`의 현재 인스턴스 번호를 표시합니다.

```
bluemix scale my-container-group
```

`my-container-group`을 2개 인스턴스로 스케일링합니다.

```
bluemix scale my-container-group -i 2
```

`my-java-app`을 3개 인스턴스, 8G 디스크 할당량 및 1024M 메모리 크기로 스케일링합니다.

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

원시 HTTP 요청을 {{site.data.keyword.Bluemix_notm}}에 실행합니다. *Content-Type*은 기본적으로 *application/json*으로 설정됩니다. 이 명령은 {{site.data.keyword.Bluemix_notm}} 다중 클라우드 제어 프록시에 요청을 전송합니다. 지원되는 경로는 [CloudFoundry API 문서](http://apidocs.cloudfoundry.org/){: new_window}의 API 경로 정의를 참조하십시오.

```
bluemix curl PATH [OPTIONS...]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*PATH*  (필수): 자원의 URL 경로입니다. 예: /v2/apps.

*OPTIONS*  (선택사항): `bluemix curl` 명령에 지원되는 옵션은 `cf curl` 명령에 지원되는 옵션과 동일합니다.

**예제**:

현재 계정의 모든 조직에 대한 정보를 봅니다.

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

모든 조직 나열

```
bluemix iam orgs [-r REGION --guid]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*-r REGION*  (선택사항): 조직 정보가 표시되는 대상 지역입니다. 'all'로 설정되면 모든 지역의 모든 조직이 나열됩니다.

*--guid* (선택사항): 조직의 GUID를 표시합니다.

**예제**:
GUID를 표시하여 `us-south` 지역의 모든 조직을 나열합니다. 

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

지정된 조직의 정보를 표시합니다.

```
bluemix iam org ORG_NAME [--guid]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME* (필수): 조직의 이름입니다.

*--guid* (선택사항): 조직의 GUID를 표시합니다.


**예제**:
GUID를 표시하여 `IBM` 조직의 정보를 표시합니다.

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

새 조직을 작성합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam org-create ORG_NAME
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME*(필수): 작성 중인 조직의 이름입니다.

**예제**:
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

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME* (필수):  복제할 기존 조직의 이름입니다.

*REGION_NAME*  (필수):  복제된 조직을 호스팅하는 지역의 이름입니다.

**예제**:

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

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*OLD_ORG_NAME* (필수): 이름이 변경될 조직의 이전 이름입니다.

*NEW_ORG_NAME* (필수): 이름이 변경될 대상 조직의 새 이름입니다.


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

현재 지역에서 지정된 조직을 삭제합니다.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME* (필수): 삭제되는 기존 조직의 이름입니다.

*-f* (선택사항): 확인하지 않고 삭제를 강제 실행합니다.

*--all* (선택사항): 모든 지역의 조직을 삭제합니다.


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


## bluemix iam account-users
{: #bluemix_iam_account_users}

계정과 연관된 사용자를 표시합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


조직 및 영역 역할이 이미 설정된 계정으로 사용자를 초대합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**전제조건**: 엔드포인트, 로그인


**명령 옵션**:

*USER_NAME* (필수): 초대되는 사용자의 이름입니다.

*ORG_NAME* (필수): 이 사용자가 초대되는 조직의 이름입니다.

*ORG_ROLE* (필수): 이 사용자가 초대되는 조직 역할의 이름입니다. 예를 들어, 다음과 같습니다. 

<dl>
<dt>OrgManager</dt>
<dd>이 역할은 사용자를 초대 및 관리하고, 플랜을 선택 및 변경하며, 지출 한계를 설정할 수 있습니다.</dd>
<dt>BillingManager</dt>
<dd>이 역할은 청구 계정 및 지불 정보를 작성하고 관리할 수 있습니다.</dd>
<dt>OrgAuditor</dt>
<dd>이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다.</dd>
</dl> 

*SPACE_NAME* (필수): 이 사용자가 초대되는 영역의 이름입니다.

*SPACE_ROLE* (필수): 이 사용자가 초대되는 영역 역할의 이름입니다. 예를 들어, 다음과 같습니다. 

<dl>
<dt>SpaceManager</dt>
<dd>이 역할은 사용자를 초대 및 관리하고 제공된 영역에 대한 기능을 사용할 수 있습니다.</dd>
<dt>SpaceDeveloper</dt>
<dd>이 역할은 앱 및 서비스를 작성하고 관리하며 로그 및 보고서를 볼 수 있습니다.</dd>
<dt>SpaceAuditor</dt>
<dd>이 역할은 영역에 대한 설정 및 로그, 보고서를 볼 수 있습니다.</dd>
</dl> 

**예제**:

사용자 `Mary`를 `IBM` 조직에 `OrgManager` 역할로 초대하고 `Cloud` 영역에 `SpaceAuditor` 역할로 초대합니다.

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

역할별로 지정된 조직의 사용자를 표시합니다.

```
bluemix iam org-users ORG_NAME [-a]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME* (필수): 조직의 이름입니다.

*-a* (선택사항): 지정된 조직의 모든 사용자를 나열하지만, 역할별로 그룹화하지는 않습니다.


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

사용자에게 조직 역할을 지정합니다. 이 조작은 조직 관리자만 수행할 수 있습니다.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*USER_NAME* (필수): 지정되는 사용자의 이름입니다.

*ORG_NAME* (필수): 이 사용자가 지정되는 조직의 이름입니다.

*ORG_ROLE* (필수): 이 사용자가 지정되는 조직 역할의 이름입니다. 예를 들어, 다음과 같습니다. 

<dl>
<dt>OrgManager</dt>
<dd>이 역할은 사용자를 초대 및 관리하고, 플랜을 선택 및 변경하며, 지출 한계를 설정할 수 있습니다.</dd>
<dt>BillingManager</dt>
<dd>이 역할은 청구 계정 및 지불 정보를 작성하고 관리할 수 있습니다.</dd>
<dt>OrgAuditor</dt>
<dd>이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다.</dd>
</dl> 

**예제**:

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

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*USER_NAME* (필수): 제거되는 사용자의 이름입니다.

*ORG_NAME* (필수): 이 사용자가 제거되는 조직의 이름입니다.

*ORG_ROLE* (필수): 이 사용자가 제거되는 조직 역할의 이름입니다. 예를 들어, 다음과 같습니다. 

<dl>
<dt>OrgManager</dt>
<dd>이 역할은 사용자를 초대 및 관리하고, 플랜을 선택 및 변경하며, 지출 한계를 설정할 수 있습니다.</dd>
<dt>BillingManager</dt>
<dd>이 역할은 청구 계정 및 지불 정보를 작성하고 관리할 수 있습니다.</dd>
<dt>OrgAuditor</dt>
<dd>이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다.</dd>
</dl> 

**예제**:

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

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME* (필수): 조직의 이름입니다.

*SPACE_NAME* (필수): 영역의 이름입니다.


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

사용자에게 영역 역할을 지정합니다. 이 조작은 영역 관리자만 수행할 수 있습니다.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*USER_NAME* (필수): 지정되는 사용자의 이름입니다.

*ORG_NAME* (필수): 이 사용자가 지정되는 조직의 이름입니다.

*SPACE_NAME* (필수): 이 사용자가 지정되는 영역의 이름입니다.

*SPACE_ROLE* (필수): 이 사용자가 지정되는 영역 역할의 이름입니다. 예를 들어, 다음과 같습니다. 

<dl>
<dt>SpaceManager</dt>
<dd>이 역할은 사용자를 초대 및 관리하고 제공된 영역에 대한 기능을 사용할 수 있습니다.</dd>
<dt>SpaceDeveloper</dt>
<dd>이 역할은 앱 및 서비스를 작성하고 관리하며 로그 및 보고서를 볼 수 있습니다.</dd>
<dt>SpaceAuditor</dt>
<dd>이 역할은 영역에 대한 설정 및 로그, 보고서를 볼 수 있습니다.</dd>
</dl> 


**예제**:

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

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*USER_NAME* (필수): 제거되는 사용자의 이름입니다.

*ORG_NAME* (필수): 이 사용자가 제거되는 조직의 이름입니다.

*SPACE_NAME* (필수): 이 사용자가 제거되는 영역의 이름입니다.

*SPACE_ROLE* (필수): 이 사용자가 제거되는 영역 역할의 이름입니다. 예를 들어, 다음과 같습니다. 

<dl>
<dt>SpaceManager</dt>
<dd>이 역할은 사용자를 초대 및 관리하고 제공된 영역에 대한 기능을 사용할 수 있습니다.</dd>
<dt>SpaceDeveloper</dt>
<dd>이 역할은 앱 및 서비스를 작성하고 관리하며 로그 및 보고서를 볼 수 있습니다.</dd>
<dt>SpaceAuditor</dt>
<dd>이 역할은 영역에 대한 설정 및 로그, 보고서를 볼 수 있습니다.</dd>
</dl> 

**예제**:

사용자 `Mary`를 `IBM` 조직 및 `Cloud` 영역에서 `SpaceManager` 역할로 제거합니다.

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

이 명령은 `cf push` 명령과 기능 및 옵션이 동일합니다.


## bluemix app list
{: #bluemix_app_list}

이 명령은 `cf apps` 명령과 기능 및 옵션이 동일합니다.


## bluemix app show
{: #bluemix_app_show}

이 명령은 `cf app` 명령과 기능 및 옵션이 동일합니다.


## bluemix app scale
{: #bluemix_app_scale}

이 명령은 `cf scale` 명령과 기능 및 옵션이 동일합니다.


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


## bluemix app stack
{: #bluemix_app_stack}

이 명령은 `cf stack` 명령과 기능 및 옵션이 동일합니다.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

이 명령은 `cf create-app-manifest` 명령과 기능 및 옵션이 동일합니다.


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

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

-d (선택사항):  `-d` 옵션을 지정하는 경우, 각 템플리트의 설명도 표시됩니다. 그렇지 않으면 각 템플리트의 ID와 이름만 표시됩니다.


## bluemix catalog template
{: #bluemix_catalog_template}

지정된 표준 유형 템플리트의 자세한 정보를 봅니다.

```
bluemix catalog template TEMPLATE_ID
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*TEMPLATE_ID*  (필수): 표준 유형 템플리트의 ID입니다. 모든 템플리트의 ID를 보려면 'bluemix templates'를 사용하십시오.

**예제**:

`mobileBackendStarter` 템플리트의 세부사항을 봅니다.

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

특정 URL 및 설명이 있는 지정된 템플리트를 기반으로 하는 cf 애플리케이션을 작성합니다. 기본적으로 새 앱이 자동으로 시작됩니다. 

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*TEMPLATE_ID*  (필수):  애플리케이션을 작성할 때 기반이 되는 템플리트입니다. 모든 템플리트의 ID를 보려면 `bluemix templates`를 사용하십시오.

*CF_APP_NAME*  (필수):  작성하는 cf 애플리케이션의 이름입니다.

-u *URL*  (선택사항):  애플리케이션의 라우트입니다. 이 값을 지정하지 않으면 앱 이름과 기본 도메인에 따라 자동으로 {{site.data.keyword.Bluemix_notm}}에서 라우트가 설정됩니다.

-d *DESCRIPTION*  (선택사항):  애플리케이션의 설명입니다.

--no-start  (선택사항):  애플리케이션을 작성한 후 자동으로 시작하지 않습니다. 값을 지정하지 않으면 애플리케이션이 작성 후 자동으로 시작됩니다. 

**예제**:

`javaHelloWorld` 템플리트를 기반으로 cf 애플리케이션 `my-app`을 작성합니다.

```
bluemix catalog template-run javaHelloWorld my-app
```

`rubyHelloWorld` 템플리트를 기반으로 라우트가 `myrubyapp.ng.bluemix.net`이고 설명이 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`인 `my-ruby-app` 애플리케이션을 작성합니다.

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

자동 시작 없이 `pythonHelloWorld` 템플리트를 기반으로 `my-python-app` 애플리케이션을 작성합니다.

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

{{site.data.keyword.Bluemix_notm}}의 모든 지역에 대한 정보를 확인합니다.

```
bluemix network regions
```

**전제조건**:  엔드포인트


## bluemix network region-set
{: #bluemix_network_region_set}

지정된 지역으로 전환합니다. 이 명령은 새 지역의 동일한 조직 및 영역을 자동으로 대상으로 설정합니다(가능한 경우). 그렇지 않으면, 사용자가 이미 로그인한 상태인 경우에 한해 새 조직 및 영역을 선택하라는 메시지를 표시합니다. API 엔드포인트는 그에 맞게 변경됩니다.

```
bluemix network region-set REGION_NAME
```

**전제조건**:  엔드포인트

**명령 옵션**:

*REGION_NAME* (필수):  전환하려는 지역의 이름입니다. `bluemix network regions` 명령을 사용하면 모든 지역 이름을 볼 수 있습니다.

**예제**:

현재 지역을 `eu-gb`로 설정합니다.

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

이 명령은 `cf routes` 명령과 기능 및 옵션이 동일합니다.


## bluemix network route-check
{: #bluemix_network_route_check}

이 명령은 `cf check-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix network route-map
{: #bluemix_network_route_map}

지정된 도메인과 호스트 이름이 있는 기존의 cf 애플리케이션 또는 컨테이너 그룹에 라우트를 맵핑합니다.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (필수):  라우트와 맵핑하는 cf 애플리케이션 또는 컨테이너 그룹의 이름입니다.

*DOMAIN*  (필수):  라우트의 도메인입니다. 예: mybluemix.net 또는 ng.bluemix.net 

-n *HOST_NAME*  (선택사항):  라우트의 호스트 이름입니다. 값을 제공하지 않으면 호스트 이름이 기본적으로 앱 이름 또는 컨테이너 그룹 이름으로 설정됩니다.

**예제**:

라우트를 지정된 도메인이 있는 `my-app`으로 맵핑합니다.

```
bluemix network route-map my-app mybluemix.net
```

라우트를 지정된 도메인과 호스트 이름이 있는 'my-container-group'으로 맵핑합니다.

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

기존의 cf 애플리케이션이나 컨테이너 그룹과 지정된 라우트의 맵핑을 해제합니다.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (필수):  cf 애플리케이션 또는 컨테이너 그룹의 이름입니다.

*DOMAIN*  (필수):  라우트의 도메인입니다(예: mybluemix.net 또는 ng.bluemix.net). 

-n *HOST_NAME*  (선택사항):  라우트의 호스트 이름입니다. 값을 제공하지 않으면 호스트 이름이 기본적으로 앱 이름 또는 컨테이너 그룹 이름으로 설정됩니다.

**예제**:

`my-app`에서 `my-app.mybluemix.net`을 맵핑 해제합니다.

```
bluemix network route-unmap my-app mybluemix.net
```

`my-container-group`에서 `abc.ng.bluexmix.net`을 맵핑 해제합니다.

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

이 명령은 `cf create-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix network route-delete
{: #bluemix_network_route_delete}

이 명령은 `cf delete-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

이 명령은 `cf delete-orphaned-routes` 명령과 기능 및 옵션이 동일합니다.


## bluemix network domains
{: #bluemix_network_domains}

이 명령은 `cf domains` 명령과 기능 및 옵션이 동일합니다.


## bluemix network domain-create
{: #bluemix_network_domain_create}

이 명령은 `cf create-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

이 명령은 `cf delete-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

이 명령은 `cf create-shared-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

이 명령은 `cf delete-shared-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix security cert
{: #bluemix_security_cert}

도메인의 인증서 정보를 나열합니다.

```
bluemix security cert DOMAIN_NAME
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*DOMAIN_NAME* (필수): 인증서를 호스팅하는 도메인입니다.

**예제**:

`ibmcxo-eventconnect.com` 도메인의 인증서 정보를 봅니다.

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

현재 조직의 지정된 도메인에 인증서를 추가합니다.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*DOMAIN* (필수):  인증서가 추가되는 도메인입니다.

-k *PRIVATE_KEY_FILE* (필수):  개인 키 파일 경로입니다.

-c *CERT_FILE* (필수):  인증서 파일 경로입니다.

-p *PASSWORD* (선택사항):  인증서의 비밀번호입니다.

-i *INTERMEDIATE_CERT_FILE* (선택사항):  중간 인증서 파일 경로입니다.

--verify-client (선택사항):  클라이언트 인증서 확인을 설정하는지 여부입니다.

**예제**:

인증서를 도메인 `ibmcxo-eventconnect.com`에 추가합니다.

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

현재 조직의 지정된 도메인에서 인증서를 제거합니다.

```
bluemix security cert-remove DOMAIN [-f]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*DOMAIN* (필수):  인증서를 제거하는 도메인입니다.

-f  (선택사항):  확인 없이 강제 삭제합니다.







## bluemix plugin repos
{: #bluemix_plugin_repos}

{{site.data.keyword.Bluemix_notm}} CLI에 등록된 모든 플러그인 저장소를 나열합니다.

```
bluemix plugin repos
```

**전제조건**: 없음


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

새 플러그인 저장소를 {{site.data.keyword.Bluemix_notm}} CLI에 추가합니다.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**전제조건**: 없음

**명령 옵션**:

*REPO_NAME*  (필수):  추가할 저장소의 이름입니다. 각 저장소의 고유 이름을 정의할 수 있습니다.

*REPO_URL*  (필수):  추가할 저장소의 URL입니다. 저장소 URL에는 프로토콜이 포함되어 있어야 합니다(예: plugins.ng.bluemix.net이 아닌 http://plugins.ng.bluemix.net). http://plugins.ng.bluemix.net이 {{site.data.keyword.Bluemix_notm}} CLI의 공식 플러그인 저장소입니다.

**예제**:

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

**전제조건**: 없음

**명령 옵션**:

*REPO_NAME*  (필수):  제거할 저장소의 이름입니다. 

**예제**:

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

**전제조건**: 없음

**명령 옵션**:

-r *REPO_NAME*  (선택사항):  지정된 저장소의 플러그인만 나열합니다.

**예제**:

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

**전제조건**: 없음


## bluemix plugin install
{: #bluemix_plugin_install}

지정된 경로 또는 저장소에서 {{site.data.keyword.Bluemix_notm}} CLI에 특정 버전의 플러그인을 설치합니다.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**전제조건**:  없음

**명령 옵션**:

*PLUGIN_PATH*|*PLUGIN_NAME* (필수):  `-r *REPO_NAME*`을 지정하지 않으면 지정된 로컬 경로 또는 원격 URL에서 플러그인이 설치됩니다.

-r *REPO_NAME*  (선택사항):  플러그인 2진이 있는 저장소의 이름입니다.
-v *VERSION*  (선택사항):  설치할 플러그인의 버전입니다. 값을 지정하지 않으면 최신 버전의 플러그인이 설치됩니다. 이 옵션은 저장소에서 플러그인을 설치하는 경우에만 유효합니다.

**예제**:

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






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

{{site.data.keyword.Bluemix_notm}} CLI에서 지정된 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall PLUGIN_NAME
```

**전제조건**: 없음

**명령 옵션**:

*PLUGIN_NAME*  (필수):  설치 제거할 플러그인의 이름입니다.

**예제**:

이전에 설치한 `IBM-Containers` 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

IBM Containers 서비스의 전체 기능을 사용하기 위해 로컬 시스템의 컨테이너 환경을 초기화합니다.

```
bluemix ic init
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**참고:** 초기화 전에 Docker CLI(docker)가 설치되어 있고 PATH 환경 변수에 구성되어 있는지 확인하십시오. 다른 지역으로 전환하려면 `bluemix region-set` 명령을 사용하십시오. 

**예제**:

`us-south` 지역으로 전환합니다.

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

실행 중인 컨테이너를 제어하거나 해당 출력을 봅니다. 컨테이너를 종료하고 중지하려면 `CTRL+C`를 사용하십시오. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} 명령을 참조하십시오. 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

--no-stdin  (선택사항): 표준 입력을 포함하지 않습니다.

--sig-proxy  (선택사항): 수신된 모든 신호를 프로세스로 프록시합니다. 기본값은 **true**입니다.

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**예제**:

다음 예제는 `my_container` 컨테이너에 접속하기 위한 요청을 보여줍니다.
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

IBM Containers 빌드 서비스를 호출하여 로컬에 또는 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 Docker 이미지를 빌드합니다. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [build](https://docs.docker.com/reference/commandline/build/){: new_window} 명령을 참조하십시오. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-t *TAG*|--tag *TAG*  (필수): 작성되는 이미지에 적용되는 저장소 이름입니다.

--no-cache  (선택사항): 이미지가 빌드될 때 캐시를 사용하지 않습니다. 기본값은 **false**입니다.

-p|--pull  (선택사항): 기본 이미지가 캐시된 경우에도 레지스트리에서 기본 이미지를 가져오려고 시도합니다.

-q|--quiet  (선택사항): 컨테이너를 통해 생성되는 상세 출력이 표시되지 않도록 합니다. 기본값은 **false**입니다.

*DOCKERFILE_LOCATION*  (필수): 로컬 호스트에 있는 Dockerfile 및 컨텍스트의 경로입니다.

**예제**:

다음 예제는 이름이 *myimage*인 이미지를 빌드하기 위한 요청을 보여줍니다. 빌드에 사용할 Dockerfile 및 기타 아티팩트는 명령이 실행되는 디렉토리와 동일한 디렉토리에 있습니다. 레지스트리 및 네임스페이스가 이미지 이름과 함께 포함되기 때문에 이미지는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 빌드됩니다.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

{{site.data.keyword.Bluemix_notm}} 저장소에 새 컨테이너를 작성합니다. 이 명령은 `docker create` 명령을 랩핑합니다. 자세한 정보는 Docker 도움말에서 [create](https://docs.docker.com/reference/commandline/create/){: new_window} 명령을 참조하십시오.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Docker 허브 이미지 또는 로컬 레지스트리의 이미지에 액세스하여 해당 이미지를 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 복사합니다.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*SOURCE_IMAGE*  (필수): 소스 저장소 및 이미지 이름입니다.

*DESTINATION_IMAGE*  (필수): 개인용 {{site.data.keyword.Bluemix_notm}} 저장소 URL이며 여기에는 네임스페이스 및 대상 이미지 이름이 포함됩니다. 이미지의 태그는 선택사항입니다. 

**예제**:

소스 저장소의 이미지를 개인용 저장소에 복사하고 해당 이미지의 태그를 추가합니다.

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

`training` 저장소의 `sinatra` 이미지를 개인용 저장소 `registry.ng.bluemix.net/mynamespace`로 복사하고 이 이미지의 이름을 `mysinatra`로 지정합니다. `mysinatra` 이미지에 대한 `v1` 태그를 추가합니다. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


컨테이너에서 명령을 실행합니다. 자세한 정보는 Docker 도움말에서 [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} 명령을 참조하십시오.

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-d|--detach  (선택사항): 백그라운드에서 지정된 명령을 실행합니다.

-it  (선택사항): 대화식 모드입니다. 표준 입력이 계속 표시되도록 합니다. 종료하려면 `exit`를 입력하십시오.

-u *USER*|--user *USER*  (선택사항): 사용자 이름입니다.

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

*CMD*  (선택사항): 지정된 컨테이너 내에서 실행할 명령입니다.

**예제**:

대화식 모드로 `my_container` 컨테이너에서 `bash` 명령을 실행합니다.

```
bluemix ic exec -it my_container bash
```

`my_container` 컨테이너에서 `date` 명령을 실행합니다.

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 컨테이너 그룹을 나열합니다.

```
bluemix ic groups
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

컨테이너 그룹을 작성할 때 컨테이너 그룹에 대해 지정한 자세한 정보(예: 환경 변수, 포트 또는 메모리)를 봅니다.

```
bluemix ic group-inspect CONTAINER_GROUP
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CONTAINER_GROUP*  (필수): 컨테이너 그룹 ID 또는 이름입니다.

**예제**:

다음 예제는 `my_group` 컨테이너 그룹을 검사하기 위한 요청을 보여줍니다.
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

지정된 컨테이너 그룹의 인스턴스를 나열합니다.

```
bluemix ic group-instances CONTAINER_GROUP
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CONTAINER_GROUP*  (필수): 컨테이너 그룹 ID 또는 이름입니다.

**예제**:

`my_group` 컨테이너 그룹의 모든 인스턴스를 나열합니다.
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

확장 가능한 컨테이너 그룹을 작성합니다.

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

-m *MEMORY*|--memory *MEMORY*  (선택사항): 그룹에 MB 단위의 메모리 한계를 지정합니다. CLI에서 컨테이너 그룹을 작성하는 경우, 각 컨테이너 인스턴스에 대한 기본값은 `64`MB입니다. {{site.data.keyword.Bluemix_notm}} 대시보드에서 컨테이너 그룹을 작성하는 경우, 각 컨테이너 인스턴스에 대한 기본값은 `256`MB입니다. 허용 값은 `64`, `256`, `512`, `1024` 및 `2048`입니다. 메모리 한계가 지정된 후에는 값을 변경할 수 없습니다.

-e *ENV*|--env *ENV*  (선택사항): 환경 변수를 설정합니다. 여기서 **ENV**는 `key=value` 쌍입니다. 여러 키를 개별적으로 나열하십시오. 따옴표를 사용하는 경우 환경 변수와 값을 함께 따옴표로 묶으십시오. 예: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`. 다음 표에서는 지정 가능한 공통으로 사용되는 일부 환경 변수를 보여줍니다.

|  환경 변수                              |     설명                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 컨테이너에 서비스를 바인드합니다. `CCS_BIND_APP` 환경 변수를 사용하여 컨테이너에 앱을 바인드하십시오. 앱은 대상 서비스에 바인드되어 브릿지 역할을 하며, 이 브릿지를 통해 {{site.data.keyword.Bluemix_notm}}는 사용자 브릿지 앱의 `VCAP_SERVICES` 정보를 실행 중인 컨테이너 인스턴스로 가져올 수 있습니다. 브릿지 앱 작성에 대한 자세한 정보는 [컨테이너에 서비스 바인딩](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}을 참조하십시오. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | 컨테이너를 작성할 때 컨테이너에 SSH 키를 추가합니다. {{site.data.keyword.Bluemix_notm}} 대시보드 또는 CLI에서 컨테이너를 작성할 때 이 환경 변수를 사용하여 SSH 키를 추가할 수 있습니다. SSH 키에 대한 자세한 정보는 [컨테이너에 로그인](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}을 참조하십시오. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 컨테이너에서 모니터링할 로그 파일을 추가합니다. `LOG_LOCATIONS` 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. |
*표 1. 공통으로 사용되는 환경 변수*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional): `VolumeId:ContainerPath[:ro]` 형식의 세부사항을 지정하여 컨테이너에 볼륨을 첨부합니다.

- *VOLUME*: 볼륨 ID 또는 이름입니다.
- *CONTAINER_PATH*: 컨테이너에서 볼륨의 절대 경로입니다.
- ro: 선택사항입니다. `ro`를 지정하면 볼륨이 기본값인 읽기/쓰기가 아니라 읽기 전용으로 설정됩니다.

-p *PORT*|--publish *PORT*  (선택사항): HTTP 트래픽을 위한 포트를 공개합니다. 그룹의 컨테이너는 HTTP 포트를 청취해야 합니다. HTTPS 요청은 작성할 수 없습니다. 컨테이너 그룹의 경우 여러 포트를 포함시킬 수 없습니다.

포트를 지정하면 호스트에 도달하려고 하는 동일한 {{site.data.keyword.Bluemix_notm}} 영역에 있는 {{site.data.keyword.Bluemix_notm}} 로드 밸런서 또는 컨테이너에서 해당 앱을 사용할 수 있습니다. 그리고 {{site.data.keyword.Bluemix_notm}} 로드 밸런서 또는 컨테이너는 해당 포트를 사용하여 동일한 {{site.data.keyword.Bluemix_notm}} 영역의 앱 및 호스트에 접속할 수 있습니다. Dockerfile에 사용 중인 이미지에 대해 포트가 지정되어 있으면 해당 포트를 포함시키십시오.

**팁:**

- IBM 인증 Liberty 서버 이미지 또는 이 이미지의 수정된 버전의 경우 포트 9080을 입력하십시오.
- IBM 인증 Node.js 이미지 또는 이 이미지의 수정된 버전의 경우 포트 8000을 입력하십시오.

--min *MIN*  (선택사항): 인스턴스의 최소 수입니다. 기본값은 **1**입니다. 인스턴스의 최소 수를 설정하는 경우, 컨테이너 그룹이 작성된 후에는 해당 값을 변경할 수 없습니다.

--max *MAX*  (선택사항): 인스턴스의 최대 수입니다. 기본값은 **2**입니다. 인스턴스의 최대 수를 설정하는 경우, 컨테이너 그룹이 작성된 후에는 해당 값을 변경할 수 없습니다.

--desired *DESIRED*  (선택사항): 필요한 인스턴스 수입니다. 기본값은 **2**입니다. 

--auto  (선택사항): 컨테이너 그룹이 작성되었고 자동 복구가 사용되는 경우, IBM Containers는 지정된 포트에 대한 HTTP 요청으로 각 인스턴스의 상태를 확인합니다.

두 개의 후속 90초 간격에서 컨테이너 인스턴스로부터 응답이 수신되지 않으면 해당 인스턴스가 제거되고 새 인스턴스로 바뀝니다. 컨테이너가 응답하면 아무 조치도 수행되지 않습니다. 이 프로세스는 계속해서 반복됩니다. 30분 창 동안 그룹의 멤버인 서로 다른 컨테이너의 총 수가 해당 그룹의 관찰된 최대 크기의 3배보다 크거나 같으면 해당 컨테이너 그룹에 대해 자동 복구가 영구적으로 사용되지 않습니다. 자동 복구를 다시 사용하려면 컨테이너 그룹을 다시 작성해야 합니다.

-n *HOST*|--hostname *HOST*  (선택사항): 호스트 이름입니다(예: `mycontainerhost`). 호스트와 도메인은 결합되어 전체 공용 라우트 URL(예: `http://mycontainerhost.mybluemix.net`)을 형성합니다. `bluemix ic group-inspect` 명령으로 컨테이너 그룹의 세부사항을 검토하면 호스트 및 도메인이 라우트로 함께 나열됩니다.

-d *DOMAIN*|--domain *DOMAIN*  (선택사항): 주로 도메인은 `.mybluemix.net`입니다. 호스트와 도메인은 결합되어 전체 공용 라우트 URL(예: `http://mycontainerhost.mybluemix.net`)을 형성합니다. `bluemix ic group-inspect` 명령으로 컨테이너 그룹의 세부사항을 검토하면 호스트 및 도메인이 라우트로 함께 나열됩니다.

--name *NAME*  (필수): 그룹에 이름을 지정합니다. `-n`은 더 이상 사용되지 않습니다.

**팁:** 컨테이너 이름은 문자로 시작해야 합니다. 이름에는 대문자, 소문자, 숫자, 마침표(`.`), 밑줄(`_`) 또는 하이픈(`-`)이 포함될 수 있습니다.

*IMAGE*  (필수): 컨테이너 그룹의 각 컨테이너 인스턴스에 포함될 이미지입니다. 이미지 뒤에 명령을 나열할 수 있지만 이미지 뒤에 옵션을 두지 마십시오. 이미지를 지정하기 전에 모든 옵션을 포함시키십시오.

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 이미지를 사용하는 경우, `registry.ng.bluemix.net/NAMESPACE/IMAGE` 형식으로 이미지를 지정하십시오.

IBM Containers에서 제공하는 이미지를 사용하는 경우 조직의 네임스페이스를 포함시키지 마십시오. `registry.ng.bluemix.net/IMAGE` 형식으로 이미지를 지정하십시오.

*CMD*  (선택사항): 실행할 컨테이너 그룹에 전달되는 명령 및 인수입니다. 이 명령은 장시간 실행되는 명령이어야 합니다. 단시간 실행되는 명령(예: **/bin/date**)은 컨테이너 충돌을 유발할 수 있으므로 사용하지 마십시오.

**참고:**
- 명령 및 해당 인수는 `bluemix ic run` 명령행의 끝에 와야 합니다.
- 위의 예제 명령에 있는 `-c`와 같이 명령 인수에 하이픈(`-`)이 포함되는 경우에는 명령 앞에 두 개의 하이픈(`--`)이 와야 합니다. 



**예제**:

IBM Containers에서 제공하는 `registry.ng.bluemix.net/ibmnode` 이미지를 사용하여 컨테이너 그룹 `my_container_group`을 작성한 후 해당 컨테이너 그룹에 대해 `ping localhost` 장시간 실행 명령을 실행합니다.

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

IBM Containers에서 제공하는 `registry.ng.bluemix.net/ibmnode` 이미지를 사용하여 컨테이너 그룹 `my_container_group`을 작성한 후 해당 컨테이너 그룹에 대해 `tail -f /dev/null` 장시간 실행 명령을 실행합니다.

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

`registry.ng.bluemix.net/ibmliberty` 이미지를 사용하여 자동 복구가 사용되는 확장 가능한 그룹 `mygroup`을 작성합니다. 포트는 `9080`이고 호스트 이름은 `mycontainerhost`이며 도메인 이름은 `.mybluemix.net`입니다.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

컨테이너 그룹을 작성합니다.


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**팁:** 컨테이너 그룹의 호스트 이름 또는 도메인을 업데이트하려면 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`을 사용하십시오.

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

--min *MIN*  (선택사항): 인스턴스의 최소 수입니다. 기본값은 **1**입니다. 인스턴스의 최소 수가 설정된 후에는 값을 변경할 수 없습니다.

--max *MAX*  (선택사항): 인스턴스의 최대 수입니다. 기본값은 **2**입니다. 인스턴스의 최대 수가 설정된 후에는 값을 변경할 수 없습니다.

--desired *DESIRED*  (선택사항): 필요한 인스턴스 수입니다. 기본값은 **2**입니다. 

**팁:** 한 번에 `--min MIN`, `--max MAX` 및 `--desired DESIRED` 옵션 중 하나만 지정할 수 있습니다.

--auto  (선택사항): 자동 복구를 사용 가능하게 설정하여 실패한 인스턴스를 자동으로 다시 시작합니다.

*CONTAINER_GROUP*  (필수): 컨테이너 그룹 ID 또는 이름입니다.

**예제**:

다음 예제는 `my_group` 컨테이너 그룹을 업데이트하기 위한 요청을 보여줍니다.
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에서 컨테이너 그룹을 제거합니다.

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

-f|--force  (선택사항): 실행 중이거나 실패한 컨테이너의 제거를 강제 실행합니다.

*CONTAINER_GROUP*  (필수): 컨테이너 그룹 ID 또는 이름입니다.

**예제**:

다음 예제는 컨테이너 그룹을 제거하기 위한 요청을 보여줍니다. 여기서 `my_group`은 컨테이너 그룹의 이름입니다.
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 사용 가능한 모든 이미지 목록을 봅니다. 자세한 정보는 Docker 도움말에서 [images](https://docs.docker.com/reference/commandline/images){: new_window} 명령을 참조하십시오. 목록에는 이미지 ID, 작성된 날짜 및 이미지 이름이 포함됩니다.

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-a|--all  (선택사항): 최근의 계층뿐만 아니라, 조직의 저장소에 있는 각 이미지의 모든 이미지 계층을 포함합니다.

--no-trunc  (선택사항): 출력을 자르지 않습니다.

-q|--quiet  (선택사항): 숫자 ID만 표시합니다.

**예제**:

다음 예제는 조직의 사용 가능한 이미지 목록을 수신하기 위한 요청을 보여줍니다.
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

컨테이너에 대한 정보를 봅니다. 자세한 정보는 Docker 도움말에서 [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} 명령을 참조하십시오.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*IMAGE*  (필수): 이미지 이름 또는 ID를 지정하여 특정 이미지에 대한 자세한 정보를 봅니다.

images  (필수): 저장소에 있는 모든 이미지에 대한 자세한 정보를 봅니다.

*CONTAINER*  (필수): 컨테이너 이름 또는 ID를 지정하여 특정 컨테이너에 대한 자세한 정보를 봅니다.

**팁:** 한 번에 *IMAGE*, images 및 *CONTAINER* 중 하나만 지정할 수 있습니다. 

**예제**:

다음 예제는 `proxy`라는 컨테이너를 검사하기 위한 요청을 보여줍니다.
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

컨테이너 클라우드 서비스 인스턴스의 상태를 설명하는 정보 세트를 봅니다. 정보에는 컨테이너 한계, 컨테이너 사용량, 실행 중인 컨테이너, 메모리 한계, 메모리 사용량, 유동 IP 주소 한계, 유동 IP 주소 사용량, CCS 호스트 URL, 레지스트리 호스트 URL 및 디버그 모드 상태가 포함됩니다.

```
bluemix ic info
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix ic ips
{: #bluemix_ic_ips}

로그인한 사용자의 사용 가능한 유동 IP 주소를 나열합니다. 목록에는 IP 주소와 해당 IP 주소가 링크된 컨테이너 ID가 포함됩니다. IP 주소가 사용되지 않는 경우에는 컨테이너 ID가 표시되지 않습니다.

```
bluemix ic ips [-a|--all]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

-a|--all  (선택사항): 모든 IP 주소를 나열합니다. 기본적으로 사용 가능한 IP 주소만 리턴됩니다. 

**예제**:

다음 예제는 조직의 IP 주소 목록을 사용 가능 여부와 관계없이 모두 수신하기 위한 요청을 보여줍니다.
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
새 유동 IP 주소를 요청합니다.

```
bluemix ic ip-request
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

컨테이너 클라우드 서비스 인스턴스에서 유동 IP 주소를 릴리스합니다. 

```
bluemix ic ip-release IP_ADDRESS
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*IP_ADDRESS*  (필수): 해제할 IP 주소입니다.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

사용 가능한 유동 IP 주소를 컨테이너에 바인딩합니다. 

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*IP_ADDRESS*  (필수): 바인드되는 IP 주소입니다.

*CONTAINER*  (필수): 바인드되는 컨테이너 ID 또는 이름입니다.

**예제**:

다음 예제는 IP 주소 `192.123.12.12`를 `proxy` 컨테이너로 바인드하기 위한 요청을 보여줍니다.
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

컨테이너에서 유동 IP 주소를 바인드 해제합니다. 

공용 IP 주소는 IBM Containers에서 제한된 자원입니다. 따라서, 영역에 할당되었지만 컨테이너에 바인드되지 않은 공용 IP 주소는 무료 평가판 사용자로부터 주기적으로(대략 주 단위로) 재확보됩니다. 종량과금제 또는 구독 고객으로부터는 바인드되지 않은 공용 IP 주소가 재확보되지 않습니다.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*IP_ADDRESS*  (필수): 바인드 해제되는 IP 주소입니다.

*CONTAINER*  (필수): 바인드 해제되는 컨테이너 ID 또는 이름입니다.

**예제**:

다음 예제는 IP 주소 `192.123.12.12`를 `proxy` 컨테이너에서 바인드 해제하기 위한 요청을 보여줍니다.
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

컨테이너를 중지하지 않고 컨테이너에서 실행 중인 프로세스를 중지합니다. 자세한 정보는 Docker 도움말에서 [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} 명령을 참조하십시오.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-s *CMD*|--signal *CMD*  (선택사항): 컨테이너에서 실행 중인 프로세스에 명령을 전송합니다.

*CONTAINER*  (필수): 컨테이너 ID 또는 이름입니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너의 프로세스를 강제 종료하기 위한 요청을 보여줍니다.
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

로그인하는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 이미지 저장소의 이름을 봅니다.

```
bluemix ic namespace-get
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

로그인하는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 이미지 저장소의 이름을 설정합니다.

*제한사항*: 저장소 네임스페이스의 이름에 하이픈(`-`)을 사용할 수 없습니다.

```
bluemix ic namespace-set NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*NAME*  (필수): 조직의 저장소 네임스페이스가 아직 설정되지 않은 경우 이를 설정하는 일회성 기능입니다. 네임스페이스를 설정한 후에는 계속하기 전에 `bluemix ic init` 명령을 사용하여 IBM Containers를 다시 초기화하십시오.


## bluemix ic pause
{: #pause}

실행 중인 컨테이너 내의 모든 프로세스를 일시정지합니다. 자세한 정보는 Docker 도움말에서 [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} 명령을 참조하십시오. 컨테이너를 중지하려면 [bluemix ic unpause](#unpause) 명령을 참조하십시오.

```
bluemix ic pause CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**응답**:

- 컨테이너가 일시정지되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`
  
 여기서 `{message}`는 관련 오류입니다. 
 
- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너를 일시정지하기 위한 요청을 보여줍니다.
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

실행 중인 컨테이너 내에 있는 모든 프로세스의 일시정지를 해제합니다. 자세한 정보는 Docker 도움말에서 [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} 명령을 참조하십시오. 컨테이너를 일시정지하려면 [bluemix ic pause](#pause) 명령을 참조하십시오.

```
bluemix ic unpause CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**응답**:

- 컨테이너의 일시정지가 해제되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다. 

 `{message}` 
 
 여기서 `{message}`는 관련 오류입니다. 
 
- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너의 일시정지를 해제하기 위한 요청을 보여줍니다.
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

컨테이너의 포트 맵핑 또는 특정 맵핑을 나열합니다. 이 명령은 `docker port` 명령을 랩핑합니다. 자세한 정보는 Docker 도움말에서 [port](https://docs.docker.com/reference/commandline/port/){: new_window} 명령을 참조하십시오.


## bluemix ic ps
{: #bluemix_ic_ps}
로그인한 사용자의 네임스페이스에서 실행 중인 컨테이너 목록을 봅니다. 기본적으로 이 명령은 실행 중인 컨테이너만 표시합니다. 자세한 정보는 Docker 도움말에서 [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} 명령을 참조하십시오.

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-a|--all  (선택사항): 모든 컨테이너(실행 중 및 중지된 컨테이너 모두)를 표시합니다.

-s|--size  (선택사항): 컨테이너의 크기를 나열합니다.

-l *NUM*|--limit *NUM*  (선택사항): 가장 최근에 작성된 컨테이너를 나열합니다. 여기서 *NUM*은 가장 최근에 작성된 컨테이너 중 리턴하려는 컨테이너 수입니다.

예를 들어, `node1`에서 `node5`까지 순차적으로 컨테이너를 작성한 경우, `bluemix ic ps --limit 2` 명령은 node4 및 node5가 마지막으로 작성된 컨테이너이므로 이 두 컨테이너를 리턴합니다.

-q|--quiet  (선택사항): 컨테이너 ID만 표시합니다.

**예제**:

다음 예제는 실행 중인 컨테이너와 중지된 컨테이너를 모두 표시하기 위한 요청을 보여줍니다.
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

컨테이너를 다시 시작합니다. 자세한 정보는 Docker 도움말에서 [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} 명령을 참조하십시오.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

-t *SECS*|--time *SECS*  (선택사항): 컨테이너가 다시 시작될 때까지 대기하는 시간(초)입니다.

**응답**:

- 컨테이너가 다시 시작되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다. 

 `{message}` 
 
 여기서 `{message}`는 관련 오류입니다. 
 
- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너를 다시 시작하기 위한 요청을 보여줍니다.
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

컨테이너를 제거합니다. 자세한 정보는 Docker 도움말에서 [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} 명령을 참조하십시오.

```
bluemix ic rm [-f|--force] CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-f|--force  (선택사항): 실행 중이거나 실패한 컨테이너의 제거를 강제 실행합니다.

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**응답**:

- 컨테이너가 제거되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다. 

 `{message}` 
 
 여기서 `{message}`는 관련 오류입니다. 
 
- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너를 제거하기 위한 요청을 보여줍니다.
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

로그인한 사용자의 네임스페이스에서 이미지를 제거합니다. 자세한 정보는 Docker 도움말에서 [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} 명령을 참조하십시오.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-R *REGISTRY*|--registry *REGISTRY*  (선택사항): 레지스트리 호스트를 변경합니다. 기본값은 `bluemix ic init` 명령에 지정한 레지스트리를 사용하는 것입니다.

*IMAGE*  (필수): 제거하려는 이미지의 이름입니다. 이미지 이름에 태그가 지정되지 않은 경우 `latest`라는 태그가 지정된 이미지가 기본적으로 삭제됩니다. 

**응답**:

- 제거됨: `{IMAGE}`

 여기서 `{IMAGE}`는 제거된 이미지의 이름입니다. 
 
- 오류! 지정된 레지스트리 호스트가 없습니다.

- 이미지 제거 실패 - 컨테이너 클라우드 레지스트리에 연결할 수 없습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다. 

 `{message}`
 
 여기서 `{message}`는 관련 오류입니다. 

**예제**:

다음 예제는 `mynamespace/myimage:latest` 이미지를 제거하기 위한 요청을 보여줍니다.
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

이미지 이름에서 생성된 컨테이너 클라우드 서비스에서 새 컨테이너를 시작합니다. 자세한 정보는 Docker 도움말에서 [run](https://docs.docker.com/reference/commandline/run/){: new_window} 명령을 참조하십시오. 



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**참고:** Cloud Foundry 명령 도구가 설치되어 있고 Cloud Foundry 토큰이 있는지 확인하십시오. `bluemix login` 및 `bluemix ic init`를 사용하여 성공적으로 로그인하면 필요한 토큰 및 인증서가 생성됩니다. 


**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

-p *PORT*|--publish *PORT*  (선택사항): HTTP 트래픽을 위한 포트를 공개합니다. Dockerfile에 사용 중인 이미지에 대해 지정된 모든 포트가 포함됩니다. 여러 `-p` 옵션을 사용하여 여러 포트를 포함시킬 수 있습니다. 포트를 공개하면 공용 IP 주소가 사용 가능한 경우 컨테이너에 공용 IP 주소가 자동으로 바인드됩니다.

컨테이너에 바인드할 기존 IP 주소가 영역에 있는 경우, 이 IP 주소를 나중에 바인드하는 대신 지정할 수 있습니다. IP 주소는 *&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt;* 형식으로 지정해야 합니다.

영역의 IP 주소 요청에 대한 자세한 정보는 [bluemix ic ip-request](#ip_request) 명령을 참조하십시오.

포트를 지정하면 호스트에 도달하려고 하는 동일한 {{site.data.keyword.Bluemix_notm}} 영역에 있는 {{site.data.keyword.Bluemix_notm}} 로드 밸런서 또는 컨테이너에서 해당 앱을 사용할 수 있습니다. Dockerfile에 사용 중인 이미지에 대해 포트가 지정되어 있으면 해당 포트를 포함시키십시오.

**팁:**

- IBM 인증 Liberty 서버 이미지 또는 이 이미지의 수정된 버전의 경우 포트 9080을 입력하십시오.
- IBM 인증 Node.js 이미지 또는 이 이미지의 수정된 버전의 경우 포트 8000을 입력하십시오.

-P  (선택사항): 이미지의 Dockerfile에 HTTP 트래픽에 대해 지정된 포트를 자동으로 공개합니다.

-m *MEMORY*|--memory *MEMORY*  (선택사항): 그룹에 MB 단위의 메모리 한계를 지정합니다. CLI에서 컨테이너 그룹을 작성하는 경우, 각 컨테이너 인스턴스에 대한 기본값은 `64`MB입니다. {{site.data.keyword.Bluemix_notm}} 대시보드에서 컨테이너 그룹을 작성하는 경우, 각 인스턴스에 대한 기본값은 `256`MB입니다. 허용 값은 `64`, `256`, `512`, `1024` 및 `2048`입니다. 메모리 한계가 지정된 후에는 값을 변경할 수 없습니다.

-e *ENV*|--env *ENV*  (선택사항): 환경 변수를 설정합니다. 여기서 **ENV**는 `key=value` 쌍입니다. 여러 키를 개별적으로 나열하십시오. 따옴표를 사용하는 경우 환경 변수와 값을 함께 따옴표로 묶으십시오. 예: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`. 다음 표에서는 지정 가능한 공통으로 사용되는 일부 환경 변수를 보여줍니다.

|      환경 변수                          |   설명                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 컨테이너에 서비스를 바인드합니다. `CCS_BIND_APP` 환경 변수를 사용하여 컨테이너에 앱을 바인드하십시오. 앱은 대상 서비스에 바인드되어 브릿지 역할을 하며, 이 브릿지를 통해 {{site.data.keyword.Bluemix_notm}}는 사용자 브릿지 앱의 `VCAP_SERVICES` 정보를 실행 중인 컨테이너 인스턴스로 가져올 수 있습니다. 브릿지 앱 작성에 대한 자세한 정보는 [컨테이너에 서비스 바인딩](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}을 참조하십시오. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | 컨테이너를 작성할 때 컨테이너에 SSH 키를 추가합니다. {{site.data.keyword.Bluemix_notm}} 대시보드 또는 CLI에서 컨테이너를 작성할 때 이 환경 변수를 사용하여 SSH 키를 추가할 수 있습니다. SSH 키에 대한 자세한 정보는 [컨테이너에 로그인](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}을 참조하십시오. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 컨테이너에서 모니터링할 로그 파일을 추가합니다. `LOG_LOCATIONS` 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. |
*표 2. 공통으로 사용되는 환경 변수*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional): `VolumeId:ContainerPath[:ro]` 형식의 세부사항을 지정하여 컨테이너에 볼륨을 첨부합니다.

- *VOLUME*: 볼륨 ID 또는 이름입니다.
- *CONTAINER_PATH*: 컨테이너에서 볼륨의 절대 경로입니다.
- ro: 선택사항입니다. `ro`를 지정하면 볼륨이 기본값인 읽기/쓰기가 아니라 읽기 전용으로 설정됩니다.

-n *NAME*|--name *NAME*  (필수): 컨테이너에 이름을 지정합니다.

*팁:* 컨테이너 이름은 문자로 시작해야 합니다. 이름에는 대문자, 소문자, 숫자, 마침표(`.`), 밑줄(`_`) 또는 하이픈(`-`)이 포함될 수 있습니다.

--link *NAME*:*ALIAS*  (선택사항): 컨테이너가 실행 중인 다른 컨테이너와 통신하도록 하려는 경우 언제든지 호스트 이름의 별명을 사용하여 이를 해결할 수 있습니다.

-it  (선택사항): 대화식 모드로 컨테이너를 실행합니다. 컨테이너가 작성된 후 표준 입력이 계속 표시되도록 합니다. 종료하려면 `exit`를 입력하십시오.

*IMAGE*  (필수): 컨테이너에 포함되는 이미지입니다. 이미지 뒤에 명령을 나열할 수 있지만 이미지 뒤에 옵션을 두지 마십시오. 이미지를 지정하기 전에 모든 옵션을 포함시키십시오.

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 이미지를 사용하는 경우, *registry.ng.bluemix.net/NAMESPACE/IMAGE* 형식으로 이미지를 지정하십시오.

IBM Containers에서 제공하는 이미지를 사용하는 경우 *registry.ng.bluemix.net/IMAGE* 형식으로 이미지를 지정하십시오.

*CMD*  (선택사항): 실행할 컨테이너에 전달되는 명령 및 인수입니다. 이 명령은 장시간 실행되는 명령이어야 합니다. 단시간 실행되는 명령(예: `/bin/date`)은 컨테이너 충돌을 유발할 수 있으므로 사용하지 마십시오.



**예제**:

`registry.ng.bluemix.net/ibmnode` 이미지에 빌드된 `my_container` 컨테이너에 대해 `sh -c "while true; do date; sleep 20; done"` 장시간 실행 명령을 실행합니다.
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


`my_namespace/nginx` 이미지(여기서 `my_namespace`는 로그인한 사용자와 연관된 네임스페이스임)를 사용하여 메모리 한계가 `1024`MB인 `proxy` 컨테이너를 작성한 후 시작합니다.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

`my_namespace/blog` 이미지를 사용하여 컨테이너를 작성한 후 시작하고 신임 정보를 환경 변수로 전달합니다. `my_namespace`는 로그인한 사용자와 연관된 네임스페이스입니다.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

`my_namespace/blog` 이미지(여기서 `my_namespace`는 로그인한 사용자와 연관된 네임스페이스임)를 사용하여 컨테이너에 볼륨을 추가합니다.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

컨테이너 그룹에 액세스하는 데 사용할 인터넷 트래픽에 대한 라우트를 설정합니다. 이 명령을 사용하여 새 라우트를 설정하거나 기존 라우트를 업데이트할 수 있습니다.

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

-n *HOST*|--hostname *HOST*  (선택사항): 라우트의 호스트 이름입니다. 호스트 이름은 전체 공용 라우트 URL의 첫 번째 파트입니다(예: URL `mycontainerhost.mybluemix.net`의 `mycontainerhost`).

-d *DOMAIN*|--domain *DOMAIN*  (선택사항): 라우트의 도메인 이름이며, 전체 공용 라우트 URL의 두 번째 파트입니다. 대부분의 경우, 도메인은 `mybluemix.net`입니다. 이 매개변수를 사용하여 개인용 도메인을
지정할 수도 있습니다. 

*CONTAINER_GROUP*  (필수): 컨테이너 그룹 ID 또는 이름입니다.

**예제**:

다음 예제는 `GROUP1`이라는 그룹의 라우트를 맵핑하기 위한 요청을 보여줍니다. 여기서 `my_host`는 호스트 이름이고 `organization.com`은 도메인입니다.
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

컨테이너 그룹에 액세스하는 데 사용할 인터넷 트래픽에 대한 라우트를 설정합니다. 이 명령을 사용하여 새 라우트를 설정하거나 기존 라우트를 업데이트할 수 있습니다.

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

-n *HOST*|--hostname *HOST*  (선택사항): 라우트의 호스트 이름입니다. 

-d *DOMAIN*|--domain *DOMAIN*  (선택사항): 라우트의 도메인 이름입니다.

*CONTAINER_GROUP*  (필수): 컨테이너 그룹 ID 또는 이름입니다.

**예제**:

다음 예제는 `GROUP1`이라는 그룹의 라우트를 맵핑 해제하기 위한 요청을 보여줍니다. 여기서 `my_host`는 호스트 이름이고 `organization.com`은 도메인입니다.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
중지된 컨테이너를 시작합니다. 자세한 정보는 Docker 도움말에서 [start](https://docs.docker.com/reference/commandline/start/){: new_window} 명령을 참조하십시오. 컨테이너를 중지하려면 [bluemix ic stop](#ic_stop) 명령을 참조하십시오.

```
bluemix ic start CONTAINER
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**응답**:

- 컨테이너가 시작되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`
  
 여기서 `{message}`는 관련 오류입니다. 
 
- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너를 시작하기 위한 요청을 보여줍니다.
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
실행 중인 컨테이너를 중지합니다. 자세한 정보는 Docker 도움말에서 [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} 명령을 참조하십시오. 컨테이너를 시작하려면 [bluemix ic start](#ic_start) 명령을 참조하십시오.

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

-t *SECS*|--time *SECS*  (선택사항): 컨테이너가 강제 종료될 때까지 대기하는 시간(초)입니다.

**응답**:

- 컨테이너가 중지되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`
  
 여기서 `{message}`는 관련 오류입니다. 
 
- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

**예제**:

다음 예제는 `proxy`라는 컨테이너를 중지하기 위한 요청을 보여줍니다.
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

하나 이상의 컨테이너에 대해 실시간 사용량 통계를 봅니다. 종료하려면 `CTRL+C`를 사용하십시오. 자세한 정보는 Docker 도움말에서 [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} 명령을 참조하십시오.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

--no-stream  (선택사항): 최근 결과만 표시하고 그 이전의 정보는 포함하지 않습니다.

**예제**:

다음 예제는 컨테이너에 대한 가장 최근의 통계를 얻기 위한 요청을 보여줍니다.
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

컨테이너에서 실행 중인 프로세스를 표시합니다. 자세한 정보는 Docker 도움말에서 [top](https://docs.docker.com/reference/commandline/top/){: new_window} 명령을 참조하십시오.

```
bluemix ic top CONTAINER [CONTAINER]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**예제**:

다음 예제는 `my_container`라는 컨테이너의 프로세스를 표시하기 위한 요청을 보여줍니다.
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

볼륨을 나열합니다.

```
bluemix ic volumes
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

볼륨을 검사합니다.

```
bluemix ic volume-inspect VOLUME_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*VOLUME_NAME*  (필수): 볼륨 이름입니다.

**예제**:

다음 예제는 볼륨을 검사하기 위한 요청입니다. 여기서 `volume_name`은 볼륨의 이름입니다.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

볼륨을 작성합니다.

```
bluemix ic volume-create VOLUME_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*VOLUME_NAME*  (필수): 볼륨 이름입니다. 이름에는 소문자, 숫자, 밑줄(`_`) 및 하이픈(`-`)이 포함될 수 있습니다.

**예제**:

다음 예제는 볼륨을 작성하기 위한 요청을 보여줍니다.
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

볼륨을 제거합니다.

```
bluemix ic volume-remove VOLUME_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*VOLUME_NAME*  (필수): 볼륨 이름입니다.

**예제**:

다음 예제는 볼륨을 제거하기 위한 요청입니다. 여기서 `volume_name`은 볼륨의 이름입니다.
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

파일 시스템을 나열합니다.

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

새 파일 시스템을 작성합니다.

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*FILE_SYSTEM_NAME* (필수): 파일 시스템 이름입니다. 이름에는 소문자, 숫자, 밑줄(`_`) 및 하이픈(`-`)이 포함될 수 있습니다.

**예제**:

다음 예제는 파일 시스템 작성 요청을 표시합니다.
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

파일 시스템을 제거합니다.

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*FILE_SYSTEM_NAME* (필수): 파일 시스템 이름입니다. 

**예제**:

다음 예제는 파일 시스템 제거 요청을 표시합니다. 여기서 `my_file_system`은 파일 시스템의 이름입니다.
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

파일 시스템을 검사합니다.

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*FILE_SYSTEM_NAME* (필수): 파일 시스템 이름입니다. 

**예제**:

다음 예제는 파일 시스템 검사 요청입니다. 여기서 `my_file_system`은 볼륨의 이름입니다.
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

모든 파일 시스템 특성을 나열합니다.

```
bluemix ic volume-fs-flavors
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

## bluemix ic wait
{: #bluemix_ic_wait}

컨테이너를 종료하고 확인으로 종료 코드를 표시합니다. 자세한 정보는 Docker 도움말에서 [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} 명령을 참조하십시오.

```
bluemix ic wait CONTAINER [CONTAINER]
```

**전제조건**:  엔드포인트, 로그인, 대상, Docker

**명령 옵션**:

*CONTAINER*  (필수): 컨테이너 이름 또는 ID입니다.

**예제**:

다음 예제는 `my_container`라는 컨테이너를 종료하기 위한 요청을 보여줍니다.
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

Docker의 버전을 표시합니다. 

```
bluemix ic version
```

**전제조건**:  Docker

IBM Containers의 버전을 보려면 `bluemix ic info`를 실행하십시오. 자세한 정보는 Docker 도움말에서 [version](https://docs.docker.com/reference/commandline/version/){: new_window} 명령을 참조하십시오.
