<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld 샘플 시작하기
{: #gettingstarted-android}

새 Android 애플리케이션을 시작하려면 HelloWorld 앱을 사용할 수 있습니다. 이 앱은 인증 없이 모바일 앱에서 {{site.data.keyword.Bluemix}} 백엔드에 연결하는 방법을 보여줍니다. 앱에는 이미 SDK가 설치되어 있습니다. 준비가 되었으면 앱에서 사용할 특정 라이브러리를 가져올 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}}에서 모바일 백엔드를 작성하십시오.
    1. 표준 유형 섹션 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 MobileFirst Services Starter를 클릭하십시오.
    2. 앱에 대한 이름 및 호스트를 입력하고 **작성**을 클릭하십시오.
    3. **완료**를 클릭하십시오.
2. GitHub에서 프로젝트를 가져오십시오. 필요에 따라 git clone 명령을 사용하여 프로젝트를 가져올 수 있습니다. 컴퓨터에서 터미널을 열고 다음 명령을 입력하십시오. 
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
```
{: codeblock}

시작하기 전에 `Gradle.zip` 파일을 다운로드하고 다운로드된 압축 파일을 선택한 디렉토리에 추출하여 Gradle을 설치하십시오. Android Studio에서는 사용자가 처음 샘플을 가져올 때 GRADLE HOME을 요청할 수 있습니다. 추출된 `Gradle.zip` 파일에 있는 `bin` 디렉토리로 해당 경로를 설정하십시오. `build.gradle` 파일은 필수 종속 항목에서 풀링하여 자동으로 프로젝트를 빌드합니다.
3. `BMSClient.getInstance().initialize()` 함수 내의 try 블록에 있는 사용자의 애플리케이션 라우트 및 GUID로 &lt;APPLICATION_ROUTE&gt; 및 &lt;APPLICATION_ID&gt;를 대체하여 프로젝트를 초기화하십시오. 
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
{: codeblock}

4. 개발 환경에서 샘플을 실행하십시오.
Android Studio 도구 모음에서 **재생** 단추를 클릭하고 시뮬레이터를 선택하십시오.

  시뮬레이터에서 **{{site.data.keyword.Bluemix_notm}} Ping**을 클릭하십시오. 샘플 앱이 {{site.data.keyword.Bluemix_notm}}의 `Node.js` 런타임에 있는 보호되는 자원으로 Get 요청을 전송합니다. 요청이 성공하면 연결이 확인되고 시뮬레이터의 텍스트가 업데이트됩니다.

  **참고:** `Node.js` 런타임 코드는 MobileFirst Services Starter 표준 유형으로 제공됩니다. 백엔드 애플리케이션이 MobileFirst Services Starter 표준 유형으로 작성되지 않은 경우, 애플리케이션이 성공적으로 연결되지 않습니다.

  Android Studio의 모바일 앱에서 {{site.data.keyword.Bluemix_notm}}에 연결되면 다음 메시지가 표시됩니다.
  연결되었습니다.
  {: screen}

  ![Hello World 애플리케이션이 {{site.data.keyword.Bluemix_notm}}에 연결됨](images/yayconnected.jpg "그림 1. Hello World 애플리케이션이 Bluemix에 연결됨")

  연결이 실패하면 다음이 표시됩니다.
  문제점이 발생했습니다.
  {: screen}

  ![Hello World 애플리케이션이 Bluemix에 연결되지 않음](images/bummer_android.jpg "그림 2. Hello World 애플리케이션이 Bluemix에 연결되지 않음")

  다음과 같이 연결 실패를 해결할 수 있습니다.
   * 라우트 및 GUID 값을 올바르게 붙여넣었는지 확인하십시오.
   * 자세한 정보는 디버그 로그를 검토하십시오.

## 다음 단계:
{: #next}
SDK를 가져와서 모바일 앱에 통합하는 방법에 대한 정보는 Bluemix 서비스 설정에 대한 정보를 참조하십시오.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 관련 링크

## 샘플
   * [HelloWorld(Android)](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [코어 API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
