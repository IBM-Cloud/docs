---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime for Swift
{: #swift_runtime}

Il Runtime per Swift su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build [IBM Bluemix per Swift](https://github.com/IBM-Swift/swift-buildpack) (ossia swift_buildpack).
Questo pacchetto di build fornisce un ambiente di runtime completo per le applicazioni Swift.
{: shortdesc}

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'[applicazione starter](https://github.com/IBM-Bluemix/Kitura-Starter) Swift basata su Kitura. L'applicazione starter Kitura è un'applicazione semplice Swift che puoi utilizzare per avere informazioni sui tipi di applicazioni del server che puoi distribuire utilizzando il linguaggio di programmazione Swift. Questa applicazione di esempio crea un server HTTP Kitura di base che restituisce del contenuto HTML al client.

**Nota:** l'applicazione starter di Kitura è pensata per essere utilizzata per scopi didattici. Puoi fare delle prove con l'applicazione starter facendo delle modifiche ed eseguirne il push all'ambiente {{site.data.keyword.Bluemix}}. Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Ridenominazione della tua applicazione
{: #renaming_your_app}

Se desideri ridenominare la tua applicazione, dallo starter Kitura o più genericamente, sono presenti alcune modifiche che devono essere effettuate. Questo evita confusione e assicura uno sviluppo senza errori.

- Ridenomina la cartella del progetto dell'applicazione in modo che corrisponda al tuo nome dell'applicazione.
- `Package.swift` - Modifica le seguenti voci:
    - `name` - Deve corrispondere al nome dell'applicazione.
    - `targets[Target(name:)]` - Deve corrispondere al nome dell'applicazione.
- `manifest.yml` - Modifica le seguenti voci:
    - `name` - Deve corrispondere al nome dell'applicazione.
    - `command` - Il nome dell'eseguibile per avviare la tua applicazione (deve corrispondere al nome specificato nel file Package.swift).

## Versioni di runtime
{: #runtime_versions}

Per impostazione predefinita, il Runtime per Swift (swift_buildpack) ospitato in {{site.data.keyword.Bluemix}} utilizza l'ultima versione GA dei file binari Swift. Questa è la sola versione di Swift direttamente supportata da IBM ed è la versione raccomandata da utilizzare nella tua applicazione. Puoi determinare questa versione supportata esaminando le [ultime informazioni sulla release](https://github.com/IBM-Swift/swift-buildpack/releases) del swift_buildpack. Il pacchetto di build può elencare altre versioni Swift come mostrato nel suo file [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Queste versioni comuni ma non supportate di Swift, sono pre memorizzate nella cache all'interno del pacchetto di build, che forniscono un tempo di provisioning ridotto.

Se desideri utilizzare una differente versione di Swift su {{site.data.keyword.Bluemix}} per la tua applicazione, puoi specificare la versione con un file `.swift-version` nella root del tuo repository. Questo file `.swift-version` definisce quale versione di Swift deve essere utilizzata dal swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Poiché vi sono frequenti aggiornamenti nel linguaggio Swift, dovresti sempre includere un file `.swift-version` in modo che la tua applicazione sia "indicata" alla versione Swift e la tua applicazione la possa utilizzare.

Tieni presente che puoi specificare una qualsiasi versione valida di Swift nel tuo file `.swift-version`. Queste versioni alternative devono corrispondere alla denominazione e vengono trasmesse direttamente da [Swift.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://swift.org/download/). Quando si utilizza una versione senza cache il provisioning sarà un po' più lungo, non esistono differenze nelle prestazioni del runtime della tua applicazione Swift.

Il swift_buildpack predefinito in {{site.data.keyword.Bluemix}} verrà utilizzato se la directory root della tua applicazione contiene un file `Package.swift`.  Se desideri utilizzare un pacchetto di build alternativo, devi specificarlo aggiungendo una voce `buildpack: {buildpackUrl}` al file manifest.yml della tua applicazione. In alternativa, puoi definirlo al momento della distribuzione, utilizzando l'argomento del comando `cf push -b {buildpackUrl}`.


## Ambienti dello sviluppatore

Gli sviluppatori dispongono di molte opzioni quando creano le applicazioni lato server con Swift. Quelle che utilizzano un dispositivo MacOS di Apple potrebbero preferire l'utilizzo dell'IDE Xcode, seppure non sia un requisito.  Le applicazioni basate su Swift che saranno distribuite ed eseguite su {{site.data.keyword.Bluemix}} possono utilizzare qualsiasi IDE o editor di programmazione.  L'evidenziazione la pulitura della sintassi per Swift sono disponibili per molti editor comuni. Lo strumento di riga di comando Swift REPL incluso nei file binari da [Swift.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://swift.org/), consente la verifica e la compilazione locale prima della distribuzione a {{site.data.keyword.Bluemix}}.

Per gli utenti MaxOS, puoi utilizzare gli [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) che semplificano la creazione, la distribuzione, la gestione e il controllo delle applicazioni Swift lato server in esecuzione su {{site.data.keyword.Bluemix}}.  


## Integrazione avanzata

L'utilizzo dei [Framework web di Kitura](http://ibm-swift.github.io/Kitura/) fornisce molte funzionalità. Kitura è modulare per natura e vorrai presto estenderne le funzionalità con SDK compressi, per fornire funzioni come l'autenticazione, l'accesso ai servizi basati su Watson e una grande varietà di database.  Kitura fornisce il supporto per molti database direttamente, mentre altri progetti open source forniscono anche le SDK per molte piattaforme del database. Il seguente è un elenco non completo di SDK fornite da Kitura da utilizzare con le risorse esterne.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 and DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant and CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Per trovare altri pacchetti Swift da includere nella tua applicazione, vai al [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) ed esegui una ricerca del database o servizio desiderato. Il catalogo del pacchetto fornisce un modo semplice di individuare i pacchetti che puoi includere nelle tue applicazioni Swift. I pacchetti possono essere aggiunti all'applicazione Swift includendo i dettagli della versione e dell'URL Git del pacchetto nel file `Package.swift` dell'applicazione. Per ulteriori dettagli sulla gestione del pacchetto, fai riferimento alla sezione [Package Manager di Swift.org](https://swift.org/package-manager/).


## Informazioni Correlate

Esistono altri strumenti online disponibili da IBM per lo sviluppatore Swift.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - Sito di destinazione principale per tutte le informazioni su IBM Swift. Puoi trovare informazioni sulle nostre offerte, blog, eventi sociali, documentazione e altro.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - Questo sito ti fornisce un ambiente per la verifica facile e veloce dei frammenti di codice Swift in molte versioni di Swift e anche su piattaforme di runtime Swift differenti. Puoi anche salvare e condividere gli esempi di codice con altri, così come esplorare esempi comuni forniti da altri utenti.


# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura Documentation and APIs](http://ibm-swift.github.io/Kitura/)
* [Kitura Starter app for Bluemix](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift release notes](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://swift.org/)
* [Swift language documentation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://swift.org/documentation)
