---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Mobil-SDK verwenden
{: #openwhisk_mobile_sdk}
*Letzte Aktualisierung: 28. März 2016*

{{site.data.keyword.openwhisk}} stellt ein Mobil-SDK für iOS- und watchOS 2-Geräte bereit, mit dem mobile Apps dazu eingerichtet werden können, ohne großen Aufwand ferne Auslöser zu aktivieren und ferne Aktionen aufzurufen. Gegenwärtig ist keine Version für Android verfügbar. Android-Entwickler können die {{site.data.keyword.openwhisk}}-REST-API direkt verwenden.
{: shortdesc}

Das Mobil-SDK wurde in Swift 2.2 geschrieben und unterstützt iOS 9 und höhere Releases.

## SDK der App hinzufügen
{: #openwhisk_add_sdk}
Sie können das Mobil-SDK mithilfe von CocoaPods, Carthage oder aus dem Quellenverzeichnis installieren.

### Mithilfe von CocoaPods installieren 

Das {{site.data.keyword.openwhisk_short}}-SDK für den mobilen Einsatz ist nur über CocoaPods für die öffentliche Verteilung verfügbar. Wenn Cocoapods installiert ist, fügen Sie die folgenden Zeilen in eine Datei mit dem Namen 'Podfile' im Projektverzeichnis der Starter-App ein. 

```
source 'https://github.com/openwhisk/openwhisk-podspecs.git'

use_frameworks!

target 'MyApp' do
     platform :ios, '9.0'
     pod 'OpenWhisk'
end

target 'MyApp WatchKit Extension' do
     platform :watchos, '2.0'
     pod 'OpenWhisk-Watch'
end
```
{: codeblock}

Geben Sie über die Befehlszeile den Befehl "pod install" ein. Dadurch wird das SDK für eine iOS-App mit einer watchOS 2-Erweiterung installiert.  Verwenden Sie die Arbeitsbereichsdatei, die Cocoapods für Ihre App erstellt, um das Projekt in Xcode zu öffnen.

### Mithilfe von Carthage installieren

Erstellen Sie eine Datei im Projektverzeichnis Ihrer App mit dem Namen 'Cartfile'. Fügen Sie die folgenden Zeilen in die Cartfile ein:
```
github "openwhisk//openwhisk-client-swift.git" ~> 0.1.0 # Or latest version
```
{: codeblock}

Geben Sie über die Befehlszeile den Befehl 'carthage update --platform ios' ein. Carthage lädt das SDK herunter und führt einen Build durch, erstellt ein Verzeichnis mit dem Namen 'Carthage' im Projektverzeichnis Ihrer App und fügt eine Datei OpenWhisk.framework in Carthage/build/iOS ein. Fügen Sie OpenWhisk.framework den eingebetteten Frameworks in Ihrem Xcode-Projekt hinzu.

### Aus Quellcode installieren

Der Quellcode wird unter https://github.com/openwhisk//openwhisk-client-swift.git zur Verfügung gestellt. Öffnen Sie in Xcode ein Projekt unter Verwendung der Datei OpenWhisk.xcodeproj.  Das Projekt enthält die beiden Schemas "OpenWhisk" und "OpenWhiskWatch", die für iOS bzw. WathOS2 vorgesehen sind.  Erstellen Sie das Projekt (Build) für die Ziele, die Sie benötigen, und fügen Sie die resultierenden Frameworks Ihrer App (in der Regel in ~/Library/Developer/Xcode/DerivedData/Ihr App-Name) hinzu.

## Starter-App-Beispiel installieren
{: #openwhisk_install_sdkstart}

Sie können die {{site.data.keyword.openwhisk_short}}-CLI zum Herunterladen von Beispielcode verwenden, der in das {{site.data.keyword.openwhisk_short}}-SDK-Framework eingebettet wird.  

Geben Sie den folgenden Befehl ein, um das Starter-App-Beispiel zu installieren:
```
wsk sdk install iOS
```
Durch diesen Befehl wird eine ZIP-Datei heruntergeladen, die die Starter-App enthält.  Im Projektverzeichnis befindet sich eine Podfile.  Führen Sie den Befehl "pod install" über ein Terminal aus, um das SDK zu installieren.
{: pre}

## Erste Schritte mit dem SDK
{: #openwhisk_sdk_getstart}

Um die Arbeit rasch aufnehmen zu können, erstellen Sie ein Objekt WhiskCredentials mit Ihren {{site.data.keyword.openwhisk_short}}-API-Berechtigungsnachweisen und eine {{site.data.keyword.openwhisk_short}}-Instanz aus diesem Objekt.

In Swift 2.1 verwenden Sie zum Beispiel den folgenden Beispielcode zum Erstellen des Berechtigungsnachweisobjekts:

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

Im obigen Beispiel werden die aus {{site.data.keyword.openwhisk_short}} abgerufenen Parameter `myKey` und `myToken` übergeben. Sie können den Schlüssel (Key) und das Token mit dem folgenden CLI-Befehl abrufen:

```
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

Die Zeichenfolgen vor und nach dem Doppelpunkt sind Ihr Schlüssel bzw. Ihr Token.

## {{site.data.keyword.openwhisk_short}}-Aktion aufrufen
{: #openwhisk_sdk_invoke}


Zum Aufrufen einer fernen Aktion können Sie `invokeAction` mit dem Aktionsnamen aufrufen. Sie können den Namensbereich angeben, zu dem die Aktion gehört, oder Sie können den Namensbereich leer lassen, um den Standardnamensbereich zu übernehmen.  Verwenden Sie ein Wörterverzeichnis (Dictionary), um die erforderlichen Parameter an die Aktion zu übergeben.

Beispiel:

```
// In diesem Beispiel wird eine Aktion zur Ausgabe einer Nachricht an die OpenWhisk-Konsole aufgerufen.
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //Operationen ausführen
            print("Error invoking action \(error.localizedDescription)")
        } else {
            print("Action invoked!")
        }

    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Im obigen Beispiel wird die Aktion `helloConsole` unter Verwendung des Standardnamensbereichs aufgerufen.

## {{site.data.keyword.openwhisk_short}}-Auslöser aktivieren
{: #openwhisk_sdk_fire}

Zur Aktivierung eines fernen Auslösers können Sie die Methode `fireTrigger` aufrufen. Übergeben Sie die erforderlichen Parameter durch ein Wörterverzeichnis.

```
// In diesem Beispiel wird ein Auslöser aktiviert, wenn sich der Standort um eine bestimmte Entfernung geändert hat.

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Trigger fired!")
        }
    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Im obigen Beispiel wird ein Auslöser mit dem Namen `locationChanged` aktiviert.

## Aktionen mit Rückgabe eines Ergebnisses verwenden
{: #openwhisk_sdk_actionresult}

Wenn die Aktion ein Ergebnis zurückgibt, geben Sie im Aufruf von 'invokeAction' für 'hasResult' den Wert 'true' an. Das Ergebnis der Aktion wird im Reply-Wörterverzeichnis zurückgegeben. Beispiel:

```
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in

        if let error = error {
            //Operationen ausführen
            print("Error invoking action \(error.localizedDescription)")

        } else {
            var result = reply["result"]
            print("Got result \(result)")
        }


    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Standardmäßig gibt das SDK nur die Aktivierungs-ID und das durch die aufgerufene Aktion erzeugte Ergebnis zurück. Wenn Sie Metadaten des gesamten Antwortobjekts abrufen wollen, zu denen der HTTP-Antwortstatuscode gehört, verwenden Sie die folgende Einstellung:

```
whisk.verboseReplies = true
```
{: codeblock}

## SDK konfigurieren
{: #openwhisk_sdk_configure}

Sie können das SDK mithilfe des Parameters 'baseURL' zur Arbeit mit verschiedenen Installationen von {{site.data.keyword.openwhisk_short}} konfigurieren. Beispiel:

```
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

In diesem Beispiel wird eine Installation verwendet, die unter 'localhost:8080' ausgeführt wird.  Wenn Sie den Parameter 'baseUrl' nicht angeben, verwendet das Mobil-SDK die Instanz, die unter https://openwhisk.ng.bluemix.net ausgeführt wird.

Sie können einen angepassten Parameter NSURLSession übergeben, wenn Sie eine besondere Netzverwaltung benötigen. Sie könnten zum Beispiel eine eigene {{site.data.keyword.openwhisk_short}}-Installation haben, die mit selbst signierten Zertifikaten arbeitet:

```
// Netzdelegate erstellen, der allen vertraut
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// NSURLSession erstellen, die den vertrauenden Delegate verwendet
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// Festlegen, dass das SDK diese urlSession anstelle der gemeinsam genutzten Standardsitzung verwendet
whisk.urlSession = session
```
{: codeblock}

### Unterstützung für qualifizierte Namen

Alle Aktionen und Auslöser haben einen vollständig qualifizierten Namen, der aus einem Namensbereich, einem Paketnamen und einem Aktions- bzw. Auslösernamen besteht. Das SDK kann diese als Parameter beim Aufruf einer Aktion bzw. Aktivieren eines Auslösers akzeptieren. Das SDK stellt zudem eine Funktion bereit, die einen vollständig qualifizierten Namen akzeptiert, der wie folgt aussieht: `/mynamespace/mypackage/nameOfActionOrTrigger`. Die Zeichenfolge für den qualifizierten Namen unterstützt unbenannte Standardwerte für Namensbereiche und Pakete, die alle {{site.data.keyword.openwhisk_short}}-Benutzer haben, sodass die folgenden Syntaxanalyseregeln gelten:

- qName = "foo" ergibt: Namensbereich = Standard, Paket = Standard, Aktion/Auslöser = "foo"
- qName = "mypackage/foo" ergibt: Namensbereich = Standard, Paket = mypackage, Aktion/Auslöser = "foo"
- qName = "/mynamespace/foo" ergibt: Namensbereich = mynamespace, Paket = Standard, Aktion/Auslöser = "foo"
- qName = "/mynamespace/mypackage/foo ergibt: Namensbereich = mynamespace, Paket = mypackage, Aktion/Auslöser = "foo"

Alle anderen Kombinationen haben einen Fehler WhiskError.QualifiedName zur Folge. Daher müssen Sie bei Verwendung von qualifizierten Namen den Aufruf in ein Konstrukt "`do/try/catch`" einschließen.

### SDK-Schaltfläche

Aus Gründen der Verwendungsfreundlichkeit enthält das SDK eine Schaltfläche `WhiskButton`, die die Schaltfläche `UIButton` erweitert, sodass sie Aktionen aufrufen kann.  Gehen Sie zur Verwendung von `WhiskButton` wie im folgenden Beispiel vor:

```
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Dies aufrufen, wenn Tastendrückereignis erkannt wird, z. B. in IBAction, um Aktion aufzurufen
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
    } else {
        print("Success: \(reply)")
    }
})

// Alternativ können Sie eine eigenständige Schaltfläche einrichten, die selbst für Tastenereignisse empfangsbereit ist und eine Aktion aufruft.

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // Verwendung der API für qualifizierte Namen erfordert do/try/catch.
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in

       if let error = error {
           print("Oh no, error: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
{: codeblock}
