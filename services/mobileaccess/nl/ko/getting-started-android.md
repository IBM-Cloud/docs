---

copyright:
  years: 2015, 2016
  
---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Android SDK 설정
{: #getting-started-android}

마지막 업데이트 날짜: 2016년 8월 2일
{: .last-updated}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 Android 애플리케이션을 계측하고 SDK를 초기화하고 보호 및 비보호 리소스를 요청하십시오.
{:shortdesc}

## 시작하기 전에
{: #before-you-begin}
다음이 있어야 합니다.
* {{site.data.keyword.amashort}} 서비스를 통해 보호하는 {{site.data.keyword.Bluemix_notm}} 애플리케이션의 인스턴스입니다. {{site.data.keyword.Bluemix_notm}} 백엔드 애플리케이션 작성 방법에 대한 자세한 정보는 [시작하기](index.html)를 참조하십시오. 
* Gradle과 작동하도록 설정된 Android Studio 프로젝트. Android 개발 환경을 설정하는 방법에 대한 자세한 정보는 [Google 개발자 도구](http://developer.android.com/sdk/index.html)를 참조하십시오. 


## {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #install-mca-sdk}

{{site.data.keyword.amashort}} 클라이언트 SDK는 Android 프로젝트용 종속성 관리자인 Gradle을 사용하여 분배됩니다. Gradle은 저장소에서 아티팩트를 자동으로 다운로드하여 Android 애플리케이션에서 사용할 수 있게 합니다. 

1. Android Studio 프로젝트를 작성하거나 기존 프로젝트를 여십시오. 

1. 애플리케이션에 대한 `build.gradle` 파일을 여십시오(프로젝트 `build.gradle` 파일이 **아님**).

1. `build.gradle` 파일의 **종속 항목** 섹션을 찾으십시오. {{site.data.keyword.amashort}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오.

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
}
```

1. 프로젝트를 Gradle과 동기화하십시오. **도구 &gt; Android &gt; Gradle 파일과 프로젝트 동기화**를 클릭하십시오. 

1. Android 프로젝트에 대한 `AndroidManifest.xml` 파일을 여십시오. `<manifest>` 요소 아래 인터넷 액세스 권한을 추가하십시오. 

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #initalize-mca-sdk}

`context`, `applicationGUID`, `applicationRoute` 및 `BMSClient.REGION_UK` 매개변수를 `initialize` 메소드에 전달하여 SDK를 초기화하십시오. 


1. {{site.data.keyword.Bluemix_notm}} 대시보드의 기본 페이지에서 사용자 앱을 클릭하십시오. **모바일 옵션**을 클릭하십시오. SDK를 초기화하려면 **애플리케이션 라우트** 및 **애플리케이션 GUID** 값이 필요합니다. 

2. Android 애플리케이션에서 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 Android 애플리케이션 기본 활동의 `onCreate` 메소드입니다. 
<br/>*applicationRoute* 및 *applicationGUID*를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션**의 값으로 대체하십시오.

 ```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID",
					BMSClient.REGION_UK);
```
`BMSClient.REGION_UK`를 적절한 지역으로 대체하십시오.

{{site.data.keyword.Bluemix_notm}} 지역을 보려면 메뉴 표시줄의 **아바타** 아이콘 ![아바타 아이콘](images/face.jpg "아바타 아이콘")을 클릭하여 **계정 및 지원** 위젯을 여십시오.

## 모바일 백엔드 애플리케이션에 대한 요청 작성
{: #request}

{{site.data.keyword.amashort}} 클라이언트 SDK가 설치되고 나면 모바일 백엔드 애플리케이션에 대한 요청 작성을 시작할 수 있습니다. 

1. 요청을 새 모바일 백엔드의 보호 엔드포인트로 전송하십시오. 브라우저에서 URL `{applicationRoute}/protected`를 여십시오. (예: `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드 애플리케이션의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 인스트루먼트되는 모바일 애플리케이션에서만 액세스할 수 있으므로 브라우저에 `Unauthorized` 메시지가 리턴됩니다.

1. Android 애플리케이션을 사용하여 동일한 엔드포인트에 대한 요청을 작성하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```

1. 요청에 성공하면 LogCat 유틸리티에 다음 출력이 표시됩니다. 

	![이미지](images/getting-started-android-success.png)

## 다음 단계
{: #next-steps}

보호 엔드포인트에 연결된 경우 신임 정보는 필요하지 않습니다. 사용자가 애플리케이션에 로그인하게 하려면 Facebook, Google 또는 사용자 정의 인증을 구성해야 합니다. 
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [사용자 정의](custom-auth-android.html)
