---



copyright:

  years: 2016, 2017

lastupdated: "2017-05-04"


---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Comandi Cloud Foundry (cf)
{: #cf}

L'interfaccia di riga comando (CLI) Cloud Foundry (cf) fornisce una serie di comandi per gestire le tue applicazioni. Le seguenti informazioni elencano i comandi cf più utilizzati per la gestione delle applicazioni e includono i relativi nomi, opzioni, utilizzo, prerequisiti, descrizioni ed esempi. Per elencare tutti i comandi cf e le informazioni di guida associate, utilizza `cf help`. Utilizza `cf nome_comando -h` per visualizzare delle informazioni di guida dettagliate per uno specifico comando.
{: shortdesc}

**Nota**: se la tua rete contiene un server proxy HTTP tra l'host che esegue i comandi cf e l'endpoint API Cloud Foundry, devi specificare il nome host o l'indirizzo IP del server proxy impostando la variabile di ambiente `HTTP_PROXY`. Per i dettagli,vedi [Utilizzo della CLI cf con un server proxy HTTP ![Icona link esterno](../../../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html){: new_window}.


## Indice dei comandi della CLI Cloud Foundry
{: #CLIname_commands_index}

Utilizza l'indice nella seguente tabella per fare riferimento ai comandi Cloud Foundry più utilizzati:

<table summary="Comandi generali di Cloud Foundry riportati in ordine alfabetico con dei link a ulteriori informazioni sul comando">
<caption>Tabella 1. Comandi generali di Cloud Foundry</caption>
 <thead>
 <th colspan="6">Comandi generali di Cloud Foundry</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](/docs/cli/reference/cfcommands/index.html#cf_api)</td>
 <td>[help](/docs/cli/reference/cfcommands/index.html#cf_help)</td>
 <td>[login](/docs/cli/reference/cfcommands/index.html#cf_login)</td>
 <td>[stacks](/docs/cli/reference/cfcommands/index.html#cf_stacks)</td>
 <td>[target](/docs/cli/reference/cfcommands/index.html#cf_target)</td>
 <td>[-v ](/docs/cli/reference/cfcommands/index.html#cf_v)</td>
 </tr>
   </tbody>
 </table>


<table summary="Comandi in ordine alfabetico per la gestione di applicazioni, spazi e servizi. Ogni comando ha un link che porta a ulteriori informazioni sul comando.">
<caption>Tabella 2. Comandi per la gestione di applicazioni, spazi e servizi</caption>
 <thead>
 <th colspan="5">Comandi per la gestione di applicazioni, spazi e servizi</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](/docs/cli/reference/cfcommands/index.html#cf_apps)</td>
 <td>[bind-service](/docs/cli/reference/cfcommands/index.html#cf_bind-service)</td>
 <td>[create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)</td>
 <td>[create-space](/docs/cli/reference/cfcommands/index.html#cf_create-space)</td>
 <td>[delete](/docs/cli/reference/cfcommands/index.html#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](/docs/cli/reference/cfcommands/index.html#cf_delete-space)</td>
 <td>[events](/docs/cli/reference/cfcommands/index.html#cf_events)</td>
 <td>[logs](/docs/cli/reference/cfcommands/index.html#cf_logs)</td>
 <td>[marketplace](/docs/cli/reference/cfcommands/index.html#cf_marketplace)</td>
 <td>[push (eseguire il)](/docs/cli/reference/cfcommands/index.html#cf_push)</td>
  </tr>
 <tr>
 <td>[ingrandire](/docs/cli/reference/cfcommands/index.html#cf_scale)</td>
 <td>[services](/docs/cli/reference/cfcommands/index.html#cf_services)
 <td>[set-env](/docs/cli/reference/cfcommands/index.html#cf_set-env)</td>
 <td>[ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)</td>
 <td>[stop](/docs/cli/reference/cfcommands/index.html#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

Utilizza questo comando per visualizzare o specificare l'URL dell'endpoint API di {{site.data.keyword.Bluemix_notm}}.

```
cf api [BluemixServerURL] [--skip-ssl-validation] [--unset]
```

<strong>Prerequisiti</strong>: Nessuno.

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>BluemixServerURL (facoltativo)</dt>
   <dd>L'URL dell'endpoint API Bluemix che devi specificare quando stabilisci una connessione a {{site.data.keyword.Bluemix_notm}}. Solitamente, questo URL è `https://api.{DomainName}`.
   Se vuoi visualizzare l'URL dell'endpoint API che stai attualmente utilizzando, non hai bisogno di specificare questo parametro per il comando cf api.</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>Disabilita il processo di convalida SSL. L'utilizzo di questo parametro può causare problemi di sicurezza.</dd>
   <dt>* --unset</dt>
   <dd>Rimuove le informazioni di connessione per tutti gli endpoint API.</dd>
    </dl>

<strong>Esempi</strong>:

Visualizza l'endpoint API corrente
```
cf api
```
{: codeblock}

Rimuovi la connessione a tutti gli endpoint API per api.ng.bluemix.net
```
cf api api.ng.bluemix.network --unset
```
{: codeblock}

Disabilita il processo di convalida SSL per api.ng.bluemix.network
```
cf api api.ng.bluemix.network --skip-ssl-validation
```
{: codeblock}


## cf apps
{: #cf_apps}

Elenca tutte le applicazioni da te distribuite nello spazio corrente. Viene visualizzato anche lo
stato di ciascuna applicazione.

Presumi di avere una istanza per un'applicazione; nella colonna delle istanze della risposta dal comando cf apps, vedi 1/1 se la tua applicazione è attiva e 0/1 se è invece inattiva. Se vedi ?/1, che indica che lo stato dell'istanza dell'applicazione è sconosciuto, puoi copiare l'URL dell'applicazione nel tuo browser per verificare se l'applicazione risponde oppure puoi controllare la parte finale del log utilizzando il comando `cf logs appname` per vedere se l'applicazione sta generando il contenuto del log.

```
cf apps
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`


## cf bind-service
{: #cf_bind-service}

Esegue il bind di un'istanza del servizio
esistente alla tua applicazione.

```
cf bind-service nome_applicazione istanza_servizio
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nome_applicazione (obbligatorio)</dt>
   <dd>Il nome dell'applicazione.</dd>
   <dt>istanza_servizio (obbligatorio)</dt>
   <dd>Il nome dell'istanza del servizio esistente.</dd>
    </dl>

<strong>Esempi</strong>:

Esegui il bind di un'istanza del servizio denominata `my_dataworks` alla tua applicazione denominata `my_app`.
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

Crea un'istanza del servizio

```
cf create-service nome_servizio piano_servizio istanza_servizio
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nome_servizio (obbligatorio)</dt>
   <dd>Il nome del servizio.</dd>
   <dt>piano_servizio (obbligatorio)</dt>
   <dd>Il nome del piano di servizio.</dd>
   <dt>istanza_servizio (obbligatorio)</dt>
   <dd>Il nome che vuoi utilizzare per la nuova istanza del servizio da te
creata.</dd>
    </dl>

<strong>Esempi</strong>:

Crea un'istanza del servizio {{site.data.keyword.dataworks_short}} con un piano `free`.
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

Crea uno spazio.

```
cf create-space nome_spazio [-o] [-q]
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nome_spazio (obbligatorio)</dt>
   <dd>Il nome dello spazio.</dd>
   <dt>*-o* (facoltativo)</dt>
   <dd>Il nome dell'organizzazione in cui vuoi creare uno spazio.</dd>
   <dt>*-q* (facoltativo)</dt>
   <dd>La quota da assegnare allo spazio appena creato. Se non viene specificata, viene automaticamente assegnata una quota predefinita.</dd>
    </dl>

<strong>Esempi</strong>:

Crea uno spazio denominato nuovo_spazio
```
cf create-space nuovo_spazio
```
{: codeblock}


## cf delete
{: #cf_delete}

Elimina
un'applicazione esistente.

```
cf delete nome_applicazione [-f] [-r]
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nome_applicazione (obbligatorio)</dt>
   <dd>Il nome dell'applicazione.</dd>
   <dt>*-f* (facoltativo)</dt>
   <dd>Forza l'eliminazione dell'applicazione senza alcuna conferma.</dd>
   <dt>*-r* (facoltativo)</dt>
   <dd>Elimina tutti i nomi dominio associati all'applicazione. </dd>
    </dl>

<strong>Esempi</strong>:

Elimina un'applicazione denominata `my_app` (richiede conferma).
```
cf delete my_app
```
{: codeblock}

Elimina un'applicazione denominata `my_app` senza richiedere conferma.
```
cf delete my_app -f
```
{: codeblock}

Elimina un'applicazione denominata `my_app` e tutti i nomi dominio associati a `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Elimina un'applicazione denominata `my_app` e tutti i nomi dominio associati a `my_app` senza richiedere conferma.
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

Elimina uno spazio.

```
cf delete-space nome_spazio [-f]
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nome_spazio (obbligatorio)</dt>
   <dd>Il nome dello spazio.</dd>
   <dt>*-f* (facoltativo)</dt>
   <dd>Forza l'eliminazione dello spazio senza alcuna conferma.</dd>
   *Nota:* l'eliminazione di uno spazio è un'operazione irreversibile.
    </dl>

<strong>Esempi</strong>:

Elimina un'applicazione denominata `my_app` (richiede conferma).
```
cf delete my_app
```
{: codeblock}

Elimina un'applicazione denominata `my_app` senza richiedere conferma.
```
cf delete my_app -f
```
{: codeblock}

Elimina un'applicazione denominata `my_app` e tutti i nomi dominio associati a `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Elimina un'applicazione denominata `my_app` e tutti i nomi dominio associati a `my_app` senza richiedere conferma.
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

Visualizza
gli eventi di runtime che sono correlati ad un'applicazione.

```
cf events [nomeapplicazione]
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nomeapplicazione</dt>
   <dd>Il nome dell'applicazione.</dd>
   </dl>

<strong>Esempi</strong>:

Visualizza gli eventi per un'applicazione denominata `my_app`.
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

Visualizza le informazioni di guida per tutti i comandi cf o per un comando cf specifico.

```
cf help [nome_comando]
```

<strong>Prerequisiti</strong>: Nessuno.

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>nome_comando (facoltativo)</dt>
   <dd>Il nome di un comando.</dd>
    </dl>

<strong>Esempi</strong>:

Visualizza le informazioni di guida per tutti i comandi cf.
```
cf help
```
{: codeblock}

Visualizza le informazioni di guida per il comando di eventi.
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

Ti fa accedere a {{site.data.keyword.Bluemix_notm}}. Se stai eseguendo l'accesso con un [ID federato](/docs/admin/account.html#signup), devi utilizzare il parametro SSO (single sign-on) per accedere. 

**Nota**: per accedere, puoi anche utilizzare una chiave API della piattaforma {{site.data.keyword.Bluemix_notm}}. Utilizza il nome utente `apikey` e il valore della tua chiave API come password. Per ulteriori informazioni sulla creazione di una chiave API, vedi [Gestione delle chiavi API](/docs/iam/apikeys.html).

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>Prerequisiti</strong>: Nessuno.

<strong>Opzioni del comando</strong>:

<dl>
<dt>*-a* https://api.{DomainName} (facoltativo)</dt>
<dd>L'URL dell'endpoint API di {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*-u* nome_utente (facoltativo)</dt>
<dd>Il tuo nome utente.</dd>
<dt>*-p* password (facoltativo)</dt>
<dd>La tua password.</dd>
<dd>*Importante:* se fornisci la tua password utilizzando il parametro *-p* sull'interfaccia riga di comando, la password potrebbe essere registrata nella cronologia della riga di comando. Per motivi di sicurezza, evita di fornire la password utilizzando il parametro
-p. Immetti invece la password quando te lo chiede l'interfaccia riga di comando.</dd>
<dt>*-sso*</dt>
<dd>Devi utilizzare l'opzione SSO (single sign-on ) quando accedi con un ID federato. Non è necessario quando accedi con un ID IBM. Se tenti di collegarti con un ID federato e non specifichi il parametro SSO, ti verrà richiesto di includerlo. Utilizza la richiesta del parametro SSO per immettere la passcode monouso all'accesso.</dd>
<dt>*-o*nome_organizzazione</dt>
<dd>Il nome dell'organizzazione alla quale desideri effettuare l'accesso.</dd>
<dt>*-s*nome_spazio</dt>
<dd>Il nome dello spazio al quale desideri effettuare l'accesso.</dd>
<dt>*--skip-ssl-validation* (facoltativo)</dt>
<dd>Disabilita il processo di convalida SSL. L'utilizzo di questo parametro può causare problemi di sicurezza.</dd>
</dl>

*Nota:* se fornisci la tua password nel parametro *-p* di questo comando, la tua password potrebbe essere registrata nel file di cronologia dei comandi della shell e potrebbe essere visibile ad altri utenti del sistema operativo locale.

<strong>Esempi</strong>:

Accedi a {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
{: codeblock}

Accedi a {{site.data.keyword.Bluemix_notm}} con un endpoint definito di `https://api.ng.bluemix.net`.
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

Accedi a {{site.data.keyword.Bluemix_notm}} con un endpoint definito di `https://api.ng.bluemix.net`, un nome utente `nome_utente` e nessuna password specificata per motivi di sicurezza.
```
cf login -a https://api.ng.bluemix.net -u nome_utente
```
{: codeblock}

Accedi a {{site.data.keyword.Bluemix_notm}} con un endpoint definito di `https://api.ng.bluemix.net`, un nome utente `nome_utente`, nessuna password specificata per motivi di sicurezza e un nome organizzazione `nome_organizzazione` e nome spazio `nome_spazio`.
```
cf login -a https://api.ng.bluemix.net -u nome_utente -o nome_organizzazione -s nome_spazio
```
{: codeblock}

Accedi a {{site.data.keyword.Bluemix_notm}} con un endpoint definito di `https://api.ng.bluemix.net` utilizzando una chiave API. Utilizza `apikey` come nome utente e la chiave API reale come password.
```
cf login -a https://api.ng.bluemix.net -u apikey -p ThisValueIsYourAPIKey
```
{: codeblock}


## cf logs
{: #cf_logs}

Visualizza i flussi di log
STDOUT e STDERR di un'applicazione.

```
cf logs nomeapplicazione [--recent]
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>*--recent* (facoltativo)</dt>
<dd>Richiama i log recenti.</dd>
</dl>

<strong>Esempi</strong>:

Visualizza i flussi di log per un'applicazione denominata `my_app`.
```
cf logs my_app
```
{: codeblock}

Visualizza i flussi di log recenti per un'applicazione denominata `my_app`.
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

Elenca tutti
i servizi disponibili nel marketplace. I servizi elencati da questo comando sono visualizzati anche nel catalogo {{site.data.keyword.Bluemix_notm}}.

```
cf marketplace
```
<strong>Prerequisiti</strong>: `cf api`

<strong>Opzioni del comando</strong>: Nessuna.

<strong>Esempi</strong>:

Elenca tutti i servizi nel marketplace
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

Distribuisce una nuova applicazione a {{site.data.keyword.Bluemix_notm}} oppure aggiorna un'applicazione esistente in {{site.data.keyword.Bluemix_notm}}.

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

<dl>
<dt>nome_applicazione (obbligatorio)</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>*-b* nome_pacchettodibuild (facoltativo)</dt>
<dd>Il nome del pacchetto di build. Il nome_pacchettodibuild può essere un pacchetto di build personalizzato in base al nome (ad esempio liberty-for-java) oppure un URL Git (ad esempio https://github.com/cloudfoundry/java-buildpack.git) oppure un URL Git con un ramo o tag (ad esempio, https://github.com/cloudfoundry/java-buildpack.git#v3.3.0 per la tag v3.3.0).</dd>
<dt>*-c* comando_di_avvio (facoltativo)</dt>
<dd>Il comando di avvio della tua applicazione. Per utilizzare il comando di avvio predefinito, specifica un valore null per questa opzione. </dd>
<dt>*-f* percorso_manifest (facoltativo)</dt>
<dd>Il percorso al file manifest. Il file manifest predefinito è manifest.yml sotto la directory root della tua applicazione.</dd>
<dt>*-i* numero_istanze (facoltativo)</dt>
<dd>Il numero di istanze.</dd>
<dt>*-k* limite_dico (facoltativo)</dt>
<dd>Il limite di disco per l'applicazione. I valori possibili sono *256M*, *1024M* o *1G*.</dd>
<dt>*-m* limite_memoria (facoltativo)</dt>
<dd>Il limite di memoria per l'applicazione. I valori possibili sono *256M*, *1024M* o *1G*.</dd>
<dt>*-n* nome_host (facoltativo)</dt>
<dd>Il nome host per l'applicazione, ad esempio *my-subdomain*.</dd>
<dt>*-p* percorso_applicazione (facoltativo)</dt>
<dd>Il percorso alla directory dell'applicazione o al file di archivio dell'applicazione.</dd>
<dt>*-s* nome_stack (facoltativo)</dt>
<dd>Lo stack per l'esecuzione delle applicazioni. Uno stack è un file system precostruito che include il sistema operativo. Utilizza `cf stacks` per visualizzare gli stack disponibili in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*-t* timeout (facoltativo)</dt>
<dd>Il tempo massimo in secondi per l'avvio dell'applicazione. Altri timeout lato server potrebbero
sovrascrivere questo valore.</dd>
<dt>*--no-hostname* (facoltativo)</dt>
<dd>Associa il dominio di sistema {{site.data.keyword.Bluemix_notm}} a questa applicazione.</dd>
<dt>*--no-manifest* (facoltativo)</dt>
<dd>Ignora il file manifest predefinito.</dd>
<dt>*--no-route* (facoltativo)</dt>
<dd>Non associa una rotta a questa applicazione.</dd>
<dt>*--no-start* (facoltativo)</dt>
<dd>Non avvia l'applicazione dopo che essa è stata distribuita.</dd>
<dt>*--random-route* (facoltativo)</dt>
<dd>Crea una rotta casuale per l'applicazione.</dd>
</dl>

<strong>Esempi</strong>:

Avvia un'applicazione denominata `my_app` con il comando di avvio predefinito.
```
cf push `my_app` -c null
```
{: codeblock}

Avvia un'applicazione denominata `my_app` con l'opzione per eseguire un file di script denominato `run.sh`.
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

Visualizza o modifica il numero di istanze,
il limite di spazio su disco e il limite di memoria per un'applicazione.

```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

<dl>
<dt>nome_applicazione (obbligatorio)</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>*-i* numero_istanze (facoltativo)</dt>
<dd>Il numero di istanze</dd>
<dt>*-k* limite_dico (facoltativo)</dt>
<dd>Il limite di disco per l'applicazione; i valori possibili sono `256M`, `1024M` o `1G`.</dd>
<dt>*-m* limite_memoria (facoltativo)</dt>
<dd>Il limite di memoria per l'applicazione; i valori possibili sono `256M`, `1024M` o `1G`.</dd>
<dt>*-f* (facoltativo)</dt>
<dd>Forza il riavvio dell'applicazione senza che venga presentata alcuna richiesta.</dd>
</dl>

<strong>Esempi</strong>:

Visualizza il numero di istanze, il limite di spazio su disco e il limite di memoria per un'applicazione denominata `my_app`.
```
cf scale my_app
```
{: codeblock}

Modifica il numero di istanze in `1234`, il limite di spazio su disco in `1G` e il limite di memoria in `1G` per un'applicazione denominata `my_app`.
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

Elenca tutti i servizi
disponibili nello spazio corrente.

```
cf services
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>: Nessuna.

<strong>Esempi</strong>:

Elenca tutti i servizi nello spazio corrente.
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

Imposta una variabile di ambiente per un'applicazione

```
cf set-env nomeapplicazione nome_var valore_var
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

<dl>
<dt>nome_applicazione (obbligatorio)</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>nome_var (obbligatorio)</dt>
<dd>Il nome della variabile di ambiente.</dd>
<dt>valore_var (obbligatorio)</dt>
<dd>Il valore della variabile di ambiente.</dd>
</dl>

<strong>Esempi</strong>:

Imposta una variabile di ambiente denominata `variable_a` con un valore `123` per l'applicazione denominata `my_app`.
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

Accedere in sicurezza al contenitore dell'applicazione. Il comando `cf ssh` può essere utilizzato per configurare una sessione SSH interattiva, eseguire comandi remoti, trasferire file e configurare l'inoltro alla porta con un'istanza del contenitore dell'applicazione specifica.

```
cf ssh
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

Per impostazione predefinita, l'accesso SSH è abilitato per le applicazioni Diego. Puoi utilizzare il comando `cf ssh-enabled` per verificare se l'accesso SSH è abilitato o il comando `cf enable-ssh` per abilitarlo se è disabilitato. 

<strong>Opzioni del comando</strong>:

<dl>
<dt>nomeapplicazione</dt>
<dd>Il nome dell'applicazione.</dd>
<dt>-c</dt>
<dd>Specifica un comando remoto per l'esecuzione.</dd>
<dt>-i</dt>
<dd>Indirizza un'istanza specifica di un'applicazione. Se non specificato, viene utilizzata la prima istanza dell'applicazione (un'istanza con indice 0).</dd>
<dt>-L</dt>
<dd>Abilita l'inoltro alla porta locale, che esegue il bind di una porta di output sulla tua macchina a una porta di input nella VM dell'applicazione.</dd>
<dt>-N</dt>
<dd>Non esegue un comando remoto.</dd>
<dt>-t, -tt o -T</dt>
<dd>Ti abilita ad eseguire una sessione SSH in modalità pseudo-tty che genera l'output di riga del terminale.<dd>
</dl>

<strong>Esempi</strong>:

Avvia una sessione SSH interattiva con un'immagine del contenitore eseguendo l'applicazione `my_app`.
```
$ cf ssh my_app
```
{: codeblock}

Esegui un solo comando nell'istanza del contenitore dell'applicazione `my_app`.
```
$ cf ssh my_app -c "ls -l"
```

Trasferisci un solo file dall'istanza del contenitore dell'applicazione `my_app`.
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

Configura l'inoltro alla porta della porta 7777 nella macchina locale alla porta 8888 nell'istanza del contenitore dell'applicazione `my_app`.
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

Elenca tutti
gli stack. Uno stack è un file system precostruito, compreso un sistema operativo che può eseguire
le applicazioni.

```
cf stacks
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`

<strong>Opzioni del comando</strong>: Nessuna.

<strong>Esempi</strong>:

Elenca tutti gli stack.
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

Arresta un'applicazione

```
cf stop nome_applicazione
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`, `cf target`

<strong>Opzioni del comando</strong>:

<dl>
<dt>nome_applicazione (obbligatorio)</dt>
<dd>Il nome dell'applicazione.</dd>
</dl>

<strong>Esempi</strong>:

Arresta l'applicazione denominata `my_app`.
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

Imposta o visualizza l'organizzazione o spazio di destinazione

```
cf target [-o org_name] [-s space_name]
```
<strong>Prerequisiti</strong>: `cf api`, `cf login`

<strong>Opzioni del comando</strong>:

<dl>
<dt>-o *nome_organizzazione* (facoltativo)</dt>
<dd>Il nome dell'organizzazione in cui si trova lo spazio.</dd>
<dt>-s *nome_spazio* (facoltativo)</dt>
<dd>Il nome dello spazio.</dd>
</dl>

<strong>Esempi</strong>:

Imposta la destinazione sull'organizzazione denominata "my_org" e sullo spazio denominato "my_space".
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

Visualizza la versione
dell'interfaccia riga di comando cf.

```
cf -v
```
<strong>Prerequisiti</strong>: Nessuno.

<strong>Opzioni del comando</strong>: Nessuna.

<strong>Esempi</strong>:

Visualizza la versione dell'interfaccia riga di comando cf.
```
cf -v
```
{: codeblock}



# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [Scarica CLI Cloud Foundry ![Icona link esterno](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases)
{: new_window}
* [Quick Reference Card - cf commands ![Icona link esterno](../../../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html)
{: new_window}
