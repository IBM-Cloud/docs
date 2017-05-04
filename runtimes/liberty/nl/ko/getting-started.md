---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Bluemix에서 Liberty 시작하기

* {: download} 축하합니다. {{site.data.keyword.Bluemix}}에 Hello World 샘플 애플리케이션을 배치했습니다. 시작하려면 이 단계별 안내서를 따르십시오. 또는 <a class="xref" href="http://bluemix.net" target="_blank" title="(샘플 코드 다운로드)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="애플리케이션 코드 다운로드" />샘플 코드를 다운로드</a>하고 직접 탐색하십시오.

이 안내서를 통해 개발 환경을 설정하고, 앱을 로컬 및 {{site.data.keyword.Bluemix}}에 배치하고, 앱에 {{site.data.keyword.Bluemix}} 데이터베이스 서비스를 통합합니다.

## 전제조건
{: #prereqs}

다음 계정과 도구가 필요합니다.
* [{{site.data.keyword.Bluemix_notm}} 계정](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git-scm.com/downloads){: new_window}
* [Maven ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://maven.apache.org/download.cgi){: new_window}

Eclipse에서 {{site.data.keyword.eclipsetoolsfull}}를 사용하여 개발하려면 [도구를 다운로드해야 합니다. ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}

## 1. 샘플 앱 복제
{: #clone}

먼저, 샘플 앱 GitHub 저장소를 복제하십시오.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. 명령행을 사용하여 로컬로 앱 실행
{: #run_locally}

Maven을 사용하여 소스 코드를 빌드하고 결과 앱을 실행하십시오.

1. 명령행에서 디렉토리를 샘플 앱이 있는 위치로 변경하십시오.

  ```
cd get-started-java
  ```
  {: pre}

1. Maven을 사용하여 종속 항목을 설치하고 .war 파일을 빌드하십시오.

  ```
mvn clean install
  ```
  {: pre}

1. Liberty에서 로컬로 앱을 실행하십시오.
  ```
mvn install liberty:run-server
  ```
  {: pre}

*The server defaultServer is ready to run a smarter planet.* 메시지가 표시되면, http://localhost:9080/GetStartedJava에서 앱을 확인하십시오.

앱을 중지하려면 앱을 시작한 명령행 창에서 *Ctrl-C*를 누르십시오.

## 3. 배치를 위한 앱 준비
{: #prepare}

{{site.data.keyword.Bluemix_notm}}에 배치하는 경우 manifest.yml 파일을 설정하는 것이 도움이 될 수 있습니다. manifest.yml에는 앱에 대한 기본 정보(예: 이름, 각 인스턴스에 할당할 메모리 크기, 라우트)가 포함됩니다. `get-started-java` 디렉토리에 샘플 manifest.yml 파일을 제공했습니다.

manifest.yml 파일을 열고 `name`을 `GetStartedJava`에서 앱 이름 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>으로 변경하십시오.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

이 manifest.yml 파일에서 **random-route: true**는 사용자 라우트가 다른 라우트와 충돌하지 않도록 앱을 위한 임의 라우트를 생성합니다. 원하는 경우, **random-route: true**를 **host: myChosenHostName**으로 바꾸고 사용하려는 호스트 이름을 제공할 수 있습니다. [자세히 보기...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. {{site.data.keyword.Bluemix_notm}}에 배치
{: #deploy}

다음 Bluemix 지역 중 하나에 앱을 배치하십시오. 최적의 대기 시간을 위해 사용자에 가장 가까운 지역을 선택하십시오.

|지역          |API 엔드포인트                             |
|:---------------|:-------------------------------|
| 미국 남부       | https://api.ng.bluemix.net     |
| 영국 | https://api.eu-gb.bluemix.net  |
| 시드니         | https://api.au-syd.bluemix.net |

1. `<API-endpoint>`를 지역의 엔드포인트로 바꿔 API 엔드포인트를 설정하십시오.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. {{site.data.keyword.Bluemix_notm}} 계정에 로그인하십시오.
  ```
cf login
  ```
  {: pre}

1. `get-started-java` 디렉토리 내에서 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하십시오.
  ```
cf push
  ```
  {: pre}

애플리케이션 배치에 몇 분이 소요될 수 있습니다. 배치가 완료되면 앱이 실행 중이라는 메시지가 표시됩니다. push 명령의 출력에 나열된 URL에서 앱을 보거나, 다음 명령을 실행하여 앱 배치 상태 및 URL을 확인하십시오.
  ```
cf apps
  ```
  {: pre}

`cf logs <Your-App-Name> --recent` 명령을 사용하여 배치 프로세스에서 오류를 해결할 수 있습니다.
{: tip}  

## 5. Eclipse를 사용하여 개발
{: #eclipse}

{{site.data.keyword.eclipsetoolsfull}}는 기존 Eclipse 환경에 설치할 수 있는 플러그인을 제공하며, 이를 통해 사용자의 IDE(Integrated Development Environment)를 {{site.data.keyword.Bluemix_notm}}와 통합할 수 있습니다.

1. [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix)가 있는지 확인하십시오.

2. **파일 > 가져오기 > Maven > 기존 Maven 프로젝트**로 이동하여 `get-started-java` 샘플을 Eclipse로 가져오십시오.

3. Liberty 서버 정의를 작성하십시오. 다음 단계에서는 새 Liberty 서버를 다운로드합니다.
  - **창 > 보기 표시 > 서버** 보기에서 마우스 오른쪽 단추를 클릭하고 **새로 작성 > 서버**를 선택하십시오.
  - **IBM > WebSphere Application Server Liberty**를 선택하십시오.
  - **아카이브 또는 저장소에서 설치**를 선택하십시오.
  - 프롬프트가 표시되면 Liberty를 설치할 새 폴더(/Users/username/liberty)에 대한 대상 경로를 입력하십시오.
  - **ibm.com에서 새 런타임 환경 다운로드 및 설치**를 선택하십시오.
  - **WAS Liberty with Java EE 7 Web Profile**을 선택하십시오.
  - 기본 옵션으로 마법사를 계속 진행하여 완료하십시오.

4. 다음과 같이 Liberty에서 로컬로 애플리케이션을 실행하십시오.
  - **창 > 웹 브라우저 > 기본 시스템 웹 브라우저**로 이동하여 웹 브라우저를 시스템 기본값으로 변경하십시오.
  - `GetStartedJava` 샘플을 마우스 오른쪽 단추로 클릭하고 **실행 도구 > 서버에서 실행**을 선택하십시오.
  - 로컬 호스트 Liberty 서버를 찾아 선택하고 **완료**를 클릭하십시오.

  몇 초 후에 애플리케이션이 http://localhost:9080/GetStartedJava에서 실행됩니다.

5. 다음과 같이 코드를 업데이트하십시오.
  - `src/main/webapp/index.html`을 열고 표제를 `<h1>Welcome.</h1>`에서 `<h1>Welcome Jane.</h1>`으로 업데이트하십시오.
  - 변경사항을 저장하십시오. Liberty에서 변경사항을 자동으로 가져옵니다.
  - 브라우저(http://localhost:9080/GetStartedJava)를 새로 고쳐 변경사항을 확인하십시오.

6. 다음과 같이 변경사항을 {{site.data.keyword.Bluemix_notm}}로 푸시하십시오.
  - 명령행의 `get-started-java` 디렉토리에서 .war 파일을 다시 빌드하십시오.
    ```
mvn clean install
    ```
    {: pre}
  - 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하십시오.
    ```
cf push
    ```
    {: pre}

이제 로컬 및 클라우드 모두에서 코드를 실행하게 되었습니다.

## 6. 데이터베이스 추가
{: #add_database}

다음으로, 이 애플리케이션에 NoSQL 데이터베이스를 추가하고 애플리케이션을 설정하여 로컬 및 {{site.data.keyword.Bluemix_notm}}에서 이를 실행할 수 있도록 합니다.

1. 브라우저에서 {{site.data.keyword.Bluemix_notm}}에 로그인하고 대시보드로 이동하십시오. **이름** 열에서 해당 이름을 클릭하여 애플리케이션을 선택하십시오.
2. **연결**을 클릭한 다음 **새로 연결**을 클릭하십시오.
3. **데이터 및 분석** 섹션에서 **Cloudant NoSQL DB**를 선택한 다음 서비스를 작성하십시오.
4. 프롬프트가 표시되면 **다시 스테이징**을 선택하십시오. {{site.data.keyword.Bluemix_notm}}가 애플리케이션을 다시 시작하고, `VCAP_SERVICES` 환경 변수를 사용하여 애플리케이션에 데이터베이스 신임 정보를 제공합니다. 이 환경 변수는 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우에만 애플리케이션에서 사용 가능합니다.

환경 변수를 사용하면 배치 설정을 소스 코드와 구분할 수 있습니다. 예를 들어, 데이터베이스 비밀번호를 하드 코딩하는 대신 소스 코드에서 참조하는 환경 변수에 이 비밀번호를 저장할 수 있습니다. [자세히 보기...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. 데이터베이스 사용
{: #use_database}
이제 이 데이터베이스를 가리키도록 로컬 코드를 업데이트합니다. 특성 파일에 서비스의 신임 정보를 저장합니다. 이 파일은 애플리케이션이 로컬로 실행 중인 경우에만 사용됩니다. {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우 신임 정보는 `VCAP_SERVICES` 환경 변수에서 읽습니다.

1. Eclipse에서 src/main/resources/cloudant.properties 파일을 여십시오.
  ```
  cloudant_url=
  ```
  {: pre}

2. 브라우저에서 {{site.data.keyword.Bluemix_notm}}로 이동하고 **앱 > _your app_ > 연결 > Cloudant > 신임 정보 보기**를 선택하십시오.

3. 신임 정보의 `url`을 복사하여 `cloudant.properties` 파일의 `url` 필드에 붙여넣고 변경사항을 저장하십시오.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. `서버` 보기에서 Eclipse의 Liberty 서버를 다시 시작하십시오.

  http://localhost:9080/GetStartedJava/에서 브라우저 보기를 새로 고치십시오. 이제 앱에 입력한 이름이 데이터베이스에 추가됩니다.

  로컬 앱과 {{site.data.keyword.Bluemix_notm}} 앱은 데이터베이스를 공유합니다. 이 중 하나의 앱에서 추가하는 이름은 브라우저를 새로 고치면 두 앱에 모두 표시됩니다.


{{site.data.keyword.Bluemix_notm}}에서 앱을 지속할 필요가 없는 경우 예상치 않은 비용이 발생하지 않도록 앱을 중지하십시오.
{: tip}  
