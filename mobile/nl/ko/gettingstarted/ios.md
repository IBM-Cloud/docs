<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# HelloWorld 샘플 시작하기
{: #gettingstarted-ios}
*마지막 업데이트 날짜: 2016년 1월 28일*

새 iOS 앱을 시작하고자 하는 경우 HelloWorld 앱을 사용할 수 있습니다. 이 앱에서는 인증 없이 모바일 앱에서 {{site.data.keyword.Bluemix}} 백엔드에 연결하는 방법을 예시합니다. 앱에는 이미 SDK가 설치되어 있습니다. 준비가 완료되면 사용자는 앱에서 사용할 특정 라이브러리를 가져올 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}}에서 모바일 백엔드를 작성하십시오.
<ol>
	<li>{{site.data.keyword.Bluemix_notm}} 카탈로그의 표준 유형 섹션에서 **MobileFirst Services 스타터**를 클릭하십시오.</li>
    <li>앱에 대한 이름 및 호스트를 입력하고 **작성**을 클릭하십시오.</li>
    <li>**완료**를 클릭하십시오.</li>
</ol>
2. GitHub에서 프로젝트를 가져오십시오.
컴퓨터에서 터미널을 열고, 다음 명령을 입력하십시오.
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. 프로젝트를 초기화하십시오.
SDK를 초기화하려면 Application Delegate의 `didFinishLaunchingWithOptions` 메소드에 다음 코드를 복사하십시오.
   * Objective-C:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. 개발 환경에서 샘플을 실행하십시오.
Xcode에서 **Product&gt; Run**을 클릭하십시오. iOS 시뮬레이터가 시작됩니다.
시뮬레이터에서 **Ping {{site.data.keyword.Bluemix_notm}}**를 클릭하십시오. 샘플 앱이 Mobile Client Access 서비스에서 권한 부여 헤더를 가져옵니다. ping 실행이 성공하면 시뮬레이터의 텍스트가 업데이트됩니다.
<br/>Xcode의 모바일 앱에서 {{site.data.keyword.Bluemix_notm}}에 연결이 완료되면 "Yay! You are connected"라는 메시지가 표시됩니다.<br/>
![Hello World 애플리케이션이 {{site.data.keyword.Bluemix_notm}}에 성공적으로 연결됨](images/yayconnected.jpg "그림 1. Hello World 애플리케이션이 {{site.data.keyword.Bluemix_notm}}에 성공적으로 연결됨")
<br/>
성공적으로 연결하면 디버그 로그인 Xcode에 다음 메시지가 포함됩니다.
```You have connected to {{site.data.keyword.Bluemix_notm}} successfully```
5. 문제점을 해결하십시오.
연결에 실패하면 "Bummer Something went wrong" 메시지가 표시됩니다. 오류에 대한 자세한 정보가 포함됩니다. <br/>
![Hello World 애플리케이션이 {{site.data.keyword.Bluemix_notm}}에 연결되지 않음](images/bummer_android.jpg "그림 2. Hello World 애플리케이션이 Bluemix에 연결되지 않음")
<br/>라우트와 GUID 값을 올바르게 붙여넣었는지 확인하십시오.
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


디버그 로그에서 자세한 정보를 확인할 수도 있습니다.

## 다음 단계:
{: #next}
SDK를 가져와 모바일 앱에 통합하는 방법에 대한 정보는 {{site.data.keyword.Bluemix}} 서비스 설정에 대한 정보를 참조하십시오.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 관련 링크

## 샘플
   * [HelloWorld 샘플](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## SDK
   * [코어 SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## API
* [코어 API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
