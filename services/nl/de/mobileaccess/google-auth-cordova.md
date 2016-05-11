---

copyright:
  years: 2015, 2016

---

# Google-Authentifizierung in Cordova-Apps aktivieren
{: #google-auth-cordova}
Zur Konfiguration von Cordova-Anwendungen für die Integration in die Google-Authentifizierung müssen Sie Änderungen am nativen Code der Cordova-Anwendung zum Beispiel in Java, Objective-C oder Swift durchführen. Jede Plattform muss separat konfiguriert werden. Verwenden Sie die native Entwicklungsumgebung, um Änderungen an nativem Code vorzunehmen, wie zum Beispiel Android Studio oder Xcode.

## Vorbereitungen
{: #before-you-begin}
* Sie müssen über eine durch {{site.data.keyword.amashort}} geschützte Ressource verfügen und ein Cordova-Projekt haben, das mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert ist.  Weitere Informationen finden Sie in [Einführung in {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) und [Cordova-Plug-in einrichten](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Schützen Sie Ihre Back-End-Anwendung manuell mit dem {{site.data.keyword.amashort}}-Server-SDK. Weitere Informationen finden Sie in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* (optional) Machen Sie sich mit den folgenden Abschnitten vertraut:
   * [Google-Authentifizierung in Android-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Google-Authentifizierung in iOS-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Android-Plattform konfigurieren
{: #google-auth-cordova-android}

Die Schritte, die zur Konfiguration der Android-Plattform einer Cordova-Anwendung für die Integration der Google-Authentifizierung erforderlich sind, sind den Schritten, die für native Anwendungen erforderlich sind, sehr ähnlich. Weitere Informationen finden Sie in [Google-Authentifizierung in Android-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html). Richten Sie die folgenden Teile ein:

* Google-Projekt für die Android-Plattform konfigurieren
* {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
* {{site.data.keyword.amashort}}-Client-SDK für Android konfigurieren

Der einzige Unterschied bei der Konfiguration von Cordova-Anwendungen besteht darin, dass Sie das {{site.data.keyword.amashort}}-Client-SDK in Ihrem JavaScript-Code anstatt im Java-Code initialisieren müssen. Die API `GoogleAuthenticationManager` muss trotzdem in Ihrem nativen Code registriert werden.

## iOS-Plattform konfigurieren
{: #google-auth-cordova-ios}

Die Schritte, die zur Konfiguration der iOS-Plattform einer Cordova-Anwendung für die Integration der Google-Authentifizierung erforderlich sind, sind den Schritten für native Anwendungen ähnlich. Der Hauptunterschied besteht darin, dass die Cordova-CLI gegenwärtig den CocoaPods-Abhängigkeitenmanager nicht unterstützt.  Sie müssen die erforderlichen Dateien für die Integration in die Google-Authentifizierung manuell hinzufügen. Weitere Informationen finden Sie in [Google-Authentifizierung in iOS-Apps aktivieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Führen Sie die folgenden Schritte aus:

* Google-Projekt für die iOS-Plattform konfigurieren
* {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren

### {{site.data.keyword.amashort}}-SDK für die Google-Authentifizierung und Google-SDK manuell installieren
{: #google-auth-cordova-ios-sdk}
1. Laden Sie das Archiv, das das [{{site.data.keyword.Bluemix}} Mobile Services SDK for iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master) enthält, herunter.

1. Wechseln Sie zum Verzeichnis `Sources/Authenticators/IMFGoogleAuthentication` und kopieren Sie alle Dateien (durch Ziehen und Übergeben) in Ihr iOS-Projekt in Xcode. Sie müssen die folgenden Dateien kopieren:

	> * IMFDefaultGoogleAuthenticationDelegate.h
	> * IMFDefaultGoogleAuthenticationDelegate.m
	> * IMFGoogleAuthenticationDelegate.h
	> * IMFGoogleAuthenticationHandler.h
	> * IMFGoogleAuthenticationHandler.m

Wählen Sie das Kontrollkästchen **Copy files....** aus.

1. Laden Sie das [Google+ iOS SDK](http://goo.gl/9cTqyZ) herunter und installieren Sie es.

1. Führen Sie Schritt 2 des Lernprogramms [Start integrating Google+ into your iOS app](https://developers.google.com/+/mobile/ios/getting-started) aus, um das Google+ iOS SDK in Ihr Xcode-Projekt zu integrieren.

Fahren Sie mit dem Abschnitt **iOS-Projekt für die Google-Authentifizierung konfigurieren** in [iOS-Plattform für die Google-Authentifizierung konfigurieren](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html) fort. Registrieren Sie `IMFGoogleAuthenticationHandler` im nativen Code, wie im Abschnitt `{{site.data.keyword.amashort}}-Client-SDK initialisieren` beschrieben. Sie müssen `IMFClient` nicht in Ihrem nativen Code initialisieren, da dies gleich im JavaScript-Code erfolgt.

Fügen Sie die folgende Zeile der Methode `application:openURL:sourceApplication:annotation` Ihres Anwendungsdelegats hinzu. Diese Zeile stellt sicher, dass alle Cordova-Plug-ins über die jeweiligen Ereignisse benachrichtigt werden.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## {{site.data.keyword.amashort}}-Client-SDK initialisieren
{: #google-auth-cordova-initialize}

Verwenden Sie den folgenden JavaScript-Code in Ihrer Cordova-Anwendung, um das {{site.data.keyword.amashort}}-Client-SDK zu initialisieren.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Ersetzen Sie die Werte für *applicationRoute* und *applicationGUID* durch die Werte für **Route** und **App-GUID**, die Sie im Abschnitt **Mobile Systemerweiterungen** Ihrer Anwendung im Dashboard ermittelt haben.

## Authentifizierung testen
{: #google-auth-cordova-test}
Nach der Initialisierung des Client-SDK können Sie mit dem Senden von Anforderungen an Ihr mobiles Back-End beginnen.

### Vorbereitungen
{: #google-auth-cordova-testing-before}
Sie müssen die {{site.data.keyword.mobilefirstbp}}-Boilerplate verwenden und bereits eine durch {{site.data.keyword.amashort}} geschützte Ressource am Endpunkt `/protected` haben. Wenn Sie einen Endpunkt `/protected` einrichten müssen, finden Sie weitere Informationen in [Ressourcen schützen](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Versuchen Sie, in Ihrem Desktop-Browser eine Anforderung an den geschützten Endpunkt Ihres mobilen Back-Ends zu senden, indem Sie `{applicationRoute}/protected` öffnen (z. B. `http://my-mobile-backend.mybluemix.net/protected`).

1. Der Endpunkt `/protected` eines mobilen Back-Ends, das mit der MobileFirst Services-Boilerplate erstellt wurde, wird mit {{site.data.keyword.amashort}} geschützt. Deshalb auf ihn nur mit mobilen Anwendungen zugegriffen werden, die mit dem {{site.data.keyword.amashort}}-Client-SDK instrumentiert wurden. Infolgedessen wird eine Nachricht `Unauthorized` (Nicht autorisiert) in Ihrem Desktop-Browser angezeigt.

1. Senden Sie eine Anforderung über Ihre Cordova-Anwendung an denselben Endpunkt. Fügen Sie den folgenden Code hinzu, nachdem Sie `BMSClient` initialisiert haben.

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


1. Führen Sie Ihre Anwendung aus. Die Google-Anmeldeanzeige wird geöffnet.

	![Bild](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Bild](images/ios-google-login.png)
	Diese Anzeige sieht möglicherweise geringfügig anders aus, wenn Sie die Facebook-App nicht auf Ihrem Gerät installiert haben oder wenn Sie zurzeit nicht bei Facebook angemeldet sind.
1. Indem Sie auf **OK** klicken, berechtigen Sie {{site.data.keyword.amashort}}, Ihre Google-Benutzeridentität zu Authentifizierungszwecken zu nutzen.

1. 	Ihre Anforderung sollte erfolgreich ausgeführt werden. Abhängig von der verwendeten Plattform sollte die folgende Ausgabe in der LogCat/Xcode-Konsole angezeigt werden.

	![Bild](images/android-google-login-success.png)

	![Bild](images/ios-google-login-success.png)
