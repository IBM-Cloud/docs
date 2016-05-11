---

copyright:
  years: 2015, 2016

---

# 配置 {{site.data.keyword.amashort}} Client SDK for Cordova
{: #custom-cordova}
配置 Cordova 應用程式，這個應用程式利用自訂鑑別來使用 {{site.data.keyword.amashort}} Client SDK，並將您的應用程式連接至 {{site.data.keyword.Bluemix}}。


## 開始之前
{: #before-you-begin}
您必須具有配置成使用自訂身分提供者的 {{site.data.keyword.amashort}} 服務實例所保護的資源。您的行動式應用程式也必須使用 {{site.data.keyword.amashort}} Client SDK 進行檢測。如需相關資訊，請參閱下列資訊：
 * [開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [設定 Cordova SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [使用自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [建立自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## 起始設定 {{site.data.keyword.amashort}} Client SDK
{: #custom-cordova-sdk}
傳遞 applicationGUID 及 applicationRoute 參數，以起始設定 SDK。

1. 取得應用程式參數值。在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。按一下**行動式選項**。即會顯示**路徑** (`applicationRoute`) 及**應用程式 GUID** (`applicationGUID`) 值。
1. 起始設定 Client SDK。

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 將 *applicationRoute* 及 *applicationGUID* 取代為來自 {{site.data.keyword.Bluemix_notm}} 儀表板上您的應用程式的**行動式選項**畫面的**路徑**及**應用程式 GUID** 值。

## 鑑別接聽器介面
{: #custom-cordva-auth}

{{site.data.keyword.amashort}} Client SDK 提供鑑別接聽器介面，以實作自訂鑑別流程。您必須新增在鑑別處理程序的不同階段所呼叫的下列方法。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

每種方法都會處理鑑別處理程序的不同階段。

### onAuthenticationChallengeReceived 方法
{: #onAuthenticationChallengeReceived}
從 {{site.data.keyword.amashort}} 服務接收自訂鑑別盤查時，會呼叫此方法。
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### 引數
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`：由 {{site.data.keyword.amashort}} Client SDK 所提供，讓開發人員可以在認證收集期間回報鑑別盤查回答或失敗（例如取消鑑別要求的使用者）。
* `challenge`：JSON 物件，包含自訂身分提供者所傳回的自訂鑑別盤查。

透過呼叫 `onAuthenticationChallengeReceived` 方法，{{site.data.keyword.amashort}} Client SDK 會將控制權委派給開發人員。{{site.data.keyword.amashort}} 會等待認證。開發人員必須收集認證，並使用下列其中一種 `authContext` 介面方法將它們回報給 {{site.data.keyword.amashort}} Client SDK。

```JavaScript
onAuthenticationSuccess: function(info){...}
```

在成功鑑別之後，會呼叫此方法。引數包括內含鑑別成功延伸資訊的選用 JSONObject。

```JavaScript
onAuthenticationFailure: function(info){...}
```

在鑑別失敗之後，會呼叫此方法。引數包括內含鑑別失敗延伸資訊的選用 JSONObject。

## authenticationContext
{: #custom-cordova-authcontext}

`authenticationContext` 值提供作為自訂鑑別接聽器的 `onAuthenticationChallengeReceived` 方法的引數。開發人員必須收集認證，並使用 `authenticationContext` 方法將認證傳回給 {{site.data.keyword.amashort}} Client SDK 或報告失敗。請使用下列其中一種方法：

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## 自訂鑑別接聽器範例實作
{: #custom-cordova-authlisten-sample}

此鑑別接聽器範例設計成使用自訂身分提供者。您可以從[此 Github 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)下載自訂身分提供者。

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// In this sample the authentication listener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authenticationContext.submitAuthenticationChallengeAnswer() API

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report
		// it back to the authenticationContext. Otherwise Mobile Client
		// Access Client SDK will remain in a waiting-for-credentials state
		// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```

## 登錄自訂鑑別接聽器
{: #custom-cordova-authreg}

建立自訂鑑別接聽器之後，請先向 `BMSClient` 登錄它，再開始使用。將下列程式碼新增至應用程式。先呼叫此程式碼，再將任何要求傳送至受保護資源。

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 使用 {{site.data.keyword.amashort}} 儀表板中所指定的 *realmName*。


## 測試鑑別
{: #custom-cordova-test}
起始設定 Client SDK 並登錄自訂 AuthenticationListener 之後，即可開始對行動式後端提出要求。

### 開始之前
{: #custom-cordova-testing-before}
您必須具有使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立的應用程式，並在 `/protected` 端點具有 {{site.data.keyword.amashort}} 所保護的資源。


1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），以在瀏覽器中將要求傳送給行動式後端的受保護端點。使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取這個端點。因此，會在瀏覽器中顯示 `Unauthorized` 訊息。

1. 使用 Cordova 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 並登錄自訂 AuthenticationListener 之後，請新增下列程式碼。

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 	當要求成功時，在 LogCat 或 Xcode 主控台中會有下列輸出：

	![影像](images/android-custom-login-success.png)

	![影像](images/ios-custom-login-success.png)
