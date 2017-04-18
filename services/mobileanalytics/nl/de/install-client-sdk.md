---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}}-Client-SDKs installieren
{: #mobileanalytics_sdk}

Die Client-SDKs für {{site.data.keyword.mobileanalytics_short}} sind derzeit für Android, iOS, WatchOS und Cordova verfügbar.
{: #shortdesc}

## Client-SDK für Android installieren
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)(https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)]

Im Lieferumfang des Client-SDKs für {{site.data.keyword.mobileanalytics_short}} ist derzeit Gradle enthalten, ein Abhängigkeitsmanager für Android-Projekte. Gradle lädt automatisch Artefakte aus Repositorys herunter und macht sie für die Android-Anwendung verfügbar.

1. Erstellen Sie ein [Android Studio-Projekt ![Symbol für externen Link](http://developer.android.com/sdk/index.html){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] oder öffnen Sie ein vorhandenes Projekt.

2. Öffnen Sie die Datei `build.gradle`, die sich in Ihrem **App-Modul** befindet.

  **Tipp**: Ihr Android-Projekt kann über zwei Dateien mit der Bezeichnung `build.gradle` verfügen: eine für das Projekt und eine für das App-Modul. Stellen Sie sicher, dass die Datei **App-Modul** verwendet wird.

3. Suchen Sie in der Datei `build.gradle` den Abschnitt `Dependencies` und fügen Sie eine Kompilierungsabhängigkeit für das {{site.data.keyword.mobileanalytics_short}}-Client-SDK hinzu. Die Anweisung für die Repositorys sollte dem folgenden Codebeispiel ähneln:

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// andere Abhängigkeiten
      }
  	```
  	{: codeblock}

4. Synchronisieren Sie das Projekt mit Gradle durch Klicken auf **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Öffnen Sie die Datei `AndroidManifest.xml` für Ihr Android-Projekt. Sie finden diese Datei unter **app > manifests**. Fügen Sie unter dem Element `<manifest>` eine Internetzugriffsberechtigung hinzu:

	```
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
   
6. Sie haben jetzt das Android-Client-SDK installiert. Als Nächstes [importieren und initialisieren](sdk.html#initalize-ma-sdk) Sie das Analytics-Client-SDK.   

## Swift-SDK installieren
{: #installing-sdk-ios}

![CocoaPods-kompatibel](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

Mit dem {{site.data.keyword.mobileanalytics_full}}-SDK können Sie die mobile Anwendung instrumentieren. Das Swift-SDK ist für iOS und WatchOS verfügbar.

### Vorbemerkungen
{: #before-you-begin-ios}

Stellen Sie sicher, dass Xcode ordnungsgemäß konfiguriert ist. Informationen zum Konfigurieren einer iOS-Entwicklungsumgebung finden Sie auf der [Apple-Entwickler-Website ![Symbol für externen Link](https://developer.apple.com/support/xcode/){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]. Lesen Sie die Informationen zu den [Xcode-Anweisungen ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] für Swift Analytics für Client-SDKs.

Das {{site.data.keyword.mobileanalytics_short}}-SDK ist im Lieferumfang von [CocoaPods ![Symbol für externen Link](https://cocoapods.org/){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] und [Carthage ![Symbol für externen Link](https://github.com/Carthage/Carthage#getting-started){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] enthalten, den Abhängigkeitsmanagern für Cocoa-Projekte. Von CocoaPods and Carthage werden automatisch Artefakte aus den Repositorys heruntergeladen und für die Anwendung verfügbar gemacht. Wählen Sie CocoaPods oder Carthage aus:

#### CocoaPods
{: #cocoapods}

1. Befolgen Sie die [Anweisungen zu Swift-SDKs für {{site.data.keyword.Bluemix_notm}} Mobile Services ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] in GitHub zur Installation von `BMSAnalytics` mithilfe von Cocoapods und zum anschließenden Hinzufügen zu Ihrer Podfile. 
	
2. Nachdem Sie das iOS-Client-SDK installiert haben, [importieren und initialisieren](sdk.html#initalize-ma-sdk) Sie das Analytics-Client-SDK.   

#### Carthage
{: #carthage}

Wenn Sie nicht CocoaPods verwenden, können Sie mit [Carthage ![Symbol für externen Link](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] Frameworks zu Ihrem Projekt hinzufügen.

1. Befolgen Sie die [Installationsanweisungen für Carthage ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] in GitHub, um `BMSAnalytics` zu installieren.

2. Nachdem Sie das iOS-Client-SDK installiert haben, [importieren und initialisieren](sdk.html#initalize-ma-sdk) Sie das Analytics-Client-SDK.

## Cordova-Plug-in installieren
{: #installing-sdk-cordova}

Mit dem {{site.data.keyword.mobileanalytics_full}}-Cordova-Plug-in können Sie die mobile Anwendung instrumentieren. 

1. Erstellen Sie ein [Cordova-Projekt ![Symbol für externen Link](http://cordova.apache.org/#getstarted){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] oder öffnen Sie ein vorhandenes Projekt.

2. Fügen Sie Android- und iOS-Plattformen zu Ihrer Cordova-Anwendung hinzu. Führen Sie einen oder beide der folgenden Befehle über die Befehlszeile aus. Derzeit wird Cordova-CLI V6.3.0 oder früher unterstützt:
   
   Android:

	 ```
	 cordova platform add android@5.2.2
	 ```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
3. Wenn Sie die Android-Plattform hinzugefügt haben, müssen Sie der Datei `config.xml` der Cordova-Anwendung die unterstützte API-Mindeststufe hinzufügen. Öffnen Sie dazu die Datei `config.xml` und fügen Sie die folgende Zeile zum Element `<platform name="android">` hinzu:

	```
	<platform name="android">  
  	 <preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	 <!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 Der Wert für *minSdkVersion* muss Version `15` oder höher sein. Im [Android Platform Guide ![Symbol für externen Link](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] finden Sie die aktuell unterstützte Ziel-SDK-Version (*targetSdkVersion*) für Ihr Android-SDK.

4. Wenn Sie das iOS-Betriebssystem hinzugefügt haben, aktualisieren Sie das Element `<platform name="ios">` mit einer Zieldeklaration:

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

5. Fügen Sie das Plug-in `bms-core` hinzu.
 	
	 ```
	 cordova plugin add bms-core
	 ```
	 {: codeblock}

6. Stellen Sie sicher, dass das Plug-in erfolgreich installiert wurde, indem Sie den folgenden Befehl ausführen:
	
	```
	cordova plugin list
	```
	{: codeblock}
	
7. [Konfigurieren Sie Ihre Android- und iOS-Umgebung ![Symbol für externen Link](https://www.npmjs.com/package/bms-core#4-configuring-your-platform){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")].

8. Sie haben nun das Cordova-Plug-in installiert und Ihre Umgebungen konfiguriert. Als Nächstes [importieren und initialisieren](sdk.html#initalize-ma-sdk) Sie das Analytics-Client-SDK.

# Zugehörige Links

## SDK
* [Android-SDK ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]  
* [iOS-SDK ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]
* [Cordova-Plug-in-Core-SDK ![Symbol für externen Link](https://www.npmjs.com/package/bms-core){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]

## API-Referenz
{: #api}
* [REST-API ![Symbol für externen Link](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]
