---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# Initializing the Cordova plug-in
{: #cordova_enable}

Before you can use the Push Notification Service Cordova plug-in, you need to initialize it by passing the application route and application GUID. After initializing the plug-in, you can connect to the server app that you have created in the Bluemix dashboard. The Cordova plug-in is the wrapper for the Android and iOS client SDKs to enable a Cordova app to communicate with Bluemix services.

1. Initialize the BMSClient by copying and pasting the following code snippet into your main JavaScript file (typically located under the **www/js** directory).

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Modify the code snippet to use your Bluemix Route and appGUID parameters. Click the **Mobile Options** link in your Bluemix Application Dashboard to get the application Route and App GUID. Use the Route and App GUID values as your parameters in your ```BMSClient.initialize``` code snippet.


	**Note**: If you have created a Cordova app using the Cordova CLI, for example, Cordova create app-name command, put this Javascript code in the **index.js** file, after the ```app.receivedEvent``` function within the o```nDeviceReady: function()``` function to initialize the BMS client.

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. Next step. [Registering Devices](t_cordova_register.html).
