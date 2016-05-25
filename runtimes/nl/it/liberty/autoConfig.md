---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configurazione automatica dei servizi di cui è stato eseguito il bind
{: #auto_config}

*Ultimo aggiornamento: 31 marzo 2016*

Puoi eseguire il bind di diversi servizi alla tua applicazione Liberty. I servizi possono essere gestiti dal contenitore, gestiti dall'applicazione o entrambe le cose, a seconda delle scelte
dello sviluppatore.

Un servizio gestito dall'applicazione è un servizio gestito interamente dall'applicazione,
senza alcuna assistenza da Liberty. L'applicazione di norma legge
VCAP_SERVICES per ottenere informazioni sul servizio di cui è stato eseguito il bind ed accede al servizio
direttamente. L'applicazione fornisce tutto il codice di accesso client necessario. Non c'è alcuna dipendenza dalle funzioni Liberty o dalla configurazione del file server.xml. La configurazione automatica del pacchetto di build Liberty non si applica ai servizi di
questo tipo.

Un servizio gestito dal contenitore è un servizio gestito dal runtime Liberty. In alcuni casi, l'applicazione può cercare il servizio di cui è stato eseguito il bind in JNDI, mentre in altri casi il servizio viene utilizzato direttamente da Liberty stesso. Il pacchetto di build Liberty legge VCAP_SERVICES per ottenere
informazioni sui servizi di cui è stato eseguito il bind. Per ogni servizio gestito dal contenitore, il pacchetto di build esegue tre funzioni.

* Genera le [variabili cloud](optionsForPushing.html#accessing_info_of_bound_services) per il servizio di cui è stato eseguito il bind.
* Installa le funzioni Liberty e il codice di accesso client richiesto per accedere al servizio di cui è stato eseguito il bind.
* Genera o aggiorna le stanze del file server.xml richieste dal servizio.

Questo processo viene indicato come configurazione automatica,
Il pacchetto di build Liberty fornisce la configurazione automatica per i seguenti tipi di servizio:

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

Come indicato, alcuni servizi possono essere gestiti dall'applicazione oppure gestiti dal
contenitore. Mongo e SQLDB sono degli esempi di tali servizi. Per impostazione predefinita,
il pacchetto di build Liberty presume che questi servizi siano gestiti dal contenitore e li configura
automaticamente. Se desideri che sia l'applicazione a gestire il servizio, puoi optare per l'esclusione della configurazione automatica per il servizio impostando la variabile di ambiente services_autoconfig_excludes. Per ulteriori informazioni, consulta [Opzione di esclusione dalla configurazione automatica del servizio](autoConfig.html#opting_out).

## Installazione delle funzioni Liberty e
codice di accesso client
{: #installation_of_liberty_features}

Quando esegui il bind a un servizio gestito dal contenitore, il servizio potrebbe richiedere che le funzioni Liberty siano configurate nella stanza featureManager nel file server.xml. Il pacchetto di build
Liberty aggiorna la stanza featureManager e installa i file binari di supporto richiesti. Se il servizio richiede i jar di driver client, essi vengono scaricati in un'ubicazione nota
nell'installazione di Liberty.

Per ulteriori dettagli, consulta la documentazione per
il tipo di servizio di cui è stato eseguito il bind.

## Generazione o aggiornamento delle stanze di configurazione di server.xml
{: #generating_or_updating_serverxml}

Quando esegui il push di un'applicazione autonoma, il pacchetto di build Liberty genera la stanza server.xml come descritto in [Opzioni per eseguire il push delle applicazioni Liberty](optionsForPushing.html#options_for_pushing) a Bluemix. Quando esegui il push di un'applicazione autonoma ed esegui il bind ai servizi gestiti dal contenitore, il pacchetto di build Liberty genera le stanze di server.xml necessarie per i servizi di cui è stato eseguito il bind.

Quando fornisci un file server.xml ed esegui il bind ai servizi gestiti dal contenitore, il pacchetto di build Liberty:

* Genera la configurazione per i servizi di cui è stato eseguito il bind se il file server.xml fornito non contiene le stanze di configurazione per i servizi di cui è stato eseguito il bind.
* Aggiorna la configurazione per i servizi di cui è stato eseguito il bind se il file server.xml fornito contiene la stanza di configurazione per i servizi di cui è stato eseguito il bind.

Per ulteriori dettagli, consulta la documentazione per
il tipo di servizio di cui è stato eseguito il bind.

## Opzione di esclusione dalla configurazione automatica del servizio
{: #opting_out}

In
alcuni casi, potresti non desiderare che il pacchetto di build Liberty configuri automaticamente
i servizi di cui è stato eseguito il bind. Valuta i seguenti scenari.

* La mia applicazione utilizza MongoDB, ma io desidero che l'applicazione gestisca
direttamente la connessione al database. L'applicazione contiene il jar di
driver client necessario. Non desidero che il pacchetto di build Liberty configuri
automaticamente il servizio Mongo.
* Sto fornendo un file server.xml e ho fornito le stanze di configurazione per l'istanza SQLDB perché richiedo una configurazione dell'origine dati non standard. Non desidero che il pacchetto di build Liberty aggiorni il mio file server.xml ma richiedo comunque che il pacchetto di build Liberty verifichi che sia installato il software di supporto appropriato.

Per optare per l'esclusione dalla configurazione automatica
del servizio, utilizza la variabile di ambiente services_autoconfig_excludes. Puoi includere questa variabile
di ambiente in un manifest.yml o impostarla utilizzando il client cf.

Puoi optare
per l'esclusione dalla configurazione automatica dei servizi in base ai singoli tipi di servizio. Puoi scegliere di optare per l'esclusione in modo totale (come nello scenario Mongo) oppure di optare per l'esclusione solo dagli aggiornamenti della configurazione del file server.xml (come nello scenario SQLDB). Il valore da te specificato per la variabile di ambiente services_autoconfig_excludes è una stringa, come mostrato di seguito.

* La stringa può contenere le specifiche di opzione di esclusione per uno o più servizi.
* La specifica dell'opzione di esclusione per un servizio specifico è service_type=option, dove:
  * service_type è l'etichetta per il servizio come visualizzata in VCAP_SERVICES.
  * L'opzione è all o config.
* Se la stringa contiene una specifica di opzione di esclusione per più di un servizio,
le singole specifiche di opzione di esclusione devono essere separate da un singolo carattere spazio vuoto.

In modo più formale, la grammatica della stringa è la seguente.

```
    Opt_out_string :: <service_type_specification[<delimitatore>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: il tipo di servizio (etichetta del servizio come si presenta in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: #codeblock}

**Importante**: il tipo di servizio da te specificato deve corrispondere all'etichetta services come si presenta nella variabile di ambiente VCAP_SERVICES. Lo spazio vuoto non è consentito.
**Importante**: non è consentito alcuno spazio vuoto in una <specifica_tipo_di_servizio>. Il solo
utilizzo consentito dello spazio vuoto è per separare più istanze <specifica_di_tipo_servizio>.

Utilizza l'opzione "all" per optare per l'esclusione da tutte le azioni di configurazione automatica per un servizio, come nello scenario Mongo sopra riportato. Utilizza l'opzione "config" per optare per l'esclusione solo dalle azioni di aggiornamento della configurazione come nello scenario SQLDB sopra riportato.

Di seguito sono riportate delle specifiche di opzione di esclusione di esempio in un file manifest.yml per gli scenari Mongo e SQLDB.

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

Sono qui di seguito
riportati degli esempi di come impostare la variabile di ambiente services_autoconfig_excludes per l'applicazione
myapp utilizzando l'interfaccia riga di comando.

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
