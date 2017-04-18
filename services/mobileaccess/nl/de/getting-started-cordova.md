---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Wichtig: Der Service {{site.data.keyword.amafull}} wird durch den Service {{site.data.keyword.appid_full}} ersetzt.**

# Cordova-Plug-in einrichten
{: #getting-started-cordova}

Instrumentieren Sie die Cordova-Clientanwendung mit dem {{site.data.keyword.amafull}}-Client-SDK. Initialisieren Sie Authorization Manager in Ihrem Android-Code (Java) oder iOS-Code (Objective C unter Verwendung von Swift-SDK und der entsprechenden Headerdatei). Initialisieren Sie den Client und setzen Sie über WebView Anforderungen an geschützte und ungeschützte Ressourcen ab.

{:shortdesc}

## Vorbereitungen
{: #before-you-begin}
Voraussetzungen:

* Eine Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Eine Instanz eines {{site.data.keyword.amafull}}-Service.
* Die URL der Back-End-Anwendung (**App-Route**). Sie benötigen diese Werte zum Senden von Anforderungen an die geschützten Endpunkte der Back-End-Anwendung.
* Der Wert für die Tenant-ID. Öffnen Sie den Service im {{site.data.keyword.amashort}}-Dashboard. Klicken Sie auf die Schaltfläche **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Sie benötigen diesen Wert für die Initialisierung von Authorization Manager.
* Die {{site.data.keyword.Bluemix_notm}}-**Region**. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol"). Der Regionswert, der angezeigt wird, sollte einer der folgenden sein: `USA (Süden)`, `Vereinigtes Königreich` oder `Sydney`. Außerdem sollte er den im WebView-JavaScript-Code erforderlichen SDK-Werten entsprechen: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` oder `BMSClient.REGION_UK`. Sie benötigen diesen Wert für die Initialisierung des {{site.data.keyword.amashort}}-Clients.
* Cordova-Anwendung oder ein vorhandenes Projekt. Weitere Informationen zur Einrichtung Ihrer Cordova-Anwendung finden Sie auf der [Cordova-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cordova.apache.org/){: new_window}.

## Cordova-Plug-in für {{site.data.keyword.amashort}} installieren
{: #getting-started-cordova-plugin}

Das {{site.data.keyword.amashort}}-Client-SDK für Cordova ist ein Cordova-Plug-in, das als Wrapper für die nativen {{site.data.keyword.amashort}}-Client-SDKs fungiert. Es wird mithilfe der Cordova-Befehlszeilenschnittstelle (CLI) und mit `npmjs`, einem Plug-in-Repository für Cordova-Projekte verteilt. Die Cordova-CLI lädt Plug-ins automatisch aus Repositorys herunter und stellt sie Ihrer Cordova-Anwendung zur Verfügung.

1. Fügen Sie Android- und/oder iOS-Plattformen zur Ihrer Cordova-Anwendung hinzu. Führen Sie einen oder beide der folgenden Befehle über die Befehlszeile aus:

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

2. Wenn Sie die Android-Plattform hinzugefügt haben, müssen Sie die minimal unterstützte API-Stufe in der Datei `config.xml` Ihrer Cordova-Anwendung hinzufügen. Öffnen Sie die Datei `config.xml` und fügen Sie die folgende Zeile dem Element `<platform name="android">` hinzu:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	{: codeblock}

	Der Wert für *minSdkVersion* muss `15` oder höher sein. In der Veröffentlichung [Android Platform Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} finden Sie Informationen zu Aktualisierungen der unterstützten Ziel-SDK-Version (*targetSdkVersion*) für das Android-SDK.

3. Wenn Sie das iOS-Betriebssystem hinzugefügt haben, aktualisieren Sie das Element `<platform name="ios">` mit einer Zieldeklaration ('target'):

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. Installieren Sie das Cordova-Plug-in für {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Konfigurieren Sie Ihre Plattform für Android und/oder iOS.

	####Android
	{: #cordova-android}

	Erstellen Sie vor dem Öffnen Ihres Projekts in Android Studio den Build Ihrer Cordova-Anwendung über Ihre Befehlszeilenschnittstelle (Command-Line Interface, CLI), um Buildfehler zu vermeiden.

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	Konfigurieren Sie Ihr Xcode-Projekt wie nachfolgend angegeben.

	1. Öffnen Sie Ihre Datei `xcode.proj` mit der neuesten Version von Xcode im Verzeichnis `<app_name>/platforms/ios`.

		**Wichtig:** Wenn Sie eine Nachricht erhalten, dass Sie eine Konvertierung zur neuesten Swift-Syntax durchführen sollen, klicken Sie auf die Schaltfläche für Abbrechen.

	2. Erstellen Sie den Build mit Xcode und führen Sie Ihre Anwendung mit Xcode aus.

	**Hinweis**: Beim Ausführen von `cordova build ios` kann der folgende Fehler auftreten. Dieses Problem ist auf einen Fehler in einem Abhängigkeits-Plug-in zurückzuführen, der unter [Issue 12 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12){: new_window} verfolgt wird. Sie können das iOS-Projekt aber weiterhin in Xcode über einen Simulator oder ein Gerät ausführen.

	```
	xcodebuild: error: Unable to find a destination matching the provided destination specifier:
			{ platform:iOS Simulator }

		Missing required device specifier option.
		The device type “iOS Simulator” requires that either “name” or “id” be specified.
		Please supply either “name” or “id”.
	```

6. Überprüfen Sie, ob das Plug-in erfolgreich installiert wurde, indem Sie den folgenden Befehl ausführen:

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. Aktivieren Sie die gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS, indem Sie auf der Registerkarte **Capabilities** die Option **Keychain Sharing** auf `On` setzen.

8. Aktivieren Sie **Defines Module** für iOS, indem Sie auf der Registerkarte **Build Settings** > **Packaging** die Option **Defines Module** auf `YES` setzen.


## {{site.data.keyword.amashort}}-Client im Cordova-WebView (JavaScript) initialisieren
{: #getting-started-cordova-initialize}

Zur Verwendung des {{site.data.keyword.amashort}}-Client-SDK müssen Sie das SDK initialisieren, indem Sie den Wert für `applicationBluemixRegion` übergeben.

Fügen Sie Ihrer Datei `index.js` den folgenden Aufruf hinzu, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren.

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**NB:** Ersetzen Sie `<applicationBluemixRegion>` durch die Region, in der Ihr {{site.data.keyword.Bluemix_notm}}-Service per Hosting bereitgestellt wird. Siehe [Vorbereitungen](#before-you-begin).

##{{site.data.keyword.amashort}} Authorization Manager im nativen Code initialisieren
{: #initializing-auth-manager}

Zur Verwendung von `BMSAuthorizationManager` müssen Sie das folgende Code-Snippet hinzufügen. Der folgende native Code initialisiert `BMSAuthorizationManager` mit dem {{site.data.keyword.amashort}}-Service `tenantId` (siehe [Vorbereitungen](#before-you-begin)).

### Android (Java)

Fügen Sie in der Methode `OnCreate` in der Datei `MainActivity.java` den Code vor `loadUrl` hinzu.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
Fügen Sie die Authorization Manager-Initialisierung in `AppDelegate.m` gemäß Ihrer Version von Xcode hinzu.

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**Hinweis:** Der Name der importierten Headerdatei besteht aus dem Modulnamen, der an die Zeichenfolge `-Swift.h` angehängt ist. Wenn beispielsweise der Modulname `Cordova` ist, lautet die Importzeile `#import "Cordova-Swift.h"`. Um nach dem Modulnamen zu suchen, rufen Sie
`Build Settings` > `Packaging` > `Product Module Name` auf.
Ersetzen Sie `<tenantId>` durch Ihre Tenant-ID (siehe [Vorbereitungen](#before-you-begin)).


## Anforderung an mobilen Back-End-Service senden
{: #getting-started-request}

Nach der Initialisierung des {{site.data.keyword.amashort}}-Client-SDK können Sie mit dem Senden von Anforderungen an Ihren mobilen Back-End-Service beginnen.

1. Versuchen Sie, eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anwendung zu senden. Öffnen Sie in Ihrem Browser die folgende URL: `{applicationRoute}/protected` (z. B. `http://my-mobile-backend.mybluemix.net/protected`).

	Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

2. Verwenden Sie Ihre Cordova-Anwendung, um eine Anforderung an denselben Endpunkt zu senden. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

	```Javascript
	var success = function(data){
	 console.log("success", data);
	 }

	 var failure = function(error){
	 console.log("failure", error);
	 }

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe in der LogCat- oder Xcode-Konsole (abhängig von der verwendeten Plattform) angezeigt:

	![Nachricht über erfolgreiche Ausführung](images/getting-started-android-success.png)

	## Nächste Schritte
	{: #next-steps}

	Wenn Sie eine Verbindung zu dem geschützten Endpunkt hergestellt haben, waren keine Berechtigungsnachweise erforderlich. Wenn Sie die Benutzer zur Anmeldung bei Ihrer Anwendung veranlassen wollen, müssen Sie eine Authentifizierung über Facebook oder Google oder eine angepasste Authentifizierung konfigurieren.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Angepasst](custom-auth-cordova.html)
