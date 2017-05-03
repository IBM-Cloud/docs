---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Bluemix에서 Tomcat 시작하기
{: #getting_started}

* {: download} 축하합니다. {{site.data.keyword.Bluemix}}에 Hello World 샘플 애플리케이션을 배치했습니다. 시작하려면 이 단계별 안내서를 따르십시오. 또는 <a class="xref" href="http://bluemix.net" target="_blank" title="(샘플 코드 다운로드)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="애플리케이션 코드 다운로드" />샘플 코드를 다운로드</a>하고 직접 탐색하십시오.

이 안내서를 통해 개발 환경을 설정하고, 앱을 로컬 및 {{site.data.keyword.Bluemix}}에 배치하고, 앱에 {{site.data.keyword.Bluemix}} 데이터베이스 서비스를 통합합니다.

## 전제조건
{: #prereqs}

다음이 필요합니다.
* [{{site.data.keyword.Bluemix_notm}} 계정](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git-scm.com/downloads){: new_window}
* [Maven ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat 버전 8.0.41 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## 1. 샘플 앱 복제
{: #clone}

이제 샘플 Tomcat 앱에 대한 작업을 시작할 준비가 되었습니다. 저장소를 복제하고 샘플 앱이 있는 디렉토리로 변경하십시오.
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

*get-started-tomcat* 디렉토리에서 파일을 확인하여 컨텐츠를 익히십시오.

## 2. 로컬로 앱 실행
{: #run_locally}

종속 항목을 설치하고 pom.xml 파일에 정의된 대로 .war 파일을 빌드하여 앱을 실행해야 합니다.

종속 항목을 설치하십시오.

```
mvn clean install  
```
{: pre}


GetStartedTomcat.war를 `target` 디렉토리에서 `tomcat-install-dir` `webapps` 디렉토리로 복사하십시오.

앱을 실행하십시오.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: screen}

http://localhost:8080/GetStartedTomcat/에서 앱 보기

`shutdown.bat|.sh`를 사용하여 앱을 중지하십시오. 명령 실행 권한을 제공해야 합니다.
{: tip}

## 3. {{site.data.keyword.Bluemix_notm}} 배치를 위해 앱 준비
{: #prepare}

{{site.data.keyword.Bluemix_notm}}에 배치하는 경우 manifest.yml 파일을 설정하는 것이 도움이 될 수 있습니다. manifest.yml에는 앱에 대한 기본 정보(예: 이름, 각 인스턴스에 할당할 메모리 크기, 라우트)가 포함됩니다. `get-started-tomcat` 디렉토리에 샘플 manifest.yml 파일을 제공했습니다.

manifest.yml 파일을 열고 `name`을 `GetStartedTomcat`에서 앱 이름 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>으로 변경하십시오.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/TomcatHelloWorldApp.war
    buildpack: java_buildpack
  ```
  {: codeblock}

이 manifest.yml 파일에서 **random-route: true**는 사용자 라우트가 다른 라우트와 충돌하지 않도록 앱을 위한 임의 라우트를 생성합니다. 원하는 경우, **random-route: true**를 **host: myChosenHostName**으로 바꾸고 사용하려는 호스트 이름을 제공할 수 있습니다. [자세히 보기...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. 앱 배치
{: #deploy}

Cloud Foundry CLI를 사용하여 앱을 배치할 수 있습니다. 

API 엔드포인트를 선택하십시오.

```
cf api <API-endpoint>
```
{:pre}

명령의 *API-endpoint*를 다음 목록의 API 엔드포인트로 바꾸십시오.

|URL                             |지역          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | 미국 남부       |
| https://api.eu-gb.bluemix.net  | 영국 |
| https://api.au-syd.bluemix.net | 시드니         |


{{site.data.keyword.Bluemix_notm}} 계정에 로그인하십시오.

```
cf login
```
{: pre}

*get-started-tomcat* 디렉토리에서 {{site.data.keyword.Bluemix_notm}}에 앱 푸시
```
cf push
```
{: pre}

이를 수행하는 데 약 2분이 걸릴 수 있습니다. 배치 프로세스에 오류가 있는 경우 `cf logs <Your-App-Name> --recent` 명령을 사용하여 문제점을 해결할 수 있습니다. 

배치가 완료되면 앱이 실행 중이라는 메시지가 표시됩니다. push 명령의 출력에 나열된 URL에서 앱을 확인하십시오. 또한
  ```
cf apps
  ```
  {: pre}
  명령을 실행하여 앱 상태를 보고 URL을 확인할 수 있습니다.

## 6. Eclipse에서 개발
{: #developing_in_eclipse}

IBM® Eclipse Tools for {{site.data.keyword.Bluemix}}는 기존 Eclipse 환경에 설치할 수 있는 플러그인을 제공하며, 이를 통해 개발자의 IDE(Integrated Development Environment)를 {{site.data.keyword.Bluemix_notm}}와 통합할 수 있습니다.

[IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix)를 다운로드하고 설치하십시오.

`파일` -> `가져오기` -> `Maven` -> `기존 Maven 프로젝트` 옵션을 사용하여 이 샘플을 Eclipse로 가져오십시오.

Tomcat 서버 정의 작성:
  - `서버` 보기에서 마우스 오른쪽 단추 클릭 -> `새로 작성` -> `서버`를 선택하십시오.
  - `Apache` -> `Tomcat v8.0 서버`를 선택하십시오.
  - `tomcat-install-dir`을 선택하십시오.
  - 기본 옵션으로 마법사를 계속 진행하여 완료하십시오.

Apache 서버에서 로컬로 애플리케이션 실행:
  - `GetStartedTomcat` 샘플을 마우스 오른쪽 단추로 클릭하고 `실행 도구` -> `서버에서 실행` 옵션을 선택하십시오.
  - 로컬 호스트 Tomcat 서버를 찾아 선택하고 완료를 클릭하십시오.
  - 몇 초 후에 애플리케이션이 http://localhost:8080/TomcatHelloWorldApp/에서 실행됩니다.

{{site.data.keyword.Bluemix_notm}} 서버 정의 작성:
  - `서버` 보기에서 마우스 오른쪽 단추 클릭 -> `새로 작성` -> `서버`를 선택하십시오.
  - `IBM` -> `IBM Bluemix`를 선택하고 마법사의 단계를 수행하십시오.
  - 신임 정보를 입력하고 `다음`을 클릭하십시오.
  - `조직` 및 `영역`을 선택하고 `완료`를 클릭하십시오.

{{site.data.keyword.Bluemix_notm}}에서 애플리케이션 실행:
  - `GetStartedTomcat` 샘플을 마우스 오른쪽 단추로 클릭하고 `실행 도구` -> `서버에서 실행` 옵션을 선택하십시오.
  - `IBM Bluemix`를 찾아 선택하고 완료를 누르십시오.
  - 마법사를 통해 배치 옵션을 사용할 수 있습니다. 애플리케이션의 고유 `이름`을 선택해야 합니다.
  - 몇 분 후에 애플리케이션이 선택한 URL에서 실행됩니다.

이제 로컬 및 클라우드에서 코드를 실행하게 되었습니다.

## 7. 데이터베이스 추가
{: #add_database}

다음으로, 이 애플리케이션에 NoSQL 데이터베이스를 추가하고 애플리케이션을 설정하여 로컬 및 Bluemix에서 이를 실행할 수 있도록 합니다.

1. 브라우저에서 {{site.data.keyword.Bluemix_notm}}에 로그인하십시오. `대시보드`로 이동하십시오. `이름` 열에서 해당 이름을 클릭하여 애플리케이션을 선택하십시오.
2. `연결`을 클릭한 다음 `새로 연결`을 클릭하십시오.
2. `데이터 및 분석` 섹션에서 `Cloudant NoSQL DB`를 선택한 다음 서비스를 `작성`하십시오.
3. 프롬프트가 표시되면 `다시 스테이징`을 선택하십시오. {{site.data.keyword.Bluemix_notm}}가 애플리케이션을 다시 시작하고, `VCAP_SERVICES` 환경 변수를 사용하여 애플리케이션에 데이터베이스 신임 정보를 제공합니다. 이 환경 변수는 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우에만 애플리케이션에서 사용 가능합니다.

환경 변수를 사용하면 배치 설정을 소스 코드와 구분할 수 있습니다. 예를 들어, 데이터베이스 비밀번호를 하드 코딩하는 대신 소스 코드에서 참조하는 환경 변수에 이 비밀번호를 저장할 수 있습니다. [자세히 보기...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 8. 데이터베이스 사용
{: #use_database}
이제 이 데이터베이스를 가리키도록 로컬 코드를 업데이트합니다. 특성 파일에 서비스의 신임 정보를 저장합니다. 이 파일은 애플리케이션이 로컬로 실행 중인 경우에만 사용됩니다. {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우 신임 정보는 VCAP_SERVICES 환경 변수에서 읽습니다.

1. Eclipse를 열고 파일 src/main/resources/cloudant.properties를 여십시오.
  ```
  cloudant_url=
  ```
  {: pre}

2. 브라우저에서 {{site.data.keyword.Bluemix_notm}} UI를 열고 앱 -> 연결 -> Cloudant -> 신임 정보 보기를 선택하십시오.

3. 신임 정보의 `url`을 복사하여 `cloudant.properties` 파일의 `url` 필드에 붙여넣고 변경사항을 저장하십시오. 결과는 다음과 비슷합니다.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. `서버` 보기에서 Eclipse의 Tomcat 서버를 다시 시작하십시오.

  http://localhost:8080/GetStartedTomcat/에서 브라우저 보기를 새로 고치십시오. 이제 앱에 입력한 이름이 데이터베이스에 추가됩니다.

  로컬 앱과 {{site.data.keyword.Bluemix_notm}} 앱은 데이터베이스를 공유합니다. 위에서 push 명령의 출력에 나열된 URL을 통해 {{site.data.keyword.Bluemix_notm}} 앱을 확인하십시오. 이 중 하나의 앱에서 추가하는 이름은 브라우저를 새로 고치면 두 앱에 모두 표시됩니다.

{{site.data.keyword.Bluemix_notm}}에서 앱을 지속할 필요가 없는 경우 예상치 않은 비용이 발생하지 않도록 앱을 중지하십시오.
{: tip}  
