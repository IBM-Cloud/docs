---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Richiama codice
{: #Get_Code}

Dopo aver completato la configurazione del tuo progetto con le funzionalità selezionate puoi scaricare il codice che ti abilita ad eseguire il codice. Il progetto scaricato è preconfigurato con le credenziali e le dipendenze SDK richieste per ogni funzionalità che hai configurato.

Avrai bisogno di completare le credenziali per i servizi che non sono configurabili nel tuo progetto scaricato. Il file `README.md` per il progetto starter contiene le istruzioni. Visualizza il file `README.md` in un visualizzatore Markdown per completare la configurazione.

## Strumenti per sviluppatori prerequisiti
{: #prereq-dev-tools}

I seguenti strumenti per sviluppatori sono necessari quando stai lavorando con il codice generato dalla {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}:


### Generale 
{: #general notoc}

* [Homebrew ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://brew.sh/)
	* Uno strumento di riga di comando per assisterti durante l'installazione di altri runtime e strumenti, come CocoaPods e Carthage, per gli sviluppatori Apple.

* [Docker ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.docker.com/get-docker)
	* Un progetto open source per il supporto nell'esecuzione e nel debug delle applicazioni nei contenitori. Necessario solo per i progetti non mobili.

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js (runtime Node e npm) per assisterti durante l'esecuzione di {{site.data.keyword.apiconnect_short}} e di altri strumenti {{site.data.keyword.Bluemix_notm}} Productivity.

	Per eseguire gli strumenti {{site.data.keyword.apiconnect_short}} localmente, utilizza Node 5.x:
	
	```
	$ brew install Node5
	```

* [Strumenti CLI Bluemix ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html) 

   Strumenti della riga di comando per distribuire i runtime Cloud Foundry da una CLI (command line interface) con {{site.data.keyword.Bluemix_notm}}.  

* [{{site.data.keyword.dev_cli_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](dev_cli.html)

	Plugin della CLI {{site.data.keyword.Bluemix_notm}} per creare, eseguire, verificare e distribuire i progetti mobili e web.
	
* Plugin [SDK Generator ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](sdk_cli.html)

	Plugin della CLI {{site.data.keyword.Bluemix_notm}} per generare le SDK dalla tua definizione API REST conforme alla [Specifica Open API ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.openapis.org/).

### Android
{: #android notoc}

* [Android Studio 2.2 o superiore![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://developer.android.com/studio)
	* Installa la versione più recente del runtime [Android 7.0 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.android.com/versions/nougat-7-0/).

### iOS
{: #ios notoc}

* [Xcode 8 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://developer.apple.com/xcode/) (raccomandato)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* Gestore dipendenze [CocoaPods ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://cocoapods.org/) per l'installazione delle dipendenze SDK iOS. Utilizza l'ultima versione:

	```
	$ sudo gem install cocoapods --pre
	```
* Gestore dipendenze [Carthage ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage) per l'installazione delle SDK {{site.data.keyword.watson}} Developer Cloud.

	```
	$ brew install carthage
	```
