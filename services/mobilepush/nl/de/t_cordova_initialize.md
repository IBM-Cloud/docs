---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# Cordova-Plug-in
{: #cordova_enable}

Bevor Sie das Cordova-Plug-in für Push Notifications Service verwenden können, müssen Sie
es initialisieren, indem Sie die Anwendungsroute und die Anwendungs-GUID übergeben. Nach der Initialisierung des
Plug-ins können Sie die Verbindung zu der Serveranwendung herstellen, die Sie im Bluemix-Dashboard
erstellt haben. Das Cordova-Plug-in ist die Oberfläche für die Android- und iOS-Client-SDKs zum Aktivieren einer Cordova-Anwendung für die Kommunikation mit Bluemix-Services.

1. Initialisieren Sie 'BMSClient', indem Sie das folgende Code-Snippet kopieren und in Ihre Haupt-JavaScript-Datei (die für gewöhnlich im Verzeichnis **www/js** gespeichert ist) einfügen.

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Ändern Sie das Code-Snippet so, dass die Parameter für die Routen und Anwendungs-GUID von Bluemix verwendet werden. Klicken Sie auf den Link **Mobile Systemerweiterungen** in Ihrem Bluemix-Anwendungsdashboard, um
die Anwendungsroute und die App-GUID abzurufen. Verwenden Sie die Werte für die Route und die App-GUID als Parameter in Ihrem Code-Snippet des Typs `BMSClient.initialize`.


	**Hinweis**: Wenn Sie beispielsweise mit der Cordova-CLI eine Cordova-App erstellt haben, erstellt Cordova den Befehl 'app-name', speichert diesen JavaScript-Code in der Datei **index.js** hinter der Funktion `app.receivedEvent` in der Funktion `onDeviceReady: function()` zum Initialisieren des BMS-Clients.

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. Nächster Schritt: [Geräte registrieren](t_cordova_register.html)
