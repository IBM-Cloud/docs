# Inizializzazione di Push SDK per applicazioni iOS
{: #enable-push-ios-notifications-install}

Per un progetto Xcode esistente, puoi impostare il Bluemix Mobile Services Client SDK utilizzando lo strumento di gestione delle dipendenze CocoaPods. Un alternativa consiste nell'installare l'SDK in modo manuale.

**Nota**: per visualizzare il file readme Swift Push, vai a https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Installazione di CocoaPods

1. Installa CocoaPods utilizzando il seguente comando nel tuo terminale Mac.
```
$ sudo gem install cocoapods
```
2. Immetti il seguente comando nel terminale per inizializzare CocoaPods. Quando immetti questo comando, assicurati di eseguirlo nella directory dove si trova il tuo progetto Xcode. Il comando `pod init` file denominato Podfile.  
```
$ pod init
```
3. Nel Podfile generato, aggiungi le dipendenze SDK di cui hai bisogno. Copia il seguente Podfile.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copia il seguente elenco come è e rimuovi le dipendenze di cui non hai bisogno
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copia il seguente elenco come è e rimuovi le dipendenze di cui non hai bisogno.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. Dal terminale, vai alla cartella del progetto e installa le dipendenze con il seguente comando:
```
$ pod update
```
Tale comando installa le tue dipendenze e crea un nuovo spazio di lavoro Xcode.  **Nota**: assicurati di aprire sempre il nuovo spazio di lavoro Xcode invece del file di progetto Xcode originale:

	```
	$ open App.xcworkspace
	```
Lo spazio di lavoro contiene il tuo progetto originale e il progetto Pods che contiene le tue dipendenze. Se vuoi modificare una cartella di origine Bluemix Mobile Services, puoi trovarla nel tuo progetto Pods, in `Pods/yourImportedSourceFolder`, ad esempio: `Pods/IMFGoogleAuthentication`.

##Utilizzo dei framework importati e delle cartelle di origine

Fai riferimento all'SDK nel tuo codice.


### Objective-C

Scrivi le direttive #import per le intestazioni pertinenti, ad esempio:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Nota**: aggiornare il tuo progetto Pods utilizzando i comandi CocoaPods `pod install` o `pod update` potrebbe sovrascrivere le cartelle di origine Bluemix Mobile Services. Se vuoi conservare le tue versioni personalizzate dei file originali, assicurati che ne sia stato eseguito il backup prime di immettere uno di questi comandi.

###Swift

**Prerequisiti**

- iOS 8.0 o successiva
- Xcode 7


Scrivi le direttive #import per le intestazioni pertinenti, ad esempio:

```
//swift
import BMSCore
import BMSPush
```


##Impostazioni di creazione

Vai a **Xcode > Build Settings > Build Options e imposta Enable Bitcode** su **No**.

**Attenzione**: a partire da iOS 9, le modifiche alla funzione ATS (App Transport Security) potrebbero influenzare il modo in cui gestisci il processo di autenticazione. I seguenti post del blog descrivono in maggiore dettaglio le modifiche:[ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) e [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
