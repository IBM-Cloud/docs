---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 시작하기
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI는 명령행 인터페이스를 사용하여 애플리케이션, 가상 서버, 컨테이너 및 기타 서비스와 상호작용하기 위한 통합된 방법을 제공합니다. 또한 {{site.data.keyword.Bluemix_notm}} CLI는 Cloud Foundry CLI, Docker CLI 및 OpenStack CLI와 같은 커뮤니티 도구를 통합하고, 다른 컴퓨팅 유형과 상호작용하도록 환경 설정을 초기화합니다. 

**제한사항**: {{site.data.keyword.Bluemix_notm}} CLI는 Cygwin에서 지원되지 않으므로 Cygwin 명령행 창에서는 {{site.data.keyword.Bluemix_notm}} CLI를 사용하지 마십시오. 

**참고**: 네트워크에 CLI를 실행하는 호스트와 {{site.data.keyword.Bluemix_notm}} 간에 HTTP 프록시 서버가 포함되어 있는 경우 HTTP_PROXY 환경 변수에 프록시 서버의 호스트 이름 또는 IP 주소를 지정해야 합니다. 

## {{site.data.keyword.Bluemix_notm}} CLI 설치
{: #install_bluemix_cli}

{{site.data.keyword.Bluemix_notm}} CLI를 설치하기 전에 먼저 [cf CLI ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}를 설치하십시오.

Mac OS 및 Windows의 경우, [{{site.data.keyword.Bluemix_notm}} CLI 패키지](/docs/cli/index.html#downloads)를 다운로드하고 설치 프로그램을 실행하십시오. 

Linux의 경우, 다음 단계를 수행하십시오. 

  1. 패키지를 다운로드하여 압축을 푸십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. `Bluemix_CLI` 디렉토리로 이동하여 루트 권한으로 `./install_bluemix_cli` 명령을 실행하십시오. 루트 사용자로 명령을 실행하거나 `sudo` 명령을 사용하여 루트 권한을 확보하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

이제 {{site.data.keyword.Bluemix_notm}} CLI 사용을 시작하거나 추가 플러그인을 설치할 수 있습니다.

## 플러그인 설치
{: #install_plug-in}

Cloud Foundry CLI와 같이 {{site.data.keyword.Bluemix_notm}} CLI는 기본 제공 명령 외에 다른 명령을 통합할 수 있도록 플러그인 확장 프레임워크를 지원합니다.

로컬 환경에서 플러그인을 설치하려면 다음 단계를 수행하십시오. 

  1. 플러그인을 다운로드하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. UNIX 계열 시스템의 경우 `chmod` 명령을 사용하여 다운로드된 파일을 실행 파일로 만들어야 합니다. 예를 들어, 다음과 같습니다. 

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. `bluemix plugin install` 명령을 사용하여 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

원격 서버에서 설치하려면 다음 단계를 수행하십시오. 

  1. `bluemix plugin install` 명령을 사용하여 원격 URL에서 직접 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

저장소에서 플러그인을 설치할 수도 있습니다. {{site.data.keyword.Bluemix_notm}}에는 {{site.data.keyword.Bluemix_notm}} CLI 플러그인 및 Cloud Foundry CLI 플러그인을 호스팅하는 저장소가 있습니다. 

  * [Cloud Foundry CLI 플러그인 저장소 ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg)는 Cloud Foundry CLI를 위한 플러그인을 호스팅합니다. 
  * [{{site.data.keyword.Bluemix_notm}} CLI 플러그인 저장소 ](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg)는 특별히 {{site.data.keyword.Bluemix_notm}} CLI를 위한 플러그인을 호스팅합니다. 

저장소에서 설치하려면 다음 단계를 수행하십시오. 

  1. 저장소에서 플러그인을 찾으십시오. {{site.data.keyword.Bluemix_notm}} CLI를 설치하고 나면, 기본적으로 공식 저장소 `Bluemix`가 추가됩니다. `bluemix plugin repo-plugins` 명령을 사용하여 `Bluemix` 저장소에 플러그인을 나열할 수 있습니다. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. `bluemix plugin install` 명령을 사용하여 `Bluemix` 저장소에서 플러그인을 설치하십시오. 예를 들어, 다음과 같습니다. 

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## {{site.data.keyword.Bluemix_notm}} CLI에 로그인
{: #log_bmcli}

{{site.data.keyword.Bluemix_notm}} CLI를 설치한 후 IBM ID 및 비밀번호를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인할 수 있습니다. 예를 들어, 다음과 같습니다. 

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

이제 {{site.data.keyword.Bluemix_notm}} 기본 제공 명령을 사용할 준비가 되었습니다. 예를 들어, 사용 가능한 모든 {{site.data.keyword.Bluemix_notm}} 표준 유형 템플리트를 나열하려면 `bluemix catalog templates` 명령을 실행하십시오. 

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# {{site.data.keyword.Bluemix_notm}}(bx) 명령
{: #bluemix_cli}

버전: 0.4.6

{{site.data.keyword.Bluemix_notm}} 명령행 인터페이스(CLI)는 사용자가 {{site.data.keyword.Bluemix_notm}}와 상호작용할 수 있도록 네임스페이스별로 그룹화된 명령 세트를 제공합니다. 일부 {{site.data.keyword.Bluemix_notm}} 명령은 기존 cf 명령의 랩퍼이며, 나머지는 {{site.data.keyword.Bluemix_notm}} 사용자에 대해 확장 기능을 제공합니다. 다음 정보에서는 {{site.data.keyword.Bluemix_notm}} CLI에서 지원하는 명령을 나열하며, 해당 이름, 옵션, 사용법, 전제조건, 설명 및 예제가 포함됩니다.
{:shortdesc}

**참고:** *전제조건*에는 명령을 사용하기 전에 필요한 조치가 설명되어 있습니다. 전제조건 조치가 없는 명령은 **없음**으로 표시됩니다. 그 밖의 경우에는 전제조건으로 다음과 같은 조치 중 하나 이상을 수행해야 할 수 있습니다.

<dl>
<dt>엔드포인트</dt>
<dd>명령을 사용하기 전에 <code>bluemix api</code>를 통해 API 엔드포인트를 설정해야 합니다.</dd>
<dt>로그인</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix login</code> 명령을 사용하여 로그인해야 합니다. 연합된 ID로 로그인하는 경우 '--sso' 옵션을 사용하여 일회성 패스코드로 인증하십시오.</dd>
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
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="조직, 영역 및 사용자 관리에 사용 가능한 Bluemix 명령.">
 <caption>표 2. 조직, 영역 및 사용자 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">조직, 영역 및 사용자 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary="Cloud Foundry 앱의 관리에 사용 가능한 Bluemix 명령.">
 <caption>표 3. cf 앱 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">cf 앱 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
 <td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
 <td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
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
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
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
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="네트워크 설정 관리에 사용 가능한 Bluemix 명령.">
 <caption>표 6. 네트워크 설정 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">네트워크 설정 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>



### bluemix help
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



### bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}} API 엔드포인트를 설정하거나 확인합니다. 이 명령은 `cf api` 명령을 랩핑 처리합니다. 

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>전제조건</strong>: 없음

<strong>명령 옵션</strong>:
   <dl>
   <dt>API_ENDPOINT(선택사항)</dt>
   <dd>대상으로 지정된 API 엔드포인트입니다(예: `https://api.chinabluemix.net`). *API_ENDPOINT* 및 `--unset` 옵션 중 하나를 지정하지 않으면 현재 API 엔드포인트가 표시됩니다. </dd>
   <dt>--unset(선택사항)</dt>
   <dd>API 엔드포인트 설정을 제거합니다.</dd>
    </dl>
<strong>예제</strong>:

API 엔드포인트를 api.chinabluemix.net으로 설정합니다.

```
bluemix api api.chinabluemix.net
```

현재 API 엔드포인트를 확인합니다.

```
bluemix api
```

API 엔드포인트를 설정 해제합니다.

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

사용자가 로그인됩니다. 이 명령은 `cf login` 명령을 랩핑 처리합니다. 명령 옵션이 `cf login` 명령 옵션과 동일합니다. 

```
bluemix login [OPTIONS...]
```

<strong>전제조건</strong>:  엔드포인트

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>명령 옵션</strong>:
`login` 명령에 지원되는 옵션에 대한 자세한 정보는 `cf login` 명령 사용법 정보에서 애플리케이션 관리를 위한 cf 명령을 참조하십시오.

<strong>참고</strong>:
연합된 ID로 로그인하는 경우 '--sso' 옵션을 사용하여 일회성 패스코드로 인증하십시오.

### bluemix logout
{: #bluemix_logout}

사용자가 로그아웃됩니다. 이 명령은 `cf logout` 명령을 랩핑 처리합니다. 

```
bluemix logout
```

<strong>전제조건</strong>: 없음


### bluemix target
{: #bluemix_target}


대상 조직 또는 영역을 설정하거나 확인합니다. 이 명령은 `cf target` 명령을 랩핑 처리합니다. 

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>전제조건</strong>: 엔드포인트, 로그인

<strong>명령 옵션</strong>:
   <dl>
   <dt>-o <i>ORG_NAME</i>(선택사항)</dt>
   <dd>대상으로 지정된 조직의 이름입니다. </dd>
   <dt>-s <i>SPACE_NAME</i>(선택사항)</dt>
   <dd>대상으로 지정된 영역의 이름입니다. </dd>
   </dl>
-o *ORG_NAME*과 -s *SPACE_NAME*을 둘 다 지정하지 않으면 현재 조직 및 영역이 표시됩니다.
<strong>예제</strong>:

현재 조직을 `MyOrg`로, 영역을 `MySpace`로 설정합니다.

```
bluemix target -o MyOrg -s MySpace
```

현재 조직과 영역을 확인합니다.

```
bluemix target
```


### bluemix info
{: #bluemix_info}

현재 지역, 클라우드 제어기 버전, 로그인과 교환 액세스 토큰의 엔드포인트 같은 유용한 엔드포인트 등 기본 {{site.data.keyword.Bluemix_notm}} 정보를 확인합니다.

```
bluemix info
```

<strong>전제조건</strong>:  엔드포인트


### bluemix config
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


### bluemix curl
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


### bluemix iam orgs
{: #bluemix_iam_orgs}

모든 조직 나열

```
bluemix iam orgs [-r REGION --guid]
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

### bluemix iam org
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

### bluemix iam org-create
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


### bluemix iam org-replicate
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


### bluemix iam org-rename
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

### bluemix iam org-delete
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


### bluemix iam spaces
{: #bluemix_iam_spaces}

이 명령은 `cf spaces` 명령과 기능 및 옵션이 동일합니다.


### bluemix iam space
{: #bluemix_iam_space}

이 명령은 `cf space` 명령과 기능 및 옵션이 동일합니다.


### bluemix iam space-create
{: #bluemix_iam_space_create}

이 명령은 `cf create-space` 명령과 기능 및 옵션이 동일합니다.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


이 명령은 `cf rename-space` 명령과 기능 및 옵션이 동일합니다.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


이 명령은 `cf delete-space` 명령과 기능 및 옵션이 동일합니다.


### bluemix iam account-users
{: #bluemix_iam_account_users}

계정과 연관된 사용자를 표시합니다. 이 조작은 계정 소유자만 수행할 수 있습니다.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
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
  <li>BillingManager: 이 역할은 청구 계정 및 지불 정보를 작성하고 관리할 수 있습니다. </li>
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


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

사용자에게 초대를 다시 보냅니다(조직 관리자 또는 계정 소유자 필요).
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
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

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

조직에 사용자를 추가합니다(조직 관리자 필요).
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
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

### bluemix iam org-role-set
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
   <li>BillingManager: 이 역할은 청구 계정 및 지불 정보를 작성하고 관리할 수 있습니다. </li>
   <li>OrgAuditor: 이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다. </li>
   </ul>
   </dd>
    </dl>

<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직에 `OrgManager` 역할로 지정합니다.

```
bluemix iam org-role-set Mary IBM OrgManager
```


### bluemix iam org-role-unset
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
   <li>BillingManager: 이 역할은 청구 계정 및 지불 정보를 작성하고 관리할 수 있습니다. </li>
   <li>OrgAuditor: 이 역할은 조직 정보 및 보고서에 대한 읽기 전용 액세스 권한을 보유합니다. </li>
   </ul>
   </dd>
    </dl>

<strong>예제</strong>:

사용자 `Mary`를 `IBM` 조직에서 `OrgManager` 역할로 제거합니다.

```
bluemix iam org-role-unset Mary IBM OrgManager
```


### bluemix iam space-users
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


### bluemix iam space-role-set
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

### bluemix iam space-role-unset
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


### bluemix app push
{: #bluemix_app_push}

이 명령은 `cf push` 명령과 기능 및 옵션이 동일합니다.


### bluemix app list
{: #bluemix_app_list}

이 명령은 `cf apps` 명령과 기능 및 옵션이 동일합니다.


### bluemix app show
{: #bluemix_app_show}

이 명령은 `cf app` 명령과 기능 및 옵션이 동일합니다.


### bluemix app scale
{: #bluemix_app_scale}

이 명령은 `cf scale` 명령과 기능 및 옵션이 동일합니다.


### bluemix app delete
{: #bluemix_app_delete}

이 명령은 `cf delete` 명령과 기능 및 옵션이 동일합니다.


### bluemix app rename
{: #bluemix_app_rename}

이 명령은 `cf rename` 명령과 기능 및 옵션이 동일합니다.


### bluemix app start
{: #bluemix_app_start}

이 명령은 `cf start` 명령과 기능 및 옵션이 동일합니다.


### bluemix app stop
{: #bluemix_app_stop}

이 명령은 `cf stop` 명령과 기능 및 옵션이 동일합니다.


### bluemix app restart
{: #bluemix_app_restart}

이 명령은 `cf restart` 명령과 기능 및 옵션이 동일합니다.


### bluemix app restage
{: #bluemix_app_restage}


이 명령은 `cf restage` 명령과 기능 및 옵션이 동일합니다.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


이 명령은 `cf restart-app-instance` 명령과 기능 및 옵션이 동일합니다.


### bluemix app events
{: #bluemix_app_events}

이 명령은 `cf events` 명령과 기능 및 옵션이 동일합니다.


### bluemix app files
{: #bluemix_app_files}

이 명령은 `cf files` 명령과 기능 및 옵션이 동일합니다.


### bluemix app logs
{: #bluemix_app_logs}

이 명령은 `cf logs` 명령과 기능 및 옵션이 동일합니다.


### bluemix app env
{: #bluemix_app_env}

이 명령은 `cf env` 명령과 기능 및 옵션이 동일합니다.


### bluemix app env-set
{: #bluemix_app_env_set}

이 명령은 `cf set-env` 명령과 기능 및 옵션이 동일합니다.


### bluemix app env-unset
{: #bluemix_app_env_unset}

이 명령은 `cf unset-env` 명령과 기능 및 옵션이 동일합니다.


### bluemix app stacks
{: #bluemix_app_stacks}

이 명령은 `cf stacks` 명령과 기능 및 옵션이 동일합니다.


### bluemix app stack
{: #bluemix_app_stack}

이 명령은 `cf stack` 명령과 기능 및 옵션이 동일합니다.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

이 명령은 `cf create-app-manifest` 명령과 기능 및 옵션이 동일합니다.


### bluemix service offerings
{: #bluemix_service_offerings}


이 명령은 `cf marketplace` 명령과 기능 및 옵션이 동일합니다.


### bluemix service list
{: #bluemix_service_list}

이 명령은 `cf services` 명령과 기능 및 옵션이 동일합니다.


### bluemix service show
{: #bluemix_service_show}

이 명령은 `cf service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service create
{: #bluemix_service_create}

이 명령은 `cf create-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service update
{: #bluemix_service_update}

이 명령은 `cf update-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service delete
{: #bluemix_service_delete}

이 명령은 `cf delete-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service rename
{: #bluemix_service_rename}

이 명령은 `cf rename-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service bind
{: #bluemix_service_bind}

이 명령은 `cf bind-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service unbind
{: #bluemix_service_unbind}

이 명령은 `cf unbind-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service key-create
{: #bluemix_service_key_create}

이 명령은 `cf create-service-key` 명령과 기능 및 옵션이 동일합니다.


### bluemix service key-delete
{: #bluemix_service_key_delete}

이 명령은 `cf delete-service-key` 명령과 기능 및 옵션이 동일합니다.


### bluemix service keys
{: #bluemix_service_keys}

이 명령은 `cf service-keys` 명령과 기능 및 옵션이 동일합니다.


### bluemix service key-show
{: #bluemix_service_key_show}

이 명령은 `cf service-key` 명령과 기능 및 옵션이 동일합니다.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

이 명령은 `cf create-user-provided-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

이 명령은 `cf update-user-provided-service` 명령과 기능 및 옵션이 동일합니다.


### bluemix catalog templates
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


### bluemix catalog template
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


### bluemix catalog template-run
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


### bluemix network regions
{: #bluemix_network_regions}

{{site.data.keyword.Bluemix_notm}}의 모든 지역에 대한 정보를 확인합니다.

```
bluemix network regions
```

<strong>전제조건</strong>:  엔드포인트


### bluemix network region-set
{: #bluemix_network_region_set}

지정된 지역으로 전환합니다. 이 명령은 새 지역의 동일한 조직 및 영역을 자동으로 대상으로 설정합니다(가능한 경우). 그렇지 않으면, 사용자가 이미 로그인한 상태인 경우에 한해 새 조직 및 영역을 선택하라는 메시지를 표시합니다. API 엔드포인트는 그에 맞게 변경됩니다.

```
bluemix network region-set REGION_NAME
```

<strong>전제조건</strong>:  엔드포인트

<strong>명령 옵션</strong>:

   <dl>
   <dt>REGION_NAME(필수)</dt>
   <dd>전환하려는 대상 지역의 이름입니다. <i>bluemix network regions</i> 명령을 사용하면 모든 지역 이름을 볼 수 있습니다.</dd>
    </dl>

<strong>예제</strong>:

현재 지역을 `eu-gb`로 설정합니다.

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

이 명령은 `cf routes` 명령과 기능 및 옵션이 동일합니다.


### bluemix network route-check
{: #bluemix_network_route_check}

이 명령은 `cf check-route` 명령과 기능 및 옵션이 동일합니다.


### bluemix network route-map
{: #bluemix_network_route_map}

지정된 도메인과 호스트 이름이 있는 기존의 cf 애플리케이션 또는 컨테이너 그룹에 라우트를 맵핑합니다.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-map my-app mychinabluemix.net
```

라우트를 지정된 도메인과 호스트 이름이 있는 'my-container-group'으로 맵핑합니다.

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

기존의 cf 애플리케이션이나 컨테이너 그룹과 지정된 라우트의 맵핑을 해제합니다.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-unmap my-app mychianbluemix.net
```

`my-container-group`에서 `abc.chinabluexmix.net`을 맵핑 해제합니다.

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

이 명령은 `cf create-route` 명령과 기능 및 옵션이 동일합니다.


### bluemix network route-delete
{: #bluemix_network_route_delete}

이 명령은 `cf delete-route` 명령과 기능 및 옵션이 동일합니다.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

이 명령은 `cf delete-orphaned-routes` 명령과 기능 및 옵션이 동일합니다.


### bluemix network domains
{: #bluemix_network_domains}

이 명령은 `cf domains` 명령과 기능 및 옵션이 동일합니다.


### bluemix network domain-create
{: #bluemix_network_domain_create}

이 명령은 `cf create-domain` 명령과 기능 및 옵션이 동일합니다.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

이 명령은 `cf delete-domain` 명령과 기능 및 옵션이 동일합니다.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

이 명령은 `cf create-shared-domain` 명령과 기능 및 옵션이 동일합니다.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

이 명령은 `cf delete-shared-domain` 명령과 기능 및 옵션이 동일합니다.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

계정의 월별 사용량 및 비용을 표시하십시오.

```
bluemix bss account-usage [-d YYYY-MM] [--json]
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
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

조직의 월별 사용량 세부사항을 표시하십시오. 이 오퍼레이션은 조직의 청구 관리자만 완료할 수 있습니다.

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

내 계정에서 조직에 대한 월별 사용량 요약을 표시하십시오.

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix security cert
{: #bluemix_security_cert}

도메인의 인증서 정보를 나열합니다.

```
bluemix security cert DOMAIN_NAME
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
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

현재 조직의 지정된 도메인에 인증서를 추가합니다.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
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
   <dt>--verify-client(선택사항)</dt>
   <dd>클라이언트 인증서 확인을 사용하는지 여부입니다. </dd>
   </dl>


<strong>예제</strong>:

인증서를 도메인 `ibmcxo-eventconnect.com`에 추가합니다.

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

현재 조직의 지정된 도메인에서 인증서를 제거합니다.

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>DOMAIN(필수)</dt>
   <dd>인증서가 제거되는 도메인입니다. </dd>
   <dt>-f(선택사항)</dt>
   <dd>확인 없이 강제 삭제합니다. </dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

{{site.data.keyword.Bluemix_notm}} CLI에 등록된 모든 플러그인 저장소를 나열합니다.

```
bluemix plugin repos
```

<strong>전제조건</strong>: 없음


### bluemix plugin repo-add
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


### bluemix plugin repo-remove
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


### bluemix plugin repo-plugins
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


### bluemix plugin list
{: #bluemix_plugin_list}

{{site.data.keyword.Bluemix_notm}} CLI에 설치된 모든 플러그인을 나열합니다.

```
bluemix plugin list
```

<strong>전제조건</strong>: 없음


### bluemix plugin install
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

`bluemix-repo` 저장소에서 최신 버전의 `container-service` 플러그인을 설치합니다.

```
bluemix plugin install container-service -r bluemix-repo
```
`bluemix-repo` 저장소에서 버전 `0.5.800`인 `container-service` 플러그인을 설치합니다.

```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
```






### bluemix plugin uninstall
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

이전에 설치한 `container-service` 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall container-service
```



# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [bx 도구 ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg)
