---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilizzo dell'SDK mobile {{site.data.keyword.openwhisk_short}}
{: #openwhisk_mobile_sdk}
*Ultimo aggiornamento: 28 marzo 2016*

{{site.data.keyword.openwhisk}} fornisce un SDK mobile per dispositivi iOS e watchOS 2 che abilita le applicazioni mobili ad attivare facilmente dei trigger remoti e richiamare azioni remote. Una versione per Android non è attualmente disponibile; gli sviluppatori Android possono utilizzare la API REST {{site.data.keyword.openwhisk}} direttamente.
{: shortdesc}

L'SDK mobile è scritto in Swift 2.2 e supporta iOS 9 e release successive.

## Aggiunta di SDK alla tua applicazione
{: #openwhisk_add_sdk}
Puoi installare l'SDK mobile utilizzando CocoaPods, Carthage oppure dalla directory di origine.

### Installazione utilizzando CocoaPods 

L'SDK {{site.data.keyword.openwhisk_short}} per dispositivi mobili è disponibile per la distribuzione pubblica tramite CocoaPods. Presumendo che Cocoapods sia installato, inserisci le seguenti righe in un file denominato 'Podfile' all'interno della directory del progetto dell'applicazione starter. 

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

Dalla riga di comando, immetti "pod install". Questo installerà l'SDK per un'applicazione iOS con un'estensione watchOS 2.  Utilizza il file di spazio di lavoro che Cocoapods crea per la tua applicazione per aprire il progetto in Xcode.

### Installazione utilizzando Carthage

Crea un file nella directory del progetto della tua applicazione e denominalo 'Cartfile'. Inserisci le seguenti righe nel Cartfile:
```
github "openwhisk//openwhisk-client-swift.git" ~> 0.1.0 # Or latest version
```
{: codeblock}

Dalla riga di comando, immetti 'carthage update --platform ios'. Carthage scarica e genera l'SDK, crea una directory denominata Carthage nella directory del progetto della tua applicazione e inserisce un file OpenWhisk.framework in Carthage/build/iOS. Aggiungi OpenWhisk.framework ai framework incorporati nel tuo progetto Xcode.

### Installazione dal codice sorgente

Il codice sorgente è disponibile in https://github.com/openwhisk//openwhisk-client-swift.git. Apri il progetto utilizzando il file OpenWhisk.xcodeproj in Xcode.  Il progetto contiene due schemi "OpenWhisk" e "OpenWhiskWatch" destinati, rispettivamente, a iOS e WathOS2.  Genera il progetto per le destinazioni che ti servono e aggiungi i framework risultanti alla tua applicazione (di norma in ~/Library/Developer/Xcode/DerivedData/il nome della tua applicazione).

## Installazione dell'esempio di applicazione starter
{: #openwhisk_install_sdkstart}

Puoi utilizzare la CLI {{site.data.keyword.openwhisk_short}} per scaricare il codice di esempio che incorpora il framework SDK {{site.data.keyword.openwhisk_short}}.  

Per installare l'esempio di applicazione starter, immetti il seguente comando:
```
wsk sdk install iOS
```
Verrà scaricato un file zip che contiene l'applicazione starter.  Nella directory del progetto è presente un Podfile.  Esegui "pod install" da un terminale per l'installare l'SDK.
{: pre}

## Introduzione all'SDK
{: #openwhisk_sdk_getstart}

Per essere rapidamente operativo, crea un oggetto WhiskCredentials con le tue credenziali API {{site.data.keyword.openwhisk_short}} e da esso crea un'istanza {{site.data.keyword.openwhisk_short}}.

Ad esempio, in Swift 2.1, utilizza il seguente codice di esempio per creare un oggetto credenziali:

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

Nell'esempio precedenti, passi `myKey` e `myToken` che ottieni da {{site.data.keyword.openwhisk_short}}. Puoi richiamare la chiave e il token con il seguente comando CLI:

```
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

Le stringhe prima e dopo il carattere due punti sono, rispettivamente, la tua chiave e il tuo token.

## Richiamo di un'azione {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_invoke}


Per richiamare un'azione remota, puoi richiamare `invokeAction` con il nome dell'azione. Puoi specificare lo spazio dei nomi a cui appartiene l'azione oppure limitarti a lasciarlo vuoto per accettare lo spazio dei nomi predefinito.  Utilizza un dizionario per passare i parametri all'azione come richiesto.

Ad esempio:

```
// In questo esempio, stiamo richiamando un'azione per stampare un messaggio sulla console OpenWhisk
var params = Dictionary<String, String>()
params["payload"] = "Salve dal dispositivo mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Errore di richiamo dell'azione \(error.localizedDescription)")
        } else {
            print("Azione richiamata!")
        }

    })
} catch {
    print("Errore \(error)")
}
```
{: codeblock}

Nell'esempio precedente, richiami l'azione `helloConsole` utilizzando lo spazio dei nomi predefinito.

## Attivazione di un trigger {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_fire}

Per attivare un trigger remoto, puoi richiamare il metodo `fireTrigger`. Passa i parametri come richiesto utilizzando un dizionario.

```
// In questo esempio, stiamo attivando un trigger quando la nostra ubicazione è variata in una certa misura

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Errore di attivazione del trigger \(error.localizedDescription)")
        } else {
            print("Trigger attivato!")
        }
    })
} catch {
    print("Errore \(error)")
}
```
{: codeblock}

Nell'esempio precedente, stai attivando un trigger denominato `locationChanged`.

## Utilizzo di azioni che restituiscono un risultato
{: #openwhisk_sdk_actionresult}

Se l'azione restituisce un risultato, imposta hasResult su true nella chiamata invokeAction. Il risultato dell'azione viene restituito nel dizionario della risposta, ad esempio:

```
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in

        if let error = error {
            //do something
            print("Errore di richiamo dell'azione \(error.localizedDescription)")

        } else {
            var result = reply["result"]
            print("È stato ottenuto il risultato \(result)")
        }


    })
} catch {
    print("Errore \(error)")
}
```
{: codeblock}

Per impostazione predefinita, l'SDK restituisce solo l'ID attivazione e gli eventuali risultati prodotti dall'azione richiamata. Per ottenere i metadati dell'intero oggetto risposta, che include il codice di stato della risposta HTTP, utilizza la seguente impostazione:

```
whisk.verboseReplies = true
```
{: codeblock}

## Configurazione dell'SDK
{: #openwhisk_sdk_configure}

Puoi configurare l'SDK per lavorare con diverse installazioni di {{site.data.keyword.openwhisk_short}} utilizzando il parametro baseURL. Ad esempio:

```
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

In questo esempio, utilizzi un'installazione in esecuzione su localhost:8080.  Se non specifichi il baseUrl, l'SDK mobile utilizza l'istanza in esecuzione in https://openwhisk.ng.bluemix.net.

Puoi passare una NSURLSession personalizzata nel caso tu richieda una gestione della rete speciale. Ad esempio, potresti avere una tua installazione di {{site.data.keyword.openwhisk_short}} che utilizza i certificati autofirmati.

```
// crea un delegato di rete che ritiene tutto attendibile
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// crea una NSURLSession che utilizza il delegato di attendibilità
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// imposta l'SDK per utilizzare questa urlSession invece di quella condivisa predefinita
whisk.urlSession = session
```
{: codeblock}

### Supporto per i nomi completi

Tutte le azioni e tutti i trigger hanno un nome completo formato da uno spazio dei nomi, un pacchetto e un nome di azione o trigger. L'SDK può accettarli come parametri quando richiama un'azione o attiva un trigger. L'SDK fornisce anche una funzione che accetta un nome completo che si presenta come `/mynamespace/mypackage/nameOfActionOrTrigger`. La stringa del nome completo supporta dei valori predefiniti senza nome per gli spazio dei nomi e i pacchetti di cui tutti gli utenti {{site.data.keyword.openwhisk_short}} dispongono, quindi si applicano le seguenti regole di analisi:

- qName = "foo" dà come risultato spazio dei nomi = default, pacchetto = default, azione/trigger = "foo"
- qName = "mypackage/foo" dà come risultato spazio dei nomi = default, pacchetto = mypackage, azione/trigger = "foo"
- qName = "/mynamespace/foo" dà come risultato spazio dei nomi = mynamespace, pacchetto = default, azione/trigger = "foo"
- qName = "/mynamespace/mypackage/foo dà come risultato spazio dei nomi = mynamespace, pacchetto = mypackage, azione/trigger = "foo"

Tutte le altre combinazioni generano un errore WhiskError.QualifiedName. Pertanto, in caso di utilizzo dei nomi comuni, devi racchiudere la chiamata in un costrutto "`do/try/catch`".

### Pulsante SDK

Per praticità, l'SDK include un `WhiskButton`, che estende il `UIButton` per consentirgli di richiamare le azioni.  Per utilizzare il `WhiskButton`, attieniti a questo esempio:

```
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Richiama quanto segue quando rilevi un evento di selezione pulsante, ad es, in una IBAction, per richiamare l'azione
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Spiacenti; si è verificato un errore: \(error)")
    } else {
        print("Operazione riuscita: \(reply)")
    }
})

// oppure, in alternativa, puoi configurare un pulsante "autonomo" che è in ascolto per eventi di selezione pulsante a esso relativi e richiama un'azione

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // utilizza l'API di nome completo che richiede do/try/catch
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in

       if let error = error {
           print("Spiacenti, si è verificato un errore: \(error)")
       } else {
           print("Operazione riuscita: \(reply)")
       }
   }
} catch {
   print("Errore di configurazione del pulsante \(error)")
}
```
{: codeblock}
