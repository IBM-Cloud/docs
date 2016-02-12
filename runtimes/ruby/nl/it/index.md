{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Ultimo aggiornamento: 12 gennaio 2016*

# Runtime Ruby
{: #ruby_runtime}

Il runtime Ruby su {{site.data.keyword.Bluemix}} si avvale del ruby_buildpack.
Il ruby_buildpack fornisce un ambiente di runtime completo per l'applicazione Ruby.
{: shortdesc}

Il ruby_buildpack viene utilizzato se la tua applicazione ha un Gemfile nella directory root. Utilizzerà quindi Bundler per installare le tue dipendenze.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter Ruby. L'applicazione starter Ruby è una semplice applicazione Ruby che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione di avvio, apportare modifiche ed eseguirne il push all'ambiente {{site.data.keyword.Bluemix}}.  Consulta il documento relativo all'[utilizzo delle applicazioni starter](../../cfapps/starter_app_usage.html) per assistenza nell'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Ruby che deve essere utilizzata dalla tua applicazione nel Gemfile della tua applicazione, ad esempio:


```
  source 'https://rubygems.org'
  ruby '2.1.7'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 2.2.2.

### Versioni disponibili
{: #available_versions}

Le seguenti versioni Ruby sono disponibili nel [pacchetto di build Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.7?cm_mc_uid=02162397679414470795470&cm_mc_sid_50200000=1447951462)
attualmente installato in {{site.data.keyword.Bluemix}}:

* 2.0.0
* 2.1.6
* 2.1.7
* 2.2.2
* 2.2.3

Se la tua applicazione richiede una versione di Ruby che non è elencata, puoi
utilizzare il [pacchetto di build Ruby](https://github.com/cloudfoundry/ruby-buildpack) esterno
per distribuire l'applicazione.

## LINK CORRELATI
{: #related_links}
* [Pacchetto di build Cloud Foundry per Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Documentazione di Ruby on Rails](http://rubyonrails.org/documentation/)
