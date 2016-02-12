{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Ultimo aggiornamento: 12 gennaio 2016*

# Runtime Go
{: #go_runtime}

Il runtime Go su {{site.data.keyword.Bluemix}} si avvale del go_buildpack.
Il go_buildpack fornisce un ambiente di runtime completo per le applicazioni Go.
{: shortdesc}

Il go_buildpack viene utilizzato se la tua applicazione contiene un file denominato *.go.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter Go. L'applicazione starter Go è una semplice applicazione Go che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push all'ambiente Bluemix. Consulta il documento relativo all'[utilizzo delle applicazioni starter](../../cfapps/starter_app_usage.html) per assistenza nell'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Go che deve essere utilizzata dalla tua applicazione impostando la proprietà GoVersion nel file Godeps/Godeps.json alla root della tua applicazione. Ad esempio:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Per ulteriori informazioni,
vedi [godep](https://github.com/tools/godep).

### Versioni disponibili
{: #available_versions}

Le seguenti versioni Go sono disponibili nel [pacchetto di build Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)
attualmente installato in {{site.data.keyword.Bluemix}}:

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

Se la tua applicazione richiede una versione di Go che non è elencata, puoi utilizzare
il [pacchetto di build Go](https://github.com/cloudfoundry/go-buildpack.git) esterno
per distribuire l'applicazione.

## LINK CORRELATI
{: #related_links}
* [GoLang](http://golang.org/)
* [Pacchetto di build Cloud Foundry per Go](https://github.com/cloudfoundry/go-buildpack)
