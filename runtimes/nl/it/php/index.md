---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*Ultimo aggiornamento: 16 marzo 2016*

Il runtime PHP su {{site.data.keyword.Bluemix}} si avvale del php_buildpack.
Il php_buildpack fornisce un ambiente di runtime completo per le applicazioni PHP.
{: shortdesc}

Il php_buildpack viene utilizzato nelle seguenti condizioni:
* La tua applicazione contiene un file composer.json oppure
* la tua applicazione contiene un file *.php oppure
* La tua applicazione definisce una variabile ${WEBDIR} nel suo file [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) e tale variabile viene impostata su una directory esistente all'interno della tua applicazione.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter PHP.  L'applicazione starter PHP è una semplice applicazione PHP che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push all'ambiente
{site.data.keyword.Bluemix}}.  Consulta il documento relativo all'[utilizzo delle applicazioni starter](../../cfapps/starter_app_usage.html) per assistenza nell'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di PHP che deve essere utilizzata dalla tua applicazione nel file composer.json. Ad esempio:

```
{
    "version": "1.5"
}
```
{: codeblock}
Per ulteriori informazioni, vedi [Pacchetti piattaforma compositore](https://getcomposer.org/doc/02-libraries.md#platform-packages).

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 5.5.30.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni PHP sono disponibili nel [pacchetto
di build PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5) attualmente installato
in {{site.data.keyword.Bluemix}}:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

Se la tua applicazione richiede una versione di PHP che non è elencata,
puoi utilizzare il [pacchetto
di build PHP](https://github.com/cloudfoundry/php-buildpack.git) esterno per distribuire l'applicazione.

# rellinks
## esempi
* [Crea e distribuisci un'API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Crea e distribuisci un conta-calorie compatibile con i dispositivi mobili](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
* [Pacchetto di build Cloud Foundry per PHP](https://github.com/cloudfoundry/php-buildpack.git)
