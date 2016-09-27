{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Runtime Swift
{: #swift_runtime}
*Ultimo aggiornamento: 10 giugno 2016*
{: .last-updated}

Il runtime Python su {{site.data.keyword.Bluemix}} si avvale del pacchetto di build Swift per Bluemix (ad es. swift_buildpack).
Il swift_buildpack fornisce un ambiente di runtime completo per le applicazioni Swift.
{: shortdesc}

Il swift_buildpack verrà utilizzato se la directory root della tua applicazione contiene un file Package.swift.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter Swift. L'applicazione starter Swift è un'applicazione semplice Swift che puoi utilizzare per avere informazioni sui tipi di applicazioni del server che puoi distribuire utilizzando il linguaggio di programmazione Swift. Questa applicazione di esempio crea un server HTTP di base che restituisce del contenuto HTML al client.

**Nota:** questa applicazione starter non è un'applicazione pronta per la produzione.  Invece, è destinata ad essere utilizzata per scopi didattici.  Puoi fare delle prove con l'applicazione di avvio, apportare modifiche ed eseguirne il push all'ambiente {{site.data.keyword.Bluemix}}. Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Il swift_buildpack installato su Bluemix supporta la versione `DEVELOPMENT-SNAPSHOT-2016-05-03-a` dei file binari Swift. Se desideri utilizzare una differente versione di Swift su Bluemix per la tua applicazione, puoi specificare la versione con un file `.swift-version` nella root del tuo repository:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

In aggiunta all'inclusione di un file `.swift-version`, hai inoltre bisogno di aggiungere il parametro `-b https://github.com/IBM-Swift/swift-buildpack` al comando `cf push`, come mostrato di seguito:

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Per un elenco completo delle versioni supportate di Swift, consulta il file [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) del pacchetto di build.

Per i dettagli sulla versione corrente del pacchetto di build di Swift che viene installato in {{site.data.keyword.Bluemix}}, fai riferimento alle informazioni sulla release di [ del pacchetto di build](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1).

Poiché vi sono frequenti modifiche nel linguaggio Swift, dovresti includere un file `.swift-version` in modo che la tua applicazione sia "indicata" alla versione Swift e la tua applicazione la possa utilizzare. Ricorda che se stai utilizzando una versione di Swift diversa da `DEVELOPMENT-SNAPSHOT-2016-05-03-a`, devi specificare il parametro `-b https://github.com/IBM-Swift/swift-buildpack` quando esegui il push della tua applicazione (come mostrato di seguito).

# rellinks
{: #rellinks}
## general
{: #general}
* [Pacchetto di build Swift per Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* [Documentazione sul linguaggio Swift](https://swift.org/)
