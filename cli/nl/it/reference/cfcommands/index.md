---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Comandi Cloud Foundry (cf)

*Ultimo aggiornamento: 29 gennaio 2016*

Puoi utilizzare i comandi Cloud Foundry (cf) per gestire le tue applicazioni.
{:shortdesc}

Le informazioni riportate di seguito elencano i comandi cf utilizzati più comunemente per
gestire le applicazioni. Per elencare tutti i comandi cf e le relative informazioni di guida, utilizza `cf help`. Utilizza `cf nome_comando -h` per visualizzare delle informazioni di guida dettagliate per uno specifico comando.

*Nota:* se la tua rete contiene un server proxy HTTP tra l'host
che esegue i comandi cf e l'endpoint API Cloud Foundry, devi specificare il nome
host o l'indirizzo IP del server proxy impostando la variabile di ambiente `HTTP_PROXY`. Per i dettagli, vedi il documento relativo all'[utilizzo della CLI cf con un server proxy HTTP](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html).

## cf api

Visualizza o specifica l'URL dell'endpoint API di {{site.data.keyword.Bluemix_notm}}.
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>L'URL dell'endpoint API Bluemix che devi specificare quando stabilisci una connessione a {{site.data.keyword.Bluemix_notm}}. Di norma, questo URL è https://api.{DomainName}.
Se vuoi visualizzare l'URL dell'endpoint API che stai attualmente utilizzando, non hai bisogno di specificare questo parametro per il comando cf api.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Disabilita il processo di convalida SSL. L'utilizzo di questo parametro può causare problemi di sicurezza.</dd>
<dt>*--unset*</dt>
<dd>Rimuove le informazioni di connessione per tutti gli endpoint API.</dd>
</dl>

## cf apps

Elenca tutte le applicazioni da te distribuite nello spazio corrente. Viene visualizzato anche lo
stato di ciascuna applicazione.

Presumi di avere una istanza per un'applicazione; nella colonna delle istanze della risposta dal comando cf apps, vedi 1/1 se la tua applicazione è attiva e 0/1 se è invece inattiva. Se vedi ?/1, che indica che lo stato dell'istanza dell'applicazione è sconosciuto, puoi copiare l'URL dell'applicazione nel tuo browser per verificare se l'applicazione risponde oppure puoi controllare la parte finale del log utilizzando il comando `cf logs nomeapplicazione` per vedere se l'applicazione sta generando del contenuto del log.

## cf bind-service

Esegue il bind di un'istanza del servizio
esistente alla tua applicazione.
```
cf bind-service nomeapplicazione istanza_servizio
```

Ad esempio, se
hai un'istanza del servizio denominata `my_dataworks` nella tua organizzazione e
nel tuo spazio correnti, puoi utilizzare `cf bind-service
my_app my_dataworks` per eseguire il bind di questa istanza del servizio alla tua applicazione.

<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>istanza_servizio</dt>
<dd>Il nome dell'istanza del servizio esistente.</dd>
</dl>

## cf create-service

Crea un'istanza
del servizio.
```
cf create-service nome_servizio piano_servizio istanza_servizio
```
Ad
esempio, puoi utilizzare `cf create-service DataWorks free my_dataworks` per
creare un'istanza del servizio {{site.data.keyword.dataworks_short}} con un
piano libero.

<dl>
<dt>nome_servizio</dt>
<dd>Il nome del servizio.</dd>
<dt>piano_servizio</dt>
<dd>Il nome del piano di servizio.</dd>
<dt>istanza_servizio</dt>
<dd>Il nome che vuoi utilizzare per la nuova istanza del servizio da te
creata.</dd>
</dl>

## cf create-space

Crea uno spazio.
```
cf create-space nome_spazio
```
<dl>
<dt>nome_spazio</dt>
<dd>Il nome dello spazio.</dd>
<dt>*-o*</dt>
<dd>Il nome dell'organizzazione in cui vuoi creare uno spazio.</dd>
<dt>*-q*</dt>
<dd>La quota da assegnare allo spazio appena creato. Se non viene specificata, viene automaticamente assegnata una quota predefinita.</dd>
</dl>

## cf delete

Elimina
un'applicazione esistente.
```
cf delete nomeapplicazione
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.<dd>
<dt>*-f*</dt>
<dd>Forza l'eliminazione dell'applicazione senza alcuna conferma. Questo parametro è facoltativo.</dd>
<dt>*-r*</dt>
<dd>Elimina tutti i nomi dominio associati all'applicazione. Questo parametro è facoltativo.</dd>
</dl>

## cf delete-space

Elimina uno spazio.
```
cf delete-space nome_spazio
```
<dl>
<dt>nome_spazio</dt>
<dd>Il nome dello spazio.</dd>
<dt>*-f*</dt>
<dd>Forza l'eliminazione dello spazio senza alcuna conferma. Questo parametro è facoltativo.</dd>
*Nota:* l'eliminazione di uno spazio è un'operazione irreversibile.
</dl>

## cf events

Visualizza
gli eventi di runtime che sono correlati ad un'applicazione.
```
cf events nomeapplicazione
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
</dl>

## cf help

Visualizza le informazioni di guida per tutti i comandi cf oppure per uno specifico comando cf se viene utilizzato il parametro nome_comando.
```
cf help nome_comando
```
<dl>
<dt>nome_comando</dt>
<dd>Il nome di un comando. Se vuoi informazioni di guida specifiche per un comando,
puoi utilizzare questo parametro.</dd>
<dd>Se non specifichi questo parametro, vengono visualizzate le informazioni di guida di tutti i
comandi cf.</dd>
</dl>


## cf login

Ti fa accedere a {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
Puoi utilizzare uno o più dei seguenti parametri quando immetti il comando cf login:
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>L'URL dell'endpoint API di {{site.data.keyword.Bluemix_notm}}. Questo parametro è facoltativo.</dd>
<dt>*-u*nome_utente</dt>
<dd>Il tuo nome utente. Questo parametro è facoltativo.</dd>
<dt>*-p*password</dt>
<dd>La tua password.</dd>
<dd>*Importante:* se fornisci la tua password utilizzando il parametro *-p* sull'interfaccia riga di comando, la password potrebbe essere registrata nella cronologia della riga di comando. Per motivi di sicurezza, evita di fornire la password utilizzando il parametro
-p. Immetti invece la password quando te lo chiede l'interfaccia riga di comando.</dd>
<dt>*-o*nome_organizzazione</dt>
<dd>Il nome dell'organizzazione alla quale desideri effettuare l'accesso.</dd>
<dt>*-s*nome_spazio</dt>
<dd>Il nome dello spazio al quale desideri effettuare l'accesso.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Disabilita il processo di convalida SSL. L'utilizzo di questo parametro può causare problemi di sicurezza.</dd>
</dl>

*Nota:* se fornisci la tua password nel parametro *-p* di questo comando, la tua password potrebbe essere registrata nel file di cronologia dei comandi della shell e potrebbe essere visibile ad altri utenti del sistema operativo locale.


## cf logs

Visualizza i flussi di log
STDOUT e STDERR di un'applicazione.
```
cf logs nomeapplicazione
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>*--recent*</dt>
<dd>Richiama i log recenti.</dd>
</dl>

## cf marketplace

Elenca tutti
i servizi disponibili nel marketplace. I servizi elencati da questo comando sono visualizzati anche nel catalogo {{site.data.keyword.Bluemix_notm}}.
```
cf marketplace
```

## cf push

Distribuisce una nuova applicazione a Bluemix oppure aggiorna un'applicazione esistente in Bluemix.
```
cf push nomeapplicazione 
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>*-b*nome_pacchettodibuild</dt>
<dd>Il nome del pacchetto di build. Il nome_pacchettodibuild può essere un pacchetto di build personalizzato in base al nome oppure un URL GIT, ad esempio `my-buildpack` o `https://github.com/heroku/heroku-buildpack-play.git`.</dd>
<dt>*-c*comando_di_avvio</dt>
<dd>Il comando di avvio della tua applicazione. Per utilizzare il comando di avvio predefinito, specifica un valore null per questa opzione. Ad
esempio:</dd>
<dd>```
cf push nomeapplicazione -c null
```</dd>
<dd>Puoi anche utilizzare questa
opzione per eseguire i file script. Ad
                                    esempio:
```
cf push nomeapplicazione -c “bash ./<run.sh>"
```</dd>
<dt>*-f*percorso_manifest</dt>
<dd>Il percorso al file manifest. Il file manifest predefinito è manifest.yml sotto la directory root della tua applicazione.</dd>
<dt>*-i*numero_istanze</dt>
<dd>Il numero di istanze.</dd>
<dt>*-k*limite_disco</dt>
<dd>Il limite di disco per l'applicazione, ad esempio *256M*, *1024M*
o *1G*.</dd>
<dt>*-m*limite_memoria</dt>
<dd>Il limite di memoria per l'applicazione, ad esempio *256M*, *1024M*
o *1G*.</dd>
<dt>*-n*nome_host</dt>
<dd>Il nome host per l'applicazione, ad esempio *my-subdomain*.</dd>
<dt>*-p*percorso_applicazione</dt>
<dd>Il percorso alla directory dell'applicazione o al file di archivio dell'applicazione.</dd>
<dt>*-t*timeout</dt>
<dd>Il tempo massimo in secondi per l'avvio dell'applicazione. Altri timeout lato server potrebbero
sovrascrivere questo valore.</dd>
<dt>*-s* nomestack</dt>
<dd>Lo stack per l'esecuzione delle applicazioni. Uno stack è un file system precostruito che include il sistema operativo. Utilizza `cf stacks` per visualizzare gli stack disponibili in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*--no-hostname*</dt>
<dd>Associa il dominio di sistema Bluemix a questa applicazione.</dd>
<dt>*--no-manifest*</dt>
<dd>Ignora il file manifest predefinito.</dd>
<dt>*--no-route*</dt>
<dd>Non associa una rotta a questa applicazione.</dd>
<dt>*--no-start*</dt>
<dd>Non avvia l'applicazione dopo che essa è stata distribuita.</dd>
<dt>*--random-route*</dt>
<dd>Crea una rotta casuale per l'applicazione.</dd>
</dl>

## cf scale

Visualizza o modifica il numero di istanze,
il limite di spazio su disco e il limite di memoria per un'applicazione.
```
cf scale nomeapplicazione -i numero_istanze -k limite_disco -m limite_memoria
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>*-i*numero_istanze</dt>
<dd>Il numero di istanze</dd>
<dt>*-k*limite_disco</dt>
<dd>Il limite di disco per l'applicazione, ad esempio *256M*, *1024M*
o *1G*.</dd>
<dt>*-m*limite_memoria</dt>
<dd>Il limite di memoria per l'applicazione, ad esempio *256M*, *1024M*
o *1G*.</dd>
<dt>*-f*</dt>
<dd>Forza il riavvio dell'applicazione senza che venga presentata alcuna richiesta.</dd>
</dl>

## cf services

Elenca tutti i servizi
disponibili nello spazio corrente.
```
cf services
```

## cf set-env

Imposta una
variabile di ambiente per un'applicazione.
```
cf set-env nomeapplicazione nome_var valore_var
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>nome_var</dt>
<dd>Il nome della variabile di ambiente.</dd>
<dt>valore_var</dt>
<dd>Il valore della variabile di ambiente.</dd>
</dl>

## cf stacks

Elenca tutti
gli stack. Uno stack è un file system precostruito, compreso un sistema operativo che può eseguire
le applicazioni.
```
cf stacks
```

## cf stop

Arresta un'applicazione.
```
cf stop nomeapplicazione
```
<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
</dl>

## cf -v

Visualizza la versione
dell'interfaccia riga di comando cf.
```
cf -v
```

# rellinks
{: #rellinks}
## general 
{: #general}
* [Quick Reference Card - cf commands](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
