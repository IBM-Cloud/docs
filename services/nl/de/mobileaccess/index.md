---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Einführung in {{site.data.keyword.amashort}}
{: #gettingstarted}
*Letzte Aktualisierung: 15. Juni 2016*
{: .last-updated}

Fügen Sie mit dem {{site.data.keyword.amafull}}-Service Sicherheitsfunktionalität zu Ihrer mobilen App hinzu. Sie können die Clientauthentifizierung und Identitätsprovider konfigurieren, damit sich Benutzer mit ihren vorhandenen Google- oder Facebook-Konten bei der App anmelden können.
{:shortdesc}

**Anmerkung:** Der {{site.data.keyword.amashort}}-Service wurde früher als Advanced Mobile Access bezeichnet.


Führen Sie die folgenden Schritte aus, um den {{site.data.keyword.amashort}}-Service betriebsbereit zu machen:

1.  Erstellen Sie mithilfe des {{site.data.keyword.Bluemix_notm}}-Dashboards eine mobile Back-End-Anwendung oder konfigurieren Sie eine vorhandene.
  - Sie können den MobileFirst Services-Starter aus dem Bluemix-Katalog auswählen.
  - Alternativ können Sie den Service an eine vorhandene Anwendung binden und ihn konfigurieren.

   Wenn Sie den Starter 'MobileFirst Services' verwenden, erhalten Sie eine Instanz einer Node.js-Laufzeit, die auf IBM {{site.data.keyword.Bluemix_notm}} aktiv ist, um Ihre angepasste Back-End-Logik zu implementieren. Ein Satz von mobilen Kernservices, die Sicherheits-, Daten-, Push- und Überwachungsfunktionen bereitstellen, wird an diese Node.js-App gebunden. Nach dem Erstellen der Node.js-App in {{site.data.keyword.Bluemix_notm}} können Sie Ihre Entwicklungsumgebung einrichten und mit der Verwendung der {{site.data.keyword.Bluemix_notm}} Mobile Services-SDKs beginnen. Sie können die SDKs verwenden, um mit einfachen API-Aufrufen auf die Services zuzugreifen, die an Ihre Cloud-App gebunden sind.
   
  
1. Schützen Sie serverseitige Ressourcen.

   Schützen Sie Ihre mobilen Back-End-Ressourcen, die in Node.js- oder Liberty for Java&trade;-Laufzeiten aktiv sind, mit für Mobilgeräte konfigurierter OAuth-Sicherheit. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).
   Weitere Informationen zur Standardanwendung für das mobile Back-End finden Sie in [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

1. Richten Sie Ihre clientseitige {{site.data.keyword.amashort}}-Kernentwicklungsumgebung ein.

   Sie können das {{site.data.keyword.amashort}}-SDK zu Ihrer vorhandenen Android-, Cordova- oder iOS-App hinzufügen. Außerdem können Sie die Beispielanwendung 'HelloAuthentication' herunterladen.
   * **Android**: ([Android-SDK einrichten](getting-started-android.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova**: ([Cordova-Plug-in einrichten](getting-started-cordova.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * **iOS (Swift-SDK)**: ([iOS-Swift-SDK einrichten](getting-started-ios-swift-sdk.html))
      ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (Objective-C-SDK)**: ([iOS-Object-C-SDK einrichten](getting-started-ios.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **Hinweis:** Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für Bluemix Mobile Services, die Verwendung und Unterstützung dieses SDK sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden. Für das Erstellen von Anwendungen wird dringend die Verwendung des Swift-SDK empfohlen (Informationen dazu siehe Abschnitt [iOS-Swift-SDK einrichten](getting-started-ios-swift-sdk.html)).

1. **Optional:** Konfigurieren Sie einen Identitätsprovider für Ihre Anwendung. Pro Anwendung können Sie einen Identitätsprovider konfigurieren. Mithilfe eines konfigurierten Identitätsproviders können sich die Benutzer Ihrer mobilen App mit ihrem vorhandenen Facebook- oder Google+-Account anmelden. Alternativ können Sie eine angepasste Authentifizierung erstellen, um zu definieren, wie sich Benutzer anmelden können.
   * [Benutzer mit Facebook-Berechtigungsnachweisen authentifizieren](facebook-auth-overview.html)
   * [Benutzer mit Google-Berechtigungsnachweisen authentifizieren](google-auth-overview.html)
   * [Benutzer mit einem angepassten Identitätsprovider authentifizieren](custom-auth.html)

1. Konfigurieren Sie die Überwachung und Protokollierung der App.

    Weitere Informationen finden Sie im Abschnitt [Apps überwachen](app-monitoring.html).

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}
* [android-helloauthentication - Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication - Beispiel (Swift-SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication - Beispiel (Objective-C-SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Kern-SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Kern-SDK (Cordova-Plug-in)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Kern-SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Kern-SDK (iOS - Objective-C - nicht mehr verwendet) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Benutzerdefinierte Authentifizierung - Einfaches Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Benutzerdefinierte Authentifizierung - Erweitertes Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API-Referenz
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C-SDK) - nicht mehr verwendet](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Zugehörige Links
{: #general}
* [Übersicht](overview.html){: new_window}
