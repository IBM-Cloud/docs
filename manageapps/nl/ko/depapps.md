---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 앱 배치
{: #deployingapps}

명령행 인터페이스 및 IDE(Integrated Development Environment) 등의 다양한 방법을 사용하여 {{site.data.keyword.Bluemix}}에 애플리케이션을 배치할 수 있습니다. 애플리케이션 Manifest를 사용하여 애플리케이션을 배치할 수도 있습니다. 애플리케이션 Manifest를 사용하면 {{site.data.keyword.Bluemix_notm}}에 애플리케이션을 배치할 때마다 지정해야 하는 배치 세부사항 수를 줄일 수 있습니다.
{:shortdesc}

## 애플리케이션 배치
{: #appdeploy}

{{site.data.keyword.Bluemix_notm}}에 애플리케이션을 배치하는 작업은 애플리케이션 스테이징 및 애플리케이션 시작이라는 두 개의 단계로 구성됩니다.

Cloud Foundry는 Diego를 지원합니다. Diego는 클라우드 플랫폼의 호스팅 및 구성을 위한 애플리케이션 개발 경험을 개선하는 기능 세트를 제공하는 새로운 기본 런타임 아키텍처입니다. 이 아키텍처 업데이트는 Cloud Foundry 플랫폼의 전반적 운영 및 성능을 향상시킵니다. 새 아키텍처는 Garden 및 Windows를 포함하여 여러 가지 애플리케이션 컨테이너 기술을 지원하고, 애플리케이션 컨테이너에 직접 로그인할 수 있는 SSH 패키지 및 기타 혁신적 변경사항을 제공합니다. 최신 아키텍처 업그레이드에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}를 참조하십시오. 


사용자가 작성하는 모든 새 애플리케이션은 Diego에서 실행되며, 사용자는 DEA에서 실행되는 기존 애플리케이션을 새 Diego 아키텍처로 마이그레이션하는 작업을 시작해야 합니다. 

**참고**: Cloud Foundry Diego 아키텍처는 모든 {{site.data.keyword.Bluemix_notm}} 퍼블릭 지역 환경에 영향을 줍니다. {{site.data.keyword.Bluemix_notm}} 데디케이티드 및 {{site.data.keyword.Bluemix_notm}} 로컬 환경은 나중에 업데이트됩니다. 

### 애플리케이션 스테이징
{: #diego}

스테이징 단계 동안 Diego는 애플리케이션 컨테이너 오케스트레이션과 관련된 모든 측면을 처리합니다. 앱을 푸시하는 경우 클라우드 제어기는 스테이징 요청을 Diego로 보내고 앱 인스턴스 할당 태스크를 넘겨받습니다. Diego 백엔드는 일련의 가상 머신 호출 셀 전체에서 로드 균형을 조정하기 위해 결함 허용 및 장기적 일관성을 보장하는 방식으로 애플리케이션 컨테이너를 조율합니다. 또한 Diego는 사용자가 해당 앱의 로그에 액세스하도록 지원합니다. 모든 Diego 구성요소가 클러스터링되도록 디자인되므로 사용자는 서로 다른 가용성 구역을 작성할 수 있습니다. 

Diego는 앱 상태의 유효성을 검증하기 위해 DEA에 사용된 동일한 PORT 기반 검사를 지원합니다. 그러나 Diego는 URL 기반 상태 검사와 같은 보다 일반적인 옵션을 가질 수 있도록 디자인되어 있으며 나중에 옵션을 사용하도록 설정할 수 있습니다. 

#### 새 앱 스테이징
{: #stageapp}

모든 새 앱이 Diego 아키텍처에 배치됩니다. 새 애플리케이션을 스테이징하려면 **cf push** 명령으로 앱을 배치하십시오. 

  1. 애플리케이션을 배치하십시오. 
  ```
  $ cf push APPLICATION_NAME
  ```

**cf push** 명령에 대한 세부사항은 [cf push](/docs/cli/reference/cfcommands/index.html#cf_push)를 참조하십시오.

### 기존 앱을 Diego로 마이그레이션
{: #migrateapp}

Diego는 {{site.data.keyword.Bluemix_notm}}를 위한 기본 Cloud Foundry 아키텍처이며 DEA에 대한 지원이 제거되므로, 각 앱을 업데이트하여 기존의 모든 애플리케이션을 마이그레이션해야 합니다. Diego 플래그로 애플리케이션을 업데이트하여 Diego로 앱을 마이그레이션하는 작업을 시작하십시오. 애플리케이션은 즉시 Diego에서 실행을 시작하려고 시도하며 DEA에서 실행을 중지합니다. 

애플리케이션이 DEA 아키텍처에서 Diego로 업데이트됨에 따라, 애플리케이션이 Diego와 호환되지 않는 경우 짧은 또는 장기적인 중단 시간을 경험할 수 있습니다. 중단 시간을 최소화하려면, 애플리케이션의 사본을 Diego에 배치한 후 라우트를 스와핑하고 DEA 애플리케이션의 규모를 축소하여 [Blue-Green 배치](/docs/manageapps/updapps.html#blue_green)를 수행하십시오. 

앱을 Diego로 마이그레이션하려면 다음 단계를 완료하십시오. 

 1.  [cf CLI ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} 및 [Diego-Enabler CLI Plugin![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}을 둘 다 설치하십시오. 
 2. [알려진 문제 목록](depapps.html#knownissues)을 검토하십시오. 
 3. Diego 플래그를 설정하여 앱이 Diego에서 실행되도록 변경하십시오. 
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

앱을 업데이트한 후 앱이 시작되었는지 확인하십시오. 마이그레이션된 앱이 시작하는 데 실패하는 경우 해당 문제를 식별하고 해결한 후 앱을 다시 시작할 때까지 앱은 오프라인 상태를 유지합니다. 

IBM은 DEA 아키텍처 지원이 제거되는 예정된 필수 마이그레이션 기간을 공지할 것이며, 앱을 마이그레이션하지 않은 경우 운영 팀에서 사용자를 위해 모든 앱을 대신 마이그레이션하게 됩니다. 

어떤 백엔드 애플리케이션이 실행 중인지 확인하려면 다음 명령을 사용하십시오. 

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

#### Diego 마이그레이션의 알려진 문제
{: #knownissues}

앱을 Diego로 마이그레이션할 때 해결해야 하는 알려진 문제는 다음과 같습니다. 

  * `--no-route` 옵션을 사용하여 배치된 작업자 애플리케이션은 정상적으로 보고되지 않습니다. 이 옵션을 사용하지 않으려면 `cf set-health-check APP_NAME none` 명령으로 포트 기반 상태 검사를 사용 안함으로 설정하십시오.
  * **cf files** 명령은 더 이상 지원되지 않습니다. 대체 명령은 **cf ssh**입니다. **cf ssh** 명령에 대한 세부사항은 [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)를 참조하십시오. 
  * 일부 앱은 많은 수의 파일 디스크립터(inode)를 사용할 수 있습니다. 이 문제가 발생하면 `cf scale APP_NAME [-k DISK]` 명령으로 앱의 디스크 할당량을 늘려야 합니다.

알려진 문제의 전체 목록은 Cloud Foundry 문서 페이지에서 [Migrating to Diego ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}를 참조하십시오. 

이전 DEA 아키텍처에 대한 지원이 제거될 때까지는 `cf disable-diego APPLICATION_NAME` 명령을 실행하여 DEA로 다시 전환할 수 있습니다. 또한 지원이 제거될 때까지 새 앱을 DEA 아키텍처에 계속 배치할 수 있습니다. 

**참고**: `disable-diego` 명령을 사용하려면 [cf CLI ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} 및 [Diego-Enabler CLI Plugin ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}을 둘 다 설치해야 합니다. 

1. 애플리케이션을 시작하지 않고 배치하십시오.
```
$ cf push APPLICATION_NAME --no-start
```
2. disable-diego 명령을 실행하십시오. 
```
$ cf disable-diego APPLICATION_NAME
```
3. 애플리케이션을 시작하십시오.
```
$ cf start APPLICATION_NAME
```

### 애플리케이션 시작
{: #startapp}

애플리케이션이 시작되면 애플리케이션 컨테이너의 인스턴스가 작성됩니다. Diego에서 실행되는 애플리케이션의 경우, **cf ssh** 또는 **cf scp** 명령을 사용하여 로그가 포함된 애플리케이션 컨테이너의 파일 시스템에 액세스할 수 있습니다. **cf files** 명령은 Diego 아키텍처에서 실행되는 앱에 대해서는 작동하지 않습니다. 

**참고**: DEA에서 실행되는 애플리케이션이 여전히 있는 경우 DEA 지원이 제거될 때까지 **cf files** 명령을 사용하여 애플리케이션 컨테이너 내에 있는 파일을 볼 수 있습니다. 

애플리케이션을 시작하는 데 실패하는 경우 애플리케이션이 중지되고 애플리케이션 컨테이너의 전체 컨텐츠가 제거됩니다. 따라서 애플리케이션이 중지되거나 애플리케이션의 스테이징 프로세스가 실패할 경우 로그 파일을 사용할 수 없습니다.

애플리케이션에 대한 로그를 더 이상 사용할 수 없어서 **cf ssh**, **cf scp** 또는 **cf files** 명령을 애플리케이션 컨테이너 내부의 스테이징 오류 원인을 확인하는 데 사용할 수 없는 경우 **cf logs** 명령을 대신 사용할 수 있습니다. **cf logs** 명령은 Cloud Foundry 로그 수집기를 사용하여 애플리케이션 로그 및 시스템 로그의 세부사항을 수집하므로, 로그 수집기 내에 버퍼된 내용을 확인할 수 있습니다. 로그 수집기에 대한 자세한 정보는 [Logging in Cloud Foundry ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}를 참조하십시오. 

**참고:** 버퍼 크기는 제한됩니다. 애플리케이션이 장시간 실행된 후 다시 시작되지 않는 경우, 로그 버퍼가 지워졌을 수 있으므로 `cf logs appname --recent` 명령을 입력할 때 로그가 표시되지 않을 수 있습니다. 따라서 대형 애플리케이션의 스테이징 오류를 디버그하기 위해 cf 명령행 인터페이스와 다른 별도의 명령행에 `cf logs appname` 명령을 입력하여 애플리케이션 배치 시 로그를 추적할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 스테이징할 때 문제점이 발견될 경우 [스테이징 오류 디버깅](/docs/debug/index.html#debugging-staging-errors)에 설명된 단계에 따라 문제점을 해결하십시오.


## cf 명령을 사용하여 애플리케이션 배치
{: #dep_apps}

명령행 인터페이스를 통해 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하는 경우 애플리케이션 언어 및 프레임워크에 따라 빌드팩을 런타임 환경으로 제공해야 합니다. Delivery Pipeline 서비스를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치할 수도 있습니다.

{{site.data.keyword.Bluemix_notm}}에서는 Java 및 Node.js를 지원하는 기본 제공 빌드팩을 제공합니다. 이 언어와 프레임워크를 사용할 경우 명령행 인터페이스를 사용하여 애플리케이션을 배치할 때 빌드팩을 지정하지 않아도 됩니다. {{site.data.keyword.Bluemix_notm}}는 Cloud Foundry를 기반으로 빌드되었으므로 명령이 기본적으로 이 빌드팩으로 설정됩니다.

외부 빌드팩을 사용하는 경우 명령 프롬프트에서 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치할 때 **-b** 옵션을 사용하여 빌드팩의 URL을 지정해야 합니다.

  * Liberty 서버 패키지를 {{site.data.keyword.Bluemix_notm}}에 배치하려면 소스 디렉토리에서 다음 명령을 사용하십시오.

  ```
  cf push
  ```

  Liberty 빌드팩에 대한 자세한 정보는 [Liberty for Java](/docs/runtimes/liberty/index.html)를 참조하십시오.

  * Java Tomcat 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하려면 다음 명령을 사용하십시오.

  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * WAR 패키지를 {{site.data.keyword.Bluemix_notm}}에 배치하려면 다음 명령을 사용하십시오.

  ```
  cf push appname -p app.war
  ```
  또는 다음 명령을 사용하여 애플리케이션 파일이 포함된 디렉토리를 지정할 수 있습니다.

  ```
  cf push appname -p "./app"
  ```

  * Node.js 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하려면 다음 명령을 사용하십시오.

  ```
  cf push appname -p app_path
  ```

Node.js 빌드팩에서 애플리케이션을 인식하려면 `package.json` 파일이 Node.js 애플리케이션에 있어야 합니다. `app.js` 파일은 애플리케이션에 대한 엔트리 스크립트이며, `package.json` 파일에 지정할 수 있습니다. 다음 예에서는 단순한 `package.json` 파일을 보여줍니다.

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

  `package.json` 파일에 대한 자세한 정보는 [package.json ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}을 참조하십시오. 

  * PHP, Ruby 또는 Python 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 배치하려면 애플리케이션 소스가 있는 디렉토리에서 다음 명령을 사용하십시오.

  ```
  cf push appname
  ```

### 단일 앱을 여러 영역에 배치

앱은 배치된 영역에 대해 특정합니다. {{site.data.keyword.Bluemix_notm}}에서는 앱을 한 영역에서 다른 영역으로 이동하거나 복사할 수 없습니다. 앱을 여러 영역에 배치하려면 다음 단계를 사용하여 앱을 사용할 각 영역에 앱을 배치해야 합니다.

  1. **cf target** 명령을 **-s** 옵션과 함께 사용하여 앱을 배치할 영역으로 전환하십시오.

  ```
  cf target -s <space_name>
  ```

  2. 앱 디렉토리로 이동한 후 **cf push** 명령을 사용하여 앱을 배치하십시오. 여기서, appname은 도메인 내에서 고유해야 합니다.

  ```
  cf push appname
  ```

## 애플리케이션 Manifest
{: #appmanifest}

애플리케이션 Manifest에는 **cf push** 명령에 적용되는 옵션이 포함되어 있습니다. 애플리케이션 Manifest를 사용하면 {{site.data.keyword.Bluemix_notm}}에 애플리케이션을 푸시할 때마다 지정해야 하는 배치 세부사항 수를 줄일 수 있습니다.

애플리케이션 Manifest에서는 작성할 애플리케이션 인스턴스 수, 애플리케이션에 할당할 메모리 양 및 디스크 할당량, 애플리케이션의 기타 환경 변수 등의 옵션을 지정할 수 있습니다. 애플리케이션 Manifest를 사용하여 애플리케이션을 자동으로 배치할 수도 있습니다. Manifest 파일의 기본 이름은 `manifest.yml`입니다.

### Manifest 파일에서 지원되는 옵션

다음 표는 애플리케이션 Manifest 파일에서 사용할 수 있는 지원되는 옵션을 보여줍니다. `manifest.yml`이 아닌 다른 파일 이름을 사용하도록 선택한 경우 **cf push** 명령과 함께 **-f** 옵션을 사용해야 합니다. 다음 예에서는 `appManifest.yml`이 파일 이름입니다.

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
{: caption="표 1. Manifest YAML 파일에서 지원되는 옵션" caption-side="top"}

### 샘플 manifest.yml 파일

다음 예는 {{site.data.keyword.Bluemix_notm}}에서 기본 제공 커뮤니티 Node.js 빌드팩을 사용하는 Node.js 애플리케이션에 대한 Manifest 파일을 보여줍니다.

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

## 환경 변수
{: #app_env}

환경 변수에는 {{site.data.keyword.Bluemix_notm}}에 배치된 애플리케이션의 환경 정보가 포함되어 있습니다. *DEA(Droplet Execution Agent)* 및 빌드팩을 통해 설정된 환경 변수 이외에도, {{site.data.keyword.Bluemix_notm}}에서 애플리케이션에 대해 애플리케이션별 환경 변수를 설정할 수도 있습니다.

**cf env** 명령을 사용하거나 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 통해 실행 중인 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 다음 환경 변수를 확인할 수도 있습니다.

  * 애플리케이션에만 해당되는 사용자 정의 변수. 사용자 정의 변수를 앱에 추가하는 방법에 대한 자세한 정보는 [사용자 정의 환경 변수 추가 ![외부 링크 아이콘](../icons/launch-glyph.svg)](#ud_env){:new_window}를 참조하십시오. 

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
  <dd>애플리케이션의 각 인스턴스가 사용할 수 있는 최대 메모리 양입니다. 애플리케이션을 푸시할 때 애플리케이션의 <span class="ph filepath">manifest.yml</span> 파일 또는 명령행에 값을 지정할 수 있습니다.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>애플리케이션과 통신하는 데 필요한 DEA의 포트입니다. DEA는 스테이징 시 애플리케이션에 포트를 할당합니다.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>빌드팩이 실행 중인 현재 작업 디렉토리입니다.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>임시 파일과 스테이징 파일이 저장되는 디렉토리입니다.</dd>
  <dt><strong>USER</strong></dt>
  <dd>DEA가 실행될 때 사용되는 사용자 ID입니다.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>DEA 호스트의 IP 주소입니다.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>배치된 애플리케이션에 대한 정보가 포함된 JSON 문자열입니다. 애플리케이션 이름, URI, 메모리 한계, 애플리케이션이 현재 상태가 된 시간소인 등이 이러한 정보에 포함됩니다. 예:
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
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
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

빌드팩을 통해 정의되는 변수는 빌드팩마다 다릅니다. 기타 호환 가능한 빌드팩은 [빌드팩 ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}을 참조하십시오. 

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
	  <dd>DEA에서 Liberty 프로파일 서버 인스턴스를 시작할 때 공유 리소스 및 서버 정의의 위치입니다.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>실행 중인 Liberty 프로파일 서버 인스턴스의 로그 파일 및 작업 디렉토리와 같은 생성된 출력의 위치입니다.</dd>
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

각 환경 변수에 대한 자세한 정보는 [Cloud Foundry Environment Variables ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}를 참조하십시오. 

## 애플리케이션 배치 사용자 정의
{: #customize_dep}

애플리케이션에 대한 배치 태스크를 사용자 정의할 수 있습니다. 예를 들어 애플리케이션 시작 명령을 지정한 다음 애플리케이션 스타트업 환경을 구성할 수 있습니다.
{:shortdesc}

### 시작 명령 지정

애플리케이션 시작 명령을 지정하려면 다음 방법 중 하나를 사용하십시오. 지정하는 시작 명령이 빌드팩에서 제공하는 기본 시작 명령을 겹쳐씁니다.

**참고:** 빌드팩 시작 명령을 우선적으로 사용하려면 **null**을 시작 명령으로 지정하십시오.

  * **cf push** 명령을 사용하고 -c 매개변수를 지정하십시오. 예를 들어, Node.js 애플리케이션을 배치하는 경우에는 **node app.js** 시작 명령을 -c 매개변수에 지정할 수 있습니다.

  ```
  cf push appname -p app_path -c "node app.js"
  ```

  * `manifest.yml` 파일에 command 매개변수를 사용하십시오. 예를 들어 Node.js 애플리케이션을 배치할 경우 **node app.js** 시작 명령을 Manifest 파일에 지정할 수 있습니다.

  ```
  command: node app.js
  ```


### 사용자 정의 환경 변수 추가
{: #ud_env}

사용자 정의 환경 변수는 애플리케이션에 고유합니다. 사용자 정의 환경 변수를 실행 중인 앱에 추가할 때는 다음과 같은 옵션이 지원됩니다.

  * {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하십시오. 다음 단계를 수행하십시오. 
    1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱 타일을 클릭하십시오. 앱 세부사항 페이지가 표시됩니다.
	2. **환경 변수**를 클릭하십시오. 
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

애플리케이션 스타트업 환경을 구성하려면 `/.profile.d` 디렉토리에 쉘 스크립트를 추가하면 됩니다. `/.profile.d` 디렉토리는 애플리케이션의 빌드 디렉토리 아래에 있습니다. `/.profile.d` 디렉토리에 있는 스크립트는 애플리케이션이 실행되기 전에 {{site.data.keyword.Bluemix_notm}}에 의해 실행됩니다. 예를 들어, `/.profile.d` 디렉토리에 다음 컨텐츠가 포함된 `node_env.sh` 파일을 삽입하여 NODE_ENV 환경 변수를 **production**으로 설정할 수 있습니다.

```
export NODE_ENV=production;
```

###파일 및 디렉토리 업로드 금지

cf 명령행 인터페이스를 사용하여 애플리케이션을 배치하는 경우 {{site.data.keyword.Bluemix_notm}}에서 얻을 수 있는 특정 파일 및 디렉토리를 건너뛰어 업로드 시간을 절약할 수 있습니다. 이러한 파일 및 디렉토리가 {{site.data.keyword.Bluemix_notm}}에 업로드되지 않게 하려면 애플리케이션의 루트 디렉토리에서 `.cfignore` 파일을 작성할 수 있습니다.

**참고:** `.cfignore` 파일은 UTF-8 형식이어야 합니다.

`.cfignore` 파일에는 무시할 파일 및 디렉토리의 이름(행마다 이름 하나)이 포함되어 있습니다. 별표(*)를 와일드카드 문자로 사용할 수 있습니다. 디렉토리를 지정하는 경우 해당 디렉토리 아래의 파일 및 서브디렉토리도 모두 무시됩니다. 예를 들어, `.cfignore` 파일의 다음 컨텐츠는 모든 `.swp` 파일과 `tmp/` 디렉토리 아래의 모든 파일 및 서브디렉토리가 {{site.data.keyword.Bluemix_notm}}에 업로드되지 않음을 나타냅니다.

```
*.swp
tmp/
```

# 관련 링크
{: #rellinks notoc}

## 관련 링크
{: #general}

* [Deploying with Application Manifests ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [IBM Continuous Delivery Pipeline for Bluemix 시작하기](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
