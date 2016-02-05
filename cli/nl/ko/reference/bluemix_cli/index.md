{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}}와 상호작용하기 위한 bx 명령
{: #bluemix_cli}

*마지막 업데이트 날짜:* 2016년 1월 5일

{{site.data.keyword.Bluemix}} 명령행 인터페이스(CLI)는 사용자가 {{site.data.keyword.Bluemix_notm}}와 상호작용할 수 있도록 네임스페이스별로 그룹화된 명령 세트를 제공합니다. bx 명령이라 하는 일부 {{site.data.keyword.Bluemix_notm}} CLI 명령은 기존 cf 명령의 랩퍼이고, 그 외 명령은 {{site.data.keyword.Bluemix_notm}}에 고유합니다. 뒤이어 나오는 정보는 {{site.data.keyword.Bluemix_notm}} CLI에서 지원되는 모든 명령과 각 명령의 이름, 옵션, 사용법, 전제조건, 설명, 예제 등을 제공합니다.
옵션, 사용법, 전제조건, 설명과 예를 포함하는 모든 명령을 나열합니다. {:shortdesc}
 
**참고:** *전제조건*에는 명령을 사용하기 전에 필요한 조치가 설명되어 있습니다. 전제조건 조치가 없는 명령은 **없음**으로 표시됩니다. 그 밖의 경우에는 전제조건으로 다음과 같은 조치 중 하나 이상을 수행해야 할 수 있습니다.
<dl>
<dt>엔드포인트</dt>
<dd>명령을 사용하기 전에 <code>bluemix api</code>를 통해 API 엔드포인트를 설정해야 합니다.</dd>
<dt>로그인</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix login</code> 명령을 사용하여 로그인해야 합니다.</dd>
<dt>대상</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix target</code> 명령을 사용하여 조직과 영역을 설정해야 합니다.</dd>
</dl>

## bluemix help
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

`catalog` 네임스페이스의 도움말을 표시합니다.

```
bluemix help catalog
```

```
bluemix catalog help
```

`info` 명령의 도움말을 표시합니다.

```
bluemix help info
```

`catalog` 네임스페이스 아래에 있는 `templates` 명령의 도움말을 표시합니다. 

```
bluemix catalog help templates
```


## bluemix api
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
사용자가 로그인됩니다. 이 명령은 `cf login` 명령을 랩핑 처리합니다. 명령 옵션이 `cf login` 명령 옵션과 동일합니다. 

```
bluemix login [OPTIONS...]
```

**전제조건**: 엔드포인트

**명령 옵션**:
`login` 명령에 지원되는 옵션에 대한 자세한 정보는 `cf login` 명령 사용법 정보에서 애플리케이션 관리를 위한 cf 명령을 참조하십시오.


## bluemix logout
사용자가 로그아웃됩니다. 이 명령은 `cf logout` 명령을 랩핑 처리합니다. 

```
bluemix logout
```

**전제조건**: 없음


## bluemix target
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
현재 지역, 클라우드 제어기 버전, 로그인과 교환 액세스 토큰의 엔드포인트 같은 유용한 엔드포인트 등 기본 {{site.data.keyword.Bluemix_notm}} 정보를 확인합니다.

```
bluemix info
```

**전제조건**:  엔드포인트





## bluemix regions
{{site.data.keyword.Bluemix_notm}}의 모든 지역에 대한 정보를 확인합니다.

```
bluemix regions
```

**전제조건**:  엔드포인트


## bluemix region-set
지정된 지역으로 전환합니다. 이 명령은 새 지역의 동일한 조직 및 영역을 자동으로 대상으로 설정합니다(가능한 경우). 그렇지 않으면, 사용자가 이미 로그인한 상태인 경우에 한해 새 조직 및 영역을 선택하라는 메시지를 표시합니다. API 엔드포인트는 그에 맞게 변경됩니다.

```
bluemix region-set REGION_NAME
```

**전제조건**:  엔드포인트

**명령 옵션**:

*REGION_NAME* (필수):  전환하려는 지역의 이름입니다. 모든 지역 이름을 보려면 `bluemix regions` 명령을 사용합니다.

**예제**:

현재 지역을 `eu-gb`로 설정합니다.

```
bluemix region-set eu-gb
```



## bluemix config
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
원시 HTTP 요청을 {{site.data.keyword.Bluemix_notm}}에 실행합니다. *Content-Type*은 기본적으로 *application/json*으로 설정됩니다. 이 명령은 cf API 엔드포인트(예: https://api.ng.bluemix.net) 대신 {{site.data.keyword.Bluemix_notm}} 콘솔 서버(예: https://console.ng.bluemix.net)로 요청을 보냅니다. 

```
bluemix curl PATH [OPTIONS...]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*PATH*  (필수): 자원의 URL 경로입니다. 예: /rest/v2/apps.

*OPTIONS*  (선택사항): `bluemix curl` 명령에 지원되는 옵션은 `cf curl` 명령에 지원되는 옵션과 동일합니다.

**예제**:

모든 표준 유형 템플리트에 대한 정보를 검색합니다.

```
bluemix curl /rest/templates
```


## bluemix iam orgs
이 명령은 조직이 있는 지역도 표시된다는 점을 제외하고 `cf orgs` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam org
이 명령은 조직이 있는 지역이 표시된다는 점을 제외하고 `cf org` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam org-create
이 명령은 `cf create-org` 명령과 기능 및 옵션이 동일합니다.





## bluemix iam org-replicate
현재 지역의 조직을 다른 지역으로 복제합니다.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*ORG_NAME* (필수):  복제할 기존 조직의 이름입니다.

*REGION_NAME*  (필수):  복제된 조직을 호스팅하는 지역의 이름입니다.

**예제**:

`OE_Runtimes_Scaling` 조직을 `eu-gb` 지역에 복제합니다.

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














## bluemix iam org-rename
이 명령은 `cf rename-org` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam org-delete
이 명령은 `cf delete-org` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam spaces
이 명령은 `cf spaces` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space
이 명령은 `cf space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-create
이 명령은 `cf create-space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-rename
이 명령은 `cf rename-space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-delete
이 명령은 `cf delete-space` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam user-create
이 명령은 `cf create-user` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam user-delete
이 명령은 `cf delete-user` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam org-users
이 명령은 `cf org-users` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam org-role-set
이 명령은 `cf set-org-role` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam org-role-unset
이 명령은 `cf unset-org-role` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-users
이 명령은 `cf space-users` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-role-set
이 명령은 `cf set-space-role` 명령과 기능 및 옵션이 동일합니다.


## bluemix iam space-role-unset
이 명령은 `cf unset-space-role` 명령과 기능 및 옵션이 동일합니다.


## bluemix catalog templates
Bluemix에서 표준 유형 템플리트를 확인합니다.

```
bluemix catalog templates [-d]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

-d (선택사항):  `-d` 옵션을 지정하는 경우, 각 템플리트의 설명도 표시됩니다. 그렇지 않으면 각 템플리트의 ID와 이름만 표시됩니다.


## bluemix catalog template-run
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




## bluemix catalog template-register

{{site.data.keyword.Bluemix_notm}}에 새 표준 유형 템플리트를 등록합니다.

```
bluemix catalog template-register TEMPLATE_ID TEMPLATE_URL
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*TEMPLATE_ID* (필수):  새로 등록된 템플리트의 ID입니다.

*TEMPLATE_URL*  (필수):  새 템플리트의 메타데이터를 호스팅하는 URL입니다.

**예제**:

`javaHelloWorld`의 이름으로 템플리트를 작성합니다.

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

기존의 표준 유형 템플리트를 등록 취소합니다.

```
bluemix catalog template-deregister TEMPLATE_ID [-f]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*TEMPLATE_ID* (필수):  `bluemix catalog templates`를 사용하여 모든 템플리트 ID를 확인합니다.

-f  (선택사항):  확인 없이 강제 등록 취소합니다.

**예제**:

확인 없이 `javaHelloWorld` 템플리트를 등록 취소합니다.

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
{{site.data.keyword.Bluemix_notm}} 템플리트 레지스트리를 확인합니다.

```
bluemix catalog template-registry
```

**전제조건**:  엔드포인트









## bluemix catalog service-broker

지정된 서비스 브로커 정보를 확인합니다.

```
bluemix catalog service-broker SERVICE_BROKER_NAME
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*SERVICE_BROKER_NAME* (필수):  방문할 서비스 브로커의 이름입니다.


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
서비스 브로커를 작성합니다. 

```
bluemix catalog service-broker-create SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE [--no-billing]
```

**전제조건**:  엔드포인트, 로그인

**명령 옵션**:

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (필수):  작성할 새 서비스 브로커를 설명하는 JSON입니다. JSON 파일 이름을 사용하거나 JSON 텍스트를 직접 사용할 수 있습니다.

--no-billing (선택사항):  이 옵션을 지정하는 경우, 서비스 브로커에 대해 청구가 사용되지 않습니다. 

**예제**:

JSON 파일로 서비스 브로커를 작성합니다.

```
bluemix catalog service-broker-create ./broker.json
```

청구 없이 JSON 텍스트로 새 서비스 브로커를 작성합니다.

```
bluemix catalog service-broker-create '{"name":"test_broker", ...}' --no-billing
```

다음 예제는 필수 필드를 모두 포함한 서비스 브로커 JSON을 보여줍니다.

```
{
    "name": "my_broker",  // the name of service broker
    "broker_url": "http://my_broker.ng.bluemix.net"  // the URL that points to the metadata of service broker
    "auth_username": "username",
	"auth_password": "password",  // The user name and password to visit the service broker url. User name and password should be sent with HTTP basic authorization.
    "visibilities": [
        {"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
기존의 서비스 브로커를 업데이트합니다.

```
bluemix catalog service-broker-update ORIGINAL_BROKER_NAME SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE
```

**전제조건**:  엔드포인트, 로그인

**명령 옵션**:

*ORIGINAL_BROKER_NAME* (필수):  업데이트할 서비스 브로커의 이름입니다.

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (필수):  서비스 브로커를 설명하는 새 JSON입니다. JSON 파일 이름을 사용하거나 JSON 텍스트를 직접 사용할 수 있습니다.

**예제**:

기존의 서비스 브로커 `auto-scaling`을 업데이트합니다.

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

서비스 브로커 JSON 형식에 대한 자세한 정보는 [bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create)를 참조하십시오.


## bluemix catalog service-broker-delete

지정된 서비스 브로커를 삭제합니다.

```
bluemix catalog service-broker-delete SERVICE_BROKER_NAME [-f]
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*SERVICE_BROKER_NAME* (필수):  삭제할 서비스 브로커의 이름입니다.

-f  (선택사항):  확인 없이 강제 삭제합니다.

**예제**:

확인 없이 서비스 브로커 `auto-scaling`을 삭제합니다.

```
bluemix catalog service-broker-delete auto-scaling -f
```














## bluemix network routes
이 명령은 `cf routes` 명령과 기능 및 옵션이 동일합니다.


## bluemix network route-check
이 명령은 `cf check-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix network route-map
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
이 명령은 `cf create-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix network route-delete
이 명령은 `cf delete-route` 명령과 기능 및 옵션이 동일합니다.


## bluemix network orphaned-routes-delete
이 명령은 `cf delete-orphaned-routes` 명령과 기능 및 옵션이 동일합니다.


## bluemix network domains
이 명령은 `cf domains` 명령과 기능 및 옵션이 동일합니다.


## bluemix network domain-create
이 명령은 `cf create-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix network domain-delete
이 명령은 `cf delete-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix network shared-domain-create
이 명령은 `cf create-shared-domain` 명령과 기능 및 옵션이 동일합니다.


## bluemix network shared-domain-delete
이 명령은 `cf delete-shared-domain` 명령과 기능 및 옵션이 동일합니다.




## bluemix security cert

지정된 호스트에 대한 인증서 정보를 나열합니다.

```
bluemix security cert HOST_NAME
```

**전제조건**: 엔드포인트, 로그인

**명령 옵션**:

*HOST_NAME* (필수):  인증서를 호스팅하는 서버의 이름입니다.

**예제**:

호스트 `ibmcxo-eventconnect.com`에서 인증서를 확인합니다.

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

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
현재 조직의 지정된 도메인에서 인증서를 제거합니다.

```
bluemix security cert-remove DOMAIN [-f]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*DOMAIN* (필수):  인증서를 제거하는 도메인입니다.

-f  (선택사항):  확인 없이 강제 삭제합니다.








## bluemix plugin repos
{{site.data.keyword.Bluemix_notm}} CLI에 등록된 모든 플러그인 저장소를 나열합니다.

```
bluemix plugin repos
```

**전제조건**: 없음


## bluemix plugin repo-add
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


## bluemix plugin repo-plugin-list
모든 추가된 저장소 또는 특정 저장소에서 사용 가능한 모든 플러그인을 나열합니다.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**전제조건**: 없음

**명령 옵션**:

-r *REPO_NAME*  (선택사항):  지정된 저장소의 플러그인만 나열합니다.

**예제**:

모든 추가된 저장소의 플러그인을 나열합니다.

```
bluemix plugin repo-plugin-list
```

`bluemix-repo` 저장소의 모든 플러그인을 나열합니다.

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
{{site.data.keyword.Bluemix_notm}} CLI에 설치된 모든 플러그인을 나열합니다.

```
bluemix plugin list
```

**전제조건**: 없음


## bluemix plugin install
지정된 경로 또는 저장소에서 {{site.data.keyword.Bluemix_notm}} CLI에 특정 버전의 플러그인을 설치합니다.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**전제조건**:  없음

**명령 옵션**:

*PLUGIN_PATH*|*PLUGIN_NAME* (필수):  `-r *REPO_NAME*`을 지정하지 않으면 지정된 로컬 경로 또는 원격 URL에서 플러그인이 설치됩니다.

-r *REPO_NAME*  (선택사항):  플러그인 2진이 있는 저장소의 이름입니다. -v *VERSION*  (선택사항):  설치할 플러그인의 버전입니다. 값을 지정하지 않으면 최신 버전의 플러그인이 설치됩니다. 이 옵션은 저장소에서 플러그인을 설치하는 경우에만 유효합니다.

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
