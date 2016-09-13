---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# 初始化 Cordova 插件
{: #cordova_enable}

开始使用 Push Notification Service Cordova 插件之前，需要通过传递应用程序路径和应用程序 GUID 对其进行初始化。 初始化该插件后，可以连接到在 Bluemix“仪表板”中创建的服务器应用程序。 Cordova 插件是 Android 和 iOS 客户机 SDK 的包装程序，可以使 Cordova 应用程序能够与 Bluemix 服务进行通信。

1. 通过将以下代码片段复制并粘贴到主 JavaScript 文件（通常位于 **www/js** 目录下）中来初始化 BMSClient。

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. 修改代码片段以使用 Bluemix 的 Route 和 appGUID 参数。 单击 Bluemix 的“应用程序仪表板”中的**移动选项**链接，以获取应用程序的“路径”和“应用程序 GUID”。 在 ```BMSClient.initialize``` 代码片段中将“路径”和“应用程序 GUID”值作为您的参数。


	**注**：如果是使用 Cordova CLI（例如，Cordova create app-name 命令）创建的 Cordova 应用程序，请将此 JavaScript 代码放入 **index.js** 文件内 ```nDeviceReady: function()``` 函数中的 ```app.receivedEvent`` 函数之后，以初始化 BMS 客户机。

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. 后续步骤： [注册设备](t_cordova_register.html)。
