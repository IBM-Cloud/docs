---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.amashort}}
{: #gettingstarted}
*Letzte Aktualisierung: 21. März 2016*

Fügen Sie mit dem {{site.data.keyword.amafull}}-Service Sicherheits- und Überwachungsfunktionen zu Ihrer mobilen App hinzu. Sie können die Clientauthentifizierung und Identitätsprovider konfigurieren, damit sich Benutzer mit ihren vorhandenen Google- oder Facebook-Konten bei der App anmelden können. Zudem können Sie Ihrer App eine Überwachungsfunktion hinzufügen, die sowohl eine Clientprotokollierung als auch das Erstellen von Nutzungsstatistiken ermöglicht.
{:shortdesc}

**Anmerkung:** Der {{site.data.keyword.amashort}}-Service wurde früher als Advanced Mobile Access bezeichnet.


Führen Sie die folgenden Schritte aus, um den {{site.data.keyword.amashort}}-Service betriebsbereit zu machen:

1. Richten Sie Ihre clientseitige Entwicklungsumgebung ein.
Sie können das {{site.data.keyword.amashort}}-SDK zu Ihrer vorhandenen Android-, Cordova- oder iOS-App hinzufügen. Außerdem können Sie die Beispielanwendung 'HelloAuthentication' herunterladen.
   * **Android**: ([SDK](getting-started-android.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova**: ([SDK](getting-started-cordova.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS (Swift-C-SDK)**: ([SDK](getting-started-ios-swift-sdk.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS (Objective-C-SDK)**: ([SDK](getting-started-ios.html)) ([Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. Schützen Sie serverseitige Ressourcen. Schützen Sie Ihre mobilen Back-End-Ressourcen, die in Node.js- oder Liberty for Java&trade;-Laufzeiten mit für Mobilgeräte konfigurierter OAuth-Sicherheit ausgeführt werden. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).

1. Optional: Konfigurieren Sie einen Identitätsprovider für Ihre Anwendung. Pro Anwendung können Sie einen Identitätsprovider konfigurieren. Mithilfe eines konfigurierten Identitätsproviders können sich die Benutzer Ihrer mobilen App mit ihrem vorhandenen Facebook- oder Google+-Account anmelden. Alternativ können Sie eine angepasste Authentifizierung erstellen, um zu definieren, wie sich Benutzer anmelden können.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Angepasst](custom-auth.html)

1. Konfigurieren Sie die Überwachung und Protokollierung der App.  Weitere Informationen finden Sie in [Überwachung von Apps](app-monitoring.html).

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}
* [android-helloauthentication - Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication - Beispiel (Swift-SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication - Beispiel (Objective-C-SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Core-SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Kern-SDK (Cordova-Plug-in)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Kern-SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Kern-SDK (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Benutzerdefinierte Authentifizierung - Einfaches Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Benutzerdefinierte Authentifizierung - Erweitertes Beispiel](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API-Referenz
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C-SDK)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Zugehörige Links
{: #general}
* [Übersicht](overview.html){: new_window}
