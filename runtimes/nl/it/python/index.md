---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}
*Ultimo aggiornamento: 16 marzo 2016*

Il runtime Python su {{site.data.keyword.Bluemix}} si avvale del python_buildpack.
Il python_buildpack fornisce un ambiente di runtime completo per le applicazioni Python.
{: shortdesc}

Il python_buildpack verrà utilizzato se la directory root della tua applicazione contiene un file requirements.txt o un file setup.py.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter Python.  L'applicazione starter Python è una semplice applicazione Python che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push
all'ambiente {{site.data.keyword.Bluemix}}.  Consulta [Utilizzo di applicazioni starter](../../cfapps/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Python che deve essere utilizzata dalla tua applicazione impostando python-versionnumber nel file runtime.txt nella root della tua applicazione. Ad esempio:

```
python-3.4.3
```
{: codeblock}

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 2.7.10.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni Python sono disponibili nel [pacchetto
di build Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1) attualmente
installato in {{site.data.keyword.Bluemix}}:

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

Se la tua applicazione richiede una versione di Python che non è elencata, puoi utilizzare
il [pacchetto di build Python](https://github.com/cloudfoundry/python-buildpack) esterno
per distribuire l'applicazione.

# rellinks
## general
* [Pacchetto di build Cloud Foundry per Python](https://github.com/cloudfoundry/python-buildpack)
