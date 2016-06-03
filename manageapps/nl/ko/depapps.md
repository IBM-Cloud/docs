---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#앱 배치
{: #deployingapps}

*마지막 업데이트 날짜: 2016년 5월 9일*

명령행 인터페이스 및 IDE(Integrated Development Environment) 등의 다양한 방법을
사용하여 {{site.data.keyword.Bluemix}}에
애플리케이션을 배치할 수 있습니다. 애플리케이션 Manifest를 사용하여 애플리케이션을
배치할 수도 있습니다. 애플리케이션 Manifest를 사용하면 {{site.data.keyword.Bluemix_notm}}에
애플리케이션을 배치할 때마다 지정해야 하는 배치 세부사항 수를 줄일 수 있습니다.
{:shortdesc}

##애플리케이션 배치
{: #appdeploy}

{{site.data.keyword.Bluemix_notm}}에 애플리케이션을 배치하는 작업은
애플리케이션 스테이징 및 애플리케이션 시작이라는 두 개의 단계로 구성됩니다.

###애플리케이션 스테이징

스테이징 단계 중 DEA(Droplet Execution Agent)에서는
cf 명령행 인터페이스 또는 `manifest.yml` 파일에 제공된 정보를 사용하여
애플리케이션 스테이징을 위해 작성할 항목을 결정합니다. DEA는 애플리케이션 스테이징에
적합한 빌드팩을 선택하며, 스테이징 프로세스의 결과가 드롭릿(droplet)입니다. {{site.data.keyword.Bluemix_notm}}에 배치하는 방법에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 아키텍처, {{site.data.keyword.Bluemix_notm}} 작동 방식](../public/index.html#publicarch)을 참조하십시오.

스테이징 프로세스 중 DEA에서 빌드팩이 애플리케이션과 일치하는지
확인합니다. 예를 들어 .war 파일의 경우 Liberty 런타임이고, .js 파일의 경우
Node.js 런타임입니다. 그런 다음 DEA에서 빌드팩과 애플리케이션 코드를 포함하는
격리된 컨테이너를 작성합니다. 이 컨테이너는 Warden 컴포넌트를 통해 관리됩니다. 자세한 정보는 [How Applications Are Staged](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}를 참조하십시오.

###애플리케이션 시작

애플리케이션이 시작되면
Warden 컨테이너의 인스턴스가 작성됩니다. **cf files** 명령을 사용하여
Warden 컨테이너의 파일 시스템에 저장된 파일(예: 로그)을 볼 수 있습니다. 애플리케이션이 시작되지 않을 경우 DEA가 애플리케이션을 중지하며 Warden 컨테이너의
전체 컨텐츠가 제거됩니다. 따라서 애플리케이션이 중지되거나 애플리케이션의
스테이징 프로세스가 실패할 경우 로그 파일을 사용할 수 없습니다.

애플리케이션에 대한 로그를 사용할 수 없어 **cf files**
명령으로 스테이징 오류의 원인을 확인할 경우 **cf logs** 명령을
대신 사용할 수 있습니다. **cf logs** 명령은 Cloud Foundry 로그 수집기를
사용하여 애플리케이션 로그 및 시스템 로그의 세부사항을 수집하므로, 로그 수집기 내에
버퍼된 내용을 확인할 수 있습니다. 로그 수집기에 대한 자세한 정보는
[Logging in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}를
참조하십시오.

**참고:** 버퍼 크기는 제한됩니다. 애플리케이션이 장시간 실행된 후 다시 시작되지 않을 경우, 로그 버퍼가 지워졌기 때문에 `cf logs appname --recent`를 입력할 때 로그가 표시되지 않을 수 있습니다. 따라서 대형 애플리케이션의 스테이징 오류를 디버그하려면 cf 명령 인터페이스와 다른 별개의 명령행에 `cf logs appname`을 입력하십시오.

{{site.data.keyword.Bluemix_notm}}에서
애플리케이션을 스테이징할 때 문제점이 발견될 경우 [스테이징 오류
디버깅](../debug/index.html#debugging-staging-errors)에 설명된 단계에 따라 문제점을 해결하십시오.

##cf 명령을 사용하여 애플리케이션 배치
{: #dep_apps}

명령행 인터페이스를 통해 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에
배치하는 경우 애플리케이션 언어 및 프레임워크에 따라 빌드팩을 런타임 환경으로
제공해야 합니다. Delivery Pipeline 서비스를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치할 수도 있습니다.

{{site.data.keyword.Bluemix_notm}}에서는 Java 및 Node.js를 지원하는 기본 제공 빌드팩을 제공합니다. 이 언어와 프레임워크를 사용할 경우 명령행 인터페이스를 사용하여 애플리케이션을
배치할 때 빌드팩을 지정하지 않아도 됩니다. {{site.data.keyword.Bluemix_notm}}는
Cloud Foundry를 기반으로 빌드되었으므로 명령이 기본적으로 이 빌드팩으로 설정됩니다.

외부 빌드팩을 사용하는 경우 명령 프롬프트에서 애플리케이션을
{{site.data.keyword.Bluemix_notm}}에
배치할 때 **-b** 옵션을 사용하여 빌드팩의 URL을 지정해야 합니다.

  * Liberty 서버 패키지를 {{site.data.keyword.Bluemix_notm}}에 배치하려면 소스 디렉토리에서 다음 명령을 사용하십시오.
  
  ```
  cf push
  ```
  
  Liberty
빌드팩에 대한 자세한 정보는 [Liberty
for Java](../runtimes/liberty/index.html)를 참조하십시오.
  
  * Java Tomcat 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하려면 다음 명령을 사용하십시오.
  
  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```
  
  * WAR 패키지를 {{site.data.keyword.Bluemix_notm}}에
배치하려면 다음 명령을 사용하십시오.
  
  ```
  cf push appname -p app.war
  ```
  또는
다음 명령을 사용하여 애플리케이션 파일이 포함된 디렉토리를 지정할 수 있습니다.
  
  ```
  cf push appname -p "./app"
  ```
  
  * Node.js 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에
배치하려면 다음 명령을 사용하십시오.
  
  ```
  cf push appname -p app_path
  ```
  
Node.js
빌드팩에서 애플리케이션을 인식하려면 `package.json` 파일이
Node.js 애플리케이션에 있어야 합니다. `app.js` 파일은 애플리케이션에
대한 엔트리 스크립트이며, `package.json` 파일에 지정할 수 있습니다. 다음 예에서는 단순한 `package.json` 파일을 보여줍니다.

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```
    
  `package.json` 파일에 대한 자세한 정보는
[package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}을
참조하십시오.
  
  * PHP, Ruby 또는 Python 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에
배치하려면 애플리케이션 소스가 있는 디렉토리에서 다음 명령을
사용하십시오.
  
  ```
  cf push appname
  ```

###단일 앱을 여러 영역에 배치

앱은 배치된 영역에 대해 특정합니다. {{site.data.keyword.Bluemix_notm}}에서는
앱을 한 영역에서 다른 영역으로 이동하거나 복사할 수 없습니다. 앱을 여러 영역에 배치하려면 다음 단계를 사용하여 앱을 사용할 각 영역에 앱을 배치해야 합니다.

  1. **cf target** 명령을 **-s** 옵션과 함께 사용하여 앱을 배치할 영역으로 전환하십시오.
  
  ```
  cf target -s <space_name>
  ```
  
  2. 앱 디렉토리로 이동한 후 **cf push** 명령을 사용하여 앱을 배치하십시오. 여기서, appname은 도메인 내에서 고유해야 합니다.
  
  ```
  cf push appname
  ```
  
##애플리케이션 Manifest
{: #appmanifest}

애플리케이션 Manifest에는 **cf push** 명령에
적용되는 옵션이 포함되어 있습니다. 애플리케이션 Manifest를 사용하면 {{site.data.keyword.Bluemix_notm}}에
애플리케이션을 푸시할 때마다 지정해야 하는 배치 세부사항 수를
줄일 수 있습니다.

애플리케이션 Manifest에서는 작성할 애플리케이션 인스턴스 수,
애플리케이션에 할당할 메모리 양 및 디스크 할당량, 애플리케이션의 기타 환경 변수
등의 옵션을 지정할 수 있습니다. 애플리케이션 Manifest를 사용하여 애플리케이션을
자동으로 배치할 수도 있습니다. Manifest 파일의 기본 이름은
`manifest.yml`입니다.

###Manifest 파일에서 지원되는 옵션

다음 표는 애플리케이션 Manifest 파일에서 사용할 수 있는 지원되는 옵션을
보여줍니다. `manifest.yml`이 아닌 다른 파일 이름을 사용하도록
선택한 경우 **cf push** 명령과 함께 **-f** 옵션을 사용해야 합니다. 다음 예에서는 `appManifest.yml`이 파일 이름입니다.

```
cf push -f appManifest.yml
```

<p>  </p>


|옵션	|설명	|사용법 또는 예|
|:----------|:--------------|:---------------|
|**buildpack**	|사용자 정의 빌드팩의 URL 또는 이름입니다.	|`buildpack: ` *buildpack_URL*|
|**disk_quota**	|애플리케이션에 할당되는 디스크 할당량입니다. 기본값은 1G입니다.	|`disk_quota: 500M`|
|**domain**	|{{site.data.keyword.Bluemix_notm}}에서 애플리케이션의 도메인 이름입니다.	|`domain:` ng.bluemix.net|
|**host**	|{{site.data.keyword.Bluemix_notm}}에서 애플리케이션의 호스트 이름입니다. 이 값은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다.	|`host: ` *host_name*|
|**name**	|{{site.data.keyword.Bluemix_notm}}에서 애플리케이션 이름입니다. 이 값은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다.	|`name: ` *appname*|
|**path**	|애플리케이션의 위치입니다. 이 값은 상대 경로 또는 절대 경로일 수 있습니다.	|`path: ` *path_to_application*|
|**command**	|애플리케이션에 대한 사용자 정의 시작 명령 또는 스크립트 파일을 실행하는 명령입니다.	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|애플리케이션에 할당할 메모리의 양입니다. 기본값은 1G입니다.	|`memory: 512M`|
|**instances**	|애플리케이션에 대해 작성할 인스턴스 수입니다.	|`instances: 2`|
|**timeout**	|애플리케이션을 시작하는 데 사용되는 최대 시간(초)입니다. 기본값은 60초입니다.	|`timeout: 80`|
|**no-route**	|애플리케이션이 백그라운드에서 실행 중인 경우, 라우트가 애플리케이션에 지정되지 않도록 하는 부울 값입니다. 기본값은 **false**입니다.	|`no-route: true`|
|**random-route**	|애플리케이션에 랜덤 라우트를 지정하는 부울 값입니다. 기본값은 **false**입니다.	|`random-route: true`|
|**services**	|애플리케이션에 바인딩할 서비스입니다.	|`services: - mysql_maptest`|
|**env**	|애플리케이션에 대한 사용자 정의 환경 변수입니다.|`env: DEV_ENV: production`|
*표 1. manifest.yml 파일에서 지원되는 옵션*

###샘플 `manifest.yml` 파일

다음 예는
{{site.data.keyword.Bluemix_notm}}에서 기본 제공
커뮤니티 Node.js 빌드팩을 사용하는 Node.js 애플리케이션에 대한 Manifest 파일을 보여줍니다.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

##환경 변수
{: #app_env}

환경 변수에는 {{site.data.keyword.Bluemix_notm}}에
배치된 애플리케이션의 환경 정보가 포함되어 있습니다. *DEA(Droplet Execution Agent)*
및 빌드팩을 통해 설정된 환경 변수 이외에도, {{site.data.keyword.Bluemix_notm}}에서
애플리케이션에 대해 애플리케이션별 환경 변수를 설정할 수도 있습니다.

**cf env** 명령을 사용하거나 {{site.data.keyword.Bluemix_notm}}
사용자 인터페이스를 통해 실행 중인 {{site.data.keyword.Bluemix_notm}}
애플리케이션의 다음 환경 변수를 확인할 수도 있습니다.
	
  * 애플리케이션에만 해당되는 사용자 정의 변수. 사용자 정의 변수를 앱에 추가하는 방법에 대한 자세한 정보는 [사용자 정의 환경 변수 추가](#ud_env){:new_window}를 참조하십시오.
	 
  * 서비스 인스턴스에 액세스하는 데 필요한 연결 정보가 포함된 VCAP_SERVICES 변수. 애플리케이션이 여러 개의 서비스에 바인딩된 경우, VCAP_SERVICES 변수에 각 서비스 인스턴스에 대한 연결 정보가 포함되어 있습니다. 예:
  
  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```
        
DEA 및 빌드팩을 통해 설정된 환경 변수에 액세스할 수도 있습니다.

DEA를 통해 정의된 변수는 다음과 같습니다.
  

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>배치된 애플리케이션의 루트 디렉토리입니다.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>애플리케이션의 각 인스턴스가 사용할 수 있는 최대 메모리 양입니다. 애플리케이션을 푸시할 때 애플리케이션의 <span class="ph filepath">manifest.yml</span> 파일
또는 명령행에 값을 지정할 수 있습니다.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>애플리케이션과 통신하는 데 필요한 DEA의 포트입니다. DEA는 스테이징 시
애플리케이션에 포트를 할당합니다.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>빌드팩이 실행 중인 현재 작업 디렉토리입니다.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>임시 파일과 스테이징 파일이 저장되는 디렉토리입니다.</dd>
  <dt><strong>USER</strong></dt>
  <dd>DEA가 실행될 때 사용되는 사용자 ID입니다.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>DEA 호스트의 IP 주소입니다.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>배치된 애플리케이션에 대한 정보가 포함된 JSON 문자열입니다. 애플리케이션 이름,
URI, 메모리 한계, 애플리케이션이 현재 상태가 된 시간소인 등이 이러한 정보에
포함됩니다. 예: 
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>배치된 애플리케이션에 바인딩된 서비스의 정보가 포함된 JSON 문자열입니다. 예:
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

빌드팩을 통해 정의되는 변수는 빌드팩마다 다릅니다. 호환되는 기타 빌드팩은
[Buildpacks](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}를
참조하십시오.

    

<ul>
    <li>Liberty 빌드팩으로 정의되는 변수는 다음과 같습니다.
	
	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>애플리케이션을 실행하는 Java SDK의 위치입니다.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>애플리케이션을 실행할 때 사용할 Java SDK 옵션입니다.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>DEA에서 Liberty 프로파일 서버 인스턴스를 시작하는 Java 명령입니다.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>DEA에서 Liberty 프로파일 서버 인스턴스를 시작할 때 공유 자원 및 서버 정의의
위치입니다.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>실행 중인 Liberty 프로파일 서버 인스턴스의 로그 파일 및 작업 디렉토리와
같은 생성된 출력의 위치입니다.</dd>
	  </dl>
</li>   
<li>Node.js 빌드팩으로 정의되는 변수는 다음과 같습니다.
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>Node.js 런타임 환경의 디렉토리입니다.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>Node.js 런타임 환경이 캐싱에 사용할 디렉토리입니다.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Node.js 런타임 환경에 사용되는 시스템 경로입니다.</dd>
	</dl>
</li>
</li>
</ul>	

다음 샘플 Node.js 코드를 사용하여 VCAP_SERVICES 환경 변수의 값을 가져올 수 있습니다. 

```
if (process.env.VCAP_SERVICES) {

    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

각 환경 변수에 대한
자세한 정보는 [Cloud Foundry
Environment Variables](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}를 참조하십시오.

## 애플리케이션 배치 사용자 정의
{: #customize_dep}

애플리케이션에 대한 배치 태스크를 사용자 정의할 수 있습니다. 예를 들어 애플리케이션 시작 명령을 지정한 다음 애플리케이션 스타트업 환경을
구성할 수 있습니다.
{:shortdesc}

### 시작 명령 지정

애플리케이션 시작 명령을 지정하려면 다음 방법 중 하나를
사용하십시오. 지정하는 시작 명령이 빌드팩에서 제공하는 기본 시작 명령을
겹쳐씁니다.

**참고:** 빌드팩 시작 명령을 우선적으로 사용하려면 **null**을 시작 명령으로 지정하십시오.

  * **cf push** 명령을 사용하고 -c 매개변수를 지정하십시오. 예를 들어, Node.js 애플리케이션을 배치하는 경우에는 **node app.js** 시작 명령을 -c 매개변수에 지정할 수 있습니다.
  
  ```
  cf push appname -p app_path -c "node app.js"
  ```
  
  * `manifest.yml` 파일에 command 매개변수를 사용하십시오. 예를 들어 Node.js 애플리케이션을 배치할 경우
**node app.js** 시작 명령을 Manifest 파일에
지정할 수 있습니다.
  
  ```
  command: node app.js
  ```
  

### 사용자 정의 환경 변수 추가
{: #ud_env}

사용자 정의 환경 변수는 애플리케이션에 고유합니다. 사용자 정의 환경 변수를 실행 중인 앱에 추가할 때는 다음과 같은 옵션이 지원됩니다.

  * {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하십시오. 다음 단계를 수행하십시오.

    1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱 타일을 클릭하십시오. 앱 세부사항 페이지가 표시됩니다.
	2. 왼쪽 탐색 분할창에서 **환경 변수**를 클릭하십시오.
	3. **사용자 정의**를 클릭하고 **추가**를 클릭하십시오.
	4. 필수 필드에 값을 입력하고 **저장**을 클릭하십시오.
  * cf 명령행 인터페이스를 사용하십시오. `cf set-env` 명령을 사용하여 사용자 정의 변수를 추가하십시오. 예: 
  ```
    cf set-env appname env_var_name env_var_value
    ```
	
  * `manifest.yml` 파일을 사용하십시오. 파일에 값 쌍을 추가하십시오. 예: 
  ```
	env:
      VAR1:value1
      VAR2:value2
    ```
	
사용자 정의 환경 변수를 추가한 후에는 다음 샘플 Node.js 코드를 사용하여 정의한 변수의 값을 가져올 수 있습니다.

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```
	
### 스타트업 환경 구성

애플리케이션 스타트업 환경을 구성하려면 `/.profile.d`
디렉토리에 쉘 스크립트를 추가하면 됩니다. `/.profile.d` 디렉토리는
애플리케이션의 빌드 디렉토리 아래에 있습니다. `/.profile.d` 디렉토리에
있는 스크립트는 애플리케이션이 실행되기 전에 {{site.data.keyword.Bluemix_notm}}에
의해 실행됩니다. 예를 들어, `/.profile.d` 디렉토리에 다음 컨텐츠가 포함된 `node_env.sh` 파일을 삽입하여 NODE_ENV 환경 변수를 **production**으로 설정할 수 있습니다.

```
export NODE_ENV=production;
```

###파일 및 디렉토리 업로드 금지

cf 명령행 인터페이스를 사용하여 애플리케이션을
배치하는 경우 {{site.data.keyword.Bluemix_notm}}에서 얻을 수 있는
특정 파일 및 디렉토리를 건너뛰어 업로드 시간을
절약할 수 있습니다. 이러한 파일 및 디렉토리가 {{site.data.keyword.Bluemix_notm}}에
업로드되지 않게 하려면 애플리케이션의 루트 디렉토리에서
`.cfignore` 파일을 작성할 수 있습니다.

**참고:** `.cfignore` 파일은 UTF-8 형식이어야 합니다.

`.cfignore` 파일에는
무시할 파일 및 디렉토리의 이름(행마다 이름 하나)이
포함되어 있습니다. 별표(*)를 와일드카드 문자로 사용할 수 있습니다. 디렉토리를 지정하는 경우 해당 디렉토리 아래의
파일 및 서브디렉토리도 모두 무시됩니다. 예를 들어, `.cfignore` 파일의
다음 컨텐츠는 모든 `.swp` 파일과
`tmp/` 디렉토리 아래의 모든 파일 및 서브디렉토리가
{{site.data.keyword.Bluemix_notm}}에 업로드되지 않음을 나타냅니다.

```
*.swp
tmp/
```

# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [Deploying with Application Manifests](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [IBM Continuous Delivery Pipeline for Bluemix 시작하기](../services/DeliveryPipeline/index.html#getstartwithCD)
