---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# {{site.data.keyword.mobileanalytics_short}}-Client-SDKs installieren
{: #mobileanalytics_sdk}

Letzte Aktualisierung: 18. Oktober 2016
{: .last-updated}

Die Client-SDKs für {{site.data.keyword.mobileanalytics_short}} sind derzeit für Android, iOS und WatchOS verfügbar.
{: #shortdesc}

## Client-SDK für Android installieren
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)(https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)]

Im Lieferumfang des Client-SDKs für {{site.data.keyword.mobileanalytics_short}} ist derzeit Gradle enthalten, ein Abhängigkeitsmanager für Android-Projekte. Gradle lädt automatisch Artefakte aus Repositorys herunter und macht sie für die Android-Anwendung verfügbar.

1. Erstellen Sie ein [Android Studio](http://developer.android.com/sdk/index.html)-Projekt oder öffnen Sie ein vorhandenes Projekt.

2. Öffnen Sie die Datei `build.gradle`, die sich in Ihrem **App-Modul** befindet.

  **Tipp**: Ihr Android-Projekt kann über zwei Dateien mit der Bezeichnung `build.gradle` verfügen: eine für das Projekt und eine für das App-Modul. Stellen Sie sicher, dass die Datei **App-Modul** verwendet wird.

3. Suchen Sie in der Datei `build.gradle` den Abschnitt `Dependencies` und fügen Sie eine Kompilierungsabhängigkeit für das {{site.data.keyword.mobileanalytics_short}}-Client-SDK hinzu. Die Anweisung für die Repositorys sollte dem folgenden Codebeispiel ähneln:

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// andere Abhängigkeiten
      }
  ```
  {: codeblock}

4. Synchronisieren Sie das Projekt mit Gradle durch Klicken auf **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Öffnen Sie die Datei `AndroidManifest.xml` für Ihr Android-Projekt. Sie finden diese Datei unter **app > manifests**. Fügen Sie unter dem Element `<manifest>` eine Internetzugriffsberechtigung hinzu:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. Sie haben jetzt das Android-Client-SDK installiert. Als Nächstes [importieren und initialisieren](sdk.html#initalize-ma-sdk-android) Sie das Analytics-Client-SDK.   

## Swift-SDK installieren
{: #installing-sdk-ios}

![CocoaPods-kompatibel](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

Mit dem {{site.data.keyword.mobileanalytics_full}}-SDK können Sie die mobile Anwendung instrumentieren. Das Swift-SDK ist für iOS und WatchOS verfügbar.

### Vorbemerkungen
{: #before-you-begin-ios}

Stellen Sie sicher, dass Xcode ordnungsgemäß konfiguriert ist. Informationen zum Konfigurieren einer iOS-Entwicklungsumgebung finden Sie auf der [Apple-Entwickler-Website](https://developer.apple.com/support/xcode/). Lesen Sie die Informationen zu den [Xcode-Voraussetzungen](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) für Swift Analytics für Client-SDKs.

Das {{site.data.keyword.mobileanalytics_short}}-SDK ist im Lieferumfang von [CocoaPods](https://cocoapods.org/) und [Carthage](https://github.com/Carthage/Carthage#getting-started) enthalten, den Abhängigkeitsmanagern für Cocoa-Projekten. Von CocoaPods and Carthage werden automatisch Artefakte aus den Repositorys heruntergeladen und für die Anwendung verfügbar gemacht.

#### CocoaPods
{: #cocoapods}

1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    Für Xcode 8: `sudo gem install cocoapods --pre`
    
   Stellen Sie sicher, dass Sie über die aktuelle Version von `BMSAnalytics` verfügen, indem Sie Ihr lokales CocoaPods-Repository wie folgt aktualisieren:
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. Befolgen Sie die [Anweisungen zu Swift-SDKs für {{site.data.keyword.Bluemix_notm}} Mobile-Services](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) in GitHub.
	
3. Nachdem Sie das iOS-Client-SDK installiert haben, [importieren und initialisieren](sdk.html#init-ma-sdk-ios) Sie das Analytics-Client-SDK.   

#### Carthage
{: #carthage}

Fügen Sie Ihrem Projekt Frameworks mit [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) hinzu.

1. Befolgen Sie die [Carthage-Installationsanweisungen](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) in GitHub.

2. Nachdem Sie das iOS-Client-SDK installiert haben, [importieren und initialisieren](sdk.html#init-ma-sdk-ios) Sie das Analytics-Client-SDK.

# Zugehörige Links

## SDK
* [Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API-Referenz
{: #api}
* [REST-API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
