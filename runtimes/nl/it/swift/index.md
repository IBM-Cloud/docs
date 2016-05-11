{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Runtime Swift
{: #swift_runtime}
*Ultimo aggiornamento: 19 febbraio 2016*

Il runtime Python su {{site.data.keyword.Bluemix}} si avvale del swift_buildpack.
Il swift_buildpack fornisce un ambiente di runtime completo per le applicazioni Swift.
{: shortdesc}

Il swift_buildpack verrà utilizzato se la directory root della tua applicazione contiene un file Package.swift.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter Swift. L'applicazione starter Swift è un'applicazione semplice Swift che puoi utilizzare per avere informazioni sui tipi di applicazioni del server che puoi distribuire utilizzando il linguaggio di programmazione Swift. Questa applicazione di esempio crea un server di base che restituisce un messaggio di saluto al client.  

**Nota:** questa applicazione starter non è un'applicazione pronta per la produzione.  Invece, è destinata ad essere utilizzata per scopi didattici.  Puoi fare delle prove con l'applicazione di avvio, apportare modifiche ed eseguirne il push all'ambiente {{site.data.keyword.Bluemix}}. Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Swift che deve essere utilizzata dalla tua applicazione con un file `.swift`-versione nella root del tuo repository.

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

Per un elenco completo delle versioni supportate di Swift, consulta il file [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) del pacchetto di build.

Per i dettagli sulla versione corrente del pacchetto di build di Swift che viene installato in {{site.data.keyword.Bluemix}}, fai riferimento alle informazioni sulla release di [ del pacchetto di build](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3).

Poiché vi sono frequenti modifiche nel linguaggio Swift, dovresti includere un file .swift-versione in modo che la tua applicazione sia "indicata" alla versione Swift e la tua applicazione la possa utilizzare.

# rellinks
## general
* [Pacchetto di build Cloud Foundry per Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* [Documentazione sul linguaggio Swift](https://swift.org/)
