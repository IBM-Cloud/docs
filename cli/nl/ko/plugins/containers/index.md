---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Containers CLI
{: #containercli}

*버전:* 1.0.0

IBM Containers CLI는 Bluemix에서 컨테이너와 컨테이너 그룹을 관리할 수 있는 {{site.data.keyword.Bluemix_notm}} CLI 플러그인입니다.
{: shortdesc}

**참고:** *전제조건*에는 명령을 사용하기 전에 필요한 조치가 설명되어 있습니다. 전제조건 조치가 없는 명령은 **없음**으로 표시됩니다. 그 밖의 경우에는 전제조건으로 다음과 같은 조치 중 하나 이상을 수행해야 할 수 있습니다.
<dl>
<dt>엔드포인트</dt>
<dd>명령을 사용하기 전에 <code>bluemix api</code>를 통해 API 엔드포인트를 설정해야 합니다.</dd>
<dt>로그인</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix login</code> 명령을 사용하여 로그인해야 합니다. 연합된 ID로 로그인하는 경우 '--sso' 옵션을 사용하여 일회성 패스코드로 인증하십시오.</dd>
<dt>대상</dt>
<dd>이 명령을 사용하기 전에 <code>bluemix target</code> 명령을 사용하여 조직과 영역을 설정해야 합니다.</dd>
<dt>Docker</dt>
<dd>Docker CLI(docker)는 IBM Containers CLI 플러그인에서 명령을 실행해야 합니다.</dd>
</dl>

<table summary="Bluemix의 컨테이너 관리에 사용 가능한 Bluemix 명령.">
 <caption>표 1. Bluemix의 컨테이너 관리를 위한 명령</caption>
 <thead>
 <th colspan="5">Bluemix의 컨테이너 관리를 위한 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

실행 중인 컨테이너를 제어하거나 해당 출력을 봅니다. 컨테이너를 종료하고 중지하려면 `CTRL+C`를 사용하십시오. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [attach ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} 명령을 참조하십시오. 

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



## bluemix ic build
{: #bluemix_ic_build}

IBM Containers 빌드 서비스를 호출하여 로컬에 또는 사설 {{site.data.keyword.Bluemix_notm}} 저장소에 Docker 이미지를 빌드합니다. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [build ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic cp
{: #bluemix_ic_cp}
컨테이너와 로컬 파일 시스템 간에 파일 또는 폴더를 복사합니다. 이 명령은 Docker CLI를 호출합니다. 자세한 정보는 Docker 도움말에서 [cp ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} 명령을 참조하십시오. 


## bluemix ic cpi
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


## bluemix ic exec
{: #bluemix_ic_exec}

컨테이너에서 명령을 실행합니다. 자세한 정보는 Docker 도움말에서 [exec ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic group-create
{: #bluemix_ic_group_create}

확장 가능한 컨테이너 그룹을 작성합니다.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
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
| CCS_BIND_APP=*&lt;appname&gt;*       | 컨테이너에 서비스를 바인드합니다. `CCS_BIND_APP` 환경 변수를 사용하여 앱을 컨테이너에 바인드하십시오. 앱은 대상 서비스에 바인드되어 브릿지 역할을 하며, 이 브릿지를 통해 {{site.data.keyword.Bluemix_notm}}는 사용자 브릿지 앱의 `VCAP_SERVICES` 정보를 실행 중인 컨테이너 인스턴스로 가져올 수 있습니다. 브릿지 앱 작성에 대한 자세한 정보는 [컨테이너에 서비스 바인딩](../../../containers/container_integrations_binding.html){: new_window}을 참조하십시오. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 브릿지 앱을 사용하지 않고 컨테이너에 직접 Bluemix 서비스를 바인드하려면 CCS_BIND_SRV를 사용하십시오. 이 바인딩을 통해 Bluemix가 실행 중인 컨테이너 인스턴스에 VCAP_SERVICES 정보를 삽입할 수 있습니다. 여러 Bluemix 서비스를 표시하려면 동일한 환경 변수의 일부로 Bluemix 서비스를 포함시키십시오. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 컨테이너에서 모니터링할 로그 파일을 추가합니다. `LOG_LOCATIONS` 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. |
{: caption="표 2. 공통으로 사용되는 환경 변수" caption-side="top"}

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


## bluemix ic group-inspect
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


## bluemix ic group-instances
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


## bluemix ic group-remove
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


## bluemix ic group-update
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


## bluemix ic groups
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


## bluemix ic images
{: #bluemix_ic_images}

조직의 개인용 {{site.data.keyword.Bluemix_notm}} 저장소에 있는 사용 가능한 모든 이미지 목록을 봅니다. 자세한 정보는 Docker 도움말에서 [images ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} 명령을 참조하십시오. 목록에는 이미지 ID, 작성된 날짜 및 이미지 이름이 포함됩니다.

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


## bluemix ic info
{: #bluemix_ic_info}

컨테이너 클라우드 서비스 인스턴스의 상태를 설명하는 정보 세트를 봅니다. 정보에는 컨테이너 한계, 컨테이너 사용량, 실행 중인 컨테이너, 메모리 한계, 메모리 사용량, 유동 IP 주소 한계, 유동 IP 주소 사용량, CCS 호스트 URL, 레지스트리 호스트 URL 및 디버그 모드 상태가 포함됩니다.

```
bluemix ic info
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


## bluemix ic init
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


## bluemix ic inspect
{: #bluemix_ic_inspect}

컨테이너에 대한 정보를 봅니다. 자세한 정보는 Docker 도움말에서 [inspect ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} 명령을 참조하십시오. 

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


## bluemix ic ip-bind
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


## bluemix ic ip-release
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


## bluemix ic ip-request
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


## bluemix ic ip-unbind
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


## bluemix ic ips
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


## bluemix ic kill
{: #bluemix_ic_kill}

컨테이너를 중지하지 않고 컨테이너에서 실행 중인 프로세스를 중지합니다. 자세한 정보는 Docker 도움말에서 [kill ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic logs
{: #bluemix_ic_logs}

실행 중인 컨테이너의 출력 또는 오류 로그를 표시합니다. 자세한 정보는 Docker 도움말에서 [logs ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} 명령을 참조하십시오. 
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

로그인하는 조직의 개인용 {{site.data.keyword.Bluemix_notm}} 이미지 저장소의 이름을 확인합니다.

```
bluemix ic namespace-get
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


## bluemix ic namespace-set
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


## bluemix ic pause
{: #pause}

실행 중인 컨테이너 내의 모든 프로세스를 일시정지합니다. 자세한 정보는 Docker 도움말에서 [pause ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} 명령을 참조하십시오. 컨테이너를 중지하려면 [bluemix ic unpause](#unpause) 명령을 참조하십시오.

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


## bluemix ic port
{: #bluemix_ic_port}

컨테이너의 포트 맵핑 또는 특정 맵핑을 나열합니다. 이 명령은 `docker port` 명령을 랩핑합니다. 자세한 정보는 Docker 도움말에서 [port ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} 명령을 참조하십시오. 


## bluemix ic ps
{: #bluemix_ic_ps}
로그인한 사용자의 네임스페이스에서 실행 중인 컨테이너 목록을 봅니다. 기본적으로 이 명령은 실행 중인 컨테이너만 표시합니다. 자세한 정보는 Docker 도움말에서 [ps ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic rename
{: #bluemix_ic_rename}
컨테이너의 이름을 바꿉니다. 자세한 정보는 Docker 도움말에서 [rename ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic reprovision
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


## bluemix ic restart
{: #bluemix_ic_restart}

컨테이너를 다시 시작합니다. 자세한 정보는 Docker 도움말에서 [restart ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic rm
{: #bluemix_ic_rm}

컨테이너를 제거합니다. 자세한 정보는 Docker 도움말에서 [rm ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic rmi
{: #bluemix_ic_rmi}

로그인한 사용자의 네임스페이스에서 이미지를 제거합니다. 자세한 정보는 Docker 도움말에서 [rmi ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic route-map
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


## bluemix ic route-unmap
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


## bluemix ic run
{: #bluemix_ic_run}

이미지 이름에서 생성된 컨테이너 클라우드 서비스에서 새 컨테이너를 시작합니다. 자세한 정보는 Docker 도움말에서 [run ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} 명령을 참조하십시오. 


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
| CCS_BIND_APP=*&lt;appname&gt;*       | 컨테이너에 서비스를 바인드합니다. `CCS_BIND_APP` 환경 변수를 사용하여 앱을 컨테이너에 바인드하십시오. 앱은 대상 서비스에 바인드되어 브릿지 역할을 하며, 이 브릿지를 통해 {{site.data.keyword.Bluemix_notm}}는 사용자 브릿지 앱의 `VCAP_SERVICES` 정보를 실행 중인 컨테이너 인스턴스로 가져올 수 있습니다. 브릿지 앱 작성에 대한 자세한 정보는 [컨테이너에 서비스 바인딩](../../../containers/container_integrations_binding.html){: new_window}을 참조하십시오. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 브릿지 앱을 사용하지 않고 컨테이너에 직접 Bluemix 서비스를 바인드하려면 CCS_BIND_SRV를 사용하십시오. 이 바인딩을 통해 Bluemix가 실행 중인 컨테이너 인스턴스에 VCAP_SERVICES 정보를 삽입할 수 있습니다. 여러 Bluemix 서비스를 표시하려면 동일한 환경 변수의 일부로 Bluemix 서비스를 포함시키십시오. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 컨테이너에서 모니터링할 로그 파일을 추가합니다. `LOG_LOCATIONS` 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. |
{: caption="표 3. 공통으로 사용되는 환경 변수" caption-side="top"}


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


## bluemix ic service-bind
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


## bluemix ic service-unbind
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


## bluemix ic start
{: #ic_start}
중지된 컨테이너를 시작합니다. 자세한 정보는 Docker 도움말에서 [start ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} 명령을 참조하십시오. 컨테이너를 중지하려면 [bluemix ic stop](#ic_stop) 명령을 참조하십시오.

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


## bluemix ic stats
{: #bluemix_ic_stats}

하나 이상의 컨테이너에 대해 실시간 사용량 통계를 봅니다. 종료하려면 `CTRL+C`를 사용하십시오. 자세한 정보는 Docker 도움말에서 [stats ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic stop
{: #ic_stop}
실행 중인 컨테이너를 중지합니다. 자세한 정보는 Docker 도움말에서 [stop ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} 명령을 참조하십시오. 컨테이너를 시작하려면 [bluemix ic start](#ic_start) 명령을 참조하십시오.

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


## bluemix ic top
{: #bluemix_ic_top}

컨테이너에서 실행 중인 프로세스를 표시합니다. 자세한 정보는 Docker 도움말에서 [top ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic unpause
{: #unpause}

실행 중인 컨테이너 내에 있는 모든 프로세스의 일시정지를 해제합니다. 자세한 정보는 Docker 도움말에서 [unpause ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} 명령을 참조하십시오. 컨테이너를 일시정지하려면 [bluemix ic pause](#pause) 명령을 참조하십시오.

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


## bluemix ic unprovision
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


## bluemix ic version
{: #bluemix_ic_version}

Docker의 버전 및 IBM Containers API를 표시합니다.

```
bluemix ic version
```

<strong>전제조건</strong>:  Docker

IBM Containers의 버전을 확인하려면 `bluemix ic info`를 실행하십시오. 자세한 정보는 [version ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} 명령을 참조하십시오. 


## bluemix ic volume-create
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


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

파일 공유를 표시합니다.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
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


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

모든 파일 공유 특성을 나열합니다.

```
bluemix ic volume-fs-flavors
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


## bluemix ic volume-fs-inspect
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


## bluemix ic volume-fs-remove
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


## bluemix ic volume-inspect
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


## bluemix ic volume-remove
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


## bluemix ic volumes
{: #bluemix_ic_volumes}

볼륨을 나열합니다.

```
bluemix ic volumes
```

<strong>전제조건</strong>:  엔드포인트, 로그인, 대상 설정


## bluemix ic wait
{: #bluemix_ic_wait}

컨테이너를 종료하고 확인으로 종료 코드를 표시합니다. 자세한 정보는 Docker 도움말에서 [wait ![외부 링크 아이콘](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} 명령을 참조하십시오. 

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


## bluemix ic wait-status
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
