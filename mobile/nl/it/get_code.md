---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Richiama codice
{: #Get_Code}

Dopo aver completato la configurazione del tuo progetto mobile con le funzionalità Push, Analytics e Authentication, puoi scaricare il codice che ti abilita ad eseguire il codice in Xcode o Android Studio. Il progetto scaricato è preconfigurato con le credenziali e le dipendenze SDK richieste per ogni funzionalità che hai configurato.

Avrai bisogno di completare le credenziali per i servizi che non sono configurabili nel tuo progetto scaricato. Il file `README.md` per il progetto starter contiene le istruzioni. Visualizza il file `README.md` in un visualizzatore Markdown per completare la configurazione.

### Strumenti per sviluppatori prerequisiti
{: prereq-dev-tools}

I seguenti strumenti per sviluppatori sono necessari quando stai lavorando con il codice generato dal dashboard {{site.data.keyword.Bluemix_notm}} Mobile:

#### Android
* [Android Studio 2.2](https://developer.android.com/studio)
	* Installa l'ultimo runtime [Android 7.0](https://www.android.com/versions/nougat-7-0/).

#### iOS
* Xcode 8.0 (raccomandato)
	* Installa l'ultimo runtime [iOS 10](http://www.apple.com/ios/ios-10/).
* [Homebrew](http://brew.sh/)
	* Uno strumento di riga di comando per assisterti durante l'installazione di altri runtime e strumenti, come CocoaPods e Carthage, per gli sviluppatori Apple.
* Gestore della dipendenza [CocoaPods](https://cocoapods.org/) per l'installazione delle dipendenze SDK iOS. Utilizza l'ultima versione:

	```
	$ sudo gem install cocoapods --pre
	```
* Gestore della dipendenza [Carthage](https://github.com/Carthage/Carthage) per l'installazione delle SDK Watson Developer Cloud.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (runtime Node e NPM) per assisterti durante l'esecuzione di API Connect Loopback e di altri strumenti Bluemix Productivity.

	Per eseguire gli strumenti API Connect localmente, utilizza Node 5.x:
	```
	$ brew install Node5
	```

* [Strumenti CLI Bluemix](http://clis.ng.bluemix.net/ui/home.html).
Strumenti della riga di comando per distribuire facilmente i runtime Cloud Foundry da una CLI (command line interface) con Bluemix.  
