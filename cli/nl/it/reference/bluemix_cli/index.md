---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Comandi {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

*Ultimo aggiornamento: 15 aprile 2016*

L'interfaccia di riga comando (CLI) {{site.data.keyword.Bluemix_notm}} fornisce una serie di comandi che vengono raggruppati in base allo spazio dei nomi per consentire agli utenti di interagire con {{site.data.keyword.Bluemix_notm}}. Alcuni comandi {{site.data.keyword.Bluemix_notm}} incapsulano comandi cf esistenti, mentre altri forniscono funzionalità estese agli utenti {{site.data.keyword.Bluemix_notm}}. Le informazioni qui di seguito elencano tutti i comandi supportati dalla CLI {{site.data.keyword.Bluemix_notm}} e includono i relativi nomi, opzioni, utilizzo, prerequisiti, descrizioni ed esempi.
{:shortdesc}
 
**Nota:** i *Prerequisiti* elencano quali azioni sono richieste prima di utilizzare il comando. I comandi che non hanno azioni prerequisite elencano **Nessuno**. Altrimenti, i prerequisiti possono includere una o più delle seguenti azioni:
<dl>
<dt>Endpoint</dt>
<dd>Un endpoint API deve essere impostato mediante <code>bluemix api</code> prima di utilizzare il comando.</dd>
<dt>Accesso</dt>
<dd>L'accesso utilizzando il comando <code>bluemix login</code> è richiesto prima di utilizzare questo comando.</dd>
<dt>Destinazione</dt>
<dd>Il comando <code>bluemix target</code> deve essere utilizzato per impostare un'organizzazione e uno spazio prima di utilizzare questo comando.</dd>
<dt>Docker</dt>
<dd>Per poter eseguire questo comando, è necessario che la CLI Docker (docker) sia installata.</dd>
</dl>

Puoi utilizzare i seguenti comandi {{site.data.keyword.Bluemix_notm}}:

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
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

Visualizzare la guida per il comando `info`:

```
bluemix help info
```

Visualizzare la guida per lo spazio dei nomi `ic`:

```
bluemix help ic
```

o 

```
bluemix ic help
```

Visualizzare la guida per il comando `group-create` sotto lo spazio dei nomi `ic`:

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
Impostare o visualizzare l'endpoint API {{site.data.keyword.Bluemix_notm}}. Questo comando include il comando `cf api`.

```
bluemix api [ENDPOINT_API][--unset]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*ENDPOINT_API*  (facoltativo): l'endpoint API di destinazione, ad esempio https://api.ng.bluemix.net.  Se non vengono specificate entrambe le opzioni *ENDPOINT_API* e `--unset`, viene visualizzato l'endpoint API corrente.

`--unset` (facoltativo): rimuovere l'impostazione di endpoint API.

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
{: #bluemix_login}

Eseguire l'accesso dell'utente. Questo comando include il comando `cf login`. Le opzioni di comando sono le stesse del comando `cf login`.

```
bluemix login [OPZIONI...]
```

**Prerequisiti**:  Endpoint

**Opzioni del comando**:
Per informazioni sulle opzioni supportate dal comando `login`, vedi le informazioni sull'utilizzo del comando `cf login` per i comandi cf per la gestione delle applicazioni.


## bluemix logout
{: #bluemix_logout}

Disconnettere l'utente. Questo comando include il comando `cf logout`.

```
bluemix logout
```

**Prerequisiti**:  Nessuno


## bluemix target
{: #bluemix_target}


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

Impostare l'organizzazione corrente su `MyOrg` e lo spazio su `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

Visualizzare l'organizzazione e lo spazio correnti:

```
bluemix target
```


## bluemix info
{: #bluemix_info}

Visualizzare le informazioni su {{site.data.keyword.Bluemix_notm}} di base, compresi la regione corrente, la versione controller cloud e alcuni utili endpoint, quali gli endpoint per l'accesso e per lo scambio di token di accesso.

```
bluemix info
```

**Prerequisiti**:  Endpoint


## bluemix config
{: #bluemix_config}


Scrivere i valori predefiniti nel file di configurazione.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

--http-timeout *TIMEOUT_IN_SECONDS*:  il valore di timeout per le richieste HTTP. Il valore predefinito è 60 secondi.

--trace true|false|*path/to/file*:  traccia le richieste HTTP nel terminale o file specificato.

--color true|false:  abilita o disabilita l'output a colori. L'output a colori è abilitato per impostazione predefinita.

--locale *LOCALE*:  imposta una locale predefinita. Se LOCALE è *CLEAR*, la locale precedente viene eliminata.

È possibile specificare solo una di queste opzioni alla volta.

**Esempi**:

Impostare il timeout della richiesta HTTP su 30 secondi:

```
bluemix config --http-timeout 30
```

Abilitare l'output di traccia per le richieste HTTP:

```
bluemix config --trace true
```

Tracciare le richieste HTTP in un file specificato */home/usera/my_trace*:

```
bluemix config --trace /home/usera/my_trace
```

Disabilitare l'output a colori:

```
bluemix config --color false
```

Impostare la locale su zh_Hans:

```
bluemix config --locale zh_Hans
```

Cancellare le impostazioni della locale:

```
bluemix config --locale CLEAR
```


## bluemix list
{: #bluemix_list}

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
{: #bluemix_scale}

Ridimensionare in modo decrementale o incrementale l'applicazione cf o il gruppo di contenitori a un conteggio istanze, una quota disco o una dimensione memoria specifici.

**Nota:** è possibile specificare solo un numero di istanze per il ridimensionamento di un gruppo di contenitori. Se non viene specificata alcuna opzione, questo comando elenca il conteggio istanze corrente per il gruppo di contenitori e anche la quota disco e la dimensione della memoria per l'applicazione cf.

```
bluemix scale NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORI [-i CONTEGGIO_ISTANZE][-k DISK_QUOTA] [-m DIMENSIONE_MEMORIA]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_APPLICAZIONE_CF*|*NOME_GRUPPO_CONTENITORI* (obbligatorio):  il nome dell'applicazione cf o del gruppo di contenitori da ridimensionare.

-i *CONTEGGIO_ISTANZE*  (facoltativo):  il nuovo numero di istanze per l'applicazione cf o il gruppo di contenitori da ridimensionare. Questa opzione è la sola opzione valida per il gruppo di contenitori da ridimensionare.

-k *QUOTA_DISCO* (facoltativo):  la nuova quota disco dell'applicazione cf. Non valido per ridimensionare un gruppo di contenitori.

-m *DIMENSIONE_MEMORIA* (facoltativo):  la nuova dimensione della memoria per l'applicazione cf. Non valido per ridimensionare un gruppo di contenitori.

**Esempi**:

Visualizzare il numero istanze corrente per `my-container-group`:

```
bluemix scale my-container-group
```

Ridimensionare `my-container-group` a 2 istanze:

```
bluemix scale my-container-group -i 2
```

Ridimensionare `my-java-app` a 3 istanze, 8G di quota disco e 1024M di dimensione della memoria:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

Eseguire una richiesta HTTP raw per {{site.data.keyword.Bluemix_notm}}. *Content-Type* è impostato su *application/json* come valore predefinito. Questo comando invia la richiesta al MCCP (Multi Cloud Control Proxy) {{site.data.keyword.Bluemix_notm}}. Per i percorsi supportati, fai riferimento alle definizioni del percorso API nella [Documentazione API CloudFoundry](http://apidocs.cloudfoundry.org/){: new_window}.

```
bluemix curl PERCORSO [OPZIONI...]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*PERCORSO*  (obbligatorio): il percorso URL della risorsa. Ad esempio, /v2/apps.

*OPZIONI*  (facoltativo): le opzioni supportate dal comando `bluemix curl` sono le stesse del comando `cf curl`.

**Esempi**:

Visualizzare le informazioni per tutte le organizzazioni dell'account corrente:

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

Elencare tutte le organizzazioni

```
bluemix iam orgs [-r REGION --guid]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*-r REGION*  (facoltativo): per la regione per cui sono visualizzate le informazioni. Se impostato su 'all', vengono elencate tutte le organizzazioni in tutte le regioni.

*--guid* (facoltativo): visualizza il GUID delle organizzazioni.

**Esempi**:
Elencare tutte le organizzazioni nella regione: `us-south` con il GUID visualizzato

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

Visualizzare le informazioni per l'organizzazione specificata.

```
bluemix iam org ORG_NAME [--guid]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*ORG_NAME* (obbligatorio): il nome dell'organizzazione.

*--guid* (facoltativo): visualizza il GUID dell'organizzazione.


**Esempi**:
Visualizzare le informazioni dell'organizzazione `IBM` con il GUID visualizzato

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

Creare una nuova organizzazione. Questa operazione può essere eseguita solo dal proprietario dell'account.

```
bluemix iam org-create ORG_NAME
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*ORG_NAME* (obbligatorio): il nome dell'organizzazione che sta venendo creata.

**Esempi**:
Creare un'organizzazione denominata `IBM`.

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replicare un'organizzazione dalla regione corrente in un'altra regione.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*NOME_ORGANIZZAZIONE* (obbligatorio):  il nome dell'organizzazione esistente che deve essere replicata.

*NOME_REGIONE*  (obbligatorio):  il nome della regione che ospita l'organizzazione replicata.

**Esempi**:

Replicare l'organizzazione `myorg` nella regione `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Ridenominare un'organizzazione. Questa operazione può essere eseguita solo da un gestore organizzazione.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*OLD_ORG_NAME* (obbligatorio):  il nome precedente dell'organizzazione che sta venendo ridenominata.

*NEW_ORG_NAME*  (obbligatorio):  il nuovo nome con cui è stata ridenominata l'organizzazione.


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Eliminare l'organizzazione specificata nella regione corrente.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*ORG_NAME* (obbligatorio):  il nome dell'organizzazione esistente che deve essere eliminata.

*-f* (facoltativo):  forza l'eliminazione senza conferma.

*--all* (facoltativo): elimina l'organizzazione da tutte le regioni.


## bluemix iam spaces
{: #bluemix_iam_spaces}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf spaces`.


## bluemix iam space
{: #bluemix_iam_space}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf space`.


## bluemix iam space-create
{: #bluemix_iam_space_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-space`.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename-space`.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-space`.


## bluemix iam account-users
{: #bluemix_iam_account_users}

Visualizza gli utenti associati con l'account. Questa operazione può essere eseguita solo dal proprietario dell'account.

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


Invita un utente nell'account con un'organizzazione e un ruolo spazio già impostati. Questa operazione può essere eseguita solo dal proprietario dell'account.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**Prerequisiti**:  Endpoint, Accesso


**Opzioni del comando**:

*USER_NAME* (obbligatorio): il nome dell'utente che sta venendo invitato.

*ORG_NAME* (obbligatorio): il nome dell'organizzazione in cui questo utente è stato invitato.

*ORG_ROLE* (obbligatorio): il nome del ruolo dell'organizzazione in cui questo utente è stato invitato. Ad esempio:

<dl>
<dt>OrgManager</dt>
<dd>Questo ruolo può invitare e gestire gli utenti, selezionare e modificare i piani e impostare i limiti di spesa.</dd>
<dt>BillingManager</dt>
<dd>Questo ruolo può creare e gestire l'account di fatturazione e le informazioni di pagamento.</dd>
<dt>OrgAuditor</dt>
<dd>Questo ruolo ha accesso di sola lettura alle informazioni e ai report dell'organizzazione.</dd>
</dl> 

*SPACE_NAME* (obbligatorio): il nome dello spazio in cui questo utente è stato invitato.

*SPACE_ROLE* (obbligatorio): il nome del ruolo dello spazio in cui questo utente è stato invitato. Ad esempio:

<dl>
<dt>SpaceManager</dt>
<dd>Questo ruolo può invitare e gestire gli utenti e abilitare le funzioni per lo spazio fornito.</dd>
<dt>SpaceDeveloper</dt>
<dd>Questo ruolo può creare e gestire le applicazioni e i servizi e visualizzare i log e i report.</dd>
<dt>SpaceAuditor</dt>
<dd>Questo ruolo può visualizzare i log, i report e le impostazioni per lo spazio.</dd>
</dl> 

**Esempi**:

Invitare l'utente `Mary` nell'organizzazione `IBM` con il ruolo `OrgManager` e lo spazio `Cloud` con il ruolo `SpaceAuditor`:

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

Visualizzare gli utenti nell'organizzazione specificata per il ruolo.

```
bluemix iam org-users ORG_NAME [-a]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*ORG_NAME* (obbligatorio): il nome dell'organizzazione.

*-a* (facoltativo): elenca tutti gli utenti nell'organizzazione specificata, non raggruppati per ruolo.


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Assegnare un ruolo dell'organizzazione ad un utente. Questa operazione può essere eseguita solo da un gestore organizzazione.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*USER_NAME* (obbligatorio): il nome dell'utente che sta venendo assegnato.

*ORG_NAME* (obbligatorio): il nome dell'organizzazione in cui questo utente è stato assegnato.

*ORG_ROLE* (obbligatorio): il nome del ruolo dell'organizzazione in cui questo utente è stato assegnato. Ad esempio:

<dl>
<dt>OrgManager</dt>
<dd>Questo ruolo può invitare e gestire gli utenti, selezionare e modificare i piani e impostare i limiti di spesa.</dd>
<dt>BillingManager</dt>
<dd>Questo ruolo può creare e gestire l'account di fatturazione e le informazioni di pagamento.</dd>
<dt>OrgAuditor</dt>
<dd>Questo ruolo ha accesso di sola lettura alle informazioni e ai report dell'organizzazione.</dd>
</dl> 

**Esempi**:

Assegnare l'utente `Mary` all'organizzazione `IBM` con il ruolo `OrgManager`:

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Rimuovere un ruolo dell'organizzazione da un utente. Questa operazione può essere eseguita solo da un gestore organizzazione.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*USER_NAME* (obbligatorio): il nome dell'utente che sta venendo rimosso.

*ORG_NAME* (obbligatorio): il nome dell'organizzazione da cui questo utente è stato rimosso.

*ORG_ROLE* (obbligatorio): il nome del ruolo dell'organizzazione da cui questo utente è stato rimosso. Ad esempio:

<dl>
<dt>OrgManager</dt>
<dd>Questo ruolo può invitare e gestire gli utenti, selezionare e modificare i piani e impostare i limiti di spesa.</dd>
<dt>BillingManager</dt>
<dd>Questo ruolo può creare e gestire l'account di fatturazione e le informazioni di pagamento.</dd>
<dt>OrgAuditor</dt>
<dd>Questo ruolo ha accesso di sola lettura alle informazioni e ai report dell'organizzazione.</dd>
</dl> 

**Esempi**:

Rimuovere l'utente `Mary` dall'organizzazione `IBM` con il ruolo `OrgManager`:

```
bluemix iam org-role-unset Mary IBM OrgManager
```


## bluemix iam space-users
{: #bluemix_iam_space_users}

Visualizzare gli utenti nello spazio specificato per il ruolo.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*ORG_NAME* (obbligatorio): il nome dell'organizzazione

*SPACE_NAME* (obbligatorio): il nome dello spazio.


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Assegnare un ruolo dello spazio ad un utente. Questa operazione può essere eseguita solo da un gestore spazio.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*USER_NAME* (obbligatorio): il nome dell'utente che sta venendo assegnato.

*ORG_NAME* (obbligatorio): il nome dell'organizzazione in cui questo utente è stato assegnato.

*SPACE_NAME* (obbligatorio): il nome dello spazio in cui questo utente è stato assegnato.

*SPACE_ROLE* (obbligatorio): il nome del ruolo dello spazio in cui questo utente è stato assegnato. Ad esempio:

<dl>
<dt>SpaceManager</dt>
<dd>Questo ruolo può invitare e gestire gli utenti e abilitare le funzioni per lo spazio fornito.</dd>
<dt>SpaceDeveloper</dt>
<dd>Questo ruolo può creare e gestire le applicazioni e i servizi e visualizzare i log e i report.</dd>
<dt>SpaceAuditor</dt>
<dd>Questo ruolo può visualizzare i log, i report e le impostazioni per lo spazio.</dd>
</dl> 


**Esempi**:

Assegnare l'utente `Mary` all'organizzazione `IBM` e allo spazio `Cloud` con il ruolo `SpaceManager`:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Rimuovere un ruolo dello spazio da un utente. Questa operazione può essere eseguita solo da un gestore spazio.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*USER_NAME* (obbligatorio): il nome dell'utente che sta venendo rimosso.

*ORG_NAME* (obbligatorio): il nome dell'organizzazione da cui questo utente è stato rimosso.

*SPACE_NAME* (obbligatorio): il nome dello spazio da cui questo utente è stato rimosso.

*SPACE_ROLE* (obbligatorio): il nome del ruolo dello spazio da cui questo utente è stato rimosso. Ad esempio:

<dl>
<dt>SpaceManager</dt>
<dd>Questo ruolo può invitare e gestire gli utenti e abilitare le funzioni per lo spazio fornito.</dd>
<dt>SpaceDeveloper</dt>
<dd>Questo ruolo può creare e gestire le applicazioni e i servizi e visualizzare i log e i report.</dd>
<dt>SpaceAuditor</dt>
<dd>Questo ruolo può visualizzare i log, i report e le impostazioni per lo spazio.</dd>
</dl> 

**Esempi**:

Rimuovere l'utente `Mary` dall'organizzazione `IBM` e dall spazio `Cloud` con il ruolo `SpaceManager`:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf push`.


## bluemix app list
{: #bluemix_app_list}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf app`.


## bluemix app scale
{: #bluemix_app_scale}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf scale`.


## bluemix app delete
{: #bluemix_app_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete`.


## bluemix app rename
{: #bluemix_app_rename}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename`.


## bluemix app start
{: #bluemix_app_start}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf start`.


## bluemix app stop
{: #bluemix_app_stop}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf stop`.


## bluemix app restart
{: #bluemix_app_restart}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf restart`.


## bluemix app restage
{: #bluemix_app_restage}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf restage`.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf restart-app-instance`.


## bluemix app events
{: #bluemix_app_events}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf events`.


## bluemix app files
{: #bluemix_app_files}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf files`.


## bluemix app logs
{: #bluemix_app_logs}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf logs`.


## bluemix app env
{: #bluemix_app_env}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf env`.


## bluemix app env-set
{: #bluemix_app_env_set}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf set-env`.


## bluemix app env-unset
{: #bluemix_app_env_unset}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf unset-env`.


## bluemix app stacks
{: #bluemix_app_stacks}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf stacks`.


## bluemix app stack
{: #bluemix_app_stack}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-app-manifest`.


## bluemix service offerings
{: #bluemix_service_offerings}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf marketplace`.


## bluemix service list
{: #bluemix_service_list}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf services`.


## bluemix service show
{: #bluemix_service_show}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf service`.


## bluemix service create
{: #bluemix_service_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-service`.


## bluemix service update
{: #bluemix_service_update}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf update-service`.


## bluemix service delete
{: #bluemix_service_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-service`.


## bluemix service rename
{: #bluemix_service_rename}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename-service`.


## bluemix service bind
{: #bluemix_service_bind}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf bind-service`.


## bluemix service unbind
{: #bluemix_service_unbind}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf unbind-service`.


## bluemix service key-create
{: #bluemix_service_key_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-service-key`.


## bluemix service key-delete
{: #bluemix_service_key_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-service-key`.


## bluemix service keys
{: #bluemix_service_keys}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf service-keys`.


## bluemix service key-show
{: #bluemix_service_key_show}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf service-key`.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-user-provided-service`.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf update-user-provided-service`.


## bluemix catalog templates
{: #bluemix_catalog_templates}

Visualizzare i template di contenitore tipo su Bluemix.

```
bluemix catalog templates [-d]
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

-d (facoltativo):  se viene specificata l'opzione `-d`, viene visualizzata anche la descrizione di ciascun template. Altrimenti, vengono visualizzati solo l'ID e il nome di ciascun template.


## bluemix catalog template
{: #bluemix_catalog_template}

Visualizzare le informazioni dettagliate di un template contenitore tipo specificato.

```
bluemix catalog template TEMPLATE_ID
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*ID_TEMPLATE* (obbligatorio):  l'ID del template contenitore tipo. Utilizza 'bluemix templates' per visualizzare gli ID di tutti i template.

**Esempi**:

Visualizzare i dettagli del template `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

Creare un'applicazione cf basata sul template specificato con l'URL e la descrizione specificati. Per impostazione predefinita, la nuova applicazione viene avviata automaticamente.

```
bluemix catalog template-run ID_TEMPLATE MOME_APPLICAZIONE_CF [-u URL] [-d DESCRIZIONE] [--no-start]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*ID_TEMPLATE*  (obbligatorio): il template su cui verrà basata l'applicazione quando verrà creata. Utilizza `bluemix templates` per visualizzare l'ID di tutti i template.

*NOME_APPLICAZIONE_CF*  (obbligatorio): il nome dell'applicazione cf da creare.

-u *URL*  (facoltativo): la rotta dell'applicazione. Se non viene specificata, la rotta viene impostata da {{site.data.keyword.Bluemix_notm}} automaticamente in base ai tuoi nome applicazione e dominio predefinito.

-d *DESCRIZIONE*  (facoltativo): descrizione dell'applicazione.

--no-start  (facoltativo): non avviare l'applicazione automaticamente dopo la sua creazione. Se non viene specificata, l'applicazione viene avviata automaticamente dopo la sua creazione.

**Esempi**:

Creare un'applicazione `my-app` basata sul template `javaHelloWorld`:

```
bluemix catalog template-run javaHelloWorld my-app
```

Creare un'applicazione `my-ruby-app` basata sul template `rubyHelloWorld` con la rotta `myrubyapp.ng.bluemix.net` e la descrizione `La mia prima applicazione ruby su {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "La mia prima applicazione ruby su {{site.data.keyword.Bluemix_notm}}."
```

Creare un'applicazione `my-python-app` basata sul template `pythonHelloWorld` senza l'avvio automatico:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

Visualizzare le informazioni per tutte le regioni su {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

**Prerequisiti**:  Endpoint


## bluemix network region-set
{: #bluemix_network_region_set}

Passare alla regione specificata. Questo comando ha automaticamente di nuovo come destinazione la stessa organizzazione e lo stesso spazio nella nuova regione, se possibile. Altrimenti, il comando richiede all'utente di selezionare una nuova organizzazione e un nuovo spazio, qualora l'utente sia già collegato. L'endpoint API viene modificato di conseguenza.

```
bluemix network region-set NOME_REGIONE
```

**Prerequisiti**:  Endpoint

**Opzioni del comando**:

*NOME_REGIONE* (obbligatorio):  il nome della regione a cui vuoi passare. Puoi utilizzare il comando `bluemix network regions` per visualizzare tutti i nomi regione.

**Esempi**:

Impostare la regione corrente su `eu-gb`:

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf routes`.


## bluemix network route-check
{: #bluemix_network_route_check}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf check-route`.


## bluemix network route-map
{: #bluemix_network_route_map}

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

Associare una rotta `my-app` con il dominio specificato:

```
bluemix network route-map my-app mybluemix.net
```

Associare una rotta a 'my-container-group' con il dominio e il nome host specificati:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

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

Annullare l'associazione di `my-app.mybluemix.net` da `my-app`:

```
bluemix network route-unmap my-app mybluemix.net
```

Annullare l'associazione di `abc.ng.bluexmix.net` da `my-container-group`:

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-route`.


## bluemix network route-delete
{: #bluemix_network_route_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-route`.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-orphaned-routes`.


## bluemix network domains
{: #bluemix_network_domains}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf domains`.


## bluemix network domain-create
{: #bluemix_network_domain_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-domain`.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-domain`.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-shared-domain`.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-shared-domain`.


## bluemix security cert
{: #bluemix_security_cert}

Elencare le informazioni sul certificato di un dominio.

```
bluemix security cert DOMAIN_NAME
```

**Prerequisiti**:  Endpoint, Accesso

**Opzioni del comando**:

*DOMAIN_NAME* (obbligatorio): il dominio che ospita il certificato.

**Esempi**:

Visualizzare le informazioni sul certificato del dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

Aggiungere un certificato al dominio specificato nell'organizzazione corrente.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*DOMINIO* (obbligatorio):  il dominio a cui viene aggiunto il certificato.

-k *PRIVATE_KEY_FILE* (obbligatorio):  il percorso del file della chiave privata.

-c *CERT_FILE* (obbligatorio):  il percorso del file del certificato.

-p *PASSWORD* (facoltativo):  la password per il certificato.

-i *INTERMEDIATE_CERT_FILE* (facoltativo):  il percorso del file del certificato intermedio.

--verify-client (facoltativo): indica se abilitare la verifica del certificato del client.

**Esempi**:

Aggiungere un certificato al dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

Rimuovere un certificato dal dominio specificato nell'organizzazione corrente.

```
bluemix security cert-remove DOMAIN [-f]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*DOMINIO* (obbligatorio):  il dominio da cui rimuovere il certificato.

-f  (facoltativo):  forza l'eliminazione senza conferma.







## bluemix plugin repos
{: #bluemix_plugin_repos}

Elencare i repository di plugin registrati nella CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

**Prerequisiti**:  Nessuno


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Aggiungere un nuovo repository di plugin alla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add NOME_REPOSITORY URL_REPOSITORY
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_REPOSITORY*  (obbligatorio): il nome del repository da aggiungere. Puoi definire un tuo nome per ciascun repository.

*URL_REPOSITORY*  (obbligatorio): l'URL del repository da aggiungere. L'URL del repository deve contenere il protocollo (ad esempio, http://plugins.ng.bluemix.net invece di plugins.ng.bluemix.net). http://plugins.ng.bluemix.net è il repository di plugin ufficiale della CLI {{site.data.keyword.Bluemix_notm}}.

**Esempi**:

Aggiungere il repository di plug-in ufficiale della CLI Bluemix come `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Rimuovere un repository di plugin dalla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove NOME_REPOSITORY
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_REPOSITORY*  (obbligatorio): il nome del repository da rimuovere.

**Esempi**:

Rimuovere il repository `bluemix-repo` dalla CLI {{site.data.keyword.Bluemix_notm}}:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Elencare tutti i plugin disponibili in tutti i repository aggiunti o in uno specifico repository.

```
bluemix plugin repo-plugins [-r NOME_REPOSITORY]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

-r *NOME_REPOSITORY*  (facoltativo): elencare solo i plugin nel repository specificato.

**Esempi**:

Elencare tutti i plugin in tutti i repository aggiunti:

```
bluemix plugin repo-plugins
```

Elencare tutti i plugin nel repository `bluemix-repo`:

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

Elencare tutti i plugin installati nella CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

**Prerequisiti**:  Nessuno


## bluemix plugin install
{: #bluemix_plugin_install}

Installare la versione specifica del plugin nella CLI {{site.data.keyword.Bluemix_notm}} dal percorso o repository specificato.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*PERCORSO_PLUGIN*|*NOME_PLUGIN* (obbligatorio):  se non viene specificato `-r *NOME_REPOSITORY*`, il plugin viene installato dal percorso locale o dall'URL remoto specificati.

-r *NOME_REPOSITORY*  (facoltativo): il nome del repository dove si trova il file binario del plugin.
-v *VERSIONE*  (facoltativo):  la versione del plugin da installare. Se non fornita, viene installata l'ultima versione del plugin. Questa opzione è valida solo quando si installa il plugin dal repository.

**Esempi**:

Installare un plugin dal file locale:

```
bluemix plugin install /downloads/new_plugin
```

Installare un plugin dall'URL remoto:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installare il plugin `IBM-Containers` dell'ultima versione dal repository `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Installare il plugin `IBM-Containers` con la versione `0.5.800` dal repository `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Disinstallare il plugin specificato dalla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall NOME_PLUGIN
```

**Prerequisiti**:  Nessuno

**Opzioni del comando**:

*NOME_PLUGIN*  (obbligatorio): il nome del plugin da disinstallare.

**Esempi**:

Disinstallare il plugin `IBM-Containers` che era stato precedentemente installato:

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

Inizializzare l'ambiente dei contenitori sulla macchina locale in uso per sfruttare appieno le funzioni del servizio IBM Containers.

```
bluemix ic init
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Nota:** prima dell'inizializzazione, accertati che la CLI Docker (docker) sia installata e configurato nella tua variabile di ambiente PATH. Per passare a un'altra regione, utilizza il comando `bluemix region-set`. 

**Esempi**:

Passare alla regione `us-south`:

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

Controllare un contenitore in esecuzione o visualizzarne l'output. Utilizza `CTRL+C` per uscire e arrestare il contenitore. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} nella guida di Docker. 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

--no-stdin  (facoltativo):  non includere l'input standard.

--sig-proxy  (facoltativo): eseguire il proxy di tutti i segnali ricevuti nel processo. Il valore predefinito è **true**.

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Esempi**:

Il seguente esempio mostra una richiesta di collegamento al contenitore `my_container`:
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

Richiamare il servizio di build IBM Containers per creare un'immagine Docker in locale o nel tuo repository {{site.data.keyword.Bluemix_notm}} privato. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [build](https://docs.docker.com/reference/commandline/build/){: new_window} nella guida di Docker. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] POSIZIONE_DOCKERFILE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

-t *TAG*|--tag *TAG*  (obbligatorio):  il nome repository da applicare all'immagine creata.

--no-cache  (facoltativo):  non utilizzare la cache quando viene creata l'immagine. Il valore predefinito è **false**.

-p|--pull  (facoltativo): provare a estrarre l'immagine di base dal registro anche se è memorizzata nella cache.

-q|--quiet  (facoltativo):  sopprimere l'output dettagliato generato dai contenitori. Il valore predefinito è **false**.

*POSIZIONE_DOCKERFILE*  (obbligatorio):  il percorso verso Dockerfile e contesto sull'host locale.

**Esempi**:

Il seguente esempio mostra una richiesta di creazione di un'immagine denominata *myimage*. Il Dockerfile e altre risorse utente da utilizzare nella creazione si trovano nella stessa directory da cui viene eseguito il comando. Poiché il registro e lo spazio dei nomi sono inclusi nel nome dell'immagine, l'immagine viene creata nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

Creare un nuovo contenitore nel tuo repository {{site.data.keyword.Bluemix_notm}}. Questo comando include il comando `docker create`. Per ulteriori informazioni, vedi il comando [create](https://docs.docker.com/reference/commandline/create/){: new_window} nella guida di Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Accedere a un'immagine Docker Hub o a un'immagine dal tuo registro locale e copiarla nel tuo repository {{site.data.keyword.Bluemix_notm}} privato.

```
bluemix ic cpi IMMAGINE_DI_ORIGINE IMMAGINE_DI_DESTINAZIONE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*IMMAGINE_DI_ORIGINE*  (obbligatorio):  il nome dell'immagine e del repository di origine.

*IMMAGINE_DI_DESTINAZIONE*  (obbligatorio):  l'URL del repository {{site.data.keyword.Bluemix_notm}} privato, che include lo spazio dei nomi e il nome dell'immagine di destinazione. Una tag per l'immagine è facoltativa.

**Esempi**:

Copiare un'immagine dal repository di origine nel repository privato ed aggiungere una tag per l'immagine:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copiare l'immagine `sinatra` dal repository `training` nel repository privato `registry.ng.bluemix.net/mynamespace` e il nome dell'immagine `mysinatra`. Aggiungere una tag `v1` per l'immagine `mysinatra`. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


Eseguire un comando all'interno di un contenitore. Per ulteriori informazioni, vedi il comando [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} nella guida di Docker.

```
bluemix ic exec [-d|--detach][-it] [-u UTENTE|--user UTENTE] CONTENITORE [CMD]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

-d|--detach (facoltativo): eseguire il comando specificato in background.

-it (facoltativo): modalità interattiva. L'input standard rimane visualizzato. Immettere "exit" per uscire.

-u *UTENTE*|--user *UTENTE*  (facoltativo):  il nome utente.

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

*CMD*  (facoltativo):  il comando da eseguire all'interno del contenitore o dei contenitori specificati.

**Esempi**:

Eseguire il comando `bash` all'interno del contenitore `my_container` nella modalità interattiva:

```
bluemix ic exec -it my_container bash
```

Eseguire il comando `date` all'interno del contenitore `my_container`:

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

Elencare i gruppi di contenitori nel repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione.

```
bluemix ic groups
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Visualizzare informazioni dettagliate, quali le variabili di ambiente, le porte o la memoria, specificate per un gruppo di contenitori al momento della creazione.

```
bluemix ic group-inspect GRUPPO_CONTENITORI
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*GRUPPO_CONTENITORI*  (obbligatorio):  il nome o l'ID del gruppo di contenitori.

**Esempi**:

Il seguente esempio mostra una richiesta di controllo del gruppo di contenitori `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Elencare istanze di un gruppo di contenitori specificato.

```
bluemix ic group-instances GRUPPO_CONTENITORI
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*GRUPPO_CONTENITORI*  (obbligatorio):  il nome o l'ID del gruppo di contenitori.

**Esempi**:

Elencare tutte le istanze del gruppo di contenitori `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Creare un gruppo di contenitori scalabile.

```
bluemix ic group-create [-p PORTA|--publish port][-m MEMORY|--memory MEMORY] [-e AMB|--env AMB][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIDERATO][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NOME] IMMAGINE [CMD]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

-m *MEMORIA*|--memory *MEMORIA*  (facoltativo):  assegnare un limite di memoria, in MB, al gruppo. Quando crei un gruppo di contenitori dalla CLI, il valore predefinito per ogni istanza del contenitore è `64` MB. Quando crei un gruppo di contenitori dal Dashboard {{site.data.keyword.Bluemix_notm}}, il valore predefinito per ogni istanza del contenitore è `256` MB. I valori accettati sono `64`, `256`, `512`, `1024` e `2048`. Una volta assegnato, il limite di memoria non può essere modificato.

-e *AMB*|--env *AMB*  (facoltativo):  impostare la variabile di ambiente, dove **AMB** è una coppia "chiave=valore". In caso di più chiavi, elencale separatamente. Se sono incluse virgolette, includile racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  La seguente tabella mostra alcune variabili di ambiente comunemente utilizzate che puoi specificare:

|  Variabile di ambiente                              |     Descrizione                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nome_applicazione&gt;*       | Eseguire il bind di un servizio a un contenitore. Utilizza la variabile di ambiente `CCS_BIND_APP` per eseguire il bind di un'applicazione al contenitore. L'applicazione viene associata tramite bind al servizio di destinazione e funge da ponte che consente a {{site.data.keyword.Bluemix_notm}} di portare le informazioni `VCAP_SERVICES` dell'applicazione ponte all'istanza del contenitore in esecuzione. Per ulteriori informazioni sulla creazione di un'applicazione ponte, vedi [Esecuzione del bind di un servizio a un contenitore](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;chiave_ssh_pubblica&gt;* | Aggiungere una chiave SSH a un contenitore quando lo si crea. Puoi aggiungere la chiave SSH utilizzando la variabile di ambiente quando crei il contenitore dal dashboard {{site.data.keyword.Bluemix_notm}} o dalla CLI. Per ulteriori informazioni sulle chiavi SSH, vedi [Accesso a un contenitore](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;&gt;percorso_verso_file* | Aggiungere un file di log da monitorare nel contenitore. Includi la variabile di ambiente `LOG_LOCATIONS` in un percorso verso il file di log. |
*Tabella 1. Variabili di ambiente di uso comune*

-v VOLUME:PERCORSO_CONTENITORE[:ro]|--volume VOLUME:PERCORSO_CONTENITORE[:ro](optional):  collegare un volume a un contenitore, specificando i dettagli nel formato "IDVolume:PercorsoContenitore[:ro]".

- *VOLUME*: l'ID o il nome del volume.
- *PERCORSO_CONTENITORE*: il percorso assoluto per il volume del contenitore.
- ro: facoltativo. La specifica di "ro" rende il volume di sola lettura invece che di lettura/scrittura come predefinito.

-p *PORTA*|--publish *PORTA*  (facoltativo):  esporre la porta al traffico HTTP. I contenitori del tuo gruppo devono essere in ascolto sulla porta HTTP. Non possono essere effettuate richieste HTTPS. Per i gruppi di contenitori, non puoi includere più porte.

Quando specifichi una porta, stai rendendo l'applicazione disponibile al programma di bilanciamento del carico {{site.data.keyword.Bluemix_notm}} o ai contenitori che stanno provando a raggiungere l'host nello stesso spazio {{site.data.keyword.Bluemix_notm}}. Quindi i contenitori o il bilanciamento del carico {{site.data.keyword.Bluemix_notm}} possono utilizzare la porta per raggiungere l'host e l'applicazione nello stesso spazio {{site.data.keyword.Bluemix_notm}}. Se nel Dockerfile è specificata una porta per l'immagine che stai utilizzando, includila.

**Suggerimento:**

- Per l'immagine Liberty Server certificata da IBM o una versione modificata di questa immagine, immetti la porta 9080.
- Per l'immagine Node.js certificata da IBM o una versione modificata di questa immagine, immetti la porta 8000.

--min *MIN* (facoltativo): il numero minimo di istanze. Il valore predefinito è **1**. Se imposti un numero minimo di istanze, una volta creato il gruppo di contenitori non è più possibile modificare questo valore.

--max *MAX* (facoltativo): il numero massimo di istanze. Il valore predefinito è **2**. Se imposti un numero massimo di istanze, una volta creato il gruppo di contenitori non è più possibile modificare questo valore.

--desired *DESIDERATO*  (facoltativo):  il numero di istanze necessario. Il valore predefinito è **2**.

--auto (facoltativo): quando si crea il gruppo di contenitori e il ripristino automatico è abilitato, IBM Containers verifica l'integrità di ciascuna istanza con una richiesta HTTP alla porta assegnata.

Se non viene ricevuta alcuna risposta da un'istanza del contenitore entro 2 intervalli consecutivi di 90 secondi, l'istanza viene rimossa e sostituita con una nuova istanza. Se il contenitore risponde non viene effettuata alcuna azione. Questo processo viene ripetuto continuamente. In una finestra di 30 minuti, se il numero totale di differenti contenitori membri del gruppo è uguale o 3 volte maggiore della dimensione massima osservata per il gruppo stesso, il ripristino automatico viene disabilitato in modo permanente per il gruppo di contenitori. Per abilitare di nuovo il ripristino automatico, devi ricreare il gruppo di contenitori.

-n *HOST*|--hostname *HOST*  (facoltativo):  il nome host, quale "mycontainerhost". L'host e il dominio si combinano per formare l'URL completo della rotta pubblica, quale ad esempio "http://mycontainerhost.mybluemix.net". Quando esamini i dettagli di un gruppo di contenitori con il comando "bluemix ic group-inspect", l'host e il dominio vengono elencati insieme come rotta.

-d *DOMINIO*|--domain *DOMINIO*  (facoltativo):  generalmente, il dominio è `.mybluemix.net`. L'host e il dominio vengono combinati per formare l'URL completo della rotta pubblica, quale ad esempio `http://mycontainerhost.mybluemix.net`. Quando esamini i dettagli di un gruppo di contenitori con il comando `bluemix ic group-inspect`, l'host e il dominio vengono elencati insieme come rotta.

--name *NOME*  (obbligatorio):  assegnare un nome al gruppo. `-n` è stato dichiarato obsoleto.

**Suggerimento:** il nome del contenitore deve iniziare con una lettera. Il nome può includere lettere maiuscole, lettere minuscole, numeri, punti `.`, caratteri di sottolineatura `_` o trattini `-`.

*IMMAGINE* (obbligatorio): l'immagine da includere in ciascuna istanza del contenitore del gruppo di contenitori. L'immagine può essere seguita da un elenco di comandi, ma non da opzioni. Includi tutte le opzioni prima di specificare l'immagine.

Se utilizzi un'immagine nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione, specificala con il seguente formato: `registry.ng.bluemix.net/SPAZIO_NOMI/IMMAGINE`.

Se utilizzi un'immagine fornita da IBM Containers, non includere lo spazio dei nomi della tua organizzazione. Specifica l'immagine con il seguente formato: `registry.ng.bluemix.net/IMMAGINE`.

*CMD* (facoltativo): il comando e gli argomenti trasmessi al gruppo di contenitori da eseguire. Questo comando deve essere un comando a esecuzione prolungata. Non utilizzare un comando di breve durata che non viene eseguito per molto tempo, quale ad esempio **/bin/date**, poiché tale comando potrebbe provocare un arresto anomalo del contenitore.

**Nota:**
- Il comando e i relativi argomenti devono trovarsi alla fine della riga di comando `bluemix ic run`.
- Se gli argomenti del comando includono il trattino `-`, come in `-c` nel comando di esempio precedente, il comando deve essere preceduto da due trattini `--`.



**Esempi**:

Creare un gruppo di contenitori `my_container_group` utilizzando l'immagine `registry.ng.bluemix.net/ibmnode` fornita da IBM Containers, quindi eseguire il comando di lunga durata `ping localhost` su tale gruppo di contenitori:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Creare un gruppo di contenitori `my_container_group` utilizzando l'immagine `registry.ng.bluemix.net/ibmnode` fornita da IBM Containers, quindi eseguire il comando di lunga durata `tail -f /dev/null` su tale gruppo di contenitori:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Creare un gruppo scalabile `mygroup` con il ripristino automatico abilitato, utilizzando l'immagine `registry.ng.bluemix.net/ibmliberty`. La porta è `9080`, il nome host è `mycontainerhost`, il nome dominio è `.mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Aggiornare un gruppo di contenitori.


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIDERATO][--auto] GRUPPO_CONTENITORI
```

**Suggerimento:** per aggiornare il nome host o il dominio di un gruppo di contenitori, utilizza `bluemix ic route-map [-n HOST][-d DOMAIN] GRUPPO_CONTENITORI`.

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

--min *MIN* (facoltativo): il numero minimo di istanze. Il valore predefinito è **1**. Una volta impostato un numero minimo di istanze, questo valore non può più essere modificato.

--max *MAX* (facoltativo): il numero massimo di istanze. Il valore predefinito è **2**. Una volta impostato un numero massimo di istanze, questo valore non può più essere modificato.

--desired *DESIDERATO*  (facoltativo):  il numero di istanze necessario. Il valore predefinito è **2**.

**Suggerimento:** è possibile specificare una sola delle seguenti opzioni alla volta: `--min MIN`, `--max MAX` o `--desired DESIDERATO`.

--auto (facoltativo): riavviare automaticamente le istanze non riuscite, abilitando il ripristino automatico.

*GRUPPO_CONTENITORI*  (obbligatorio):  il nome o l'ID del gruppo di contenitori.

**Esempi**:

Il seguente esempio mostra una richiesta di aggiornamento del gruppo di contenitori `my_group`:
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Rimuovere un gruppo di contenitori dal repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione.

```
bluemix ic group-remove [-f|--force] GRUPPO_CONTENITORI
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

-f|--force (facoltativo): forza la rimozione di un contenitore in esecuzione o in errore.

*GRUPPO_CONTENITORI*  (obbligatorio):  il nome o l'ID del gruppo di contenitori.

**Esempi**:

Il seguente esempio mostra una richiesta di rimozione di un gruppo di contenitori, dove `my_group` è il nome del gruppo di contenitori.
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

Visualizzare un elenco di tutte le immagini disponibili nel repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione. Per ulteriori informazioni, vedi il comando [images](https://docs.docker.com/reference/commandline/images){: new_window} nella guida di Docker. L'elenco include l'ID immagine, la data di creazione e il nome dell'immagine.

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

-a|--all  (facoltativo):  includere tutti i livelli di immagine per ciascuna immagine del repository dell'organizzazione e non solo il più recente.

--no-trunc  (facoltativo): non troncare l'output.

-q|--quiet  (facoltativo):  visualizzare solo gli ID numerici.

**Esempi**:

Il seguente esempio mostra una richiesta di elenco delle immagini disponibili per l'organizzazione:
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Visualizzare le informazioni su un contenitore. Per ulteriori informazioni, vedi il comando [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} nella guida di Docker.

```
bluemix ic inspect [IMMAGINE|images|CONTENITORE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*IMMAGINE*  (obbligatorio):  visualizzare informazioni dettagliate su un'immagine specifica indicando l'ID o il nome dell'immagine.

images  (obbligatorio):  visualizzare informazioni dettagliate su tutte le immagini del repository.

*CONTENITORE*  (obbligatorio):  visualizzare informazioni dettagliate su un contenitore specifico, indicando l'ID o il nome del contenitore.

**Suggerimento:** non è possibile specificare le immagini *IMMAGINE* e il *CONTENITORE* contemporaneamente. 

**Esempi**:

Il seguente esempio mostra una richiesta di controllo di un contenitore denominato `proxy`: 
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

Visualizzare un insieme di informazioni che descrivono lo stato dell'istanza del servizio cloud del contenitore. Le informazioni includono limite dei contenitori, utilizzo dei contenitori, contenitori in esecuzione, limite di memoria, utilizzo della memoria, limite dell'indirizzo IP mobile, utilizzo dell'indirizzo IP mobile, URL host CCS, URL host del registro e stato della modalità di debug.

```
bluemix ic info
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix ic ips
{: #bluemix_ic_ips}

Elencare gli indirizzi IP a virgola mobile disponibili per l'utente che ha effettuato l'accesso. L'elenco include gli indirizzi IP e l'ID contenitore a cui sono collegati gli indirizzi IP. Se l'indirizzo IP non è in uso, non verrà visualizzato alcun ID contenitore.

```
bluemix ic ips [-a|--all]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

-a|--all  (facoltativo):  elencare tutti gli indirizzi IP. Per impostazione predefinita,
vengono restituiti solo gli indirizzi IP disponibili.

**Esempi**:

Il seguente esempio mostra una richiesta di elenco di tutti gli indirizzi IP per l'organizzazione, disponibili o meno.
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
Richiedere un nuovo indirizzo IP mobile.

```
bluemix ic ip-request
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Rilasciare un indirizzo IP a virgola mobile dall'istanza del servizio cloud del contenitore.

```
bluemix ic ip-release INDIRIZZO_IP
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*INDIRIZZO_IP*  (obbligatorio):  l'indirizzo IP da rilasciare.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Eseguire il bind di un indirizzo IP a virgola mobile disponibile a un contenitore.

```
bluemix ic ip-bind CONTENITORE INDIRIZZO_IP
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*INDIRIZZO_IP*  (obbligatorio):  l'indirizzo IP da associare mediante bind.

*CONTENITORE*  (obbligatorio):  il nome o l'ID del contenitore da associare mediante bind.

**Esempi**:

Il seguente esempio mostra una richiesta di bind dell'indirizzo IP `192.123.12.12 al` contenitore `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Annullare il bind di un indirizzo IP a virgola mobile dal relativo contenitore.

Gli indirizzi IP pubblici sono una risorsa limitata di IBM Containers. Pertanto, gli indirizzi IP pubblici assegnati a uno spazio e non associati mediante bind a un contenitore vengono recuperati periodicamente dagli utenti della versione di prova, approssimativamente su base settimanale. Gli indirizzi IP non associati non sono mai recuperati dai clienti con pagamento a consumo o con una sottoscrizione.

```
bluemix ic ip-unbind INDIRIZZO_IP CONTENITORE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*INDIRIZZO_IP*  (obbligatorio):  l'indirizzo IP per cui annullare l'associazione mediante bind.

*CONTENITORE*  (obbligatorio):  il nome o l'ID del contenitore per cui annullare l'associazione mediante bind.

**Esempi**:

Il seguente esempio mostra una richiesta di annullamento del bind dell'indirizzo IP `192.123.12.12` dal contenitore `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

Arrestare un processo in esecuzione in un contenitore senza arrestare il contenitore. Per ulteriori informazioni, vedi il comando [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} nella guida di Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTENITORE
```

**Prerequisiti**:  Endpoint, Login, Target, Docker

**Opzioni del comando**:

-s *CMD*|--signal *CMD*  (facoltativo):  inviare un comando al processo in esecuzione nel contenitore.

*CONTENITORE* (obbligatorio): l'ID o il nome del contenitore.

**Esempi**:

Il seguente esempio mostra una richiesta di terminazione di un contenitore denominato `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Visualizzare il nome del repository di immagini {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione a cui si desidera accedere.

```
bluemix ic namespace-get
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Impostare il nome del repository di immagini {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione a cui si accede.

*Limitazione*: non puoi utilizzare un trattino `-` nel nome del tuo spazio dei nomi del repository.

```
bluemix ic namespace-set NOME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME*  (obbligatorio):  una funzione da eseguire una sola volta per impostare lo spazio dei nomi del repository per la tua organizzazione, se non già impostato. Una volta impostato lo spazio dei nomi, reinizializza IBM Containers attraverso il comando `bluemix ic init` prima di continuare.


## bluemix ic pause
{: #pause}

Mettere in pausa tutti i processi all'interno di un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} nella guida di Docker. Per arrestare un contenitore, vedi il comando [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTENITORE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Risposte**:

- Contenitore correttamente in pausa.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`
  
 Dove `{messaggio}` è
l'errore correlato.
 
- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

**Esempi**:

Il seguente esempio mostra una richiesta di messa in pausa di un contenitore denominato `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

Riprendere tutti i processi all'interno di un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} nella guida di Docker. Per mettere in pausa un contenitore, vedi il comando [bluemix ic pause](#pause).

```
bluemix ic unpause CONTENITORE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Risposte**:

- Esecuzione del contenitore ripresa correttamente.

- Comando non riuscito con il servizio cloud del contenitore 

 `{messaggio}` 
 
 Dove `{messaggio}` è
l'errore correlato.
 
- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

**Esempi**:

Il seguente esempio mostra una richiesta di ripresa dell'esecuzione di un contenitore denominato `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Elenca le associazioni delle porte o un'associazione specifica del contenitore. Questo comando include il comando `docker port`. Per ulteriori informazioni, vedi il comando [port](https://docs.docker.com/reference/commandline/port/){: new_window} nella guida di Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Visualizzare un elenco di contenitori in esecuzione nello spazio dei nomi dell'utente che ha effettuato l'accesso. Per impostazione predefinita, questo comando mostra solo i contenitori in esecuzione. Per ulteriori informazioni, vedi il comando [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} nella guida di Docker.

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

-a|--all  (facoltativo):  mostrare tutti gli i contenitori, sia in esecuzione che arrestati.

-s|--size  (facoltativo):  elencare le dimensioni dei contenitori.

-l *NUM*|--limit *NUM*  (facoltativo):  elencare i contenitori creati più di recente, dove *NUM* è il numero dei contenitori creati più di recente che desideri restituire.

Ad esempio, se hai creato i contenitori da "node1" a "node5" in modo sequenziale, il comando "bluemix ic ps --limit 2" restituisce "node4" e "node5" perché sono gli ultimi due contenitori creati.

-q|--quiet  (facoltativo):  visualizzare solo gli ID contenitore.

**Esempi**:

Il seguente esempio mostra una richiesta di visualizzazione di tutti i contenitori in esecuzione e arrestati:
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

Riavviare un contenitore. Per ulteriori informazioni, vedi il comando [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} nella guida di Docker.

```
bluemix ic restart CONTENITORE [-t SECONDI|--time SECONDI]
```

**Prerequisiti**:  Endpoint, Login, Target, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

-t *SECONDI*|--time *SECONDI*  (facoltativo):  il numero di secondi di attesa prima che il contenitore venga riavviato.

**Risposte**:

- Contenitore riavviato correttamente.

- Comando non riuscito con il servizio cloud del contenitore 

 `{messaggio}` 
 
 Dove `{messaggio}` è
l'errore correlato.
 
- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

**Esempi**:

Il seguente esempio mostra una richiesta di riavvio di un contenitore denominato `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Rimuovere un contenitore. Per ulteriori informazioni, vedi il comando [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} nella guida di Docker.

```
bluemix ic rm [-f|--force] CONTENITORE
```

**Prerequisiti**:  Endpoint, Login, Target, Docker

**Opzioni del comando**:

-f|--force (facoltativo): forza la rimozione di un contenitore in esecuzione o in errore.

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Risposte**:

- Contenitore rimosso correttamente.

- Comando non riuscito con il servizio cloud del contenitore 

 `{messaggio}` 
 
 Dove `{messaggio}` è
l'errore correlato.
 
- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore.

**Esempi**:

Il seguente esempio mostra una richiesta di rimozione di un contenitore denominato `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Rimuovere un'immagine dallo spazio dei nomi dell'utente che ha effettuato l'accesso. Per ulteriori informazioni, vedi il comando [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} nella guida di Docker.

```
bluemix ic rmi [-R REGISTRO|--registry REGISTRO] IMMAGINE
```

**Prerequisiti**:  Endpoint, Login, Target, Docker

**Opzioni del comando**:

-R *REGISTRO*|--registry *REGISTRO*  (facoltativo):  modificare l'host del registro. Per impostazione predefinita verrà utilizzato il registro che hai specificato nel comando `bluemix ic init`.

*IMMAGINE*  (obbligatorio):  il nome dell'immagine da rimuovere. Se non viene specificata
una tag nel nome immagine, per impostazione predefinita viene eliminata
l'immagine contrassegnata come `latest`.

**Risposte**:

- Rimozione di: `{IMMAGINE}`

 Dove `{IMMAGINE}` è il
nome dell'immagine che è stata rimossa.
 
- Errore. Nessun host registro specificato.

- Rimozione dell'immagine non riuscita - Impossibile connettersi al registro cloud del contenitore

- Comando non riuscito con il servizio cloud del contenitore 

 `{messaggio}`
 
 Dove `{messaggio}` è
l'errore correlato.

**Esempi**:

Il seguente esempio mostra una richiesta di rimozione dell'immagine `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

Avviare un nuovo contenitore nel servizio cloud del contenitore da
un nome immagine. Per ulteriori informazioni, vedi il comando [run](https://docs.docker.com/reference/commandline/run/){: new_window} nella guida di Docker.



```
bluemix ic run [-p PORTA|--publish PORTA][-P] [-m MEMORIA|--memory MEMORIA][-e ENV|--env ENV] [-v VOLUME:PERCORSO_CONTENITORE] -n NOME|--name NOME [--link NOME:ALIAS][-it] IMMAGINE [CMD [CMD ...]]
```
**Nota:** accertati che lo strumento di comando Cloud Foundry sia installato e che disponi di un token Cloud Foundry. Se si accede correttamente tramite `bluemix login` e `bluemix ic init`, vengono creati i certificati e i token richiesti. 


**Prerequisiti**:  Endpoint, Login, Target, Docker

**Opzioni del comando**:

-p *PORTA*|--publish *PORTA*  (facoltativo):  esporre la porta al traffico HTTP. Includi le eventuali porte specificate nel Dockerfile per l'immagine che stai utilizzando. Puoi includere più porte con più opzioni `-p`. L'esposizione di una porta comporta automaticamente il bind di un indirizzo IP pubblico, se disponibile, al contenitore.

Se disponi già di un indirizzo IP nello spazio che desideri associare mediante bind al contenitore, puoi specificare l'indirizzo IP invece di eseguirne il bind successivamente. L'indirizzo IP deve essere specificato nel seguente formato: *&lt;indirizzo_IP&gt;:&lt;porta_contenitore&gt;:&lt;porta_contenitore&gt;*

Per ulteriori informazioni sulla richiesta di indirizzi IP per uno spazio, vedi il comando [bluemix ic ip-request](#ip_request).

Quando specifichi una porta, stai rendendo l'applicazione disponibile al programma di bilanciamento del carico {{site.data.keyword.Bluemix_notm}} o ai contenitori dello stesso spazio {{site.data.keyword.Bluemix_notm}} che stanno provando a raggiungere l'host. Se nel Dockerfile è specificata una porta per l'immagine che stai utilizzando, includila.

**Suggerimento:**

- Per l'immagine Liberty Server certificata da IBM o una versione modificata di questa immagine, immetti la porta 9080.
- Per l'immagine Node.js certificata da IBM o una versione modificata di questa immagine, immetti la porta 8000.

-P (facoltativo):  esporre automaticamente le porte specificate nel Dockerfile dell'immagine per il traffico HTTP.

-m *MEMORIA*|--memory *MEMORIA*  (facoltativo):  assegnare un limite di memoria, in MB, al gruppo. Quando crei un gruppo di contenitori dalla CLI, il valore predefinito per ogni istanza del contenitore è `64` MB.  Quando crei un gruppo di contenitori dal Dashboard {{site.data.keyword.Bluemix_notm}}, il valore predefinito per ciascuna istanza è `256` MB. I valori accettati sono `64`, `256`, `512`, `1024` e `2048`. Una volta assegnato, il limite di memoria non può essere modificato.

-e *AMB*|--env *AMB*  (facoltativo):  impostare la variabile di ambiente, dove **AMB** è una coppia "chiave=valore". In caso di più chiavi, elencale separatamente. Se includi virgolette, fallo racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`. La seguente tabella mostra alcune variabili di ambiente comunemente utilizzate che puoi specificare:

|      Variabile di ambiente                          |   Descrizione                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nome_applicazione&gt;*       | Eseguire il bind di un servizio a un contenitore. Utilizza la variabile di ambiente `CCS_BIND_APP` per eseguire il bind di un'applicazione al contenitore. L'applicazione viene associata mediante bind al servizio di destinazione e funge da ponte che consente a {{site.data.keyword.Bluemix_notm}} di portare le informazioni `VCAP_SERVICES` dell'applicazione ponte nell'istanza del contenitore in esecuzione. Per ulteriori informazioni sulla creazione di un'applicazione ponte, vedi [Esecuzione del bind di un servizio a un contenitore](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;chiave_ssh_pubblica&gt;* | Aggiungere una chiave SSH a un contenitore quando lo si crea. Puoi aggiungere la chiave SSH utilizzando la variabile di ambiente quando crei un contenitore dal dashboard {{site.data.keyword.Bluemix_notm}} o dalla CLI. Per ulteriori informazioni sulle chiavi SSH, vedi [Accesso a un contenitore](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;&gt;percorso_verso_file* | Aggiungere un file di log da monitorare nel contenitore. Includi la variabile di ambiente `LOG_LOCATIONS` in un percorso verso il file di log. |
*Tabella 2. Variabili di ambiente di uso comune*

-v VOLUME:PERCORSO_CONTENITORE[:ro]|--volume VOLUME:PERCORSO_CONTENITORE[:ro](optional):  collegare un volume a un contenitore, specificando i dettagli nel seguente formato: "IDVolume:PercorsoContenitore[:ro]".

- *VOLUME*: l'ID o il nome del volume.
- *PERCORSO_CONTENITORE*: il percorso assoluto per il volume del contenitore.
- ro: facoltativo. La specifica di "ro" rende il volume di sola lettura invece che di lettura/scrittura come predefinito.

-n *NOME*|--name *NOME*  (obbligatorio):  assegnare un nome al contenitore.

*Suggerimento:* il nome del contenitore deve iniziare con una lettera. Il nome può includere lettere maiuscole, lettere minuscole, numeri, punti `.`, caratteri di sottolineatura `_` o trattini `-`.

--link *NOME*:*ALIAS* (facoltativo): ogni volta che desideri che un contenitore comunichi con un altro contenitore in esecuzione, puoi farvi riferimento utilizzando un alias del nome host.

-it  (facoltativo):  eseguire il contenitore in modalità interattiva. Una volta creato il contenitore, mantieni l'input standard visualizzato. Immetti `exit` per uscire.

*IMMAGINE* (obbligatorio): l'immagine da includere nel contenitore. L'immagine può essere seguita da un elenco di comandi, ma non da opzioni. Includi tutte le opzioni prima di specificare un'immagine.

Se utilizzi un'immagine nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione, specificala con il seguente formato: *registry.ng.bluemix.net/SPAZIO_NOMI/IMMAGINE*.

Se utilizzi un'immagine fornita da IBM Containers, specificala con il seguente formato: *registry.ng.bluemix.net/IMMAGINE*.

*CMD* (facoltativo): il comando e gli argomenti trasmessi al contenitore da eseguire. Questo comando deve essere un comando a esecuzione prolungata. Non utilizzare un comando di breve durata che non viene eseguito per molto tempo, quale ad esempio `/bin/date`, poiché tale comando potrebbe provocare un arresto anomalo del contenitore.



**Esempi**:

Esegui il comando a esecuzione prolungata `sh -c "while true; do date; sleep 20; done"` sul contenitore `mio_contenitore` creato sull'immagine `registry.ng.bluemix.net/ibmnode`. 
```
bluemix ic run --name mio_contenitore registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Creare e successivamente riavviare un contenitore `proxy` con un limite di memoria di `1024` MB utilizzando l'immagine `mio_spazioNomi/nginx`, dove `mio_spazioNomi` è lo spazio dei nomi associato agli utenti che hanno effettuato l'accesso.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Creare e successivamente riavviare un contenitore utilizzando l'immagine `mio_spazioNomi/blog`, trasmettere le credenziali come variabili di ambiente. `mio_spazioNomi` è lo spazio dei nomi associato agli utenti che hanno effettuato l'accesso.
```
bluemix ic run -n mio_contenitore -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/mio_spazioNomi/blog
```

Aggiungere un volume a un contenitore utilizzando l'immagine `mio_spazioNomi/blog`, dove `mio_spazioNomi` è lo spazio dei nomi associato agli utenti che hanno effettuato l'accesso.
```
bluemix ic run -n mio_contenitore -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/mio_spazioNomi/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Stabilire la rotta per il traffico internet da utilizzare per accedere al gruppo di contenitori. Puoi utilizzare questo comando per stabilire una nuova rotta o aggiornarne una esistente.

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] GRUPPO_CONTENITORI
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

-n *HOST*|--hostname *HOST*  (facoltativo):  il nome host della rotta. Il nome host costituisce la prima parte dell'URL completo della rotta pubblica, quale ad esempio `mycontainerhost` nell'URL `mycontainerhost.mybluemix.net`.

-d *DOMINIO*|--domain *DOMINIO*  (facoltativo):  il nome dominio della rotta, che costituisce la seconda parte dell'URL completo della rotta pubblica. Nella maggior parte dei casi, il dominio è `mybluemix.net`. Puoi anche utilizzare questo parametro per specificare un dominio privato.

*GRUPPO_CONTENITORI*  (obbligatorio):  il nome o l'ID del gruppo di contenitori.

**Esempi**:

Il seguente esempio mostra una richiesta di associazione della rotta del gruppo denominato "GRUPPO1", dove "mio_host" è il nome dell'host e "organization.com" è il dominio.
```
bluemix ic route-map -n mio_host -d organization.com GRUPPO1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Stabilire la rotta per il traffico internet da utilizzare per accedere al gruppo di contenitori. Puoi utilizzare questo comando per stabilire una nuova rotta o aggiornarne una esistente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] GRUPPO_CONTENITORI
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

-n *HOST*|--hostname *HOST*  (facoltativo):  il nome host della rotta.

-d *DOMINIO*|--domain *DOMINIO*  (facoltativo):  il nome dominio della rotta.

*GRUPPO_CONTENITORI*  (obbligatorio):  il nome o l'ID del gruppo di contenitori.

**Esempi**:

Il seguente esempio mostra una richiesta di annullamento dell'associazione della rotta del gruppo denominato "GRUPPO1", dove "mio_host" è il nome dell'host e "organization.com" è il dominio.
```
bluemix ic route-unmap -n mio_host -d organization.com GRUPPO1
```


## bluemix ic start
{: #ic_start}
Avviare un contenitore arrestato. Per ulteriori informazioni, vedi il comando [start](https://docs.docker.com/reference/commandline/start/){: new_window} nella guida di Docker. Per arrestare un contenitore, vedi il comando [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTENITORE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Risposte**:

- Contenitore avviato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`
  
 Dove `{messaggio}` è
l'errore correlato.
 
- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

**Esempi**:

Il seguente esempio mostra una richiesta di avvio di un contenitore denominato `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
Arrestare un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} nella guida di Docker. Per avviare un contenitore, vedi il comando [bluemix ic start](#ic_start).

```
bluemix ic stop CONTENITORE [-t SECONDI|--time SECONDI]
```

**Prerequisiti**:  Endpoint, Login, Target, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

-t *SECONDI*|--time *SECONDI*  (facoltativo):  il numero di secondi di attesa prima che il contenitore venga terminato.

**Risposte**:

- Contenitore arrestato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`
  
 Dove `{messaggio}` è
l'errore correlato.
 
- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

**Esempi**:

Il seguente esempio mostra una richiesta di arresto di un contenitore denominato `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Visualizzare le statistiche di utilizzo in tempo reale per uno o più contenitori. Utilizza `CTRL+C` per chiudere. Per ulteriori informazioni, vedi il comando [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} nella guida di Docker.

```
bluemix ic stats [--no-stream] CONTENITORE [CONTENITORE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

--no-stream  (facoltativo):  visualizzare solo il risultato più recente, senza includere informazioni precedenti.

**Esempi**:

Il seguente esempio mostra una richiesta di visualizzazione delle statistiche più recenti su un contenitore:
```
bluemix ic stats --no-stream mio_contenitore
```


## bluemix ic top
{: #bluemix_ic_top}

Mostrare i processi in esecuzione nel contenitore. Per ulteriori informazioni, vedi il comando [top](https://docs.docker.com/reference/commandline/top/){: new_window} nella guida di Docker.

```
bluemix ic top CONTENITORE [CONTENITORE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Esempi**:

Il seguente esempio mostra una richiesta di visualizzazione dei processi di un contenitore denominato `mio_contenitore`.
```
bluemix ic top mio_contenitore
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Elencare i volumi.

```
bluemix ic volumes
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Ispezionare un volume.

```
bluemix ic volume-inspect NOME_VOLUME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_VOLUME*  (obbligatorio):  il nome del volume.

**Esempi**:

Il seguente esempio è una richiesta di ispezione di un volume, dove `nome_volume` è il nome del volume.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Creare un volume.

```
bluemix ic volume-create NOME_VOLUME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_VOLUME*  (obbligatorio):  il nome del volume. Il nome può contenere lettere minuscole, numeri, caratteri di sottolineatura `_` e trattini `-`.

**Esempi**:

Il seguente esempio mostra una richiesta di creazione di un volume.
```
bluemix ic volume-create nome_volume 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Rimuovere un volume.

```
bluemix ic volume-remove NOME_VOLUME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_VOLUME*  (obbligatorio):  il nome del volume.

**Esempi**:

Il seguente esempio mostra una richiesta di rimozione di un volume, dove `nome_volume` è il nome del volume.
```
bluemix ic volume-remove nome_volume
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Elencare i file system.

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Creare un nuovo file system.

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*FILE_SYSTEM_NAME*  (obbligatorio):  il nome del file system. Il nome può contenere lettere minuscole, numeri, caratteri di sottolineatura `_` e trattini `-`.

**Esempi**:

Il seguente esempio mostra una richiesta di creazione di un file system.
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Rimuovere un file system.

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*FILE_SYSTEM_NAME*  (obbligatorio):  il nome del file system. 

**Esempi**:

Il seguente esempio mostra una richiesta di rimozione di un file system, dove `my_file_system` è il nome del file system.
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Ispezionare un file system.

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*FILE_SYSTEM_NAME*  (obbligatorio):  il nome del file system. 

**Esempi**:

Il seguente esempio è una richiesta di ispezione di un file system, dove `my_file_system` è il nome del volume.
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Elencare tutte le caratteristiche del file system.

```
bluemix ic volume-fs-flavors
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

## bluemix ic wait
{: #bluemix_ic_wait}

Chiudere un contenitore e visualizzare il codice di uscita come conferma. Per ulteriori informazioni, vedi il comando [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} nella guida di Docker.

```
bluemix ic wait CONTENITORE [CONTENITORE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione, Docker

**Opzioni del comando**:

*CONTENITORE*  (obbligatorio):  l'ID o il nome del contenitore.

**Esempi**:

Il seguente esempio mostra una richiesta di chiusura di un contenitore denominato `mio_contenitore`:
```
bluemix ic wait mio_contenitore
```


## bluemix ic version
{: #bluemix_ic_version}

Mostrare la versione di Docker. 

```
bluemix ic version
```

**Prerequisiti**:  Docker

Per visualizzare la versione di IBM Containers, eseguire `bluemix ic info`. Per ulteriori informazioni, vedi il comando [version](https://docs.docker.com/reference/commandline/version/){: new_window} nella guida di Docker.
