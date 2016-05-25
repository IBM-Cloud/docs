---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}
*Ultimo aggiornamento: 16 marzo 2016*

Il runtime Go su {{site.data.keyword.Bluemix}} si avvale della tecnologia go_buildpack.
go_buildpack fornisce un ambiente di runtime completo per la applicazione GO.
{: shortdesc}

go_buildpack viene utilizzato se la tua applicazione contiene un file denominato *.go.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} Fornisce un'applicazione starter Go.  L'applicazione starter Go è un'applicazione Go semplice che fornisce un template che puoi utilizzare per la tua applicazione. Puoi sperimentare l'applicazione starter ed effettuare e inviare modifiche all'ambiente Bluemix  Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Go che deve essere utilizzata dalla tua applicazione impostando la proprietà GoVersion nel file Godeps/Godeps.json a livello della root della tua applicazione. Ad esempio:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Per ulteriori informazioni, consulta [godep](https://github.com/tools/godep){: new_window}.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni Go sono disponibili nel
[pacchetto di build Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2){: new_window}
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
il [pacchetto di build Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window}
esterno per distribuire l'applicazione.

# rellinks
## general
* [GoLang](http://golang.org/){: new_window}
* [Pacchetto di build Cloud Foundry per Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
