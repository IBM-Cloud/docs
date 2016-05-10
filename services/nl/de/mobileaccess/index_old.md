---

copyright:
  years: 2015, 2016
  
---

{:shortdesc: .shortdesc}

# Einführung in {{site.data.keyword.amashort}}
{: #getting-started}

Der {{site.data.keyword.amafull}}-Service stellt Sicherheits- und Überwachungsfunktionen für Ihre mobile Anwendung bereit. Sie können die Clientauthentifizierung und Identitätsprovider konfigurieren. Zudem können Sie Ihrer App eine Überwachungsfunktion hinzufügen, die sowohl eine Clientprotokollierung als auch das Erstellen von Nutzungsstatistiken ermöglicht.

Anmerkung: Der Mobile Client Access-Service wurde früher als Advanced Mobile Access bezeichnet.
{: shortdesc}

1. Richten Sie ein mobiles Back-End in Bluemix ein und konfigurieren Sie das SDK in Ihrer mobilen App. Weitere Informationen finden Sie in der [Einführung](getting-started.html).
1. Schützen Sie serverseitige Ressourcen. Schützen Sie Ihre mobilen Back-End-Ressourcen, die in Node.js- oder Liberty for Java&trade;-Laufzeiten mit für Mobilgeräte konfigurierter OAuth-Sicherheit ausgeführt werden. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).
1. Optional: Konfigurieren Sie einen Identitätsprovider für Ihre Anwendung. Pro Anwendung können Sie einen Identitätsprovider konfigurieren. Mithilfe eines konfigurierten Identitätsproviders können sich die Benutzer Ihrer mobilen App mit ihrem vorhandenen Facebook- oder Google+-Account anmelden. Alternativ können Sie eine angepasste Authentifizierung erstellen, um zu definieren, wie sich Benutzer anmelden können.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Angepasst](custom-auth.html)
1. Konfigurieren Sie die Überwachung und Protokollierung der App.  Weitere Informationen finden Sie in [Überwachung von Apps](app-monitoring.html).


># Zugehörige Links {:class="linklist"}
>## Lernprogramme und Beispiele {:id="samples"}
>* [android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)
>* [ios-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)
>
># Zugehörige Links {:class="linklist"}
>## API-Referenz{:id="api"}
>* [API-Kernreferenz (Android)](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
>* [API-Kernreferenz (iOS)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
>
># Zugehörige Links {:class="linklist"}
>## SDK {:id="sdk"}
>* [Kern-SDK (iOS)](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)  
>* [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)
>* [bms-clientsdk-cordova-plugin-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
>
>{:elementKind="article" id="rellinks"}
