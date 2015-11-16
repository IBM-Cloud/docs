{:shortdesc: .shortdesc}

# bluemix 명령
{: #bluemix_cli}

*마지막 업데이트 날짜:* 2015년 10월 19일

Bluemix 명령행 인터페이스(CLI)는 사용자가 Bluemix와 상호작용할 수 있도록 네임스페이스별로 그룹화된 명령 세트를 제공합니다. 일부 Bluemix 명령은 기존 cf 명령의 랩퍼이며 나머지 일부는 Bluemix의 고유한 명령입니다. 다음 정보는 Bluemix CLI에 의해 지원되는 모든 명령을 나열하며 이름, 옵션, 사용법, 전제조건, 설명 및 예제를 포함합니다.
{:shortdesc}
 
**참고:** *전제조건*은 명령을 사용하기 전에 필요한 조치를 나열합니다. 전제조건 조치가 없는 명령에는 **없음**이 나열됩니다. 그렇지 않으면 전제조건에 다음 조치 중 하나 이상이 포함될 수 있습니다.
<dl>
<dt>**엔드포인트**</dt>
<dd>명령을 사용하기 전에 API 엔드포인트가 `bluemix api`를 통해 설정되어야 합니다.</dd>
<dt>**로그인**</dt>
<dd>이 명령을 사용하기 전에 `bluemix login` 명령을 사용하여 로그인해야 합니다.</dd>
<dt>**대상**</dt>
<dd>이 명령을 사용하기 전에 조직 및 영역을 설정하기 위해 `bluemix target` 명령이 사용되어야 합니다.</dd>
</dl>

## bluemix help
첫 번째 레벨의 기본 제공 명령 및 Bluemix CLI의 지원되는 네임스페이스에 대한 일반 도움말 또는 특정 기본 제공 명령 또는 네임스페이스에 대한 도움말을 표시합니다.

```
Bluemix 도움말 [COMMAND|NAMESPACE]
```

**전제조건**:  없음

**명령 옵션**:

*COMMAND*|*NAMESPACE*(선택적): 도움말이 표시되는 대상 명령 또는 네임스페이스입니다. 지정되지 않으면 Bluemix CLI에 대한 일반 도움말이 표시됩니다.

**예제**:

Bluemix CLI에 대한 일반 도움말 표시:

```
bluemix help
```

`catalog` 네임스페이스에 대한 도움말 표시:

```
bluemix help catalog
```

```
bluemix catalog help
```

`info` 명령에 대한 도움말 표시:

```
bluemix help info
```

`catalog` 네임스페이스 아래의 `templates` 명령에 대한 도움말 표시:

```
bluemix catalog help templates
```


## bluemix api
Bluemix API 엔드포인트를 설정하거나 봅니다. 이 명령은 `cf api` 명령을 랩핑합니다.

```
bluemix api [API_ENDPOINT][--unset]
```

**전제조건**:  없음

**명령 옵션**:

*API_ENDPOINT*(선택적): 대상이 되는 API 엔드포인트이며 예를 들어, https://api.ng.bluemix.net입니다. *API_ENDPOINT* 및 `–unset` 옵션이 둘 다 지정되지 않으면 현재 API 엔드포인트가 표시됩니다.

`--unset`(선택적): API 엔드포인트 설정을 제거합니다.

**예제**:

api.ng.bluemix.net에 대한 API 엔드포인트 설정:

```
bluemix api api.ng.bluemix.net
```

현재 API 엔드포인트 보기:

```
bluemix api
```

API 엔드포인트를 설정하지 않음:

```
bluemix api --unset
```


## bluemix login
사용자를 로그인합니다. 이 명령은 `cf login` 명령을 랩핑합니다.명령 옵션은 `cf login` 명령 옵션과 동일합니다.

```
bluemix login [OPTIONS...]
```

**전제조건**:  엔드포인트

**명령 옵션**:
`login` 명령에서 지원되는 옵션에 대한 정보는 `cf login` 명령 사용 정보에서 애플리케이션 관리에 필요한 cf 명령을 참조하십시오.


## bluemix logout
사용자를 로그아웃합니다. 이 명령은 `cf logout` 명령을 랩핑합니다.

```
bluemix logout
```

**전제조건**:  없음


## bluemix target
대상 조직 또는 영역을 설정하거나 봅니다. 이 명령은 `cf target` 명령을 랩핑합니다.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**전제조건**:  엔드포인트, 로그인

**명령 옵션**:

-o *ORG_NAME*(선택적):  대상이 되는 조직의 이름입니다.

-s *SPACE_NAME*(선택적):  대상이 되는 영역의 이름입니다.

-o *ORG_NAME* 또는 -s *SPACE_NAME*이 지정되지 않은 경우, 현재 조직 및 영역이 표시됩니다.

**예제**:

현재 조직을 'MyOrg'로, 영역을 'MySpace'로 설정:

```
bluemix target -o MyOrg -s MySpace
```

현재 조직 및 영역 보기:

```
bluemix target
```


## bluemix info
현재 영역, 클라우드 제어기 버전, 일부 유용한 엔드포인트(로그인용 엔드포인트 등) 및 액세스 토큰 교환 등을 포함하는 기본 Bluemix 정보를 봅니다.

```
bluemix info
```

**전제조건**:  엔드포인트


## bluemix list
현재 영역 내의 cf 애플리케이션, 컨테이너 그룹 및 VM 그룹을 모두 나열합니다.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**전제조건**:  엔드포인트, 로그인, 대상

**명령 옵션**:

apps(선택적):  애플리케이션 정보만 표시합니다.

containers(선택적):  컨테이너 정보만 표시합니다.

container-groups(선택적):  컨테이너 그룹 정보만 표시합니다.

vm-groups(선택적):  VM 그룹 정보만 표시합니다.

한 번에 'apps', 'containers', 'container-groups' 또는 'vm-groups' 중 하나만 지정할 수 있습니다. 아무것도 지정하지 않으면 모든 cf 앱, 컨테이너, 그룹 및 VM 그룹이 나열됩니다.

**예제**:

모든 cf 애플리케이션 나열:

```
bluemix list apps
```

모든 컨테이너 인스턴스 나열:

```
bluemix list containers
```

모든 앱, 컨테이너, 컨테이너 그룹 및 VM 그룹 나열:

```
bluemix list
```


## bluemix scale
cf 애플리케이션 또는 컨테이너 그룹을 지정된 인스턴스 개수, 디스크 할당량 및 메모리 크기로 스케일 축소하거나 스케일 확장합니다.

**참고:** 컨테이너 그룹 스케일링에는 인스턴스 수만 지정할 수 있습니다. 옵션을 지정하지 않으면 이 명령이 컨테이너 그룹에 대한 현재 인스턴스 개수를 나열하고 cf 애플리케이션에 대한 디스크 할당량 및 메모리 크기도 나열합니다.

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**전제조건**:  엔드포인트, 로그인, 대상

**명령 옵션**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*(필수):  스케일링할 cf 애플리케이션 또는 컨테이너 그룹의 이름입니다.

-i *INSTANCE_COUNT*(선택적):  스케일링할 cf 애플리케이션 또는 컨테이너 그룹에 대한 새 인스턴스 수입니다. 이 선택사항은 스케일링할 컨테이너 그룹에 대해서만 유효한 옵션입니다.

-k *DISK_QUOTA*(선택적):  cf 애플리케이션의 새 디스크 할당량입니다. 컨테이너 그룹 스케일링에는 유효하지 않습니다.

-m *MEMORY_SIZE*(선택적):  cf 애플리케이션의 새 메모리 크기입니다. 컨테이너 그룹 스케일링에는 유효하지 않습니다.

**예제**:

'my-container-group'에 대한 현재 인스턴스 수 표시:

```
bluemix scale my-container-group
```

'my-container-group'을 2 인스턴스로 스케일링:

```
bluemix scale my-container-group -i 2
```

'my-java-app'을 3 인스턴스, 8G 디스크 할당량 및 1024M 메모리 크기로 스케일링:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Bluemix에 대한 원시 HTTP 요청을 실행합니다. "Content-Type"은 기본적으로 "application/json"으로 설정됩니다. 이 명령은 cf API 엔드포인트(예: https://api.ng.bluemix.net) 대신 Bluemix 콘솔 서버(예: https://console.ng.bluemix.net)에 요청을 전송합니다.

```
bluemix curl PATH [OPTIONS...]
```

**전제조건**:  엔드포인트, 로그인

**명령 옵션**:

*PATH*(필수):  자원의 URL 경로입니다. 예를 들어, /rest/v2/apps입니다.

*OPTIONS*(선택적):  'bluemix curl' 명령에 의해 지원되는 옵션은 'cf curl' 명령에 의해 지원되는 옵션과 동일합니다.

**예제**:

모든 표준 유형 템플리트에 대한 정보 검색:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
이 명령의 기능 및 옵션은 'cf orgs' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org
이 명령의 기능 및 옵션은 'cf org' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org-create
이 명령의 기능 및 옵션은 'cf create-org' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org-rename
이 명령의 기능 및 옵션은 'cf rename-org' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org-delete
이 명령의 기능 및 옵션은 'cf delete-org' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam spaces
이 명령의 기능 및 옵션은 'cf spaces' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space
이 명령의 기능 및 옵션은 'cf space' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space-create
이 명령의 기능 및 옵션은 'cf create-space' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space-rename
이 명령의 기능 및 옵션은 'cf rename-space' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space-delete
이 명령의 기능 및 옵션은 'cf delete-space' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam user-create
이 명령의 기능 및 옵션은 'cf create-user' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam user-delete
이 명령의 기능 및 옵션은 'cf delete-user' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org-users
이 명령의 기능 및 옵션은 'cf org-users' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org-role-set
이 명령의 기능 및 옵션은 'cf set-org-role' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam org-role-unset
이 명령의 기능 및 옵션은 'cf unset-org-role' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space-users
이 명령의 기능 및 옵션은 'cf space-users' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space-role-set
이 명령의 기능 및 옵션은 'cf set-space-role' 명령의 기능 및 옵션과 동일합니다.


## bluemix iam space-role-unset
이 명령의 기능 및 옵션은 'cf unset-space-role' 명령의 기능 및 옵션과 동일합니다.


## bluemix catalog templates
Bluemix에서 표준 유형 템플리트를 봅니다.

```
bluemix catalog templates [-d]
```

**전제조건**:  엔드포인트, 로그인

**명령 옵션**:

-d(선택적):  '-d' 옵션이 지정되면 각 템플리트에 대한 설명도 표시됩니다. 그렇지 않으면 각 템플리트의 ID 및 이름만 표시됩니다.


## bluemix catalog template-run
지정된 URL 및 설명이 있는 지정된 템플리트를 기반으로 하는 cf 애플리케이션의 작성입니다. 기본적으로 새 앱이 자동으로 시작됩니다.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**전제조건**:  엔드포인트, 로그인, 대상

**명령 옵션**:

*TEMPLATE_ID*(필수):  애플리케이션이 작성될 때 애플리케이션의 기반이 되는 템플리트입니다. 모든 템플리트의 ID를 보려면 'bluemix templates'를 사용하십시오.

*CF_APP_NAME*(필수):  작성될 cf 애플리케이션의 이름입니다.

-u *URL*(선택적):  애플리케이션의 라우트입니다. 지정되지 않은 경우, 사용자의 앱 이름 및 기본 도메인을 기반으로 하여 Bluemix에 의해 자동으로 라우트가 지정됩니다.

-d *DESCRIPTION*(선택적):  애플리케이션에 대한 설명입니다.

--no-start(선택적):  애플리케이션이 작성된 후에 애플리케이션을 자동으로 시작하지 않습니다. 지정되지 않은 경우, 애플리케이션이 작성된 후에 자동으로 시작됩니다.

**예제**:

'javaHelloWorld' 템플리트를 기반으로 하여 cf 애플리케이션 'my-app' 작성:

```
bluemix catalog template-run javaHelloWorld my-app
```

'myrubyapp.ng.bluemix.net' 라우트 및 'My first ruby app on Bluemix' 설명이 있는 'rubyHelloWorld' 템플리트를 기반으로 하여 'my-ruby-app' 애플리케이션 작성:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on Bluemix."
```

자동 시작 없이 'pythonHelloWorld' 템플리트를 기반으로 하여 'my-python-app' 애플리케이션 작성:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Bluemix의 모든 지역에 대한 정보를 봅니다.

```
bluemix network regions
```

**전제조건**:  엔드포인트


## bluemix network region-set
지정된 지역으로 전환합니다. 이 명령은 가능하면 새 지역의 동일한 조직 및 영역으로 자동으로 대상을 다시 지정합니다. 또는 사용자가 이미 로그인한 경우에는 사용자가 새 조직 및 영역을 선택하도록 프롬프트합니다. API 엔드포인트가 이에 따라 변경됩니다.

```
bluemix network region-set REGION_NAME
```

**전제조건**:  엔드포인트

**명령 옵션**:

*REGION_NAME*(필수):  전환할 지역의 이름입니다. 'bluemix regions' 명령을 사용하면 모든 지역 이름을 볼 수 있습니다.

**예제**:

현재 지역을 'eu-gb'로 설정:

```
bluemix network region-set eu-gb
```


## bluemix network routes
이 명령의 기능 및 옵션은 'cf routes' 명령의 기능 및 옵션과 동일합니다.


## bluemix network route-check
이 명령의 기능 및 옵션은 'cf check-route' 명령의 기능 및 옵션과 동일합니다.


## bluemix network route-map
라우트를 지정된 도메인 및 호스트 이름이 있는 기존 cf 애플리케이션 또는 컨테이너 그룹에 맵핑합니다.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**전제조건**:  엔드포인트, 로그인, 대상

**명령 옵션**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*(필수):  라우트와 맵핑될 cf 애플리케이션 또는 컨테이너 그룹의 이름입니다.

*DOMAIN*(필수):  라우트의 도메인입니다. 예를 들어, mybluemix.net 또는 ng.bluemix.net입니다. 

-n *HOST_NAME*(선택적):  라우트의 호스트 이름입니다. 제공되지 않은 경우, 호스트 이름이 기본적으로 앱 이름 또는 컨테이너 그룹 이름으로 설정됩니다.

**예제**:

라우트를 지정된 도메인이 있는 'my-app'에 맵핑:

```
bluemix network route-map my-app mybluemix.net
```

라우트를 지정된 도메인 및 호스트 이름이 있는 'my-container-group'에 맵핑:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
지정된 라우트를 기존 cf 애플리케이션 또는 컨테이너 그룹에서 맵핑 해제합니다.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**전제조건**:  엔드포인트, 로그인, 대상

**명령 옵션**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*(필수):  cf 애플리케이션 또는 컨테이너 그룹의 이름입니다.

*DOMAIN*(필수):  라우트의 도메인입니다. 예를 들어, mybluemix.net 또는 ng.bluemix.net입니다. 

-n *HOST_NAME*(선택적):  라우트의 호스트 이름입니다. 제공되지 않은 경우, 호스트 이름이 기본적으로 앱 이름 또는 컨테이너 그룹 이름으로 설정됩니다.

**예제**:

'my-app.mybluemix.net'을 'my-app'에서 맵핑 해제:

```
bluemix network route-unmap my-app mybluemix.net
```

'abc.ng.bluexmix.net'을 'my-container-group'에서 맵핑 해제:

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
이 명령의 기능 및 옵션은 'cf create-route' 명령의 기능 및 옵션과 동일합니다.


## bluemix network route-delete
이 명령의 기능 및 옵션은 'cf delete-route' 명령의 기능 및 옵션과 동일합니다.


## bluemix network orphaned-routes-delete
이 명령의 기능 및 옵션은 'cf delete-orphaned-routes' 명령의 기능 및 옵션과 동일합니다.


## bluemix network domains
이 명령의 기능 및 옵션은 'cf domains' 명령의 기능 및 옵션과 동일합니다.


## bluemix network domain-create
이 명령의 기능 및 옵션은 'cf create-domain' 명령의 기능 및 옵션과 동일합니다.


## bluemix network domain-delete
이 명령의 기능 및 옵션은 'cf delete-domain' 명령의 기능 및 옵션과 동일합니다.


## bluemix network shared-domain-create
이 명령의 기능 및 옵션은 'cf create-shared-domain' 명령의 기능 및 옵션과 동일합니다.


## bluemix network shared-domain-delete
이 명령의 기능 및 옵션은 'cf delete-shared-domain' 명령의 기능 및 옵션과 동일합니다.


## bluemix plugin repos
Bluemix CLI에 등록된 모든 플러그인 저장소를 나열합니다.

```
bluemix plugin repos
```

**전제조건**:  없음


## bluemix plugin repo-add
새 플러그인 저장소를 Bluemix CLI에 추가합니다.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**전제조건**:  없음

**명령 옵션**:

*REPO_NAME*(필수):  추가할 저장소의 이름입니다. 각 저장소에 대해 직접 이름을 정의할 수 있습니다.

*REPO_URL*(필수):  추가할 저장소의 URL입니다. 저장소 URL에 프로토콜(예: http://plugins.ng.bluemix.net instead of plugins.ng.bluemix.net)이 포함되어야 합니다. http://plugins.ng.bluemix.net은 Bluemix CLI의 공식 플러그인 저장소입니다.

**예제**:

Bluemix CLI의 공식 플러그인 저장소를 'bluemix-repo'로 추가:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Bluemix CLI에서 플러그인 저장소를 제거합니다.

```
bluemix plugin repo-remove REPO_NAME
```

**전제조건**:  없음

**명령 옵션**:

*REPO_NAME*(필수):  제거할 저장소의 이름입니다.

**예제**:

Bluemix CLI에서 'bluemix-repo' 저장소 제거:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
추가된 모든 저장소 또는 특정 저장소 내의 사용 가능한 모든 플러그인을 나열합니다.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**전제조건**:  없음

**명령 옵션**:

-r *REPO_NAME*(선택적):  지정된 저장소의 플러그인만 나열합니다.

**예제**:

추가된 모든 저장소 내의 모든 플러그인 나열:

```
bluemix plugin repo-plugin-list
```

'bluemix-repo' 저장소 내의 모든 플러그인 나열:

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Bluemix CLI에 설치된 모든 플러그인을 나열합니다.

```
bluemix plugin list
```

**전제조건**:  없음


## bluemix plugin install
지정된 경로 또는 저장소로부터 Bluemix CLI에 플러그인을 설치합니다.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**전제조건**:  없음

**명령 옵션**:

*PLUGIN_PATH*|*PLUGIN_NAME*(필수):  '-r *REPO_NAME*'이 지정되지 않으면 지정된 로컬 경로 또는 원격 URL에서 플러그인이 설치됩니다.

-r *REPO_NAME*(선택적):  플러그인 2진이 위치한 저장소의 이름입니다.

**예제**:

로컬 파일에서 플러그인 설치:

```
bluemix plugin install /downloads/new_plugin
```

원격 URL에서 플러그인 설치:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

'bluemix-repo' 저장소에서 'IBM-Containers' 플러그인 설치:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Bluemix CLI에서 지정된 플러그인을 설치 제거합니다.

```
bluemix plugin uninstall PLUGIN_NAME
```

**전제조건**:  없음

**명령 옵션**:

*PLUGIN_NAME*(필수):  설치 제거할 플러그인의 이름입니다.

**예제**:

이전에 설치된 'IBM-Containers' 플러그인 설치 제거:

```
bluemix plugin uninstall IBM-Containers
```
