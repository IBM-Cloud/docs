---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# Cordova 플러그인 초기화
{: #cordova_enable}

푸시 알림 서비스 Cordova 플러그인을 사용할 수 있으려면 애플리케이션 라우트와 애플리케이션 GUID를 전달하여 플러그인을 초기화해야 합니다. 플러그인을 초기화한 후 Bluemix 대시보드에서 작성한 서버 앱에 연결할 수 있습니다. Cordova 플러그인은 Cordova 앱이 Bluemix 서비스와 통신할 수 있도록 해주는 Android 및 iOS 클라이언트 SDK용 랩퍼입니다. 

1. 다음 코드 스니펫을 복사하여 기본 JavaScript 파일(일반적으로 **www/js** 디렉토리 아래에 있음)에 붙여넣어 BMSClient를 초기화하십시오. 

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Bluemix Route 및 appGUID 매개변수를 사용하려면 코드 스니펫을 수정하십시오. Bluemix 애플리케이션 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 애플리케이션 GUID를 확보하십시오. ```BMSClient.initialize``` 코드 스니펫에서 라우트 및 앱 GUID 값을 매개변수로 사용하십시오. 


	**참고**: Cordova CLI(예: Cordova create app-name 명령)를 사용하여 Cordova 앱을 작성한 경우 이 Javascript 코드를 **index.js** 파일에서 ```onDeviceReady: function()``` 함수의 ```app.receivedEvent`` 함수 뒤에 넣어서 BMS 클라이언트를 초기화하십시오. 

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. 다음 단계. [디바이스를 등록하십시오.](t_cordova_register.html) 
