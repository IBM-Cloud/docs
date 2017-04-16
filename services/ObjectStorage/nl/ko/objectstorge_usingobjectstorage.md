---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 사용 시작 {: #using-object-storage}

*마지막 업데이트 날짜: 2016년 8월 13일*
{: .last-updated}


## {{site.data.keyword.objectstorageshort}} 사용자 인터페이스 사용 {: #using-object-storage-ui}

### UI 요소 및 탐색
{{site.data.keyword.objectstorageshort}}가 프로비저닝되면 {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 대시보드에서 인스턴스 정보를 볼 수 있습니다. 대시보드에서 {{site.data.keyword.objectstorageshort}} 인스턴스를 선택하여 자세한 정보가 포함된 패널을 표시하십시오.   
#### 사용량 데이터
애플리케이션의 홈 페이지에 인스턴스에 대한 스토리지 사용량 정보가 표시됩니다. 여기에는 현재 **스토리지 컨테이너** 수와 모든 컨테이너에 있는 **오브젝트** 수의 총계도 표시됩니다. 메모리 사용량(메가바이트)이 나열되어 있습니다. **이용된 스토리지**는 현재 사용되는 영역의 크기를 가리킵니다. 
#### 조치
최신 사용 데이터를 검색하려면 **새로 고치기** 단추를 클릭하십시오.    
#### 오브젝트 브라우저
오브젝트 브라우저를 사용하여 오브젝트 스토리지 컨테이너 및 오브젝트를 관리하십시오. 사용자는 기타 조치 중에서 컨테이너를 작성하고, 파일을 업로드하고, 컨테이너 및 파일을 삭제할 수 있습니다.


## {{site.data.keyword.Bluemix_notm}} 앱에서 {{site.data.keyword.objectstorageshort}} 사용 {: #using-object-storage-from-bluemix-app}

### 작성 후 {{site.data.keyword.objectstorageshort}} 서비스를 애플리케이션에 바인딩하는 방법 {: #bind-object-storage-to-application}
1.	{{site.data.keyword.Bluemix_notm}} 대시보드에서 바인딩할 앱을 선택하십시오. 
2.	앱 개요에서 **서비스 또는 API 바인드**를 클릭하십시오. 
3.	서비스 목록에서 {{site.data.keyword.objectstorageshort}} 인스턴스를 선택한 후 **추가**를 클릭하십시오. 
4.	프롬프트되면 **다시 스테이징**을 클릭하십시오. 새 서비스를 사용하려면 앱을 다시 스테이징해야 합니다.

### 바인딩된 컨텍스트

바인딩된 컨텍스트에서 {{site.data.keyword.objectstorageshort}}를 사용하려는 경우 애플리케이션 바인딩 프로세스를 통해 간접적으로 클라우드 신임 정보가 제공됩니다. 서비스 인스턴스를 애플리케이션에 바인딩한 후에는 다음 예제와 비슷한 구성이 `VCAP_SERVICES` 환경 변수에 추가됩니다. 

```
{
"Object-Storage": [
{
  "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
         "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
       }
  ]
}
```

## Swift CLI를 사용하여 {{site.data.keyword.objectstorageshort}}에 액세스 {: #using-swift-cli}

인터넷을 통하거나 IBM {{site.data.keyword.Bluemix_notm}}의 애플리케이션과 가상 서버에서 {{site.data.keyword.objectstorageshort}} 서비스에 액세스할 수 있습니다. {{site.data.keyword.objectstorageshort}} 서비스의 일반적인 유스 케이스는 다음과 같습니다. 

* 인스턴스에서 볼륨 데이터 백업
* 대량의 데이터를 전송하는 경우 중개 위치로 사용
* 직접 연결되지 않은 환경 간 데이터 전송
* 중앙 저장소 역할 수행

{{site.data.keyword.objectstorageshort}} 서비스는 OpenStack Swift를 기반으로 하며 호환 가능한 클라이언트 애플리케이션을 사용하여 서비스에 액세스할 수 있습니다. 이 절에서는 Python Swift 클라이언트({{site.data.keyword.objectstorageshort}} API와 해당 확장기능의 명령행 인터페이스(CLI))를 사용하여 컨테이너와 파일 관련 작업을 수행하는 방법을 설명합니다. 

### Swift 클라이언트 설치 {: #install-swift-client}

다음 필수 소프트웨어가 아직 설치되지 않은 경우 이를 설치하십시오. 자세한 정보는 [OpenStack 문서](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}를 참조하십시오. 
* Python 2.7 이상
* 설치 도구 패키지
* pip 패키지

다음과 같이 Python pip를 사용하여 Python Swift 클라이언트를 설치하십시오. 

```
	sudo pip install python-swiftclient
```

다음 명령을 실행하여 Python Keystone 클라이언트를 설치하십시오.

```
	sudo pip install python-keystoneclient
```

### 클라이언트 설정 {: #setup-swift-client}

Swift 클라이언트는 다음 환경 변수에서 인증 정보를 가져옵니다. 
* `OS_AUTH_URL`은 엔드포인트 URL
* `OS_USER_ID`는 사용자 이름
* `OS_PASSWORD`는 비밀번호

다음과 같이 인증 정보를 설정하십시오. 

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

{{site.data.keyword.objectstorageshort}} 사용자 인터페이스의 **서비스 신임 정보** 페이지에 {{site.data.keyword.objectstorageshort}} 서비스의 신임 정보 값이 있습니다. 

**참고:** Swift 클라이언트에 대해 환경 변수 `OS_AUTH_URL`을 구성할 때 {{site.data.keyword.objectstorageshort}} 사용자 인터페이스에서 신임 정보의 `auth_url`에 `/v3`을 추가하십시오. 


### 컨테이너에 대한 작업 {: #work-with-containers}

컨테이너 나열:
```
	swift list
```
컨테이너 작성:
```
	swift post <container_name>
```
컨테이너의 컨텐츠 나열:
```
	swift list <container_name>
```
### 오브젝트에 대한 작업 {: #work-with-objects}

#### 컨테이너에 파일 추가
```
	swift upload <container_name> <file_name>
```
#### 컨테이너에 5GB를 초과하는 파일 추가

5GB보다 큰 파일을 업로드할 경우 파일을 작은 청크로 분할해야 합니다. `-segment-size` 매개변수를 제공하여 Swift 클라이언트에서 해당 업로드를 처리하도록 지시할 수 있습니다. 
```
	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
각 세그먼트는 개별 컨테이너 `<container_name>_segments`에 병렬로 업로드됩니다. 모든 세그먼트가 업로드되면 원래 파일 이름 `<file_name>`을 사용하여 원래 컨테이너 `<container_name>`에서 하나의 파일에 세그먼트를 다운로드할 수 있도록 Swift가 Manifest 파일을 작성합니다. 예를 들어, 다음 명령은 세그먼트 크기 `1073741824`로 `test_container`라는 컨테이너에서 `large_file`이라는 파일을 업로드합니다. 
```
	swift upload test_container -S 1073741824 large_file
```
다음 명령을 실행하여 파일을 다운로드할 수 있습니다.
```
	swift download test_container large_file
```
#### 파일 다운로드
```
	swift download <container_name> <file_name>
```
#### 컨테이너에 디렉토리 추가

Swift에는 실제 디렉토리 구조가 없지만 이름을 지정하여 디렉토리 레이아웃을 표시합니다. 컨테이너에 디렉토리를 추가하려면 다음 명령을 실행하십시오.
```
	swift upload <container_name> <directory_name>
```
이 명령은 전체 디렉토리 구조를 상대 경로로 업로드합니다. 예를 들어, `/mnt/volume1`을 지정하는 경우 디렉토리 구조 mnt/volume1이 모든 파일 이름에 첨부되어 디렉토리 구조를 표시합니다.


#### 디렉토리 다운로드

디렉토리 구조를 다운로드하려면 `-prefix` 매개변수를 사용하여 다운로드하려는 디렉토리 또는 디렉토리 구조를 표시하십시오. 
```
	swift download <container_name> --prefix <directory>
```
#### 파일 삭제
```
	swift delete <container_name> <file_name>
```
### 오브젝트 버전화에 대한 작업 {: #work-with-object-versioning}

`X-Versions-Location` 플래그를 사용하여 컨테이너에서 각 오브젝트의 버전을 설정할 수 있습니다. 이를 수행하려면, 다음과 같이 추가 컨테이너를 작성하여 오브젝트의 이전 버전을 유지하십시오. 

Swift 클라이언트를 사용하는 경우 다음과 같이 설정할 수 있습니다. 
```
	swift post container_one -H "X-Versions-Location:container_two"
```
Curl을 사용 중인 경우에는 다음과 같이 설정할 수 있습니다.
```
	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one
```
예제에서는 `container_one`에 저장된 오브젝트의 이전 버전을 포함하도록 `container_two`가 설정되었습니다. 따라서, `container_one`이 오브젝트의 최신 버전을 포함하고 `container_two`는 오브젝트의 이전 버전을 포함합니다. 버전화가 작동하기 위해서는 `container_two`가 있어야 합니다. 버전화를 설정하면 `container_one`으로 오브젝트를 업로드할 때 오브젝트의 기존 버전이 있는 경우 새 버전이 `container_one`에 작성되므로 기존 버전은 `container_two`로 이동됩니다. `container_one`에서 오브젝트를 삭제하는 경우, 오브젝트의 이전 버전은 `container_two`에서 다시 `container_one`으로 이동됩니다. 

`container_two`의 오브젝트는 다음과 같은 형식으로 이름이 자동 지정됩니다. `<Length><Object_name>/<Timestamp>`.

`Length`는 오브젝트 이름의 길이를 나타냅니다. 이 값은 3자이며 0으로 채워진 16진수입니다. `Object_name`은 오브젝트의 이름입니다. `Timestamp`는 오브젝트의 이 특정 버전이 원래 업로드된 때를 나타내는 시간소인입니다.

버전화를 사용 안함으로 설정하려면, `X-Remove-Versions-Location` 플래그를 사용하십시오. 
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
또는
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one
```
다음은 버전화 사용에 대한 전체 예입니다.

1. 컨테이너 작성: 
```
		$ swift post container_one
		$
```
2. container_one에 대한 버전화 설정:
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. container_two 작성:
```
		$ swift post container_two
		$
```
4. 처음으로 오브젝트를 container_one에 업로드:
```
		$ swift upload container_one object
		object
		$
```
5. container_one의 오브젝트 나열:
```
		$ swift list container_one
		object
		$
```
6. container_two의 오브젝트 나열:
```
		$ swift list container_two
		$
```
7. 오브젝트의 새 버전을 container_one에 업로드:
```
		$ swift upload container_one object
		object
		$
```
8. container_one의 오브젝트 나열:
```
		$ swift list container_one
		object
		$
```
9. container_two의 오브젝트 나열:
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. container_one의 오브젝트 삭제:
```
		$ swift delete container_one object
		object
		$
```
11. 컨테이너 둘 다 나열:
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### 오브젝트 삭제 스케줄링 {: #schedule-object-deletion}

지정된 시간에 만료되도록 오브젝트를 설정할 수 있습니다. 즉, 오브젝트의 삭제를 스케줄링할 수 있습니다. `X-Delete-At` 또는 `X-Delete-After` 헤더 중 하나를 이용하여 이를 수행할 수 있습니다. `X-Delete-At` 헤더는 오브젝트를 삭제하는 epoch 시간을 나타내는 정수를 사용합니다. `X-Delete_After` 헤더는 오브젝트가 삭제되고 난 후의 시간(초)을 나타내는 정수를 사용합니다. 

컨테이너의 오브젝트에 게시하는 Swift 클라이언트를 사용하는 경우 다음 예를 참조하십시오. 

* 오브젝트를 "2016/04/01 08:00:00"에 삭제되도록 설정하려면, 다음 명령을 사용하십시오. 
```
		swift post -H "X-Delete-At:1459515600" container object
```
* 지금부터 1시간 안에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 
```
		swift post -H "X-Delete-After:3600" container object
```
이를 수행하고 나면, `swift stat container object` 명령은 epoch 시간으로 적절한 만기가 포함된 `X-Delete-At` 헤더를 표시합니다.

* 오브젝트에서 만기 시간을 제거하려면, 다음 명령을 사용하십시오. 
```
		swift post -H "X-Remove-Delete-After:" container object
```
cURL을 사용하는 경우 명령은 다음과 같습니다.

* 오브젝트를 "2016/04/01 08:00:00"에 삭제되도록 설정하려면, 다음 명령을 사용하십시오. 
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object
```
* 지금부터 1시간 안에 오브젝트를 삭제하도록 설정하려면, 다음 명령을 사용하십시오. 
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object
```
* 오브젝트에 헤더가 있는지 확인하려면, 다음 명령을 사용하십시오. 
```
		cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object
```
* 만기 시간을 제거하려면, 다음 명령을 사용하십시오. 
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object
```
**참고:** 표시된 정확한 시간에 오브젝트가 실제로 삭제되지 않을 수 있습니다. 그러나, 사실 오브젝트는 지정된 시간에 만기되고, 더 이상 연결할 수 없습니다. 다음 번에 Swift 클러스터에서 구성된 swift-object-expirer 디먼을 실행하면 실제로 삭제가 실행됩니다.





### 임시 URL 작성 {: #create-temporary-url}

임시 URL은 추가 인증할 필요 없이 오브젝트를 다운로드하기 위해 지정된 기간 동안 사용할 수 있는 추측하기 어려운 긴 URL입니다. 다음 단계를 수행하여 임시 URL을 생성하십시오.

1. 인증 계정을 식별하십시오.
2. 비밀 키를 설정하십시오.
3. 임시 URL을 작성하십시오.

#### 인증 계정 식별

Swift `stat` 명령은 계정에 대한 정보를 인쇄합니다. 
```
	swift stat
```
계정 필드를 찾아 *계정* 뒤에 나오는 전체 문자열(`AUTH_` 포함)을 기록해두십시오.

#### 비밀 키 설정

사용자가 선택하는 무엇이든 이 키가 될 수 있지만 우수 사례는 추측하기 어려운 긴 임의의 문자열을 선택하는 것입니다.
```
	swift post -m "Temp-URL-Key:<key>"
```
Swift `stat` 명령을 실행하여 `Temp-URL-Key`가 설정되어 있는지 확인하십시오.
```
	swift stat
```

#### 임시 URL 작성

Swift `tempurl` 명령은 이러한 위치 인수를 사용합니다. 

* [method] GET을 사용하여 다운로드합니다. PUT을 사용하여 업로드합니다. 
* [seconds] 임시 URL을 사용할 수 있는 시간(초) 
* [path] `/v1/<auth_account>/<container_name>/<object_name>`으로 표현되는 오브젝트의 전체 경로. 자세한 정보는 [{{site.data.keyword.objectstorageshort}} URL](#access-points)을 참조하십시오. 
* [key] 2단계에서 설정한 키

```
swift tempurl GET <seconds> <path> <key>
```

이 명령은 전체 URL을 가져오기 위해 클러스터 이름에 추가할 수 있는 URL을 리턴합니다. curl, wget 또는 Firefox와 같은 호환 가능한 HTTP 클라이언트를 사용하여 오브젝트를 다운로드하려면 전체 URL을 사용하십시오.

## Swift REST API를 사용하여 {{site.data.keyword.objectstorageshort}}에 액세스 {: #using-swift-restapi}

명령행 클라이언트 인터페이스(예: cURL)에서 Swift REST API를 사용하거나 애플리케이션에서 API를 호출할 수 있습니다.  

### {{site.data.keyword.objectstorageshort}} URL {: #access-points}

{{site.data.keyword.objectstorageshort}} API와 상호작용하려면 다음과 같이 {{site.data.keyword.objectstorageshort}} URL을 생성하십시오.
```
	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
```


URL은 다섯 개의 파트로 구성됩니다. `<API version>`은 v1입니다. {{site.data.keyword.objectstorageshort}} 사용자 인터페이스에서 `<project ID>`, `<container namespace>` 및 {{site.data.keyword.objectstorageshort}}의 `<object namespace>`를 찾을 수 있습니다. `<access point>`의 경우 다음 표를 참조하십시오. 


| **지역**  |   **공용 액세스 지점**                     |
|-------------|-----------------------------------------------|
| 댈러스      | https://dal.objectstorage.open.softlayer.com/ |
| 런던        | https://lon.objectstorage.open.softlayer.com/ |


*표 1. {{site.data.keyword.objectstorageshort}} 액세스 지점*


### {{site.data.keyword.objectstorageshort}} API

{{site.data.keyword.objectstorageshort}} REST API 옵션과 예제의 전체 목록은 [OpenStack Swift API 전체 참조](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}를 참조하십시오.

## 여러 지역에서 {{site.data.keyword.objectstorageshort}} 사용 {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 서비스에서는 댈러스와 런던 스토리지 지역을 지원합니다. 해당 스토리지 지역은 {{site.data.keyword.objectstorageshort}} 서비스 인스턴스가 작성되는 {{site.data.keyword.Bluemix_notm}} 지역(예: 미국 남부와 영국)에 독립적입니다. 예를 들어, {{site.data.keyword.objectstorageshort}} 인스턴스를 미국 남부 {{site.data.keyword.Bluemix_notm}} 지역에서 작성하는 경우 댈러스 또는 런던 스토리지 지역에서 데이터를 읽고 쓸 수 있습니다.  

미국 남부 {{site.data.keyword.Bluemix_notm}} 지역의 경우 댈러스 스토리지 지역이 기본입니다. 영국 {{site.data.keyword.Bluemix_notm}} 지역의 경우에는 런던 스토리지 지역이 기본입니다. {{site.data.keyword.objectstorageshort}} 사용자 인터페이스는 항상 {{site.data.keyword.Bluemix_notm}} 지역의 기본 스토리지 지역으로 시작합니다. 지역을 전환하려면 {{site.data.keyword.objectstorageshort}} 지역 드롭 다운 목록을 클릭한 후 다른 지역을 선택하십시오.

**참고:** {{site.data.keyword.objectstorageshort}} 서비스는 스토리지 지역 간 복제를 지원하지 않습니다.

### 다중 지역 액세스

{{site.data.keyword.objectstorageshort}} 서비스를 사용하려면 [OpenStack Keystone에 인증](#keystone-authentication)해야 합니다. 인증이 완료되면 응답으로 `X-Subject-Token` 및 {{site.data.keyword.objectstorageshort}} 엔드포인트를 사용할 수 있습니다. 

예를 들어, 댈러스 스토리지 지역에서 `my_container` 컨테이너를 작성하려면 다음과 같이 curl 명령에 댈러스 액세스 지점을 지정하십시오. 
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

런던 스토리지 지역에서 `my_container` 컨테이너를 작성하려면, 다음과 같이 curl 명령에 런던 액세스 지점을 지정하십시오. 
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**참고:** Keystone에서 획득한 `X-Subject-Token`은 스토리지 지역 간에 작동합니다. 다른 지역의 액세스 지점에 대한 자세한 정보는 [Object Storage 액세스 지점](#access-points) 표를 참조하십시오.


## 인증 및 신임 정보 이해 {: #understanding-authentication-credentials}

### 애플리케이션을 바인딩하지 않고 {{site.data.keyword.objectstorageshort}} 신임 정보 생성

{{site.data.keyword.Bluemix_notm}} 애플리케이션 외부에서 사용할 {{site.data.keyword.objectstorageshort}} 클라우드 신임 정보를 생성하려면 {{site.data.keyword.objectstorageshort}} 인스턴스의 서비스 키를 생성해야 합니다. 사용자 인터페이스의 사이드바에서 **서비스 신임 정보**를 선택하거나 Cloud Foundry CLI(버전 6.11.3 이상)를 사용하여 새 키를 생성할 수 있습니다. {{site.data.keyword.objectstorageshort}} 인스턴스의 서비스 키를 생성하고 검색한 후에는 클라우드 통합 정보를 통해 OpenStack SDK 또는 OpenStack Identity API를 사용하여 Keystone 토큰을 요청하고 Swift 계정을 사용하여 오브젝트를 관리할 수 있습니다.

Cloud Foundry CLI를 사용하여 키를 작성하려면 로그인한 후 다음 명령을 실행하십시오. 
 ```
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>
```
Cloud Foundry CLI에서 서비스 신임 정보를 검색하려면 다음 명령을 실행하십시오.
```
	cf service-key <object_storage_instance_name> <unique_name_for_this_key>
```

### 클라우드 프로젝트 및 사용자
새 {{site.data.keyword.objectstorageshort}} 인스턴스를 프로비저닝하면 IBM 퍼블릭 클라우드에 격리된 Keystone 프로젝트가 작성됩니다. 새 애플리케이션을 {{site.data.keyword.objectstorageshort}} 인스턴스에 바인딩하면 프로젝트에 대한 액세스 권한이 있는 새 Keystone 사용자가 작성됩니다. 인스턴스를 디프로비저닝하면 프로젝트 및 사용자가 삭제됩니다. 

### OpenStack Identity(Keystone) v3 {: #keystone-authentication}
신임 정보 구조는 사용자 애플리케이션에 최적으로 맞는 OpenStack 토큰 요청 메소드 또는 OpenStack SDK를 선택할 수 있는 전체 속성 세트를 포함합니다.

권장되는 v3 토큰 요청은 아래 curl 명령에 표시된 것처럼 다음 사이트에 대한 POST 요청입니다. https://identity.open.softlayer.com/v3/auth/tokens 
```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "K/jyIi2jR=1?D.TP"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
{{site.data.keyword.objectstorageshort}} 서비스에 요청을 작성하는 경우 응답 헤더의 `X-Subject-Token` 필드 값을 `X-Auth-Token` 필드로 사용하십시오. 예제 응답은 다음과 같습니다. {{site.data.keyword.objectstorageshort}} 관련 정보만 표시하도록 응답이 조정됩니다. 

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json
```
	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints" : [
	          {
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {},
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```

{{site.data.keyword.objectstorageshort}} URL은 서비스 카탈로그에 있습니다. 서비스 카탈로그는 토큰 요청의 응답 본문에 포함되어 있습니다. 응답은 사용 가능한 OpenStack 서비스의 전체 카탈로그입니다. `object-store` 유형의 서비스 카탈로그에서 엔드포인트를 선택하고 신임 정보의 지역 필드와 일치하는 지역을 선택하십시오. 

**참고:** 공용 인터페이스(`publicURL`)를 사용하십시오. 내부 인터페이스(`internalURL`)는 {{site.data.keyword.Bluemix_notm}}에서 액세스할 수 없습니다. 



## 세분화된 액세스 제어를 사용하여 파일 보안 {: #fine-grained-access-control}

세분화된 액세스 제어는 다중 사용자가 동일한 컨테이너에 파일을 저장하는 경우에 도움말 보안 파일을 나열합니다.

참고: 이 문서에서 설명하는 프로시저에는 Swift CLI가 필요합니다. 자세한 정보는 [Swift CLI와 함께 {{site.data.keyword.objectstorageshort}} 사용](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli)을 참조하십시오.


### 액세스 유형 {: #access-types}

서비스에 대한 액세스는 사용자 역할 및 컨테이너 액세스 제어 목록에 의해 제어됩니다. {{site.data.keyword.objectstorageshort}} 사용자는 관리자 또는 비관리자일 수 있습니다. 액세스 제어 목록은 컨테이너 레벨에서 관리자에 의해 사용될 수 있으며 서비스 인스턴스, 스토리지 계정 또는 프로젝트 레벨에 대해 사용할 수 없습니다.

<table>
  <tr>
    <th> 관리 사용자(admin) </th>
    <th> 비관리 사용자(member) </th>
  </tr>
  <tr>
    <td> 액세스 제어 관리 </td>
    <td> 기본적으로 서비스 또는 해당 컨테이너에 대한 액세스가 없음 </td>
  </tr>
  <tr>
    <td> 컨테이너를 작성하고 삭제할 수 있음 </td>
    <td> 컨테이너 읽기/쓰기 ACL을 기반으로 하여 조치를 수행할 수 있음 </td>
  </tr>
  <tr>
    <td> 컨테이너에 대해 읽고 쓸 수 있음 </td>
    <td> admin에 의해 결정된 대로 조치를 수행할 수 있음 </td>
  </tr>
</table>

*표 1: 정의된 사용자 역할*

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스, Cloud Foundry API 또는 Cloud Foundry CLI를 통해 {{site.data.keyword.objectstorageshort}} 사용자를 관리할 수 있습니다.



### {{site.data.keyword.objectstorageshort}} 서비스 신임 정보 생성 {: #generating}

새 {{site.data.keyword.Bluemix_notm}} 콘솔에서 {{site.data.keyword.objectstorageshort}} 사용자에 대한 새 서비스 신임 정보를 생성할 수 있습니다. 새 콘솔을 보려면 **새 {{site.data.keyword.Bluemix_notm}} 시도**를 클릭하십시오.

1.  개발자 역할을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 관리할 서비스 인스턴스의 영역 내에 위치해야 합니다.
2. **서비스 신임 정보** 탭을 클릭하십시오.
3. **새 신임 정보**를 클릭하십시오.
4. 신임 정보에 대한 이름을 제공하십시오.
5. **인라인 구성 매개변수 추가** 텍스트 필드에 작성할 역할에 대한 신임 정보에 관한 정보를 입력하십시오. 이 정보는 JSON 페이로드로 형식화되어야 합니다.
  - 관리 사용자 작성: `{"role":"admin"}`
  - 비관리 사용자 작성: `{"role":"member"}`
5. **추가**를 클릭하십시오.

cURL 명령 또는 Swift CLI를 사용하여 서비스 신임 정보를 생성하려면 다음 단계를 따르십시오.

1. 개발자 역할을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. 관리할 서비스 인스턴스의 영역 내에 위치해야 합니다.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```

2. 서비스 신임 정보를 생성하십시오. `service-key-name`이 신임 정보의 이름이 됩니다. Cloud Foundry 명령 또는 cURL 명령을 사용할 수 있습니다.

  Cloud Foundry 명령:
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```

  예:

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  cURL 명령:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```

3. 작성한 서비스 키에 대한 신임 정보의 유효성을 검증하십시오.

  Cloud Foundry 명령:
  ```
  cf service-key <service_key_name> <member_name>
  ```
  예:
  Object-Storage-Acl-Test라는 이름의 서비스 인스턴스에 대한 멤버 서비스 키 작성
  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  cURL 명령:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```



### 액세스 지정 {: #assigning-access}  

admin 역할을 가진 {{site.data.keyword.objectstorageshort}} 사용자만이 다른 사용자에 대한 컨테이너에 읽기 또는 쓰기 액세스를 부여할 수 있습니다. 

CLI에서 읽기 액세스를 부여하려면 `--read-acl` 또는 `-r` 옵션을 사용하십시오.

1. 사용자가 작성한 서비스 신임 정보 내에 있는 정보를 사용하여 신임 정보를 인증하십시오. 출력으로 오브젝트 스토리지 URL 및 인증 토큰을 수신합니다.

  Swift 명령:
  ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL 명령:
  ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
3. 다음 명령을 실행하여 읽기 액세스를 부여하십시오.

  Swift 명령:
  ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
4. 읽기 ACL 값을 확인하십시오.

  Swift 명령:
  ```
  swift stat <container_name>
  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
  출력 예:
  ```
  HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
  ```

읽기 ACL 조합을 조작할 수 있습니다.

<table>
  <tr>
    <th> 권한 </th>
    <th> 읽기 ACL 옵션 </th>
  </tr>
  <tr>
    <td> 계정 소속에 상관없이 모든 참조자 읽기 </td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> 모든 참조자 및 목록에 대한 읽기 및 나열 </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> 특정 프로젝트의 지정된 사용자에 대한 읽기 및 나열 </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 지정된 사용자에 대한 읽기 및 나열 </td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 읽기 및 나열 </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 읽기 및 나열 </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*표 2: 옵션별 읽기 액세스 권한*

참고: 액세스 제어 목록을 구분하려면 쉼표(,)를 사용하십시오. 예: `-read-acl project id:user_id1, project_id2:user_id2`.


쓰기 액세스를 부여하려면 Swift CLI를 통해 `--write-acl` 또는 `-w` 옵션을 사용하십시오. 

1. 사용자가 작성한 서비스 신임 정보 내에 있는 정보를 사용하여 신임 정보를 인증하십시오. 출력으로 오브젝트 스토리지 URL 및 인증 토큰을 수신합니다.

  Swift 명령:
  ```
  export OS_USER_ID="<user_id>"
  export OS_PASSWORD="<password>"
  export OS_TENANT_ID=<tenant_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL 명령:
  ```
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
2. 다음 명령을 실행하여 쓰기 액세스를 부여하십시오.

  Swift 명령:
  ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
3. 쓰기 ACL 값을 확인하십시오.

  Swift 명령:
  ```
  swift stat <container_name>
  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```


쓰기 ACL 조합을 조작할 수 있습니다.

<table>
  <tr>
    <th> 권한 </th>
    <th> 쓰기 ACL 옵션 </th>
  </tr>
  <tr>
    <td> 특정 프로젝트의 지정된 사용자에 대한 쓰기 </td>
    <td> `<project_id>:<user_id>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 지정된 사용자에 대한 쓰기 </td>  
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td> `<project_id>:<*>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*표 3: 옵션별 쓰기 액세스 권한*

참고: 액세스 제어 목록을 구분하려면 쉼표(,)를 사용하십시오. 예: `-write-acl project id:user_id1, project_id2:user_id2`.




### 액세스 제거 {: #removing-access}

컨테이너에서 읽기 ACL 제거:

  Swift 명령:
  ```
  swift post <container_name> --read-acl “”
  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

컨테이너에서 쓰기 ACL 제거:

  Swift 명령:
  ```
  swift post <container_name> --write-acl “”
  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

ACL을 제거했는지 여부 확인:

  Swift 명령:
  ```
  swift stat <container_name>
  ```

  출력 예:
  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  cURL 명령:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```




## {{site.data.keyword.objectstorageshort}} 바인드 해제 및 디프로비저닝 {: #deprovisioning-object-storage}

### {{site.data.keyword.objectstorageshort}} 서비스 디프로비저닝 방법
1.	{{site.data.keyword.Bluemix_notm}} 대시보드에서 서비스를 선택하십시오.   
2.	기어 아이콘을 클릭한 후 **서비스 삭제**를 선택하십시오. 

**주의:** IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 디프로비저닝하면 클라우드 프로젝트와 Swift 계정이 삭제됩니다. 디프로비저닝된 인스턴스의 모든 컨테이너와 오브젝트가 Swift에서 삭제되며 이를 복원할 수 없습니다.

### 애플리케이션 바인드 해제 또는 서비스 키 삭제

{{site.data.keyword.objectstorageshort}} 인스턴스에서 애플리케이션을 바인드 해제하거나 서비스 키를 삭제하면 신임 정보가 삭제됩니다. {{site.data.keyword.objectstorageshort}} 계정은 {{site.data.keyword.objectstorageshort}} 인스턴스가 디프로비저닝될 때까지 삭제되지 않습니다. [새 서비스 키를 리바인드하거나 작성하여](#bind-object-storage-to-application) 새 클라우드 신임 정보를 생성할 수 있습니다.
