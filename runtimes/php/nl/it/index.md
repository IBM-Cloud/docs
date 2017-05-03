---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

Il runtime PHP su {{site.data.keyword.Bluemix}} si avvale del php_buildpack.
Il php_buildpack fornisce un ambiente di runtime completo per le applicazioni PHP.
{: shortdesc}

Il php_buildpack viene utilizzato nelle seguenti condizioni:
* La tua applicazione contiene un file composer.json oppure
* la tua applicazione contiene un file *.php oppure
* La tua applicazione definisce una variabile ${WEBDIR} nel suo file [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) e tale variabile viene impostata su una directory esistente all'interno della tua applicazione.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter PHP.  L'applicazione starter PHP è una semplice applicazione PHP che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push
all'ambiente {{site.data.keyword.Bluemix}}.  Consulta il documento relativo all'[utilizzo delle applicazioni starter](/docs/cfapps/starter_app_usage.html) per assistenza nell'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di PHP che deve essere utilizzata dalla tua applicazione nel file composer.json. Ad esempio:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Per ulteriori informazioni, consulta [Composer Package links  ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://getcomposer.org/doc/04-schema.md#package-links).

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 5.5.34.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni PHP sono disponibili nel [pacchetto
di build PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.10) attualmente installato
in {{site.data.keyword.Bluemix}}:

* 5.5.33
* 5.5.34
* 5.6.19
* 5.6.20
* 7.0.4
* 7.0.5

Se la tua applicazione richiede una versione di PHP che non è elencata,
puoi utilizzare il [pacchetto
di build PHP](https://github.com/cloudfoundry/php-buildpack.git) esterno per distribuire l'applicazione.

# rellinks
{: #rellinks notoc}
## Esercitazioni ed esempi
{: #samples notoc}
* [Crea e distribuisci un'API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Crea e distribuisci un conta-calorie compatibile con i dispositivi mobili](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
{: #general notoc}
* [Pacchetto di build Cloud Foundry per PHP](https://github.com/cloudfoundry/php-buildpack.git)
