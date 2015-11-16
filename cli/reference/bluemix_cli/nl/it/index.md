{:shortdesc: .shortdesc}

# comandi bluemix
{: #bluemix_cli}

*Ultimo aggiornamento: * 19 ottobre 2015

L'interfaccia riga di comando (CLI, command line interface) Bluemix fornisce una serie di comandi raggruppati in base allo spazio dei nomi per consentire agli utenti di interagire con Bluemix. Alcuni comandi CLI Bluemix incapsulano comandi cf esistenti e altri sono univoci per Bluemix. Le seguenti informazioni elencano tutti i comandi supportati dalla CLI Bluemix e ne includono i nomi, le opzioni, l'utilizzo, i prerequisiti, le descrizioni e gli esempi.
{:shortdesc}
 
**Nota:** I *Prerequisiti* elencano quali azioni sono richieste prima di utilizzare il comando. I comandi che non hanno alcuna azione prerequisita elencano **Nessuno**. Altrimenti, i prerequisiti possono includere una o più delle seguenti azioni:
<dl>
<dt>**Endpoint**</dt>
<dd>Un endpoint API deve essere impostato mediante la `api bluemix` prima di utilizzare il comando.</dd>
<dt>**Login**</dt>
<dd>Il login utilizzando il comando `bluemix login` è richiesto prima di utilizzare questo comando.</dd>
<dt>**Target**</dt>
<dd>Il comando `bluemix target` deve essere utilizzato per impostare un'organizzazione e uno spazio prima di utilizzare questo comando.</dd>
</dl>

## bluemix help
Visualizzare la guida generale per i comandi integrati di primo livello e gli spazi dei nomi supportati della CLI Bluemix oppure la guida per uno specifico spazio dei nomi o comando integrato.

```
bluemix help [COMANDO|SPAZIODEINOMI]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*COMANDO*|*SPAZIODEINOMI*  (facoltativo):  Il comando o lo spazio dei nomi per cui viene visualizzata la guida. In caso di mancata specifica, viene visualizzata la guida generale per la CLI Bluemix.

**Esempi**:

Visualizzare la guida generale per la CLI Bluemix:

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

Visualizzare la guida per il comando `templates` nello spazio dei nomi `catalog`:

```
bluemix catalog help templates
```


## bluemix api
Impostare o visualizzare l'endpoint API Bluemix. Questo comando incapsula il comando `cf api`.

```
bluemix api [ENDPOINT_API][--unset]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*ENDPOINT_API*  (facoltativo):  l'endpoint API di destinazione, ad esempio https://api.ng.bluemix.net. Se non vengono specificate né l'opzione *ENDPOINT_API* né quella `–unset`, viene visualizzato l'endpoint API corrente.

`--unset`  (facoltativo): rimuovere l'impostazione dell'endpoint API.

**Esempi**:

Impostare l'endpoint API su api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Visualizzare l'endpoint API corrente:

```
bluemix api
```

Annullare l'impostazione dell'endpoint API:

```
bluemix api --unset
```


## bluemix login
Eseguire il login dell'utente. Questo comando incapsula il comando `cf login`. Le opzioni di comando sono le stesse opzioni di comando di `cf login`.

```
bluemix login [OPZIONI...]
```

**Prerequisiti**:  Endpoint

**Opzioni di comando**:
Per informazioni sulle opzioni supportate dal comando `login`, consulta le informazioni sull'utilizzo del comando `cf login` per i comandi cf per gestire le applicazioni.


## bluemix logout
Eseguire il logout dell'utente. Questo comando incapsula il comando `cf logout`.

```
bluemix logout
```

**Prerequisiti**:  Nessuno


## bluemix target
Impostare o visualizzare l'organizzazione o lo spazio di destinazione. Questo comando incapsula il comando `cf target`. 

```
bluemix target [-o NOME_ORGANIZZAZIONE] [-s NOME_SPAZIO]
```

**Prerequisiti**:  Endpoint, Login

**Opzioni del comando**:

-o *NOME_ORGANIZZAZIONE*  (facoltativo): il nome dell'organizzazione di destinazione.

-s *NOME_SPAZIO*  (facoltativo): il nome dello spazio di destinazione.

Se non viene specificato né -o *NOME_ORGANIZZAZIONE* né -s *NOME_SPAZIO*, vengono visualizzati l'organizzazione e lo spazio correnti.

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
Visualizzare le informazioni Bluemix di base, compresa la regione corrente, la versione controller cloud e alcuni utili endpoint, come gli endpoint per il login e per lo scambio di token di accesso.

```
bluemix info
```

**Prerequisiti**:  Endpoint


## bluemix list
Elencare tutte le applicazioni cf e tutti i contenitori, i gruppi di contenitori e i gruppi di VM nello spazio corrente.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Prerequisiti**:  Endpoint, Login, Target

**Opzioni del comando**:

apps  (facoltativo):  visualizzare solo le informazioni sulle applicazioni.

containers  (facoltativo): visualizzare solo le informazioni sui contenitori.

container-groups  (facoltativo):  visualizzare solo le informazioni sui gruppi di contenitori.

vm-groups  (facoltativo):  visualizzare solo le informazioni sui gruppi di VM.

Può essere specificata solo una delle opzioni `apps`, `containers`, `container-groups` o `vm-groups` per volta. Se non viene specificata nessuna di esse, vengono elencate tutte le applicazioni cf e tutti i contenitori, i gruppi di contenitori e i gruppi di VM.

**Esempi**:

Elencare tutte le applicazioni cf:

```
bluemix list apps
```

Elencare tutte le istanze contenitore:

```
bluemix list containers
```

Elencare tutte le applicazioni e tutti i contenitori, i gruppi di contenitori e i gruppi di VM:

```
bluemix list
```


## bluemix scale
Ridimensionare in modo decrementale o incrementale l'applicazione cf o il gruppo di contenitori a un conteggio istanze, una quota disco e una dimensione della memoria specifici.

**Nota:** per il ridimensionamento di un gruppo di contenitori può essere specificato solo un numero istanze. Se non viene specificata alcuna opzione, questo comando elenca il conteggio istanze corrente per il gruppo di contenitori e anche la quota disco e la dimensione della memoria per l'applicazione cf.

```
bluemix scale NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI [-i CONTEGGIO_ISTANZE] [-k QUOTA_DISCO] [-m DIMENSIONE_MEMORIA]
```

**Prerequisiti**:  Endpoint, Login, Target

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI*  (obbligatorio):  il nome dell'applicazione cf o del gruppo di contenitori da ridimensionare.

-i *CONTEGGIO_ISTANZE*  (facoltativo):  il nuovo numero istanze per l'applicazione cf o il gruppo di contenitori da ridimensionare. Questa opzione è la sola opzione valida per il gruppo di contenitori da ridimensionare.

-k *QUOTA_DISCO*  (facoltativo):  la nuova quota disco dell'applicazione cf. Non valido per il ridimensionamento di un gruppo di contenitori.

-m *DIMENSIONE_MEMORIA*  (facoltativo):  la nuova dimensione memoria per l'applicazione cf. Non valido per il ridimensionamento di un gruppo di contenitori.

**Esempi**:

Visualizzare il numero istanze corrente per 'my-container-group':

```
bluemix scale my-container-group
```

Ridimensionare 'my-container-group' a 2 istanze:

```
bluemix scale my-container-group -i 2
```

Ridimensionare 'my-java-app' a 3 istanze, 8G di quota disco e 1024M di dimensione memoria:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Eseguire una richiesta HTTP raw a Bluemix. "Content-Type" è, per impostazione predefinita, "application/json". Questo comando invia una richiesta al server di console Bluemix (ad esempio, https://console.ng.bluemix.net) invece che all'endpoint API cf (ad esempio, https://api.ng.bluemix.net).

```
bluemix curl PERCORSO [OPZIONI...]
```

**Prerequisiti**:  Endpoint, Login

**Opzioni del comando**:

*PERCORSO*  (obbligatorio):  il percorso URL della risorsa. Ad esempio, /rest/v2/apps.

*OPZIONI*  (facoltativo):  le opzioni supportate dal comando `bluemix curl` sono le stesse del comando `cf curl`.

**Esempi**:

Recuperare le informazioni per tutti i template di contenitore tipo.

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

**Prerequisiti**:  Endpoint, Login

**Opzioni del comando**:

-d  (facoltativo):  se viene specificata l'opzione '-d', viene visualizzata anche la descrizione di ciascun template. Altrimenti, vengono visualizzati solo l'ID e il nome di ciascun template.


## bluemix catalog template-run
Creare un'applicazione cf basata sul template specificato con l'URL e la descrizione specificati. Per impostazione predefinita, la nuova applicazione viene avviata automaticamente.

```
bluemix catalog template-run ID_TEMPLATE NOME_APPLICAZIONE_CF [-u URL] [-d DESCRIZIONE] [--no-start]
```

**Prerequisiti**:  Endpoint, Login, Target

**Opzioni del comando**:

*ID_TEMPLATE*  (obbligatorio):  il template su cui sarà basata l'applicazione quando verrà creata. Utilizzare 'bluemix templates' per visualizzare l'ID di tutti i template.

*NOME_APPLICAZIONE_CF*  (obbligatorio):  il nome dell'applicazione cf da creare.

-u *URL*  (facoltativo):  l'instradamento dell'applicazione. Se questa opzione non viene specificata, l'instradamento viene impostato da Bluemix automaticamente sulla base del nome della tua applicazione e del dominio facoltativo.

-d *DESCRIZIONE*  (facoltativo):  la descrizione dell'applicazione.

--no-start  (facoltativo): non avviare l'applicazione automaticamente dopo che è stata creata. Se questa opzione non viene specificata, l'applicazione viene avviata automaticamente dopo essere stata creata.

**Esempi**:

Creare un'applicazione cf 'my-app' basata sul template 'javaHelloWorld':

```
bluemix catalog template-run javaHelloWorld my-app
```

Creare un'applicazione 'my-ruby-app' basata sul template 'rubyHelloWorld' con l'instradamento 'myrubyapp.ng.bluemix.net' e la descrizione 'La mia prima applicazione ruby su Bluemix.':

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "La mia prima applicazione ruby su Bluemix."
```

Creare un'applicazione 'my-python-app' basata sul template 'pythonHelloWorld' senza l'avvio automatico:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Visualizzare le informazioni per tutte le regioni su Bluemix.

```
bluemix network regions
```

**Prerequisiti**:  Endpoint


## bluemix network region-set
Passare alla regione specificata. Questo comando reindirizza automaticamente alla stessa organizzazione e allo stesso spazio nella nuova regione, se possibile, oppure richiede all'utente di selezionare una nuova organizzazione e un nuovo spazio, se l'utente è già collegato. L'endpoint API viene modificato di conseguenza.

```
bluemix network region-set NOME_REGIONE
```

**Prerequisiti**:  Endpoint

**Opzioni del comando**:

*NOME_REGIONE*  (obbligatorio):  il nome della regione alla quale si vuole passare. Puoi utilizzare il comando `bluemix regions` per visualizzare tutti i nomi regione.

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
Associare un instradamento a un'applicazione cf o a un gruppo di contenitori esistenti che hanno il dominio e il nome host specificati.

```
bluemix network route-map NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI  DOMINIO  [-n NOME_HOST]
```

**Prerequisiti**:  Endpoint, Login, Target

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI*  (obbligatorio): il nome dell'applicazione cf o del gruppo di contenitori da associare a un instradamento.

*DOMINIO*  (obbligatorio): il dominio dell'instradamento. Ad esempio, mybluemix.net o ng.bluemix.net. 

-n *NOME_HOST*  (facoltativo): il nome host dell'instradamento. Se non viene fornito, il nome host viene impostato sul nome dell'applicazione o sul nome del gruppo di contenitori per impostazione predefinita.

**Esempi**:

Associare un instradamento a 'my-app' con il dominio specificato:

```
bluemix network route-map my-app mybluemix.net
```

Associare un instradamento a 'my-container-group' con il dominio e il nome host specificati:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Annullare l'associazione dell'instradamento specificato a un'applicazione cf o a un gruppo di contenitori esistenti.

```
bluemix network route-unmap NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI  DOMINIO  [-n NOME_HOST]
```

**Prerequisiti**:  Endpoint, Login, Target

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI*  (obbligatorio): il nome dell'applicazione cf o del gruppo di contenitori.

*DOMINIO*  (obbligatorio): il dominio dell'instradamento (ad esempio, mybluemix.net o ng.bluemix.net). 

-n *NOME_HOST*  (facoltativo): il nome host dell'instradamento. Se non viene fornito, il nome host viene impostato sul nome dell'applicazione o sul nome del gruppo di contenitori per impostazione predefinita.

**Esempi**:

Annullare l'associazione di 'my-app.mybluemix.net' a 'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Annullare l'associazione di 'abc.ng.bluexmix.net' a 'my-container-group':

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
Elencare tutti i repository di plugin registrati nella CLI Bluemix.

```
bluemix plugin repos
```

**Prerequisiti**:  Nessuno


## bluemix plugin repo-add
Aggiungere un nuovo repository di plugin alla CLI Bluemix.

```
bluemix plugin repo-add NOME_REPOSITORY URL_REPOSITORY
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_REPOSITORY*  (obbligatorio): il nome del repository da aggiungere. Puoi definire un tuo nome per ciascun repository.

*URL_REPOSITORY*  (obbligatorio): l'URL del repository da aggiungere. L'URL del repository deve contenere il protocollo (ad esempio, http://plugins.ng.bluemix.net invece di plugins.ng.bluemix.net). http://plugins.ng.bluemix.net è il repository di plugin ufficiale della CLI Bluemix.

**Esempi**:

Aggiungere il repository di plugin ufficiale della CLI Bluemix come 'bluemix-repo':

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Rimuovere un repository di plugin dalla CLI Bluemix.

```
bluemix plugin repo-remove NOME_REPOSITORY
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_REPOSITORY*  (obbligatorio):  il nome del repository da rimuovere.

**Esempi**:

Rimuovere il repository 'bluemix-repo' dalla CLI Bluemix:

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

-r *NOME_REPOSITORY*  (facoltativo):  elencare solo i plugin nel repository specificato.

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
Elencare tutti i plugin installati nella CLI Bluemix.

```
bluemix plugin list
```

**Prerequisiti**:  Nessuno


## bluemix plugin install
Installare il plugin per la CLI Bluemix dal percorso o dal repository specificati.

```
bluemix plugin install PERCORSO_PLUGIN|NOME_PLUGIN [-r NOME_REPOSITORY]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*PERCORSO_PLUGIN*|*NOME_PLUGIN*  (obbligatorio):  se non viene specificato '-r *NOME_REPOSITORY*', il plugin viene installato dal percorso locale o dall'URL remoto specificati.

-r *NOME_REPOSITORY*  (facoltativo): il nome dl repository dove si trova il binario del plugin.

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
Disinstallare il plugin specificato dalla CLI Bluemix.

```
bluemix plugin uninstall NOME_PLUGIN
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_PLUGIN*  (obbligatorio): il nome del plugin da disinstallare.

**Esempi**:

Disinstallare il plugin 'IBM-Containers' che era stato installato precedentemente:

```
bluemix plugin uninstall IBM-Containers
```
