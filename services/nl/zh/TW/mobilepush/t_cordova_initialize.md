---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# 起始設定 Cordova 外掛程式
{: #cordova_enable}

您需要透過傳遞應用程式路徑及應用程式 GUID 來起始設定 Push Notification Service Cordova 外掛程式，才能使用該外掛程式。在起始設定外掛程式之後，您可以連接至在 Bluemix 儀表板中所建立的伺服器應用程式。Cordova 外掛程式是 Android 及 iOS Client SDK 的封套，可讓 Cordova 應用程式與 Bluemix 服務通訊。

1. 複製下列程式碼 Snippet，並將其貼入您的主要 JavaScript 檔案（通常位於 **www/js** 目錄下），以起始設定 BMSClient。

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. 修改程式碼 Snippet，以使用您的 Bluemix「路徑」及「應用程式 GUID」參數。按一下「Bluemix 應用程式儀表板」中的**行動式選項**鏈結，以取得應用程式的「路徑」及「應用程式 GUID」。請使用「路徑」及「應用程式 GUID」的值，作為 ```BMSClient.initialize``` 程式碼 Snippet 中的參數。


	**附註**：如果您已使用 Cordova CLI（例如，Cordova create app-name 指令）建立 Cordova 應用程式，請將此 Javascript 程式碼放置在 **index.js** 檔案中 ```onDeviceReady: function()``` 函數內的 ```app.receivedEvent`` 函數後面，以起始設定 BMS 用戶端。

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. 後續步驟。[登錄裝置](t_cordova_register.html)。
