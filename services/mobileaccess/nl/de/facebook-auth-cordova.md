---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Facebook-Authentifizierung für Cordova-Apps aktivieren
{: #facebook-auth-cordova}


Zur Konfiguration von {{site.data.keyword.amafull}}-Cordova-Anwendungen für die Integration in die Facebook-Authentifizierung müssen Sie Änderungen am nativen Code der Cordova-Anwendung in Java, Objective-C oder Swift durchführen. Konfigurieren Sie jede Plattform separat. Diese Cordova-Anwendung muss bereits mit dem {{site.data.keyword.amashort}}-SDK instrumentiert sein. 


Verwenden Sie die native Entwicklungsumgebung, um Änderungen an nativem Code vorzunehmen, wie zum Beispiel Android Studio oder Xcode.
{:shortdesc}

## Vorbereitungen
{: #facebook-auth-before}
Voraussetzungen:
* Cordova-Projekt, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist. Informationen dazu siehe [Cordova-Plug-in einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung einer {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung finden Sie in der [Einführung](index.html).
* Facebook-App-ID. Weitere Informationen finden Sie in [Facebook-App-ID über das Facebook-Entwicklerportal anfordern](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).



## Android-Plattform konfigurieren
{: #facebook-auth-cordova-android}

Die Schritte, die zur Konfiguration der Android-Plattform einer Cordova-Anwendung für die Integration der Facebook-Authentifizierung erforderlich sind, sind den Schritten, die für native Android-Anwendungen erforderlich sind, sehr ähnlich. Weitere Informationen finden Sie in [Facebook-Authentifizierung in Android-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Führen Sie die folgenden Schritte aus:

* Facebook-Anwendung für die Android-Plattform konfigurieren
* {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren

### {{site.data.keyword.amashort}}-Client-SDK für Android konfigurieren

Konfigurieren Sie das {{site.data.keyword.amashort}}-Client-SDK für Android in Ihrer Cordova-Anwendung.

1. Öffnen Sie in Ihrem Android-Projektordner die Datei `build.gradle` für das Anwendungsmodul (**nicht** die Projektdatei `build.gradle`). Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') und fügen Sie eine neue Abhängigkeit 'compile' für das Client-SDK hinzu:

	```Gradle
	dependencies {
     		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
     		name:'facebookauthentication',
     		version: '1.+',
     		ext: 'aar',
     		transitive: true
     		// other dependencies  
		 }
	```
	
2. Synchronisieren Sie Ihr Projekt mit Gradle, indem Sie auf **Tools > Android > Sync Project with Gradle Files** klicken.

3. Öffnen Sie die Datei `android/res/values/strings.xml` und fügen Sie die Zeichenfolge `facebook_app_id` hinzu, die Ihre Facebook-App-ID enthält.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	
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

2. Initialisieren Sie für Cordova-Anwendungen das {{site.data.keyword.amashort}}-Client-SDK in Ihrem JavaScript-Code anstatt im Java-Code. Die API `FacebookAuthenticationManager` muss trotzdem in Ihrem nativen Code registriert werden. Fügen Sie diesen Code zur Methode `onCreate` für Hauptaktivitäten hinzu:  

	```Java
	FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

6. Fügen Sie Ihrer Aktivität den folgenden Code hinzu:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	      super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	          .onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## iOS-Plattform konfigurieren
{: #facebook-auth-cordova-ios}

Die Schritte, die zur Konfiguration der iOS-Plattform einer Cordova-Anwendung für die Integration der Facebook-Authentifizierung erforderlich sind, sind den Schritten ähnlich, die für native iOS-Anwendungen erforderlich sind. Der Hauptunterschied besteht darin, dass die Cordova-CLI gegenwärtig den CocoaPods-Abhängigkeitenmanager nicht unterstützt. Sie müssen Dateien, die für die Integration in die Facebook-Authentifizierung erforderlich sind, manuell hinzufügen. Weitere Informationen finden Sie in [Facebook-Authentifizierung in iOS-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Führen Sie die folgenden Schritte aus:

* Facebook-Anwendung für die iOS-Plattform konfigurieren
* {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren

### {{site.data.keyword.amashort}}-SDK für die Facebook-Authentifizierung und Facebook-SDK manuell installieren
{: #facebook-auth-cordova-ios-sdk}
1. Laden Sie das Archiv, das das [{{site.data.keyword.Bluemix_notm}}Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) enthält, herunter.

1. Wechseln Sie zum Verzeichnis `Sources/Authenticators/IMFFacebookAuthentication` und kopieren Sie alle Dateien (durch Ziehen und Übergeben) in Ihr iOS-Projekt in Xcode. Kopieren Sie die folgenden Dateien:

	* IMFDefaultFacebookAuthenticationDelegate.h
	* IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	Wählen Sie bei entsprechender Aufforderung durch Xcode die Option **Copy files...** aus.

1. Laden Sie [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg) herunter und installieren Sie das SDK.

1. Das Facebook-SDK wird im Verzeichnis `~/Documents/FacebookSDK` installiert. Navigieren Sie zu diesem Verzeichnis und kopieren Sie (Ziehen und Übergeben) die Datei `FacebookSDK.framework` in Ihr iOS-Projekt in Xcode.

1. Klicken Sie auf Ihr Projektstammverzeichnis in Xcode und wählen Sie **Build Phases** aus.

1. Fügen Sie die Datei `FacebookSDK.framework` zur Liste der verlinkten Bibliotheken in **Link binary with libraries** (Binärdatei mit Bibliotheken verbinden) hinzu.

 Siehe [iOS-Plattform für die Facebook-Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Registrieren Sie die `IMFFacebookAuthenticationHandler`-API im nativen Code, wie im Abschnitt **{{site.data.keyword.amashort}}-Client-SDK initialisieren** beschrieben. Initialisieren Sie nicht `IMFClient` in Ihrem nativen Code.

Fügen Sie die folgende Zeile der Methode `application:openURL:sourceApplication:annotation` Ihres Anwendungsdelegats hinzu. Dieser Code stellt sicher, dass alle Cordova-Plug-ins über die jeweiligen Ereignisse benachrichtigt werden.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #facebook-auth-cordova-init}

Verwenden Sie den folgenden JavaScript-Code in Ihrer Cordova-Anwendung, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

Ersetzen Sie `applicationRoute` und `applicationGUID` durch die Werte für **Route** und **App-GUID** aus **Mobile Systemerweiterungen**.
	



##{{site.data.keyword.amashort}}-AuthorizationManager initialisieren
Verwenden Sie den folgenden JavaScript-Code in Ihrer Cordova-Anwendung, um den {{site.data.keyword.amashort}} AuthorizationManager zu initialisieren.
```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```
{: codeblock}

Ersetzen Sie den Wert für `tenantId` durch den Wert für `tenantId` des {{site.data.keyword.amashort}}-Service. Diesen Wert erhalten Sie, wenn Sie auf die Schaltfläche **Berechtigungsnachweise anzeigen** der Kachel für den {{site.data.keyword.amashort}}-Service klicken.



## Authentifizierung testen
{: #facebook-auth-cordova-test}
Nach der Initialisierung des Client-SDK und der Registrierung des Facebook-Authentifizierungsmanagers können Sie mit dem Senden von Anforderungen an Ihre mobile Back-End-Anwendung beginnen.

### Vorbereitungen
Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Versuchen Sie, von Ihrem Browser aus eine Anforderung an den geschützten Endpunkt Ihrer neu erstellten mobilen Back-End-Anwendung zu senden. Öffnen Sie die folgende URL: `{applicationRoute}/protected`. Beispiel: `http://my-mobile-backend.mybluemix.net/protected`
<br/>Der Endpunkt `/protected` einer mobilen Back-End-Anwendung, die mit der MobileFirst Services Starter-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Eine Nachricht `Unauthorized` (Nicht autorisiert) wird in Ihrem Browser zurückgegeben. Diese Nachricht wird deshalb zurückgegeben, weil auf diesen Endpunkt nur mobile Anwendungen zugreifen können, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert sind.

1. Senden Sie eine Anforderung über Ihre Cordova-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
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
