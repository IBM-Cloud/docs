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

# Einführung in {{site.data.keyword.amashort}}
{: #gettingstarted}

Fügen Sie mit dem {{site.data.keyword.amafull}}-Service Sicherheit zu Ihrer mobilen App hinzu. Sie können die Clientberechtigung für den Zugriff auf geschützte Back-End-Ressourcen konfigurieren, die auf {{site.data.keyword.Bluemix}} ausgeführt werden. Verwenden Sie Identitätsprovider (Google und Facebook) oder angepasste Identitäten, um Benutzer zu authentifizieren und Zugriff auf geschützte Back-End-Ressourcen und Web-Apps zu gewähren.
{:shortdesc}

**Anmerkung:** Der {{site.data.keyword.amashort}}-Service wurde früher als Advanced Mobile Access bezeichnet.


Führen Sie die folgenden Schritte aus, um den {{site.data.keyword.amashort}}-Service betriebsbereit zu machen:

1. Verwenden Sie zum Erstellen eines gebundenen oder nicht gebundenen Service eine der folgenden Optionen:
 * Erstellen Sie eine {{site.data.keyword.Bluemix_notm}}-Anwendung mithilfe der **MobileFirst Services Starter**-Boilerplate aus dem Katalog. Dadurch wird ein {{site.data.keyword.amashort}}-Service erstellt, der an eine {{site.data.keyword.Bluemix_notm}}-Back-End-Anwendung gebunden ist.
 * Erstellen Sie einen {{site.data.keyword.amashort}}-Service mithilfe der {{site.data.keyword.amashort}}-Konsole. Sie können den Service an eine vorhandene Back-End-Anwendung binden und ihn in der {{site.data.keyword.amashort}}-Konsole konfigurieren.

   Wenn Sie den Starter 'MobileFirst Services' verwenden, erhalten Sie eine Instanz einer Node.js-Laufzeit, die auf IBM {{site.data.keyword.Bluemix_notm}} aktiv ist, um Ihre angepasste Back-End-Logik zu implementieren. Ein Satz von mobilen Kernservices, die Sicherheits-, Daten-, Push- und Überwachungsfunktionen bereitstellen, wird an diese Node.js-App gebunden. Nach dem Erstellen der Node.js-App in {{site.data.keyword.Bluemix_notm}} können Sie Ihre Entwicklungsumgebung einrichten und mit der Verwendung der {{site.data.keyword.Bluemix_notm}} Mobile Services-SDKs beginnen. Sie können die SDKs verwenden, um mit einfachen API-Aufrufen auf die Services zuzugreifen, die an Ihre Cloud-App gebunden sind.

	Weitere Informationen zum Erstellen von und Arbeiten mit Projekten, Anwendungen und Services finden Sie in [IBM Bluemix Mobile-Dashboard](https://console.{DomainName}/docs/mobile/index.html).

2. Schützen Sie serverseitige Ressourcen.

   Schützen Sie Ihre mobilen Back-End-Ressourcen, die in Node.js- oder Liberty for Java&trade;-Laufzeiten aktiv sind, mit für Mobilgeräte konfigurierter OAuth-Sicherheit. Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).
   Weitere Informationen zur mobilen Back-End-Anwendung finden Sie in der Beispielanwendung [bms-hellotodo-strongloop ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "Symbol für externen Link"){: new_window}.

3. Richten Sie Ihre {{site.data.keyword.amashort}}-Kernentwicklungsumgebung ein.

  ####Cliententwicklung
  {: #client-development}

	Sie können das {{site.data.keyword.amashort}}-SDK folgendermaßen zu Ihrer vorhandenen Android-, iOS- oder Cordova-App hinzufügen:
   * Android: ([Android-SDK einrichten](getting-started-android.html)) ([Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Symbol für externen Link"){: new_window})
    * iOS (Swift-SDK): ([iOS-Swift-SDK einrichten](getting-started-ios-swift-sdk.html)) ([Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Symbol für externen Link"){: new_window})    
   * Cordova: ([Cordova-Plug-in einrichten](getting-started-cordova.html)) ([Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "Symbol für externen Link"){: new_window})


 ####Webentwicklung
 {: #web-development}

   Der {{site.data.keyword.amashort}}-Service kann Ihre Webanwendung ohne spezielles SDK schützen. Zusätzlich zu dem durch den {{site.data.keyword.amashort}}-Service zur Verfügung gestellten Schutz können Sie unterschiedliche Identitätsprovider nutzen. Durch die {{site.data.keyword.amashort}}-Integration können alle Webanwendungen unabhängig von der implementierten Technologie die Vorteile des OAuth2-Protokolls nutzen. Die folgenden Abschnitte enthalten Informationen darüber, wie Sie Ihre {{site.data.keyword.amashort}}-Web-App für den Zugriff auf den {{site.data.keyword.amashort}}-Service über unterschiedliche Identitätsprovider einrichten:

   * [Facebook-Authentifizierung für Webanwendungen aktivieren](facebook-auth-web.html)
   * [Google-Authentifizierung für Webanwendungen aktivieren](google-auth-web.html)
   * [Angepasste Authentifizierung für Webanwendungen aktivieren](custom-auth-web.html)

**Optional:** Konfigurieren Sie einen Identitätsprovider für Ihre Anwendung. Pro Anwendung können Sie einen Identitätsprovider konfigurieren. Mithilfe eines konfigurierten Identitätsproviders können sich die Benutzer Ihrer mobilen App mit ihrem vorhandenen Facebook- oder Google+-Account anmelden. Alternativ können Sie eine angepasste Authentifizierung erstellen, um zu definieren, wie sich Benutzer anmelden können.
   * [Benutzer mit Facebook-Berechtigungsnachweisen authentifizieren](facebook-auth-overview.html)
   * [Benutzer mit Google-Berechtigungsnachweisen authentifizieren](google-auth-overview.html)
   * [Benutzer mit einem angepassten Identitätsprovider authentifizieren](custom-auth.html)

## Lernprogramme und Beispiele
{: #samples}

* [Beispiel 'android-helloauthentication' ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Symbol für externen Link"){: new_window}
* [Beispiel 'ios-helloauthentication' (Swift-SDK) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Symbol für externen Link"){: new_window}

## SDK
{: #sdk}

* [Core-SDK (Android) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Symbol für externen Link"){: new_window}

* [Beispiel 'ios-helloauthentication' (Swift SDK) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Symbol für externen Link"){: new_window}

* [Angepasste Authentifizierung - einfaches Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Symbol für externen Link"){: new_window}

* [Angepasste Authentifizierung - erweitertes Beispiel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Symbol für externen Link"){: new_window}


