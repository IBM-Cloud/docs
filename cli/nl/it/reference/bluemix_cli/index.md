{:shortdesc: .shortdesc}

# Comandi bx per interagire con {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Ultimo aggiornamento* 19 ottobre 2015

L'interfaccia di riga comando (CLI) {{site.data.keyword.Bluemix}} fornisce una serie di comandi che vengono raggruppati in base allo spazio dei nomi per consentire agli utenti di interagire con {{site.data.keyword.Bluemix_notm}}. Alcuni comandi CLI {{site.data.keyword.Bluemix_notm}}, che sono denominati comandi bx, sono dei wrapper di comandi cf esistenti e  altri sono univoci per {{site.data.keyword.Bluemix_notm}}. Le informazioni qui di seguito elencano tutti i comandi supportati dalla CLI {{site.data.keyword.Bluemix_notm}} e includono i relativi nomi, opzioni, utilizzo, prerequisiti, descrizioni ed esempi.
{:shortdesc}
 
**Nota:** i *Prerequisiti* elencano quali azioni sono richieste prima di utilizzare il comando. I comandi che non hanno azioni prerequisite elencano **Nessuno**. Altrimenti, i prerequisiti possono includere una o più delle seguenti azioni:
<dl>
<dt>**Endpoint**</dt>
<dd>Un endpoint API deve essere impostato mediante `bluemix api` prima di utilizzare il comando.</dd>
<dt>**Accesso**</dt>
<dd>L'accesso utilizzando il comando `bluemix login` è richiesto prima di utilizzare questo comando.</dd>
<dt>**Destinazione**</dt>
<dd>Il comando `bluemix target` deve essere utilizzato per impostare un'organizzazione e uno spazio prima di utilizzare questo comando.</dd>
</dl>

## bluemix help
Visualizzare la guida generale per i comandi integrati di primo livello e gli spazi dei nomi supportati della CLI {{site.data.keyword.Bluemix_notm}} oppure la guida per un comando o uno spazio dei nomi integrati specifici.

```
bluemix help [COMANDO|SPAZIODENOMI]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*COMANDO*|*SPAZIODEINOMI*  (facoltativo):  il comando o lo spazio dei nomi per cui viene visualizzata la guida. Se non viene specificata, viene visualizzata la guida generale per la CLI {{site.data.keyword.Bluemix_notm}}.

**Esempi**:

Visualizzare la guida generale per la CLI {{site.data.keyword.Bluemix_notm}}:

```
bluemix help
```

Visualizzare la guida per lo spazio dei nomi `catalog`:

```
bluemix help catalog
```

```
bluemix catalog help
```

Visualizzare la guida per il comando `info`:

```
bluemix help info
```

Visualizzare la guida per il comando `templates` sotto lo spazio dei nomi `catalog`:

```
bluemix catalog help templates
```


## bluemix api
Impostare o visualizzare l'endpoint API {{site.data.keyword.Bluemix_notm}}. Questo comando include il comando `cf api`.

```
bluemix api [ENDPOINT_API][--unset]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*ENDPOINT_API*  (facoltativo): l'endpoint API di destinazione, ad esempio https://api.ng.bluemix.net. Se non vengono specificate entrambe le opzioni *ENDPOINT_API* e `--unset`, viene visualizzato l'endpoint API corrente.

`--unset`  (facoltativo):  Rimuovere l'impostazione di endpoint API.

**Esempi**:

Impostare l'endpoint API su api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Visualizzare l'endpoint API corrente:

```
bluemix api```

Annullare l'impostazione dell'endpoint API:

```
bluemix api --unset
```


## bluemix login
Eseguire l'accesso dell'utente. Questo comando include il comando `cf login`.Le opzioni di comando sono le stesse del comando `cf login`.

```
bluemix login [OPZIONI...]
```

**Prerequisiti**:  Endpoint

**Opzioni del comando**:
Per informazioni sulle opzioni supportate dal comando `login`, vedi le informazioni sull'utilizzo del comando `cf login` per i comandi cf per la gestione delle applicazioni.


## bluemix logout
Disconnettere l'utente. Questo comando include il comando `cf logout`.

```
bluemix logout
```

**Prerequisiti**:  Nessuno


## bluemix target
Impostare o visualizzare l'organizzazione o lo spazio di destinazione. Questo comando include il comando `cf target`.

```
bluemix target [-o NOME_ORGANIZZAZIONE] [-s NOME_SPAZIO]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

-o *NOME_ORGANIZZAZIONE*  (facoltativo): il nome dell'organizzazione di destinazione.

-s *NOME_SPAZIO*  (facoltativo): il nome dello spazio di destinazione. 

Se non viene specificata né l'opzione -o *NOME_ORGANIZZAZIONE* né quella -s *NOME_SPAZIO*, vengono visualizzati l'organizzazione e lo spazio correnti.

**Esempi**:

Impostare l'organizzazione corrente su 'MyOrg' e lo spazio corrente su 'MySpace':

```
bluemix target -o MyOrg -s MySpace
```

Visualizzare l'organizzazione e lo spazio correnti:

```
bluemix target
```


## bluemix info
Visualizzare le informazioni su {{site.data.keyword.Bluemix_notm}} di base, compresi la regione corrente, la versione controller cloud e alcuni utili endpoint, quali gli endpoint per l'accesso e per lo scambio di token di accesso.

```
bluemix info
```

**Prerequisiti**:  Endpoint


## bluemix list
Elencare tutte le applicazioni cf e tutti i contenitori, i gruppi di contenitori e i gruppi di macchine virtuali nello spazio corrente.

```
bluemix list [applicazioni|contenitori|gruppi-contenitori|gruppi-macchinevirtuali]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

applicazioni  (facoltativo):  visualizzare solo le informazioni sulle applicazioni.

contenitori (facoltativo): visualizzare solo le informazioni sui contenitori.

gruppi-contenitori (facoltativo): visualizzare solo le informazioni sui gruppi di contenitori.

gruppi-macchinevirtuali (facoltativo): visualizzare solo le informazioni sui gruppi di macchine virtuali.

È possibile specificare solo uno di `applicazioni`, `contenitori`, `gruppi-contenitori` o `gruppi-macchinevirtuali` per volta. Se non viene specificata nessuna di tali opzioni, vengono elencati tutte le applicazioni cf e tutti i contenitori, i gruppi di contenitori e i gruppi di macchine virtuali.

**Esempi**:

Elencare tutte le applicazioni cf:

```
bluemix list apps
```

Elencare tutte le istanze contenitore:

```
bluemix list containers
```

Elencare tutte le applicazioni e tutti i contenitori, gruppi di contenitori e gruppi di macchine virtuali:

```
bluemix list
```


## bluemix scale
Ridimensionare in modo decrementale o incrementale l'applicazione cf o il gruppo di contenitori a un conteggio istanze, una quota disco o una dimensione memoria specifici.

**Nota:** È possibile specificare solo un numero istanze per il ridimensionamento di un gruppo di contenitori. Se non viene specificata alcuna opzione, questo comando elenca il conteggio istanze corrente per il gruppo di contenitori e anche la quota disco e la dimensione della memoria per l'applicazione cf.

```
bluemix scale NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI [-i CONTEGGIO_ISTANZE] [-k QUOTA_DISCO] [-m DIMENSIONE_MEMORIA]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI*  (obbligatorio): Il nome dell'applicazione cf o del gruppo di contenitori da ridimensionare.

-i *CONTEGGIO_ISTANZE*  (facoltativo):  il nuovo numero di istanze per l'applicazione cf o il gruppo di contenitori da ridimensionare. Questa opzione è la sola opzione valida per il gruppo di contenitori da ridimensionare.

-k *QUOTA_DISCO*  (facoltativo):  la nuova quota disco dell'applicazione cf. Non valido per ridimensionare un gruppo di contenitori.

-m *DIMENSIONE_MEMORIA*  (facoltativo):  la nuova dimensione della memoria per l'applicazione cf. Non valido per ridimensionare un gruppo di contenitori.

**Esempi**:

Visualizzare il numero istanze corrente per 'my-container-group':

```
bluemix scale my-container-group
```

Ridimensionare 'my-container-group' a 2 istanze:

```
bluemix scale my-container-group -i 2
```

Scalare 'my-java-app' a 3 istanze, 8G di quota disco e 1024M di dimensione della memoria:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Eseguire una richiesta HTTP raw per {{site.data.keyword.Bluemix_notm}}. Per impostazione predefinita, "Content-Type" è "application/json". Questo comando invia una richiesta al server della console {{site.data.keyword.Bluemix_notm}} (ad esempio https://console.ng.bluemix.net) invece che all'endpoint API cf (ad esempio https://api.ng.bluemix.net).

```
bluemix curl PERCORSO [OPZIONI...]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*PERCORSO*  (obbligatorio): il percorso URL della risorsa. Ad esempio, /rest/v2/apps.

*OPZIONI*  (facoltativo): le opzioni supportate dal comando `bluemix curl` sono le stesse del comando `cf curl`.

**Esempi**:

Richiamare le informazioni per tutti i template di contenitore tipo:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf orgs`.


## bluemix iam org
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf org`.


## bluemix iam org-create
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-org`.


## bluemix iam org-rename
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename-org`.


## bluemix iam org-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-org`.


## bluemix iam spaces
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf spaces`.


## bluemix iam space
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf space`.


## bluemix iam space-create
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-space`.


## bluemix iam space-rename
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename-space`.


## bluemix iam space-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-space`.


## bluemix iam user-create
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-user`.


## bluemix iam user-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-user`.


## bluemix iam org-users
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf org-users`.


## bluemix iam org-role-set
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf set-org-role`.


## bluemix iam org-role-unset
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf unset-org-role`.


## bluemix iam space-users
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf space-users`.


## bluemix iam space-role-set
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf set-space-role`.


## bluemix iam space-role-unset
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf unset-space-role`.


## bluemix catalog templates
Visualizzare i template di contenitore tipo su Bluemix.

```
bluemix catalog templates [-d]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

-d  (facoltativo):  se viene specificata l'opzione '-d', viene visualizzata anche la descrizione di ciascun template. Altrimenti, vengono visualizzati solo l'ID e il nome di ciascun template.


## bluemix catalog template-run
Creare un'applicazione cf basata sul template specificato con l'URL e la descrizione specificati. Per impostazione predefinita, la nuova applicazione viene avviata automaticamente.

```
bluemix catalog template-run ID_TEMPLATE MOME_APPLICAZIONE_CF [-u URL] [-d DESCRIZIONE] [--no-start]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*ID_TEMPLATE*  (obbligatorio): il template su cui verrà basata l'applicazione quando verrà creata. Utilizzare 'bluemix templates' per visualizzare l'ID di tutti i template.

*NOME_APPLICAZIONE_CF*  (obbligatorio): il nome dell'applicazione cf da creare.

-u *URL*  (facoltativo): la rotta dell'applicazione. Se non viene specificata, la rotta viene impostata da {{site.data.keyword.Bluemix_notm}} automaticamente in base ai tuoi nome applicazione e dominio predefinito.

-d *DESCRIZIONE*  (facoltativo): descrizione dell'applicazione.

--no-start  (facoltativo): non avviare l'applicazione automaticamente dopo la sua creazione. Se non viene specificata, l'applicazione viene avviata automaticamente dopo la sua creazione.

**Esempi**:

Creare un'applicazione cf 'my-app' basata sul template 'javaHelloWorld':

```
bluemix catalog template-run javaHelloWorld my-app
```

Creare un'applicazione 'my-ruby-app' basata sul template 'rubyHelloWorld' con la rotta 'myrubyapp.ng.bluemix.net' e la descrizione 'La mia prima applicazione ruby su {{site.data.keyword.Bluemix_notm}}.':

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "La mia prima applicazione ruby su {{site.data.keyword.Bluemix_notm}}."
```

Creare un'applicazione 'my-python-app' basata sul template 'pythonHelloWorld' senza l'avvio automatico:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Visualizzare le informazioni per tutte le regioni su {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

**Prerequisiti**:  Endpoint


## bluemix network region-set
Passare alla regione specificata. Questo comando ha automaticamente di nuovo come destinazione la stessa organizzazione e lo stesso spazio nella nuova regione, se possibile, altrimenti chiede all'utente di selezionare una nuova organizzazione e un nuovo spazio se l'utente è già collegato. L'endpoint API viene modificato di conseguenza.

```
bluemix network region-set NOME_REGIONE
```

**Prerequisiti**:  Endpoint

**Opzioni del comando**:

*NOME_REGIONE*  (obbligatorio):  il nome della regione a cui vuoi passare. Puoi utilizzare il comando `bluemix regions` per visualizzare tutti i nomi regione.

**Esempi**:

Impostare la regione corrente su 'eu-gb':

```
bluemix network region-set eu-gb
```


## bluemix network routes
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf routes`.


## bluemix network route-check
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf check-route`.


## bluemix network route-map
Associare una rotta a un'applicazione cf o a un gruppo di contenitori esistenti che hanno il dominio e il nome host specificati.

```
bluemix network route-map NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI  DOMINIO  [-n NOME_HOST]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI*  (obbligatorio): il nome dell'applicazione o del gruppo di contenitori da associare a una rotta.

*DOMINIO* (obbligatorio): il dominio della rotta. Ad esempio, mybluemix.net o ng.bluemix.net. 

-n *NOME_HOST*  (facoltativo): il nome host della rotta. Se non viene fornito, il nome host è impostato sul nome applicazione o sul nome gruppo di contenitori per impostazione predefinita.

**Esempi**:

Associare una rotta a 'my-app' con il dominio specificato:

```
bluemix network route-map my-app mybluemix.net
```

Associare una rotta a 'my-container-group' con il dominio e il nome host specificati:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Annullare l'associazione della rotta specificata a un'applicazione cf o a un gruppo di contenitori esistenti.

```
bluemix network route-unmap NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI  DOMINIO  [-n NOME_HOST]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI*  (obbligatorio): il nome dell'applicazione cf o del gruppo di contenitori.

*DOMINIO* (obbligatorio): il dominio della rotta (ad esempio, mybluemix.net o ng.bluemix.net). 

-n *NOME_HOST*  (facoltativo): il nome host della rotta. Se non viene fornito, il nome host è impostato sul nome applicazione o sul nome gruppo di contenitori per impostazione predefinita.

**Esempi**:

Annullare l'associazione di 'my-app.mybluemix.net' da 'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Annullare l'associazione di 'abc.ng.bluexmix.net' da 'my-container-group':

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-route`.


## bluemix network route-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-route`.


## bluemix network orphaned-routes-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-orphaned-routes`.


## bluemix network domains
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf domains`.


## bluemix network domain-create
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-domain`.


## bluemix network domain-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-domain`.


## bluemix network shared-domain-create
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-shared-domain`.


## bluemix network shared-domain-delete
Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-shared-domain`.


## bluemix plugin repos
Elencare i repository di plugin registrati nella CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos```

**Prerequisiti**:  Nessuno


## bluemix plugin repo-add
Aggiungere un nuovo repository di plugin alla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add NOME_REPOSITORY URL_REPOSITORY
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_REPOSITORY*  (obbligatorio): il nome del repository da aggiungere. Puoi definire un tuo nome per ciascun repository.

*URL_REPOSITORY*  (obbligatorio): l'URL del repository da aggiungere. L'URL del repository deve contenere il protocollo (ad esempio, http://plugins.ng.bluemix.net invece di plugins.ng.bluemix.net). http://plugins.ng.bluemix.net è il repository di plugin ufficiale della CLI {{site.data.keyword.Bluemix_notm}}.

**Esempi**:

Aggiungere il repository di plugin ufficiale della CLI Bluemix come 'bluemix-repo':

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Rimuovere un repository di plugin dalla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove NOME_REPOSITORY
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_REPOSITORY*  (obbligatorio): il nome del repository da rimuovere.

**Esempi**:

Rimuovere il repository 'bluemix-repo' dalla CLI {{site.data.keyword.Bluemix_notm}}:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Elencare tutti i plugin disponibili in tutti i repository aggiunti o in uno specifico repository.

```
bluemix plugin repo-plugin-list [-r NOME_REPOSITORY]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

-r *NOME_REPOSITORY*  (facoltativo): elencare solo i plugin nel repository specificato.

**Esempi**:

Elencare tutti i plugin in tutti i repository aggiunti:

```
bluemix plugin repo-plugin-list
```

Elencare tutti i plugin nel repository 'bluemix-repo':

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Elencare tutti i plugin installati nella CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

**Prerequisiti**:  Nessuno


## bluemix plugin install
Installare il plugin nella CLI in {{site.data.keyword.Bluemix_notm}} dal percorso o dal repository specificati.

```
bluemix plugin install PERCORSO_PLUGIN|NOME_PLUGIN [-r NOME_REPOSITORY]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*PERCORSO_PLUGIN*|*NOME_PLUGIN*  (obbligatorio):  se non viene specificato '-r *NOME_REPOSITORY*', il plugin viene installato dal percorso locale o dall'URL remoto specificati.

-r *NOME_REPOSITORY*  (facoltativo): il nome del repository dove si trova il file binario del plugin.

**Esempi**:

Installare un plugin dal file locale:

```
bluemix plugin install /downloads/new_plugin
```

Installare un plugin dall'URL remoto:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installare il plugin 'IBM-Containers' dal repository 'bluemix-repo':

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Disinstallare il plugin specificato dalla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall NOME_PLUGIN
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_PLUGIN*  (obbligatorio): il nome del plugin da disinstallare.

**Esempi**:

Disinstallare il plugin 'IBM-Containers' che era stato precedentemente installato:

```
bluemix plugin uninstall IBM-Containers
```
