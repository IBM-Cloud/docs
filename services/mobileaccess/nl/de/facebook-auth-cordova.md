---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Facebook-Authentifizierung für Cordova-Apps aktivieren
{: #facebook-auth-cordova}

Zur Konfiguration von {{site.data.keyword.amafull}}-Cordova-Anwendungen für die Integration in die Facebook-Authentifizierung müssen Sie jede Plattform einzeln konfigurieren. Die Cordova-Anwendung muss bereits mit dem {{site.data.keyword.amashort}}-SDK instrumentiert sein.

Sowohl die native Plattform als auch der Cordova-WebView-JavaScript-Code müssen für die Facebook-Authentifizierung geändert werden.

Verwenden Sie die native Entwicklungsumgebung, um Änderungen an nativem Code vorzunehmen, wie zum Beispiel Android Studio oder Xcode.
{:shortdesc}

## Vorbereitungen
{: #facebook-auth-before}

Voraussetzungen:
* Cordova-Projekt (Android oder iOS), das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist. Informationen dazu siehe [Cordova-Plug-in einrichten](getting-started-cordova.html#getting-started-cordova-plugin).
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-End-Service finden Sie in der [Einführung](index.html).
* Anwendungsroute. Dies ist die URL Ihrer Back-End-Anwendung.
* Wert für `tenantId`. Öffnen Sie das {{site.data.keyword.amashort}}-Service-Dashboard. Klicken Sie auf **Mobile Systemerweiterungen**. Im Feld **App-GUID/TenantId** wird der Wert `tenantId` (auch als `appGUID` bezeichnet) angezeigt. Diese Werte benötigen Sie für die Initialisierung des SDK und zum Senden von Anforderungen an den Back-End-Service.
*  Suchen Sie die Region, in der der {{site.data.keyword.Bluemix_notm}}-Service gehostet wird. Ihre aktuelle {{site.data.keyword.Bluemix_notm}}-Region finden Sie im Header neben dem Symbol **Avatar** ![Avatarsymbol](images/face.jpg "Avatarsymbol") in der Menüleiste. Der Regionswert muss einer der folgenden sein: **USA (Süden)**, **Sydney** oder **Vereinigtes Königreich**. Die genauen konstanten Werte des SDK, die diesen Namen entsprechen, sind in den Codebeispielen angegeben.
* Facebook-Anwendungs- und App-ID. Weitere Informationen finden Sie in [Facebook-App-ID über das Facebook-Entwicklerportal anfordern](facebook-auth-overview.html#facebook-appID).



## Android-Plattform konfigurieren
{: #facebook-auth-cordova-android}

Die Schritte, die zur Konfiguration der Android-Plattform einer Cordova-Anwendung für die Integration der Facebook-Authentifizierung erforderlich sind, sind den Schritten, die für native Android-Anwendungen erforderlich sind, sehr ähnlich. Weitere Informationen finden Sie in [Facebook-Authentifizierung in Android-Apps aktivieren](facebook-auth-android.html). Führen Sie die folgenden Schritte aus:

* [Facebook-Anwendung für die Android-Plattform konfigurieren](facebook-auth-android.html#facebook-auth-android-config). Hier erfahren Sie, wie Sie die Facebook-Authentifizierung auf der Site 'Facebook for Developers' für Android-Apps einrichten.
* [MCA für die Facebook-Authentifizierung konfigurieren](facebook-auth-android.html#facebook-auth-android-mca). Hier erfahren Sie, wie Sie den {{site.data.keyword.amashort}}-Service auf dem {{site.data.keyword.Bluemix}}-Server für die Facebook-Authentifizierung für Android-Apps einrichten.


### {{site.data.keyword.amashort}}-Facebook-Client-SDK für die Android-Plattform konfigurieren
{: #configure_android}

Das {{site.data.keyword.amashort}}-Facebook-Client-SDK muss mit Gradle in Ihrem nativen Android-App-Projekt hinzugefügt werden.

1. Öffnen Sie in Ihrem Android-Projektordner die Datei `build.gradle` für das Anwendungsmodul (**nicht** die Projektdatei `build.gradle`). Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') und fügen Sie eine neue Abhängigkeit 'compile' für das Client-SDK hinzu:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// andere Abhängigkeiten
	}
	```
	{: codeblock}

2. Klicken Sie auf **Tools > Android > Sync Project with Gradle Files**, um Ihr Projekt mit Gradle zu synchronisieren.

3. Öffnen Sie die Datei `android/res/values/strings.xml` und fügen Sie die Zeichenfolge `<facebook_app_id>` hinzu, die Ihre Facebook-App-ID enthält.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

4. Gehen Sie in der Datei `AndroidManifest.xml` Ihres Android-Projekts (`android/manifests/AndroidManifest.xml`) wie folgt vor:

	* Fügen Sie die erforderlichen Metadaten für das Facebook-SDK dem Element <application> hinzu:

    ```XML
    <application .......>
    <meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

    <activity ...../>
    <activity ...../>
    </application>
    ```
    {: codeblock}

   * Fügen Sie unter Ihren vorhandenen Aktivitäten ein Facebook-Aktivitätselement hinzu:

    ```XML
    <application .....>
        <activity ...../>
		<activity ...../>

        <activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name"
        />
    </application>
    ```
    {: codeblock}

5. Fügen Sie dem Java-Code Ihrer Aktivität Folgendes hinzu.

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	   super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	      .onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### Authorization Manager im nativen Android-Code initialisieren
{: #initialize_android}

Die API `FacebookAuthenticationManager` muss trotzdem in Ihrem nativen Code registriert werden. Fügen Sie diesen Code mithilfe von `<tenantId>` zur Methode `onCreate` für Hauptaktivitäten hinzu (siehe [Vorbereitungen](#before-you-begin)).

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## iOS-Plattform konfigurieren
{: #facebook-auth-cordova-ios}

Die erforderlichen Schritte zum Konfigurieren der iOS-Plattform einer Cordova-Anwendung für die Integration der Facebook-Authentifizierung sind den Schritten ähnlich, die für native iOS-Swift-Anwendungen erforderlich sind (Headerdateien für die Verwendung von Objective-C-Code mit dem Swift-SDK werden benötigt). Der Hauptunterschied besteht darin, dass die Cordova-CLI gegenwärtig den CocoaPods-Abhängigkeitenmanager nicht unterstützt. Sie müssen Dateien, die für die Integration des {{site.data.keyword.amashort}}-Clients in die Facebook-Authentifizierung erforderlich sind, manuell hinzufügen. Weitere Informationen finden Sie in [Facebook-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)](facebook-auth-ios-swift-sdk.html). Führen Sie die folgenden Schritte aus:

* [Facebook-Anwendung für die iOS-Plattform konfigurieren](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config). Hier erfahren Sie, wie Sie den Service für die Facebook-Authentifizierung auf der Site 'Facebook for Developers' einrichten.
* [MCA für die Facebook-Authentifizierung konfigurieren](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca). Hier erfahren Sie, wie Sie den {{site.data.keyword.amashort}}-Service auf dem {{site.data.keyword.Bluemix}}-Server konfigurieren.
* [MCA-Facebook-Client-SDK für iOS konfigurieren](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk). Hier erfahren Sie, wie Sie das {{site.data.keyword.amashort}}-iOS-Swift-SDK für die Facebook-Authentifizierung mit CocoaPods installieren.


### Gemeinsame Nutzung der Schlüsselkette (Keychain) für iOS aktivieren
{: #enable_keychain}

Aktivieren Sie `Keychain Sharing`. Rufen Sie dazu die Registerkarte `Capabilities` auf und setzen Sie `Keychain Sharing` in Ihrem Xcode-Projekt auf `On`.

### {{site.data.keyword.amashort}} Authorization Manager in Objective-C initialisieren
{: #initialize_objc}

Authorization Manager muss im nativen Objective-Code in der Datei `app-delegate.m ` gemäß Ihrer Version von Xcode initialisiert werden.

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

	{

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
}


	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

	   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application 
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**Hinweis:** Der Name der importierten Headerdatei besteht aus dem Modulnamen, der an die Zeichenfolge `-Swift.h` angehängt ist. Wenn beispielsweise der Modulname `Cordova` ist, lautet die Importzeile `#import "Cordova-Swift.h"`. Um nach dem Modulnamen zu suchen, rufen Sie
`Build Settings` > `Packaging` > `Product Module Name` auf.

Ersetzen Sie `<tenantId>` durch Ihre Tenant-ID (siehe [Vorbereitungen](#facebook-auth-before)).


##{{site.data.keyword.amashort}}-Client-SDK im Cordova-WebView initialisieren
{: #initialize_webview}

Verwenden Sie für alle Plattformen den folgenden JavaScript-Code in Ihrem Cordova-JavaScript-WebView, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren.

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

Ersetzen Sie `<applicationBluemixRegion>` durch Ihre Region (siehe [Vorbereitungen](#facebook-auth-before)).

## Authentifizierung testen
{: #facebook-auth-cordova-test}

Nach der Initialisierung des Client-SDK und der Registrierung des Facebook-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihren mobile Back-End-Service beginnen.

### Vorbereitungen
{: #testing_auth_before}

Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).

1. Versuchen Sie, von Ihrem Browser aus eine Anforderung an den geschützten Endpunkt Ihrer mobilen Back-End-Anwendung zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`. Beispiel: `http://my-mobile-backend.mybluemix.net/protected`.

	Der Endpunktwert `/protected` sollte ein beliebiger geschützter Endpunkt eines mobilen Back-End-Service sein, der mit der MobileFirst Services Starter-Boilerplate erstellt wurde und mit {{site.data.keyword.amashort}} geschützt wird. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Senden Sie eine Anforderung über Ihre Cordova-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Führen Sie Ihre Anwendung aus. Es wird ein Facebook-Anmeldefenster angezeigt:

	![Bild](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Bild](images/ios-facebook-login.png)

	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie die Facebook-App nicht auf Ihrem Gerät installiert haben oder wenn Sie zurzeit nicht bei Facebook angemeldet sind.

1. Klicken Sie auf **OK**, um {{site.data.keyword.amashort}} zu berechtigen, Ihre Facebook-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Wenn Ihre Anforderung erfolgreich ist, wird die folgende Ausgabe im Dienstprogramm LogCat oder in der Xcode-Konsole angezeigt:

	![Nachricht über die erfolgreiche Facebook-Authentifizierung für Android](images/android-facebook-login-success.png)

	![Nachricht über die erfolgreiche Facebook-Authentifizierung für iOS](images/ios-facebook-login-success.png)
