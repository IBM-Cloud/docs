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

<table summary="Bluemix의 컨테이너 관리에 사용 가능한 Bluemix 명령.">
 <caption>표 7. Bluemix의 컨테이너 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">Bluemix의 컨테이너 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](index.html#bluemix_ic_service-bind)</td>
 <td>[bluemix ic service-unbind](index.html#bluemix_ic_service-unbind)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](index.html#unpause)</td>
 <td>[bluemix ic unprovision](index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
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

`ic` 플러그인의 도움말을 표시합니다.

```
bluemix help ic
```

또는

```
bluemix ic help
```

`ic` 플러그인 아래에 있는 `group-create` 명령의 도움말을 표시합니다. 

```
bluemix ic help group-create
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

`bluemix-repo` 저장소에서 최신 버전의 `IBM-Containers` 플러그인을 설치합니다.

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
`bluemix-repo` 저장소에서 버전 `0.5.800`인 `IBM-Containers` 플러그인을 설치합니다.

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
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

이전에 설치한 `IBM-Containers` 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

실행 중인 컨테이너를 제어하거나 해당 출력을 봅니다. 컨테이너를 종료하고 중지하려면 `CTRL+C`를 사용하십시오. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [attach ](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>--no-stdin(선택사항)</dt>
   <dd>표준 입력을 포함하지 않습니다. </dd>
   <dt>--sig-proxy(선택사항)</dt>
   <dd>수신된 모든 신호를 프로세스에 프록시합니다. 기본값은 <i>true</i>입니다. </dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
    </dl>

<strong>예제</strong>:

다음 예제는 `my_container` 컨테이너에 접속하기 위한 요청을 보여줍니다. 
```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

IBM Containers 빌드 서비스를 호출하여 로컬에 또는 사설 {{site.data.keyword.Bluemix_notm}} 저장소에 Docker 이미지를 빌드합니다. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [build ](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i>(필수)</dt>
   <dd>작성되는 이미지에 적용되는 저장소 이름입니다. </dd>
   <dt>--no-cache(선택사항)</dt>
   <dd>이미지가 빌드될 때 캐시를 사용하지 않습니다. 기본값은 <i>false</i>입니다.</dd>
   <dt>--pull(선택사항)</dt>
   <dd>캐시된 경우에도 레지스트리에서 기본 이미지를 가져오려고 시도합니다.</dd>
   <dt>-q|--quiet(선택사항)</dt>
   <dd>컨테이너에 의해 생성되는 상세 출력을 억제합니다. 기본값은 <i>false</i>입니다.</dd>
   <dt><i>DOCKERFILE_LOCATION</i>(필수)</dt>
   <dd>로컬 호스트의 Dockerfile 및 컨텍스트에 대한 경로입니다. </dd>
    </dl>

<strong>예제</strong>:

다음 예제는 이름이 *myimage*인 이미지를 빌드하기 위한 요청을 보여줍니다. 빌드에 사용할 Dockerfile 및 기타 아티팩트는 명령이 실행되는 디렉토리와 동일한 디렉토리에 있습니다. 레지스트리 및 네임스페이스가 이미지 이름과 함께 포함되기 때문에 이미지는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 빌드됩니다. 
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


### bluemix ic cp
{: #bluemix_ic_cp}
컨테이너와 로컬 파일 시스템 간에 파일 또는 폴더를 복사합니다. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [cp ](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 


### bluemix ic cpi
{: #bluemix_ic_cpi}

Docker 허브 이미지 또는 로컬 레지스트리의 이미지에 액세스하여 해당 이미지를 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 복사합니다.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i>(필수)</dt>
   <dd>소스 저장소 및 이미지 이름입니다. </dd>
   <dt><i>DESTINATION_IMAGE</i>(필수)</dt>
   <dd>개인용 {{site.data.keyword.Bluemix_notm}} 저장소 URL이며, 여기에는 네임스페이스 및 대상 이미지 이름이 포함됩니다. 이미지의 태그는 선택사항입니다. </dd>
   </dl>

<strong>예제</strong>:

소스 저장소의 이미지를 개인용 저장소에 복사하고 해당 이미지의 태그를 추가합니다.

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

`training` 저장소의 `sinatra` 이미지를 개인용 저장소 `registry.ng.bluemix.net/mynamespace`로 복사하고 이 이미지의 이름을 `mysinatra`로 지정합니다. `mysinatra` 이미지에 대한 `v1` 태그를 추가합니다.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

컨테이너에서 명령을 실행합니다. 자세한 정보는 Docker 도움말에서 [exec ](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-d|--detach(선택사항)</dt>
   <dd>백그라운드에서 지정된 명령을 실행합니다. </dd>
   <dt>-it(선택사항)</dt>
   <dd>대화식 모드입니다. 표준 입력이 계속 표시되도록 합니다. 종료하려면 <i>exit</i>를 입력하십시오.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i>(선택사항)</dt>
   <dd>사용자 이름입니다. </dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   <dt><i>CMD</i>(선택사항)</dt>
   <dd>지정된 컨테이너 내에서 실행할 명령입니다. </dd>
   </dl>

<strong>예제</strong>:

대화식 모드로 `my_container` 컨테이너에서 `bash` 명령을 실행합니다.

```
bluemix ic exec -it my_container bash
```

`my_container` 컨테이너에서 `date` 명령을 실행합니다.

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

확장 가능한 컨테이너 그룹을 작성합니다.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i>(필수)</dt>
   <dd>컨테이너 그룹의 각 컨테이너 인스턴스에 포함되는 이미지입니다. 이미지 뒤에 명령을 나열할 수 있지만 이미지 뒤에 옵션을 두지 마십시오. 이미지를 지정하기 전에 모든 옵션을 포함시키십시오.<br><br>조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 이미지를 사용하는 경우, <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i> 형식으로 이미지를 지정하십시오.<br><br>IBM Containers에서 제공하는 이미지를 사용하는 경우 조직의 네임스페이스를 포함시키지 마십시오. <i>registry.ng.bluemix.net/IMAGE</i> 형식으로 이미지를 지정하십시오.</dd>
   <dt>--name <i>GROUP_NAME</i>(필수)</dt>
   <dd>그룹에 이름을 지정합니다. <i>-n</i>은 더 이상 사용되지 않습니다.<br>
   <strong>팁:</strong> 컨테이너 이름은 문자로 시작해야 합니다. 이름에는 대문자, 소문자, 숫자, 마침표 ".", 밑줄 "_" 또는 하이픈 "-"이 포함될 수 있습니다. </dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i>(선택사항)</dt>
   <dd>그룹에 MB 단위의 메모리 한계를 지정합니다. CLI에서 컨테이너 그룹을 작성하는 경우, 각 컨테이너 인스턴스에 대한 기본값은 <i>64</i>MB입니다. {{site.data.keyword.Bluemix_notm}} 대시보드에서 컨테이너 그룹을 작성하는 경우, 각 컨테이너 인스턴스에 대한 기본값은 <i>256</i>MB입니다. 허용 값은 <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> 및 <i>2048</i>입니다. 메모리 한계가 지정된 후에는 값을 변경할 수 없습니다.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i>(선택사항)</dt>
   <dd>호스트 이름입니다(예: <i>mycontainerhost</i>). 호스트 및 도메인은 결합되어 전체 공용 라우트 URL(예: <i>http://mycontainerhost.mybluemix.net</i>)을 구성합니다. <i>bluemix ic group-inspect</i> 명령으로 컨테이너 그룹의 세부사항을 검토하면 호스트 및 도메인이 라우트로 함께 나열됩니다.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>(선택사항)</dt>
   <dd>일반적으로, 도메인은 <i>.mybluemix.net</i>입니다. 호스트와 도메인은 결합되어 전체 공용 라우트 URL(예: <i>http://mycontainerhost.mybluemix.net</i>)을 형성합니다. <i>bluemix ic group-inspect</i> 명령으로 컨테이너 그룹의 세부사항을 검토하면 호스트 및 도메인이 라우트로 함께 나열됩니다.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i>(선택사항)</dt>
   <dd>환경 변수를 설정하십시오.여러 키를 개별적으로 나열하십시오. 따옴표를 사용하는 경우 환경 변수와 값을 함께 따옴표로 묶으십시오. 예: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  다음 표에서는 지정 가능한 공통으로 사용되는 일부 환경 변수를 보여줍니다.</dd>
    </dl>


|  환경 변수                              |     설명                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 컨테이너에 서비스를 바인드합니다. `CCS_BIND_APP` 환경 변수를 사용하여 앱을 컨테이너에 바인드하십시오. 앱은 대상 서비스에 바인드되어 브릿지 역할을 하며, 이 브릿지를 통해 {{site.data.keyword.Bluemix_notm}}는 사용자 브릿지 앱의 `VCAP_SERVICES` 정보를 실행 중인 컨테이너 인스턴스로 가져올 수 있습니다. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 브릿지 앱을 사용하지 않고 컨테이너에 직접 Bluemix 서비스를 바인드하려면 CCS_BIND_SRV를 사용하십시오. 이 바인딩을 통해 Bluemix가 실행 중인 컨테이너 인스턴스에 VCAP_SERVICES 정보를 삽입할 수 있습니다. 여러 Bluemix 서비스를 표시하려면 동일한 환경 변수의 일부로 Bluemix 서비스를 포함시키십시오. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 컨테이너에서 모니터링할 로그 파일을 추가합니다. `LOG_LOCATIONS` 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. |
{: caption="표 8. 공통으로 사용되는 환경 변수" caption-side="top"}


 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i>(선택사항)</dt>
   <dd> 파일에서 환경 변수를 가져오며 여기서 ENVFILE은 로컬 디렉토리에 있는 파일의 경로입니다. 파일의 모든 행은 하나의 키=값 쌍을 나타냅니다. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (선택사항)</dt>
   <dd><i>VolumeId:ContainerPath[:ro]</i> 형식의 세부사항을 지정하여 컨테이너에 볼륨을 첨부합니다.
   <ul>
   <li><i>VOLUME</i>: 볼륨 ID 또는 이름입니다.</li>
   <li><i>CONTAINER_PATH</i>: 컨테이너의 볼륨에 대한 절대 경로입니다. </li>
   <li>ro: 선택사항입니다. <i>ro</i>를 지정하면 기본값 "읽기/쓰기"가 아닌 "읽기 전용"으로 볼륨이 설정됩니다. </li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>(선택사항)</dt>
   <dd>HTTP 트래픽에 대한 포트를 공개합니다. 그룹의 컨테이너는 HTTP 포트를 청취해야 합니다. HTTPS 요청은 작성할 수 없습니다. 컨테이너 그룹의 경우 여러 포트를 포함시킬 수 없습니다.<br><br>포트를 지정하면 호스트에 도달하려고 하는 동일한 {{site.data.keyword.Bluemix_notm}} 영역에 있는 {{site.data.keyword.Bluemix_notm}} 로드 밸런서 또는 컨테이너에서 해당 앱을 사용할 수 있습니다. 그리고 {{site.data.keyword.Bluemix_notm}} 로드 밸런서 또는 컨테이너는 해당 포트를 사용하여 동일한 {{site.data.keyword.Bluemix_notm}} 영역의 앱 및 호스트에 접속할 수 있습니다. Dockerfile에 사용 중인 이미지에 대해 포트가 지정되어 있으면 해당 포트를 포함시키십시오.<br>
   <strong>팁</strong>: <ul>
   <li>IBM 인증 Liberty 서버 이미지 또는 이 이미지의 수정된 버전의 경우 포트 9080을 입력하십시오.</li>
   <li>IBM 인증 Node.js 이미지 또는 이 이미지의 수정된 버전의 경우 포트 8000을 입력하십시오.</li>
   </ul>
   </dd>
   <dt>-P(선택사항)</dt>
   <dd>모든 포트를 공개합니다. </dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i>(선택사항)</dt>
   <dd>최소 인스턴스 수입니다. 기본값은 1입니다. 최소 인스턴스 수를 설정하는 경우, 컨테이너 그룹이 작성된 후에는 해당 값을 변경할 수 없습니다.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i>(선택사항)</dt>
   <dd>최대 인스턴스 수입니다. 기본값은 2입니다. 최대 인스턴스 수를 설정하는 경우, 컨테이너 그룹이 작성된 후에는 해당 값을 변경할 수 없습니다.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>(선택사항)</dt>
   <dd>필요한 인스턴스 수입니다. 기본값은 2입니다.</dd>
   <dt>--auto(선택사항)</dt>
   <dd>컨테이너 그룹이 작성되고 자동 복구가 사용되는 경우, IBM Containers는 지정된 포트에 대한 HTTP 요청으로 각 인스턴스의 상태를 확인합니다. <br>
   두 개의 후속 90초 간격에서 컨테이너 인스턴스로부터 응답이 수신되지 않으면 해당 인스턴스가 제거되고 새 인스턴스로 바뀝니다. 컨테이너가 응답하면 아무 조치도 수행되지 않습니다. 이 프로세스는 계속해서 반복됩니다. 30분 창 동안 그룹의 멤버인 서로 다른 컨테이너의 총 수가 해당 그룹의 관찰된 최대 크기의 3배보다 크거나 같으면 해당 컨테이너 그룹에 대해 자동 복구가 영구적으로 사용되지 않습니다. 자동 복구를 다시 사용하려면 컨테이너 그룹을 다시 작성해야 합니다.</dd>
  <dt>--anti(선택사항)</dt>
  <dd> 컨테이너 그룹의 가용성을 높이려면 anti-affinity를 사용하십시오. --anti 옵션은 사용자 그룹의 모든 컨테이너 인스턴스를 별도의 실제 컴퓨팅 노드에 배치하여 하드웨어 장애로 인해 그룹의 모든 컨테이너가 충돌하는 경우가 줄어들도록 강제 실행합니다. 각 Bluemix 지역과 조직에서 배치에 사용할 수 있는 컴퓨팅 노드의 세트는 제한되어 있으므로 그룹 크기가 큰 경우 이 옵션을 사용하지 못할 수 있습니다. 배치에 성공하지 못한 경우에는 그룹의 컨테이너 인스턴스 수를 줄이거나 --anti 옵션을 제거하십시오. </dd>
   <dt><i>CMD</i>(선택사항)</dt>
   <dd>실행할 컨테이너 그룹에 전달되는 명령 및 인수입니다. 이 명령은 장시간 실행되는 명령이어야 합니다. 단시간 실행되는 명령(예: <i>/bin/date</i>)은 컨테이너 충돌을 유발할 수 있으므로 사용하지 마십시오.<br> <strong>참고:</strong> <ul>
   <li>명령 및 해당 인수는 <i>bluemix ic run</i> 명령행의 끝에 와야 합니다.</li>
   <li>앞의 예제 명령의 <i>-c</i>에서와 같이 명령 인수에 하이픈 "-"이 이 포함되면, 명령 앞에 두 개의 하이픈 "--"이 있어야 합니다. </li>
   </ul></dd>
   </dl>


<strong>예제</strong>:

IBM Containers에서 제공하는 `registry.ng.bluemix.net/ibmnode` 이미지를 사용하여 컨테이너 그룹 `my_container_group`을 작성한 후 해당 컨테이너 그룹에 대해 `ping localhost` 장시간 실행 명령을 실행합니다.

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

IBM Containers에서 제공하는 `registry.ng.bluemix.net/ibmnode` 이미지를 사용하여 컨테이너 그룹 `my_container_group`을 작성한 후 해당 컨테이너 그룹에 대해 `tail -f /dev/null` 장시간 실행 명령을 실행합니다.

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

`registry.ng.bluemix.net/ibmliberty` 이미지를 사용하여 자동 복구가 사용되는 확장 가능한 그룹 `mygroup`을 작성합니다. 포트는 `9080`이고 호스트 이름은 `mycontainerhost`이며 도메인 이름은 `mybluemix.net`입니다. 
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

컨테이너 그룹을 작성할 때 컨테이너 그룹에 대해 지정한 자세한 정보(예: 환경 변수, 포트 또는 메모리)를 봅니다.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i>(필수)</dt>
   <dd>컨테이너 그룹 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `my_group` 컨테이너 그룹을 검사하기 위한 요청을 보여줍니다. 
```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

지정된 컨테이너 그룹의 인스턴스를 나열합니다.

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i>(필수)</dt>
   <dd>컨테이너 그룹 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

`my_group` 컨테이너 그룹의 모든 인스턴스를 나열합니다. 
```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

영역에서 컨테이너 그룹을 제거합니다.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>-f|--force(선택사항)</dt>
   <dd>실행 중이거나 실패한 컨테이너를 강제 제거합니다. </dd>
   <dt><i>GROUP_NAME</i>(필수)</dt>
   <dd>컨테이너 그룹 ID 또는 이름입니다. </dd>
   </dl>


<strong>예제</strong>:

다음 예제는 컨테이너 그룹을 제거하기 위한 요청을 보여줍니다. 여기서 `my_group`은 컨테이너 그룹의 이름입니다. 
```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

컨테이너 그룹을 작성합니다.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**팁:** 컨테이너 그룹의 호스트 이름 또는 도메인을 업데이트하려면 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`을 사용하십시오.

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:
 <dl>
   <dt>--anti(선택사항)</dt>
   <dd>컨테이너 그룹의 가용성을 높이려면 anti-affinity를 사용하십시오. --anti 옵션은 사용자 그룹의 모든 컨테이너 인스턴스를 별도의 실제 컴퓨팅 노드에 배치하여 하드웨어 장애로 인해 그룹의 모든 컨테이너가 충돌하는 가능성이 줄어들도록 강제 실행합니다. 각 Bluemix 지역과 조직에서 배치에 사용할 수 있는 컴퓨팅 노드의 세트는 제한되어 있으므로 그룹 크기가 큰 경우 이 옵션을 사용하지 못할 수 있습니다. 배치에 성공하지 못한 경우에는 그룹의 컨테이너 인스턴스 수를 줄이거나 --anti 옵션을 제거하십시오. </dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>(선택사항)</dt>
   <dd>필요한 인스턴스 수입니다. 기본값은 <i>2</i>입니다. </dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(선택사항)</dt>
   <dd>환경 변수를 설정하십시오.여러 키를 개별적으로 나열하십시오. 따옴표를 사용하는 경우 환경 변수와 값을 함께 따옴표로 묶으십시오. 예: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  </dd>
   <dt><i>GROUP_NAME</i>(필수)</dt>
   <dd>컨테이너 그룹 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `my_group` 컨테이너 그룹을 업데이트하기 위한 요청을 보여줍니다. 
```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 컨테이너 그룹을 나열합니다.

```
bluemix ic groups [-q]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:
	<dl>
	<dt>-q(선택사항)</dt>
   	<dd>그룹 ID만 표시합니다. </dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 사용 가능한 모든 이미지 목록을 봅니다. 자세한 정보는 Docker 도움말에서 [images ](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 목록에는 이미지 ID, 작성된 날짜 및 이미지 이름이 포함됩니다.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-a|--all(선택사항)</dt>
   <dd>최근의 계층뿐만 아니라, 조직의 저장소에 있는 각 이미지의 모든 이미지 계층을 포함합니다. </dd>
   <dt>-f(선택사항)</dt>
   <dd>제공된 조건으로 이미지의 목록을 필터링합니다.</dd>
   <dt>--no-trunc(선택사항)</dt>
   <dd>출력을 자르지 않습니다. </dd>
   <dt>-q|--quiet(선택사항)</dt>
   <dd>숫자 ID만 표시합니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 조직의 사용 가능한 이미지 목록을 수신하기 위한 요청을 보여줍니다. 
```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

컨테이너 클라우드 서비스 인스턴스의 상태를 설명하는 정보 세트를 봅니다. 정보에는 컨테이너 한계, 컨테이너 사용량, 실행 중인 컨테이너, 메모리 한계, 메모리 사용량, 유동 IP 주소 한계, 유동 IP 주소 사용량, CCS 호스트 URL, 레지스트리 호스트 URL 및 디버그 모드 상태가 포함됩니다.

```
bluemix ic info
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


### bluemix ic init
{: #bluemix_ic_init}

IBM Containers 서비스의 전체 기능을 사용하기 위해 로컬 시스템의 컨테이너 환경을 초기화합니다.

```
bluemix ic init
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

**참고:** 초기화 전에 Docker CLI(docker)가 설치되어 있고 PATH 환경 변수에 구성되어 있는지 확인하십시오. 다른 지역으로 전환하려면 `bluemix region-set` 명령을 사용하십시오.

<strong>예제</strong>:

`us-south` 지역으로 전환합니다.

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

컨테이너에 대한 정보를 봅니다. 자세한 정보는 Docker 도움말에서 [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} 명령을 참조하십시오.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>IMAGE</i>(필수)</dt>
   <dd>이미지 이름 또는 ID를 지정하여 특정 이미지에 대한 자세한 정보를 봅니다.</dd>
   <dt>images(필수)</dt>
   <dd>저장소에 있는 모든 이미지에 대한 자세한 정보를 봅니다.</dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID를 지정하여 특정 컨테이너에 대한 자세한 정보를 봅니다. </dd>
   </dl>

**팁:** 한 번에 *IMAGE*, *images* 또는 *CONTAINER* 중 하나만 지정할 수 있습니다. 

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너를 검사하기 위한 요청을 보여줍니다. 
```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

사용 가능한 유동 IP 주소를 컨테이너에 바인딩합니다. 

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i>(필수)</dt>
   <dd>바인드되는 IP 주소입니다.</dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>바인드되는 컨테이너 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 IP 주소 `192.123.12.12`를 `proxy` 컨테이너로 바인드하기 위한 요청을 보여줍니다. 
```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

컨테이너 클라우드 서비스 인스턴스에서 유동 IP 주소를 릴리스합니다. 

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i>(필수)</dt>
   <dd>릴리스할 IP 주소입니다.</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
새 유동 IP 주소를 요청합니다.

```
bluemix ic ip-request [-q]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>-q(선택사항)</dt>
   <dd>해당 IP 주소에 바인딩된 컨테이너의 ID 없이 IP 주소만 나열합니다. </dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

컨테이너에서 유동 IP 주소를 바인드 해제합니다. 

공인 IP 주소는 IBM Containers에서 제한된 리소스입니다. 따라서, 영역에 할당되었지만 컨테이너에 바인드되지 않은 공인 IP 주소는 무료 평가판 사용자로부터 주기적으로(대략 주 단위로) 재확보됩니다. 종량과금제 또는 구독 고객으로부터는 바인드되지 않은 공인 IP 주소가 재확보되지 않습니다.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i>(필수)</dt>
   <dd>언바인드되는 IP 주소입니다.</dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>언바인드되는 컨테이너 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 IP 주소 `192.123.12.12`를 `proxy` 컨테이너에서 바인드 해제하기 위한 요청을 보여줍니다. 
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

로그인한 사용자의 사용 가능한 유동 IP 주소를 나열합니다. 목록에는 IP 주소와 해당 IP 주소가 링크된 컨테이너 ID가 포함됩니다. IP 주소가 사용되지 않는 경우에는 컨테이너 ID가 표시되지 않습니다.

```
bluemix ic ips [-q]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>-q(선택사항)</dt>
   <dd>해당 IP 주소에 바인딩된 컨테이너의 ID 없이 IP 주소만 나열합니다. </dd>
   </dl>


<strong>예제</strong>:

다음 예제는 조직의 모든 IP 주소 목록을 수신하기 위한 요청을 보여줍니다. 
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

컨테이너를 중지하지 않고 컨테이너에서 실행 중인 프로세스를 중지합니다. 자세한 정보는 Docker 도움말에서 [kill ](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i>(선택사항)</dt>
   <dd>컨테이너에서 실행 중인 프로세스에 명령을 전송합니다. </dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 ID 또는 이름입니다. </dd>
   </dl>


<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너의 프로세스를 강제 종료하기 위한 요청을 보여줍니다. 
```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

실행 중인 컨테이너의 출력 또는 오류 로그를 표시합니다. 자세한 정보는 Docker 도움말에서 [logs ](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

로그인하는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 이미지 저장소의 이름을 확인합니다.

```
bluemix ic namespace-get
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

로그인하는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 이미지 저장소의 이름을 설정합니다.

*제한사항*: 저장소 네임스페이스의 이름에 하이픈(`-`)을 사용할 수 없습니다.

```
bluemix ic namespace-set NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>NAME</i>(필수)</dt>
   <dd>아직 설정되지 않은 경우, 조직의 저장소 네임스페이스를 설정하는 일회성 기능입니다. 네임스페이스를 설정한 후에는 계속하기 전에 `bluemix ic init` 명령을 사용하여 IBM Containers를 다시 초기화하십시오.</dd>
   </dl>


### bluemix ic pause
{: #pause}

실행 중인 컨테이너 내의 모든 프로세스를 일시정지합니다. 자세한 정보는 Docker 도움말에서 [pause ](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 컨테이너를 중지하려면 [bluemix ic unpause](#unpause) 명령을 참조하십시오.

```
bluemix ic pause CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:
   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>

<strong>응답</strong>:

- 컨테이너가 일시정지되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너를 일시정지하기 위한 요청을 보여줍니다. 
```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

컨테이너의 포트 맵핑 또는 특정 맵핑을 나열합니다. 이 명령은 `docker port` 명령을 랩핑합니다. 자세한 정보는 Docker 도움말에서 [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 


### bluemix ic ps
{: #bluemix_ic_ps}
로그인한 사용자의 네임스페이스에서 실행 중인 컨테이너 목록을 봅니다. 기본적으로 이 명령은 실행 중인 컨테이너만 표시합니다. 자세한 정보는 Docker 도움말에서 [ps ](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-a|--all(선택사항)</dt>
   <dd>모든 컨테이너(실행 중 및 중지된 컨테이너 모두)를 표시합니다. </dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i>(선택사항)</dt>
   <dd>특정 환경 변수 값이 있는 컨테이너를 검색합니다. 컨테이너를 검사할 때 CLI 응답의 Env 섹션에 표시된 환경 변수 키 또는 값으로 컨테이너를 필터링할 수 있습니다. SEARCH_CRITERIA를 검색 중인 키 또는 값으로 대체합니다. 검색 기준이 정확하게 일치할 필요는 없습니다.</dd>
   <dt>-s|--size(선택사항)</dt>
   <dd>컨테이너의 크기를 나열합니다. </dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i>(선택사항)</dt>
   <dd>가장 최근에 작성된 컨테이너를 나열합니다. 여기서 <i>NUM</i>은 리턴하고자 하는 가장 최근에 작성된 컨테이너의 수입니다. <br><br> 예를 들어, 컨테이너 <i>node1</i>에서 <i>node5</i>까지 순차적으로 작성한 경우에 <i>bluemix ic ps --limit 2</i> 명령은 "node4" 및 "node5"를 리턴합니다. 이는 마지막으로 작성된 두 개의 컨테이너이기 때문입니다. </dd>
   <dt>-q|--quiet(선택사항)</dt>
   <dd>컨테이너 ID만 표시합니다. </dd>
   </dl>


<strong>예제</strong>:

다음 예제는 실행 중인 컨테이너와 중지된 컨테이너를 모두 표시하기 위한 요청을 보여줍니다. 
```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
컨테이너의 이름을 바꿉니다. 자세한 정보는 Docker 도움말에서 [rename ](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

<dl>
   <dt><i>OLD_NAME</i>(필수)</dt>
   <dd>컨테이너의 이전 이름입니다. </dd>
   <dt><i>NEW_NAME</i>(필수)</dt>
   <dd>컨테이너의 새 이름입니다. </dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

로그인한 Bluemix 영역에서 IBM Containers 서비스를 다시 작성합니다. 영역의 원래 할당량은 유지보수됩니다. 

<strong>중요</strong>: 이 명령을 실행할 때 이 영역에 있는 단일 컨테이너와 그룹은 다시 프로비저닝된 영역으로 마이그레이션되지 않고 마이그레이션 프로세스 중에 제거됩니다. 

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>명령 옵션</strong>:

   <dl>
   <dt>--force|-f(선택사항)</dt>
   <dd>Bluemix 영역에서 IBM Containers 서비스를 다시 작성하도록 강제 실행합니다. </dd>
   <dt><i>AVAILABILITY_ZONE</i>(선택사항)</dt>
   <dd>컨테이너가 배치된 IBM Containers 가용성 구역의 이름입니다. 가용성 구역이 지정되지 않으면 지역에 설정된 기본 가용성 구역이 사용됩니다. </dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

컨테이너를 다시 시작합니다. 자세한 정보는 Docker 도움말에서 [restart ](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>(선택사항)</dt>
   <dd>컨테이너가 다시 시작될 때까지 대기하는 시간(초)입니다. </dd>
   </dl>


<strong>응답</strong>:

- 컨테이너가 다시 시작되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너를 다시 시작하기 위한 요청을 보여줍니다. 
```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

컨테이너를 제거합니다. 자세한 정보는 Docker 도움말에서 [rm ](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-f|--force(선택사항)</dt>
   <dd>실행 중이거나 실패한 컨테이너를 강제 제거합니다. </dd>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>

<strong>응답</strong>:

- 컨테이너가 제거되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너를 제거하기 위한 요청을 보여줍니다. 
```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

로그인한 사용자의 네임스페이스에서 이미지를 제거합니다. 자세한 정보는 Docker 도움말에서 [rmi ](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i>(선택사항)</dt>
   <dd>레지스트리 호스트를 변경합니다. 기본값은 <i>bluemix ic init</i> 명령에 지정한 레지스트리를 사용하는 것입니다.</dd>
   <dt><i>IMAGE</i>(필수)</dt>
   <dd>제거하려는 이미지의 이름입니다. 이미지 이름에 태그가 지정되지 않은 경우 <i>latest</i>라는 태그가 지정된 이미지가 기본적으로 삭제됩니다. </dd>
   </dl>

<strong>응답</strong>:

- 제거됨: `{IMAGE}`

 여기서 `{IMAGE}`는 제거된 이미지의 이름입니다. 

- 오류! 지정된 레지스트리 호스트가 없습니다.

- 이미지 제거 실패 - 컨테이너 클라우드 레지스트리에 연결할 수 없습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

<strong>예제</strong>:

다음 예제는 `mynamespace/myimage:latest` 이미지를 제거하기 위한 요청을 보여줍니다. 
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

컨테이너 그룹에 액세스하는 데 사용할 인터넷 트래픽에 대한 라우트를 설정합니다. 이 명령을 사용하여 새 라우트를 설정하거나 기존 라우트를 업데이트할 수 있습니다.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>(선택사항)</dt>
   <dd>라우트의 호스트 이름입니다. 호스트 이름은 전체 공용 라우트 URL의 첫 번째 파트입니다(예: URL <i>mycontainerhost.mybluemix.net</i>의 <i>mycontainerhost</i>).</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>(선택사항)</dt>
   <dd>라우트의 도메인 이름이며, 이는 전체 공용 라우트 URL의 두 번째 파트입니다. 대부분의 경우, 도메인은 <i>mybluemix.net</i>입니다. 이 매개변수를 사용하여 개인용 도메인을 지정할 수도 있습니다. </dd>
   <dt><i>CONTAINER_GROUP</i>(필수)</dt>
   <dd>컨테이너 그룹 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `GROUP1`이라는 그룹의 라우트를 맵핑하기 위한 요청을 보여줍니다. 여기서 `my_host`는 호스트 이름이고 `mybluemix.net`은 도메인입니다. 
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

컨테이너 그룹에 액세스하는 데 사용할 인터넷 트래픽에 대한 라우트를 설정합니다. 이 명령을 사용하여 새 라우트를 설정하거나 기존 라우트를 업데이트할 수 있습니다.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>(선택사항)</dt>
   <dd>라우트의 호스트 이름입니다. </dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>(선택사항)</dt>
   <dd>라우트의 도메인 이름입니다. </dd>
   <dt><i>CONTAINER_GROUP</i>(필수)</dt>
   <dd>컨테이너 그룹 ID 또는 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `GROUP1`이라는 그룹의 라우트를 맵핑 해제하기 위한 요청을 보여줍니다. 여기서 `my_host`는 호스트 이름이고 `organization.com`은 도메인입니다. 
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


### bluemix ic run
{: #bluemix_ic_run}

이미지 이름에서 생성된 컨테이너 클라우드 서비스에서 새 컨테이너를 시작합니다. 자세한 정보는 Docker 도움말에서 [run ](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**참고:** Cloud Foundry 명령 도구가 설치되어 있으며 Cloud Foundry 토큰이 있는지 확인하십시오. `bluemix login` 및 `bluemix ic init`를 사용하여 성공적으로 로그인하면 필수 토큰 및 인증서가 생성됩니다.


<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>(선택사항)</dt>
   <dd>HTTP 트래픽에 대한 포트를 공개합니다. Dockerfile에 사용 중인 이미지에 대해 지정된 모든 포트가 포함됩니다. 여러 <i>-p</i> 옵션을 사용하여 여러 포트를 포함시킬 수 있습니다. 포트를 공개하면 공인 IP 주소가 사용 가능한 경우 컨테이너에 공인 IP 주소가 자동으로 바인드됩니다.<br><br>컨테이너에 바인드할 기존 IP 주소가 영역에 있는 경우, 이 IP 주소를 나중에 바인드하는 대신 지정할 수 있습니다. IP 주소는 &lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br> 형식으로 지정해야 합니다.<br>영역의 IP 주소 요청에 대한 자세한 정보는 <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> 명령을 참조하십시오.<br><br>포트를 지정하면 호스트에 도달하려고 하는 동일한 {{site.data.keyword.Bluemix_notm}} 영역에 있는 {{site.data.keyword.Bluemix_notm}} 로드 밸런서 또는 컨테이너에서 해당 앱을 사용할 수 있습니다. Dockerfile에 사용 중인 이미지에 대해 포트가 지정되어 있으면 해당 포트를 포함시키십시오.<br><br><strong>팁:</strong><ul><li>IBM 인증 Liberty 서버 이미지 또는 이 이미지의 수정된 버전의 경우 포트 9080을 입력하십시오.</li><li>IBM 인증 Node.js 이미지 또는 이 이미지의 수정된 버전의 경우 포트 8000을 입력하십시오.</li></ul></dd>
   <dt>-P(선택사항)</dt>
   <dd>HTTP 트래픽에 대해 이미지의 Dockerfile에 지정된 포트를 자동으로 공개합니다. </dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i>(선택사항)</dt>
   <dd>그룹에 MB 단위의 메모리 한계를 지정합니다. CLI에서 컨테이너 그룹을 작성하는 경우, 각 컨테이너 인스턴스에 대한 기본값은 64MB입니다. {{site.data.keyword.Bluemix_notm}} 대시보드에서 컨테이너 그룹을 작성하는 경우, 각 인스턴스에 대한 기본값은 256MB입니다. 허용되는 값은 64, 256, 512, 1024 및 2048입니다. 메모리 한계가 지정된 후에는 값을 변경할 수 없습니다.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i>(선택사항)</dt>
   <dd>환경 변수를 설정합니다. 여기서 <i>ENV</i>는 "key=value" 쌍입니다. 여러 키를 개별적으로 나열하십시오. 따옴표를 사용하는 경우 환경 변수와 값을 함께 따옴표로 묶으십시오. 예: -e "key1=value1" -e "key2=value2" -e "key3=value3". 다음 표에서는 지정 가능한 공통으로 사용되는 일부 환경 변수를 보여줍니다.</dd>
   </dl>


|      환경 변수                          |   설명                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 컨테이너에 서비스를 바인드합니다. `CCS_BIND_APP` 환경 변수를 사용하여 앱을 컨테이너에 바인드하십시오. 앱은 대상 서비스에 바인드되어 브릿지 역할을 하며, 이 브릿지를 통해 {{site.data.keyword.Bluemix_notm}}는 사용자 브릿지 앱의 `VCAP_SERVICES` 정보를 실행 중인 컨테이너 인스턴스로 가져올 수 있습니다. 브릿지 앱 작성에 대한 자세한 정보는 [컨테이너에 서비스 바인딩](/docs/containers/container_integrations_binding.html){: new_window}을 참조하십시오. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 브릿지 앱을 사용하지 않고 컨테이너에 직접 Bluemix 서비스를 바인드하려면 CCS_BIND_SRV를 사용하십시오. 이 바인딩을 통해 Bluemix가 실행 중인 컨테이너 인스턴스에 VCAP_SERVICES 정보를 삽입할 수 있습니다. 여러 Bluemix 서비스를 표시하려면 동일한 환경 변수의 일부로 Bluemix 서비스를 포함시키십시오. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 컨테이너에서 모니터링할 로그 파일을 추가합니다. `LOG_LOCATIONS` 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. |
{: caption="표 9. 공통으로 사용되는 환경 변수" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (선택사항)</dt>
   <dd><i>VolumeId:ContainerPath[:ro]</i> 형식의 세부사항을 지정하여 컨테이너에 볼륨을 첨부합니다.
   <ul>
   <li><i>VOLUME</i>: 볼륨 ID 또는 이름입니다.</li>
   <li><i>CONTAINER_PATH</i>: 컨테이너의 볼륨에 대한 절대 경로입니다. </li>
   <li>ro: 선택사항입니다. <i>ro</i>를 지정하면 기본값 "읽기/쓰기"가 아닌 "읽기 전용"으로 볼륨이 설정됩니다. </li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i>(필수)</dt>
   <dd>컨테이너에 이름을 지정합니다. <br> <strong>팁:</strong> 컨테이너 이름은 문자로 시작해야 합니다. 이름에는 대문자, 소문자, 숫자, 마침표 ".", 밑줄 "_" 또는 하이픈 "-"이 포함될 수 있습니다. </dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i>(선택사항)</dt>
   <dd>컨테이너가 실행 중인 다른 컨테이너와 통신하도록 하려는 경우, 호스트 이름의 별명을 사용하여 이를 처리할 수 있습니다. </dd>
   <dt>-it(선택사항)</dt>
   <dd>대화식 모드로 컨테이너를 실행합니다. 컨테이너가 작성된 후 표준 입력이 계속 표시되도록 합니다. 종료하려면 <i>exit</i>를 입력하십시오.</dd>
   <dt><i>IMAGE</i>(필수)</dt>
   <dd>컨테이너에 포함되는 이미지입니다. 이미지 뒤에 명령을 나열할 수 있지만 이미지 뒤에 옵션을 두지 마십시오. 이미지를 지정하기 전에 모든 옵션을 포함시키십시오.이미지를 지정하기 전에 모든 옵션을 포함시키십시오.<br><br>조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 이미지를 사용하는 경우, <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i> 형식으로 이미지를 지정하십시오.<br><br>IBM Containers에서 제공하는 이미지를 사용하는 경우, <i>registry.ng.bluemix.net/IMAGE</i> 형식으로 이미지를 지정하십시오.</dd>
   <dt><i>CMD</i>(선택사항)</dt>
   <dd>실행할 컨테이너 그룹에 전달되는 명령 및 인수입니다. 이 명령은 장시간 실행되는 명령이어야 합니다. 단시간 실행되는 명령(예: <i>/bin/date</i>)은 컨테이너 충돌을 유발할 수 있으므로 사용하지 마십시오.</dd>
   </dl>


<strong>예제</strong>:

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


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

실행 중인 컨테이너 그룹에 서비스를 추가합니다. 이 명령은 컨테이너 그룹에만 사용할 수 있습니다. 단일 컨테이너는 bluemix ic run 명령의 일부로 서비스를 바인드해야 합니다. 

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE 
```
<strong>명령 옵션</strong>:

   <dl>
   <dt><i>GROUP_NAME</i>(필수)</dt>
   <dd>그룹 ID 또는 이름입니다. </dd>
   <dt><i>SERVICE_INSTANCE</i>(필수)</dt>
   <dd>컨테이너 그룹에 추가할 서비스 인스턴스의 이름입니다. </dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

실행 중인 컨테이너 그룹에서 서비스를 제거합니다. 이 명령은 컨테이너 그룹에만 사용할 수 있습니다. 단일 컨테이너는 컨테이너를 제거하고 서비스가 없는 새 컨테이너를 작성해야 합니다. 

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE 
```
<strong>명령 옵션</strong>:

   <dl>
   <dt><i>GROUP_NAME</i>(필수)</dt>
   <dd>그룹 ID 또는 이름입니다. </dd>
   <dt><i>SERVICE_INSTANCE</i>(필수)</dt>
   <dd>컨테이너 그룹에 추가할 서비스 인스턴스의 이름입니다. </dd>
   </dl>


### bluemix ic start
{: #ic_start}
중지된 컨테이너를 시작합니다. 자세한 정보는 Docker 도움말에서 [start ](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 컨테이너를 중지하려면 [bluemix ic stop](#ic_stop) 명령을 참조하십시오.

```
bluemix ic start CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>


<strong>응답</strong>:

- 컨테이너가 시작되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너를 시작하기 위한 요청을 보여줍니다. 
```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

하나 이상의 컨테이너에 대해 실시간 사용량 통계를 봅니다. 종료하려면 `CTRL+C`를 사용하십시오. 자세한 정보는 Docker 도움말에서 [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} 명령을 참조하십시오.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   <dt>--no-stream(선택사항)</dt>
   <dd>최근 결과만 표시하고 그 이전의 정보는 포함하지 않습니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 컨테이너에 대한 가장 최근의 통계를 얻기 위한 요청을 보여줍니다. 
```
bluemix ic stats --no-stream my_container
```


### bluemix ic stop
{: #ic_stop}
실행 중인 컨테이너를 중지합니다. 자세한 정보는 Docker 도움말에서 [stop ](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 컨테이너를 시작하려면 [bluemix ic start](#ic_start) 명령을 참조하십시오.

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>(선택사항)</dt>
   <dd>컨테이너가 강제 종료될 때까지 대기하는 시간(초)입니다. </dd>
   </dl>

<strong>응답</strong>:

- 컨테이너가 중지되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너를 중지하기 위한 요청을 보여줍니다. 
```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

컨테이너에서 실행 중인 프로세스를 표시합니다. 자세한 정보는 Docker 도움말에서 [top ](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `my_container`라는 컨테이너의 프로세스를 표시하기 위한 요청을 보여줍니다. 
```
bluemix ic top my_container
```


### bluemix ic unpause
{: #unpause}

실행 중인 컨테이너 내에 있는 모든 프로세스의 일시정지를 해제합니다. 자세한 정보는 Docker 도움말에서 [unpause ](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 컨테이너를 일시정지하려면 [bluemix ic pause](#pause) 명령을 참조하십시오.

```
bluemix ic unpause CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>

<strong>응답</strong>:

- 컨테이너의 일시정지가 해제되었습니다.

- 컨테이너 클라우드 서비스에서 명령이 실패했습니다.

 `{message}`

 여기서 `{message}`는 관련 오류입니다. 

- 명령 실패 - 컨테이너 클라우드 서비스에 연결할 수 없습니다.

<strong>예제</strong>:

다음 예제는 `proxy`라는 컨테이너의 일시정지를 해제하기 위한 요청을 보여줍니다. 
```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

사용자가 로그인한 Bluemix 영역에서 IBM Containers 서비스를 삭제합니다. 

<strong>주의</strong>: 이 명령을 실행하면 모든 단일 컨테이너와 컨테이너 그룹이 유실됩니다. 사용자의 영역은 여전히 Bluemix에서 사용할 수 있습니다. IBM Containers를 다시 사용하려면 `bluemix ic reprovision`을 실행하여 IBM Containers 서비스를 다시 프로비저닝해야 합니다. 

```
bluemix ic reprovision [--force|-f] 
```
<strong>명령 옵션</strong>:

   <dl>
   <dt>--force|-f(선택사항)</dt>
   <dd>Bluemix 영역에서 Bluemix의 삭제를 강제 실행합니다. </dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

Docker의 버전 및 IBM Containers API를 표시합니다.

```
bluemix ic version
```

<strong>전제조건</strong>:  Docker

IBM Containers의 버전을 확인하려면 `bluemix ic info`를 실행하십시오. 자세한 정보는 [version ](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

볼륨을 작성합니다.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>FS_NAME</i>(선택사항)</dt>
   <dd>파일 공유 이름입니다. 파일 공유가 사용 가능하거나 이름이 지정되지 않으면 볼륨이 영역의 기본 파일 공유로 빌드됩니다.</dd>
   <dt><i>VOLUME_NAME</i>(필수)</dt>
   <dd>볼륨 이름입니다. 이름에는 소문자, 숫자, 밑줄 "_" 및 하이픈 "-"이 포함될 수 있습니다. </dd>
   </dl>


<strong>예제</strong>:

다음 예제는 볼륨을 작성하기 위한 요청을 보여줍니다. 
```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

파일 공유를 표시합니다.

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

파일 공유를 작성합니다.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i>(필수)</dt>
   <dd>파일 공유 이름입니다. 이름에는 소문자, 숫자, 밑줄 "_" 및 하이픈 "-"이 포함될 수 있습니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 파일 공유 작성 요청을 표시합니다. 
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

모든 파일 공유 특성을 나열합니다.

```
bluemix ic volume-fs-flavors
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

파일 공유를 검사합니다.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i>(필수)</dt>
   <dd>파일 공유 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 파일 공유 검사 요청입니다. 여기서 `my_file_share`는 파일 공유의 이름입니다.
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

파일 공유를 제거합니다.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i>(필수)</dt>
   <dd>파일 공유 이름입니다. </dd>
   </dl>

<strong>예제</strong>:

다음 예제는 파일 공유 제거 요청을 표시합니다. 여기서 `my_file_share`는 파일 공유의 이름입니다. 
```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

볼륨을 검사합니다.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i>(필수)</dt>
   <dd>볼륨 이름입니다.</dd>
   </dl>

<strong>예제</strong>:

다음 예제는 볼륨을 검사하기 위한 요청입니다. 여기서 `volume_name`은 볼륨의 이름입니다. 
```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

볼륨을 제거합니다.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i>(필수)</dt>
   <dd>볼륨 이름입니다.</dd>
    </dl>

<strong>예제</strong>:

다음 예제는 볼륨을 제거하기 위한 요청입니다. 여기서 `volume_name`은 볼륨의 이름입니다. 
```
bluemix ic volume-remove volume_name
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

볼륨을 나열합니다.

```
bluemix ic volumes
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


### bluemix ic wait
{: #bluemix_ic_wait}

컨테이너를 종료하고 확인으로 종료 코드를 표시합니다. 자세한 정보는 Docker 도움말에서 [wait ](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg) 명령을 참조하십시오. 

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `my_container`라는 컨테이너를 종료하기 위한 요청을 보여줍니다. 
```
bluemix ic wait my_container
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

단일 컨테이너 또는 컨테이너 그룹이 일시적이지 않은 상태에 도달하도록 대기합니다. 이 대기 시간 동안 명령행은 리턴하지 않으며 사용자는 명령을 입력할 수 없습니다. 컨테이너가 일시적이지 않은 상태에 도달하는 즉시 확인 메시지가 표시됩니다. 단일 컨테이너에서 일시적이지 않은 상태는 실행 중, 시스템 종료, 충돌, 일시정지 또는 일시중단입니다. 컨테이너 그룹의 경우 일시적이지 않은 상태는 CREATE_COMPLETE, UPDATE_COMPLETE 또는 FAILED입니다. 

```
bluemix ic wait-status CONTAINER
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상, Docker

<strong>명령 옵션</strong>:

   <dl>
   <dt><i>CONTAINER</i>(필수)</dt>
   <dd>컨테이너 이름 또는 ID입니다.</dd>
   </dl>

<strong>예제</strong>:

다음 예제는 `my_container`라는 컨테이너를 종료하기 위한 요청을 보여줍니다. 
```
bluemix ic wait my_container
```



# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [bx 도구 ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![외부 링크 아이콘](../../../icons/launch-glyph.svg)
