---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Richiama codice
{: #Get_Code}

Dopo aver completato la configurazione del tuo progetto mobile con le funzionalità selezionate puoi scaricare il codice che ti abilita ad eseguire il codice in Xcode o Android Studio. Il progetto scaricato è preconfigurato con le credenziali e le dipendenze SDK richieste per ogni funzionalità che hai configurato.

Avrai bisogno di completare le credenziali per i servizi che non sono configurabili nel tuo progetto scaricato. Il file `README.md` per il progetto starter contiene le istruzioni. Visualizza il file `README.md` in un visualizzatore Markdown per completare la configurazione.

### Strumenti per sviluppatori prerequisiti
{: #prereq-dev-tools}

I seguenti strumenti per sviluppatori sono necessari quando stai lavorando con il codice generato dal dashboard {{site.data.keyword.Bluemix_notm}} Mobile:

#### Android
* [Android Studio 2.2 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://developer.android.com/studio "Icona link esterno")
	* Installa la versione più recente del runtime [Android 7.0 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.android.com/versions/nougat-7-0/ "Icona link esterno").

#### iOS
* [Xcode 8.0 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://developer.apple.com/xcode/ "Icona link esterno") (consigliato)
	* Installa la versione più recente del runtime [iOS 10 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://www.apple.com/ios/ios-10/ "Icona link esterno").
* [Homebrew ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://brew.sh/ "Icona link esterno")
	* Uno strumento di riga di comando per assisterti durante l'installazione di altri runtime e strumenti, come CocoaPods e Carthage, per gli sviluppatori Apple.
* Gestore dipendenze [CocoaPods ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cocoapods.org/ "Icona link esterno") per l'installazione delle dipendenze SDK iOS. Utilizza l'ultima versione:

	```
	$ sudo gem install cocoapods --pre
	```
* Gestore dipendenze [Carthage ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage "Icona link esterno") per l'installazione degli SDK Watson Developer Cloud.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (runtime Node e NPM) per assisterti durante l'esecuzione di API Connect Loopback e di altri strumenti Bluemix Productivity.

	Per eseguire gli strumenti API Connect localmente, utilizza Node 5.x:
	```
	$ brew install Node5
	```

* [Strumenti CLI Bluemix ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html "Icona link esterno").
Strumenti della riga di comando per distribuire facilmente i runtime Cloud Foundry da una CLI (command line interface) con Bluemix.  
