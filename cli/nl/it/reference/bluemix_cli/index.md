---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione alla CLI {{site.data.keyword.Bluemix_notm}}
{: #getting-started}

La CLI {{site.data.keyword.Bluemix_notm}} ti fornisce un modo unico di interagire con le tue applicazioni, server virtuali, contenitori e altri servizi utilizzando un'interfaccia riga di comando. La CLI {{site.data.keyword.Bluemix_notm}} integra inoltre gli strumenti della community, come le CLI Cloud Foundry, Docker e OpenStack e inizializza le impostazioni dell'ambiente per interagire con diversi tipi di calcolo.

**Restrizione**: la CLI {{site.data.keyword.Bluemix_notm}} non è supportata da Cygwin, per cui non utilizzare la CLI {{site.data.keyword.Bluemix_notm}} nella finestra della riga di comando di Cygwin.

**Nota**: se la tua rete contiene un server proxy HTTP tra l'host che esegue la CLI e {{site.data.keyword.Bluemix_notm}}, devi specificare il nome host o l'indirizzo IP del server proxy nella variabile di ambiente HTTP_PROXY.

## Installazione della CLI {{site.data.keyword.Bluemix_notm}}
{: #install_bluemix_cli}

Prima di installare la CLI {{site.data.keyword.Bluemix_notm}}, installa la [CLI cf ![icona link esterno](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

Per Mac OS e Windows, scarica il [pacchetto CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#downloads) ed esegui il programma di installazione.

Per Linux, segui la seguente procedura:

  1. Scarica il pacchetto ed estrailo. Ad
esempio:

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. Passa alla directory `Bluemix_CLI` ed esegui il comando `./install_bluemix_cli` con l'autorizzazione root. Puoi eseguire il comando come utente root o utilizzare il comando `sudo` per ottenere l'autorizzazione root. Ad
esempio:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

Puoi ora iniziare a utilizzare la CLI {{site.data.keyword.Bluemix_notm}} o installare ulteriori plug-in.

## Installazione di un plugin
{: #install_plug-in}

Come la CLI Cloud Foundry, la CLI {{site.data.keyword.Bluemix_notm}} supporta un framework di estensione plug-in per integrare altri comandi oltre a quelli già integrati.

Per installare un plugin dal tuo ambiente locale, completa la seguente procedura:

  1. Scarica il plug-in. Ad
esempio:

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. Per un sistema simile a Unix, devi rendere eseguibile il file scaricato utilizzando il comando `chmod`. Ad
esempio:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Installa il plug-in utilizzando il comando `bluemix plugin install`. Ad
esempio:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Per l'installazione da un server remoto, attieniti alla seguente procedura:

  1. Installa il plug-in da un URL remoto direttamente utilizzando il comando `bluemix plugin install`. Ad
esempio:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Puoi inoltre installare un plugin dal repository. {{site.data.keyword.Bluemix_notm}} dispone di repository che ospitano i plugin della CLI {{site.data.keyword.Bluemix_notm}} e plugin della CLI Cloud Foundry:

  * [Repository di plug-in CLI Cloud Foundry ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg), che contiene i plug-in per la CLI di Cloud Foundry.
  * [Repository di plug-in CLI {{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![Icona link esterno](../../../icons/launch-glyph.svg), che contiene i plug-in specifici per la CLI {{site.data.keyword.Bluemix_notm}}.

Per l'installazione da un repository, attieniti alla seguente procedura:

  1. Trova il plug-in nel repository. Dopo aver installato la CLI {{site.data.keyword.Bluemix_notm}}, il repository ufficiale `Bluemix` viene aggiunto per impostazione predefinita. Puoi elencare i plugin nel repository `Bluemix` utilizzando il comando `bluemix plugin repo-plugins`. Ad
esempio:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Installa il plug-in dal repository `Bluemix` utilizzando il comando `bluemix plugin install`. Ad
esempio:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## Accesso alla CLI {{site.data.keyword.Bluemix_notm}}
{: #log_bmcli}

Dopo aver installato la CLI {{site.data.keyword.Bluemix_notm}}, puoi accedere a {{site.data.keyword.Bluemix_notm}} utilizzando il tuo ID IBM e password. Ad
esempio:

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

Sei ora pronto a utilizzare i comandi integrati di {{site.data.keyword.Bluemix_notm}}. Ad esempio, esegui il comando `bluemix catalog templates` per elencare tutti i template di contenitore tipo {{site.data.keyword.Bluemix_notm}} disponibili:

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# Comandi {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

Versione: 0.4.6

L'interfaccia di riga comando (CLI) {{site.data.keyword.Bluemix_notm}} fornisce una serie di comandi che vengono raggruppati in base allo spazio dei nomi per consentire agli utenti di interagire con {{site.data.keyword.Bluemix_notm}}. Alcuni comandi {{site.data.keyword.Bluemix_notm}} incapsulano comandi cf esistenti, mentre altri forniscono funzionalità estese agli utenti {{site.data.keyword.Bluemix_notm}}. Le seguenti informazioni elencano i comandi supportati dalla CLI {{site.data.keyword.Bluemix_notm}} e includono i relativi nomi, opzioni, utilizzo, prerequisiti, descrizioni ed esempi.
{:shortdesc}

**Nota:** i *Prerequisiti* elencano quali azioni sono richieste prima di utilizzare il comando. I comandi che non hanno azioni prerequisite elencano **Nessuno**. Altrimenti, i prerequisiti possono includere una o più delle seguenti azioni:

<dl>
<dt>Endpoint</dt>
<dd>Un endpoint API deve essere impostato mediante <code>bluemix api</code> prima di utilizzare il comando.</dd>
<dt>Accesso</dt>
<dd>L'accesso utilizzando il comando <code>bluemix login</code> è richiesto prima di utilizzare questo comando. Se stai eseguendo l'accesso con l'ID federato, utilizza l'opzione '--sso' per autenticarti con il passcode temporale.</dd>
<dt>Destinazione</dt>
<dd>Il comando <code>bluemix target</code> deve essere utilizzato per impostare un'organizzazione e uno spazio prima di utilizzare questo comando.</dd>
<dt>Docker</dt>
<dd>Per poter eseguire questo comando, è necessario che la CLI Docker (docker) sia installata.</dd>
</dl>

## indice comandi bluemix
{: #bx_commands_index}

Utilizza gli indici delle seguenti tabelle per fare riferimento ai comandi bluemix più utilizzati.

**Nota:** puoi utilizzare il formato breve dei comandi bluemix; ad esempio `bx api` è l'abbreviazione di `bluemix api`.


<table summary="Comandi bluemix generali.">
<caption>Tabella 1. Comandi bluemix generali</caption>
 <thead>
 <th colspan="5">Comandi bluemix generali</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="Comandi bluemix che puoi utilizzare per la gestione di organizzazioni, spazi e utenti.">
<caption>Tabella 2. Comandi per la gestione di organizzazioni, spazi e utenti</caption>
 <thead>
 <th colspan="5">Comandi per la gestione di organizzazioni, spazi e utenti</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary=" Comandi bluemix che puoi utilizzare per la gestione delle applicazioni Cloud Foundry.">
<caption>Tabella 3. Comandi per la gestione di applicazioni cf</caption>
 <thead>
 <th colspan="5">Comandi per la gestione di applicazioni cf</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
 <td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
 <td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 </tr>
  </tbody>
 </table>


<table summary="Comandi bluemix che puoi utilizzare per la gestione dei servizi Bluemix.">
<caption>Tabella 4. Comandi per la gestione dei servizi Bluemix</caption>
 <thead>
 <th colspan="5">Comandi per la gestione dei servizi Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>


<table summary="comandi bluemix che puoi utilizzare per gestire il catalogo, i plug-in, la fatturazione e le impostazioni di sicurezza Bluemix.">
<caption>Tabella 5. Comandi per la gestione delle impostazioni di sicurezza, dei plug-in, della fatturazione e del catalogo Bluemix</caption>
 <thead>
 <th colspan="5">Comandi per la gestione delle impostazioni di sicurezza, dei plug-in, della fatturazione e del catalogo Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="Comandi bluemix che puoi utilizzare per la gestione delle impostazioni di rete.">
<caption>Tabella 6. Comandi per la gestione delle impostazioni di rete</caption>
 <thead>
 <th colspan="5">Comandi per la gestione delle impostazioni di rete</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>



### bluemix help
{: #bluemix_help}
Visualizzare la guida generale per i comandi integrati di primo livello e gli spazi dei nomi supportati della CLI {{site.data.keyword.Bluemix_notm}} oppure la guida per un comando o uno spazio dei nomi integrati specifici.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>COMANDO|SPAZIO_DEI_NOMI (facoltativo)</dt>
   <dd>Il comando o lo spazio dei nomi per cui viene visualizzata la guida. Se non viene specificata, viene visualizzata la guida generale per la CLI {{site.data.keyword.Bluemix_notm}}.</dd>
   </dl>



<strong>Esempi</strong>:

Visualizzare la guida generale per la CLI {{site.data.keyword.Bluemix_notm}}:

```
bluemix help
```

Visualizzare la guida per il comando `info`:

```
bluemix help info
```



### bluemix api
{: #bluemix_api}
Impostare o visualizzare l'endpoint API {{site.data.keyword.Bluemix_notm}}. Questo comando include il comando `cf api`.

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>ENDPOINT_API (facoltativo)</dt>
   <dd>L'endpoint API di destinazione, ad esempio `https://api.chinabluemix.net`. Se non vengono specificate entrambe le opzioni *ENDPOINT_API* e `--unset`, viene visualizzato l'endpoint API corrente.</dd>
   <dt>--unset (facoltativo)</dt>
   <dd>Rimuovere l'impostazione di endpoint API.</dd>
    </dl>
<strong>Esempi</strong>:

Impostare l'endpoint API su api.chinabluemix.net:

```
bluemix api api.chinabluemix.net
```

Visualizzare l'endpoint API corrente:

```
bluemix api
```

Annullare l'impostazione dell'endpoint API:

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

Eseguire l'accesso dell'utente. Questo comando include il comando `cf login`. Le opzioni di comando sono le stesse del comando `cf login`.

```
bluemix login [OPZIONI...]
```

<strong>Prerequisiti</strong>:  Endpoint

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>Opzioni del comando</strong>:
Per informazioni sulle opzioni supportate dal comando `login`, vedi le informazioni sull'utilizzo del comando `cf login` per i comandi cf per la gestione delle applicazioni.

<strong>Nota</strong>:
Se stai eseguendo l'accesso con l'ID federato, utilizza l'opzione '--sso' per autenticarti con il passcode temporale.

### bluemix logout
{: #bluemix_logout}

Disconnettere l'utente. Questo comando include il comando `cf logout`.

```
bluemix logout
```

<strong>Prerequisiti</strong>:  Nessuno


### bluemix target
{: #bluemix_target}


Impostare o visualizzare l'organizzazione o lo spazio di destinazione. Questo comando include il comando `cf target`.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>-o <i>NOME_ORGANIZZAZIONE</i> (facoltativo)</dt>
   <dd>Il nome dell'organizzazione di destinazione.</dd>
   <dt>-s <i>NOME_SPAZIO</i> (facoltativo)</dt>
   <dd>Il nome dello spazio di destinazione.</dd>
   </dl>
Se non viene specificata né l'opzione -o *NOME_ORGANIZZAZIONE* né quella -s *NOME_SPAZIO*, vengono visualizzati l'organizzazione e lo spazio correnti.
<strong>Esempi</strong>:

Impostare l'organizzazione corrente su `MyOrg` e lo spazio su `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

Visualizzare l'organizzazione e lo spazio correnti:

```
bluemix target
```


### bluemix info
{: #bluemix_info}

Visualizzare le informazioni su {{site.data.keyword.Bluemix_notm}} di base, compresi la regione corrente, la versione controller cloud e alcuni utili endpoint, quali gli endpoint per l'accesso e per lo scambio di token di accesso.

```
bluemix info
```

<strong>Prerequisiti</strong>:  Endpoint


### bluemix config
{: #bluemix_config}


Scrivere i valori predefiniti nel file di configurazione.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>Il valore di timeout per le richieste HTTP. Il valore predefinito è 60 secondi.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>Traccia le richieste HTTP nel terminale o file specificato.</dd>
   <dt>--color true|false</dt>
   <dd>Abilita o disabilita l'output a colori. L'output a colori è abilitato per impostazione predefinita.</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>Imposta una locale predefinita. Se la LOCALE è <i>CLEAR</i>, la locale precedente viene eliminata.</dd>
   <dt>--check-version true|false</dt>
   <dd>Abilita o disabilita il controllo della versione della CLI</dd>
   </dl>

È possibile specificare solo una di queste opzioni alla volta.

<strong>Esempi</strong>:

Impostare il timeout della richiesta HTTP su 30 secondi:

```
bluemix config --http-timeout 30
```

Abilitare l'output di traccia per le richieste HTTP:

```
bluemix config --trace true
```

Traccia le richieste HTTP in un file specificato */home/usera/my_trace*:

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


### bluemix curl
{: #bluemix_curl}

Eseguire una richiesta HTTP raw per {{site.data.keyword.Bluemix_notm}}. *Content-Type* è impostato su *application/json* come valore predefinito. Questo comando invia la richiesta al MCCP (Multi Cloud Control Proxy) {{site.data.keyword.Bluemix_notm}}. Per i percorsi supportati, fai riferimento alle definizioni del percorso API nella [Documentazione API CloudFoundry ](http://apidocs.cloudfoundry.org/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg).

```
bluemix curl PERCORSO [OPZIONI...]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt><i>PERCORSO</i> (obbligatorio)</dt>
   <dd>Il percorso URL della risorsa. Ad esempio, /v2/apps.</dd>
   <dt><i>OPZIONI</i> (facoltativo)</dt>
   <dd>Le opzioni supportate dal comando `bluemix curl` sono le stesse del comando `cf curl`.</dd>
   </dl>

<strong>Esempi</strong>:

Visualizzare le informazioni per tutte le organizzazioni dell'account corrente:

```
bluemix curl /v2/organizations
```


### bluemix iam orgs
{: #bluemix_iam_orgs}

Elencare tutte le organizzazioni

```
bluemix iam orgs [-r REGION --guid]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>-r <i>REGIONE</i> (facoltativo)</dt>
   <dd>Regione per cui vengono visualizzare le informazioni sull'organizzazione. Se impostato su 'all', vengono elencate tutte le organizzazioni in tutte le regioni.</dd>
   <dt>--guid (facoltativo)</dt>
   <dd>Visualizzare il GUID delle organizzazioni.</dd>
   </dl>

<strong>Esempi</strong>:

Elencare tutte le organizzazioni della regione: `us-south` con il GUID visualizzato

```
bluemix iam orgs -r us-south --guid
```

### bluemix iam org
{: #bluemix_iam_org}

Visualizzare le informazioni per l'organizzazione specificata.

```
bluemix iam org ORG_NAME [--guid]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione.</dd>
   <dt>--guid (facoltativo)</dt>
   <dd>Visualizzare il GUID dell'organizzazione.</dd>
   </dl>

<strong>Esempi</strong>:

Mostrare le informazioni dell'organizzazione `IBM` con il GUID visualizzato

```
bluemix iam org IBM --guid
```

### bluemix iam org-create
{: #bluemix_iam_org_create}

Creare una nuova organizzazione. Questa operazione può essere eseguita solo dal proprietario dell'account.

```
bluemix iam org-create ORG_NAME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione in fase di creazione.</dd>
   </dl>

<strong>Esempi</strong>:

Creare un'organizzazione denominata `IBM`.

```
bluemix iam org-create IBM
```


### bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replicare un'organizzazione dalla regione corrente in un'altra regione.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione esistente che deve essere replicata.</dd>
   <dt>NOME_REGIONE (obbligatorio)</dt>
   <dd>Il nome della regione che ospita l'organizzazione replicata.</dd>
   </dl>

<strong>Esempi</strong>:

Replicare l'organizzazione `myorg` nella regione `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


### bluemix iam org-rename
{: #bluemix_iam_org_rename}

Rinominare un'organizzazione. Questa operazione può essere eseguita solo da un gestore organizzazione.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORG_PRECEDENTE (obbligatorio)</dt>
   <dd>Il vecchio nome dell'organizzazione da rinominare.</dd>
   <dt>NUOVO_NOME_ORG (obbligatorio)</dt>
   <dd>Il nuovo nome con cui viene rinominata l'organizzazione.</dd>
   </dl>

### bluemix iam org-delete
{: #bluemix_iam_org_delete}

Eliminare l'organizzazione specificata nella regione corrente.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione esistente che deve essere eliminata.</dd>
   <dt>-f (facoltativo)</dt>
   <dd>Forzare l'eliminazione senza conferma.</dd>
   <dt>--all (facoltativo)</dt>
   <dd>Eliminare l'organizzazione da tutte le regioni.</dd>
   </dl>


### bluemix iam spaces
{: #bluemix_iam_spaces}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf spaces`.


### bluemix iam space
{: #bluemix_iam_space}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf space`.


### bluemix iam space-create
{: #bluemix_iam_space_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-space`.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename-space`.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-space`.


### bluemix iam account-users
{: #bluemix_iam_account_users}

Visualizza gli utenti associati con l'account. Questa operazione può essere eseguita solo dal proprietario dell'account.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}


Invita un utente nell'account con un'organizzazione e un ruolo spazio già impostati. Questa operazione può essere eseguita solo dal proprietario dell'account.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso


<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_UTENTE (obbligatorio)</dt>
   <dd>Il nome dell'utente invitato.</dd>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione in cui viene invitato l'utente.</dd>
   <dt>RUOLO_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome del ruolo organizzazione in cui viene invitato l'utente. Per esempio:
   <ul>
  <li>OrgManager: questo ruolo può invitare e gestire utenti, selezionare e modificare piani e impostare limiti di spesa.</li>
  <li>BillingManager: questo ruolo può creare e gestire l'account di fatturazione e le informazioni sul pagamento.</li>
  <li>OrgAuditor: questo ruolo dispone di un accesso in sola lettura a report e informazioni sull'organizzazione.</li>
  </ul> </dd>
   <dt>NOME_SPAZIO (obbligatorio)</dt>
   <dd>Il nome dello spazio in cui viene invitato l'utente.</dd>
   <dt>RUOLO_SPAZIO (obbligatorio)</dt>
   <dd>Il nome dello spazio in cui viene invitato l'utente. Il nome del ruolo spazio in cui viene invitato l'utente. Per esempio:
   <ul>
<li>SpaceManager: questo ruolo può invitare e gestire utenti e attivare funzioni per un dato spazio.</li>
<li>SpaceDeveloper: questo ruolo può creare e gestire applicazioni e servizi e visualizzare log e report.</li>
<li>SpaceAuditor: questo ruolo può visualizzare log, report e impostazioni per lo spazio.</li>
</ul>
</dd>
</dl>

<strong>Esempi</strong>:

Invitare l'utente `Mary` nell'organizzazione `IBM` con il ruolo `OrgManager` e lo spazio `Cloud` con il ruolo `SpaceAuditor`:

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Invia di nuovo l'invito a un utente (è richiesto il gestore organizzazione o il proprietario account)
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
{: #bluemix_iam_org_users}

Visualizzare gli utenti nell'organizzazione specificata per il ruolo.

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione.</dd>
   <dt>-a (facoltativo)</dt>
   <dd>Elencare tutti gli utenti dell'organizzazione specificata, non raggruppati per ruolo.</dd>
    </dl>

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Aggiungi un utente nell'organizzazione (è richiesto il gestore organizzazione).
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Rimuovi un utente dall'organizzazione (gestore organizzazione o solo l'utente)
```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Opzioni del comando</strong>:
  <dl>
   <dt>--force, -f</dt>
   <dd>Forzare l'eliminazione senza conferma.</dd>
 </dl>

### bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Assegnare un ruolo dell'organizzazione ad un utente. Questa operazione può essere eseguita solo da un gestore organizzazione.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
  <dl>
   <dt>NOME_UTENTE (obbligatorio)</dt>
   <dd>Il nome dell'utente in fase di assegnazione.</dd>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione a cui viene assegnato l'utente.</dd>
   <dt>RUOLO_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome del ruolo organizzazione a cui viene assegnato l'utente. Per esempio:
   <ul>
   <li>OrgManager: questo ruolo può invitare e gestire utenti, selezionare e modificare piani e impostare limiti di spesa.</li>
   <li>BillingManager: questo ruolo può creare e gestire l'account di fatturazione e le informazioni sul pagamento.</li>
   <li>OrgAuditor: questo ruolo dispone di un accesso in sola lettura a report e informazioni sull'organizzazione.</li>
   </ul>
   </dd>
    </dl>

<strong>Esempi</strong>:

Assegnare l'utente `Mary` all'organizzazione `IBM` con il ruolo `OrgManager`:

```
bluemix iam org-role-set Mary IBM OrgManager
```


### bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Rimuovere un ruolo dell'organizzazione da un utente. Questa operazione può essere eseguita solo da un gestore organizzazione.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_UTENTE (obbligatorio)</dt>
   <dd>Il nome dell'utente in fase di eliminazione.</dd>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione da cui viene eliminato l'utente.</dd>
   <dt>RUOLO_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome del ruolo organizzazione da cui viene eliminato l'utente. Per esempio:
   <ul>
   <li>OrgManager: questo ruolo può invitare e gestire utenti, selezionare e modificare piani e impostare limiti di spesa.</li>
   <li>BillingManager: questo ruolo può creare e gestire l'account di fatturazione e le informazioni sul pagamento.</li>
   <li>OrgAuditor: questo ruolo dispone di un accesso in sola lettura a report e informazioni sull'organizzazione.</li>
   </ul>
   </dd>
    </dl>

<strong>Esempi</strong>:

Rimuovere l'utente `Mary` dall'organizzazione `IBM` con il ruolo `OrgManager`:

```
bluemix iam org-role-unset Mary IBM OrgManager
```


### bluemix iam space-users
{: #bluemix_iam_space_users}

Visualizzare gli utenti nello spazio specificato per il ruolo.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione.</dd>
   <dt>NOME_SPAZIO (obbligatorio)</dt>
   <dd>Il nome dello spazio.</dd>
   </dl>


### bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Assegnare un ruolo dello spazio ad un utente. Questa operazione può essere eseguita solo da un gestore spazio.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_UTENTE (obbligatorio)</dt>
   <dd>Il nome dell'utente in fase di assegnazione.</dd>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione a cui viene assegnato l'utente.</dd>
   <dt>NOME_SPAZIO (obbligatorio)</dt>
   <dd>Il nome dello spazio a cui è assegnato l'utente.</dd>
   <dt>RUOLO_SPAZIO (obbligatorio)</dt>
   <dd>Il nome del ruolo spazio a cui è assegnato l'utente. Per esempio:
   <ul>
   <li>SpaceManager: questo ruolo può invitare e gestire utenti e attivare funzioni per un dato spazio.</li>
   <li>SpaceDeveloper: questo ruolo può creare e gestire applicazioni e servizi e visualizzare log e report.</li>
   <li>SpaceAuditor: questo ruolo può visualizzare log, report e impostazioni per lo spazio.</li>
   </ul></dd>
    </dl>

<strong>Esempi</strong>:

Assegnare l'utente `Mary` all'organizzazione `IBM` e allo spazio `Cloud` con il ruolo `SpaceManager`:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

### bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Rimuovere un ruolo dello spazio da un utente. Questa operazione può essere eseguita solo da un gestore spazio.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_UTENTE (obbligatorio)</dt>
   <dd>Il nome dell'utente in fase di eliminazione.</dd>
   <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
   <dd>Il nome dell'organizzazione da cui viene eliminato l'utente.</dd>
   <dt>NOME_SPAZIO (obbligatorio)</dt>
   <dd>Il nome dello spazio da cui viene eliminato l'utente.</dd>
   <dt>RUOLO_SPAZIO (obbligatorio)</dt>
   <dd>Il nome del ruolo spazio da cui viene eliminato l'utente. Per esempio:
   <ul>
   <li>SpaceManager: questo ruolo può invitare e gestire utenti e attivare funzioni per un dato spazio.</li>
   <li>SpaceDeveloper: questo ruolo può creare e gestire applicazioni e servizi e visualizzare log e report.</li>
   <li>SpaceAuditor: questo ruolo può visualizzare log, report e impostazioni per lo spazio.</li>
   </ul></dd>
    </dl>


<strong>Esempi</strong>:

Rimuovere l'utente `Mary` dall'organizzazione `IBM` e dall spazio `Cloud` con il ruolo `SpaceManager`:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


### bluemix app push
{: #bluemix_app_push}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf push`.


### bluemix app list
{: #bluemix_app_list}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf apps`.


### bluemix app show
{: #bluemix_app_show}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf app`.


### bluemix app scale
{: #bluemix_app_scale}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf scale`.


### bluemix app delete
{: #bluemix_app_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete`.


### bluemix app rename
{: #bluemix_app_rename}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename`.


### bluemix app start
{: #bluemix_app_start}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf start`.


### bluemix app stop
{: #bluemix_app_stop}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf stop`.


### bluemix app restart
{: #bluemix_app_restart}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf restart`.


### bluemix app restage
{: #bluemix_app_restage}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf restage`.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf restart-app-instance`.


### bluemix app events
{: #bluemix_app_events}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf events`.


### bluemix app files
{: #bluemix_app_files}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf files`.


### bluemix app logs
{: #bluemix_app_logs}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf logs`.


### bluemix app env
{: #bluemix_app_env}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf env`.


### bluemix app env-set
{: #bluemix_app_env_set}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf set-env`.


### bluemix app env-unset
{: #bluemix_app_env_unset}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf unset-env`.


### bluemix app stacks
{: #bluemix_app_stacks}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf stacks`.


### bluemix app stack
{: #bluemix_app_stack}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf stack`.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-app-manifest`.


### bluemix service offerings
{: #bluemix_service_offerings}


Questo comando ha la stessa funzione e le stesse opzioni del comando `cf marketplace`.


### bluemix service list
{: #bluemix_service_list}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf services`.


### bluemix service show
{: #bluemix_service_show}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf service`.


### bluemix service create
{: #bluemix_service_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-service`.


### bluemix service update
{: #bluemix_service_update}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf update-service`.


### bluemix service delete
{: #bluemix_service_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-service`.


### bluemix service rename
{: #bluemix_service_rename}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf rename-service`.


### bluemix service bind
{: #bluemix_service_bind}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf bind-service`.


### bluemix service unbind
{: #bluemix_service_unbind}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf unbind-service`.


### bluemix service key-create
{: #bluemix_service_key_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-service-key`.


### bluemix service key-delete
{: #bluemix_service_key_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-service-key`.


### bluemix service keys
{: #bluemix_service_keys}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf service-keys`.


### bluemix service key-show
{: #bluemix_service_key_show}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf service-key`.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-user-provided-service`.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf update-user-provided-service`.


### bluemix catalog templates
{: #bluemix_catalog_templates}

Visualizzare i template di contenitore tipo su Bluemix.

```
bluemix catalog templates [-d]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-d (facoltativo)</dt>
   <dd>Se viene specificata l'opzione <i>-d</i>, viene visualizzata anche la descrizione di ciascun template. Altrimenti, vengono visualizzati solo l'ID e il nome di ciascun template.</dd>
   </dl>


### bluemix catalog template
{: #bluemix_catalog_template}

Visualizzare le informazioni dettagliate di un template contenitore tipo specificato.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>ID_TEMPLATE (obbligatorio)</dt>
   <dd>L'ID del template contenitore tipo. Utilizza <i>bluemix template</i> per visualizzare l'ID di tutti i template.</dd>
   </dl>


<strong>Esempi</strong>:

Visualizzare i dettagli del template `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


### bluemix catalog template-run
{: #bluemix_catalog_template_run}

Creare un'applicazione cf basata sul template specificato con l'URL e la descrizione specificati. Per impostazione predefinita, la nuova applicazione viene avviata automaticamente.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>ID_TEMPLATE (obbligatorio)</dt>
   <dd>Il template su cui verrà basata l'applicazione quando verrà creata. Utilizza <i>bluemix templates</i> per visualizzare l'ID di tutti i template.</dd>
   <dt>NOME_APPLICAZIONE_CF (obbligatorio)</dt>
   <dd>Il nome dell'applicazione cf da creare.</dd>
   <dt>-u <i>URL</i> (facoltativo)</dt>
   <dd>La rotta dell'applicazione. Se non specificata, la rotta viene impostata automaticamente da Bluemix, in base al tuo nome applicazione e al tuo dominio predefinito.</dd>
   <dt>-d <i>DESCRIZIONE</i> (facoltativo)</dt>
   <dd>Descrizione dell'applicazione.</dd>
   <dt>--no-start (facoltativo)</dt>
   <dd>Non avviare l'applicazione automaticamente una volta creata. Se non viene specificata, l'applicazione viene avviata automaticamente dopo la sua creazione.</dd>
   </dl>


<strong>Esempi</strong>:

Creare un'applicazione `my-app` basata sul template `javaHelloWorld`:

```
bluemix catalog template-run javaHelloWorld my-app
```

Creare un'applicazione `my-ruby-app` basata sul template `rubyHelloWorld` con la rotta `myrubyapp.chinabluemix.net` e la descrizione `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Creare un'applicazione `my-python-app` basata sul template `pythonHelloWorld` senza l'avvio automatico:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


### bluemix network regions
{: #bluemix_network_regions}

Visualizzare le informazioni per tutte le regioni su {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

<strong>Prerequisiti</strong>:  Endpoint


### bluemix network region-set
{: #bluemix_network_region_set}

Passare alla regione specificata. Questo comando ha automaticamente di nuovo come destinazione la stessa organizzazione e lo stesso spazio nella nuova regione, se possibile. Altrimenti, il comando richiede all'utente di selezionare una nuova organizzazione e un nuovo spazio, qualora l'utente sia già collegato. L'endpoint API viene modificato di conseguenza.

```
bluemix network region-set NOME_REGIONE
```

<strong>Prerequisiti</strong>:  Endpoint

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_REGIONE (obbligatorio)</dt>
   <dd>Il nome della regione a cui si desidera passare. Puoi utilizzare il comando <i>bluemix network regions</i> per visualizzare tutti i nomi regione.</dd>
    </dl>

<strong>Esempi</strong>:

Impostare la regione corrente su `eu-gb`:

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf routes`.


### bluemix network route-check
{: #bluemix_network_route_check}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf check-route`.


### bluemix network route-map
{: #bluemix_network_route_map}

Associare una rotta a un'applicazione cf o a un gruppo di contenitori esistenti che hanno il dominio e il nome host specificati.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORE (obbligatorio)</dt>
   <dd>Il nome dell'applicazione cf o del gruppo di contenitori da associare a una rotta.</dd>
   <dt>DOMINIO (obbligatorio)</dt>
   <dd>Il dominio della rotta. Ad esempio, mychinabluemix.net o chinabluemix.net. </dd>
   <dt>-n <i>NOME_HOST</i> (facoltativo)</dt>
   <dd>Il nome host della rotta. Se non viene fornito, il nome host è impostato sul nome applicazione o sul nome gruppo di contenitori per impostazione predefinita.</dd>
   </dl>

<strong>Esempi</strong>:

Associare una rotta `my-app` con il dominio specificato:

```
bluemix network route-map my-app mychinabluemix.net
```

Associare una rotta a 'my-container-group' con il dominio e il nome host specificati:

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

Annullare l'associazione della rotta specificata a un'applicazione cf o a un gruppo di contenitori esistenti.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_APPLICAZIONE_CF|NOME_GRUPPO_CONTENITORE (obbligatorio)</dt>
   <dd>Il nome dell'applicazione cf o del gruppo di contenitori.</dd>
   <dt>DOMINIO (obbligatorio)</dt>
   <dd>Il dominio della rotta (ad esempio, mychinabluemix.net o chinabluemix.net).</dd>
   <dt>-n <i>NOME_HOST</i> (facoltativo)</dt>
   <dd>Il nome host della rotta. Se non viene fornito, il nome host è impostato sul nome applicazione o sul nome gruppo di contenitori per impostazione predefinita.</dd>
   </dl>

<strong>Esempi</strong>:

Annullare l'associazione di `my-app.mychinabluemix.net` da `my-app`:

```
bluemix network route-unmap my-app mychianbluemix.net
```

Annullare l'associazione di `abc.chinabluexmix.net` da `my-container-group`:

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-route`.


### bluemix network route-delete
{: #bluemix_network_route_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-route`.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-orphaned-routes`.


### bluemix network domains
{: #bluemix_network_domains}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf domains`.


### bluemix network domain-create
{: #bluemix_network_domain_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-domain`.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-domain`.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf create-shared-domain`.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Questo comando ha la stessa funzione e le stesse opzioni del comando `cf delete-shared-domain`.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

Mostra i costi e l'utilizzo mensile del tuo account.

```
bluemix bss account-usage [-d YYYY-MM] [--json]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

<dl>
  <dt>-d MONTH_DATE (facoltativo)</dt>
  <dd>Visualizza i dati per il mese e la data specificando l'utilizzo nel formato YYYY-MM. Se non specificato, viene mostrato l'utilizzo del mese corrente.</dd>
  <dt>--json (facoltativo)</dt>
  <dd>Visualizza il risultato di utilizzo nel formato JSON.</dd>
</dl>

<strong>Esempi</strong>:

Mostra il report del costo e l'utilizzo dell'account per 2016-06:

```
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

Mostra i dettagli dell'utilizzo mensile di un'organizzazione. Questa operazione può essere eseguita solo da un gestore della fatturazione dell'organizzazione.

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

<dl>
  <dt>NOME_ORGANIZZAZIONE (obbligatorio)</dt>
  <dd>Nome dell'organizzazione.</dd>
  <dt>-d MONTH_DATE (facoltativo)</dt>
  <dd>Visualizza i dati per il mese e la data specificata tramite l'utilizzo nel formato YYYY-MM. Se non specificato, viene mostrato l'utilizzo del mese corrente.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nome della regione che ospita l'organizzazione. Se impostato su 'all', viene mostrato l'utilizzo dell'organizzazione in tutte le regioni.</dd>
  <dt>--json (facoltativo)</dt>
  <dd>Visualizza il risultato di utilizzo nel formato JSON.</dd>
</dl>



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

Mostra il riepilogo dell'utilizzo mensile per le organizzazioni nel mio account.

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

<dl>
  <dt>-d MONTH_DATE (facoltativo)</dt>
  <dd>Visualizza i dati per il mese e la data specificata tramite l'utilizzo nel formato YYYY-MM. Se non specificato, viene mostrato l'utilizzo del mese corrente.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nome della regione che ospita le organizzazioni. Se impostato su 'all', viene mostrato il riepilogo dell'utilizzo delle organizzazioni in tutte le regioni.</dd>
  <dt>--json (facoltativo)</dt>
  <dd>Visualizza il risultato di utilizzo nel formato JSON.</dd>
</dl>



### bluemix security cert
{: #bluemix_security_cert}

Elencare le informazioni sul certificato di un dominio.

```
bluemix security cert DOMAIN_NAME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_DOMINIO (obbligatorio)</dt>
   <dd>Il dominio che ospita il certificato.</dd>
   </dl>



<strong>Esempi</strong>:

Visualizzare le informazioni sul certificato del dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

Aggiungere un certificato al dominio specificato nell'organizzazione corrente.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>DOMINIO (obbligatorio)</dt>
   <dd>Il dominio a cui viene aggiunto il certificato.</dd>
   <dt>-k <i>FILE_CHIAVE PRIVATA</i> (obbligatorio)</dt>
   <dd>Il percorso del file della chiave privata.</dd>
   <dt>-c <i>FILE_CERTIFICATO</i> (obbligatorio)</dt>
   <dd>Il percorso del file del certificato.</dd>
   <dt>-p <i>PASSWORD</i> (facoltativo)</dt>
   <dd>La password per il certificato.</dd>
   <dt>-i <i>FILE_CERTIFICATO_INTERMEDIO</i> (optional)</dt>
   <dd>Il percorso del file di certificato intermedio.</dd>
   <dt>--verify-client (facoltativo)</dt>
   <dd>Stabilire se abilitare la verifica del certificato del client.</dd>
   </dl>


<strong>Esempi</strong>:

Aggiungere un certificato al dominio `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

Rimuovere un certificato dal dominio specificato nell'organizzazione corrente.

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>DOMINIO (obbligatorio)</dt>
   <dd>Il dominio da cui rimuovere il certificato.</dd>
   <dt>-f (facoltativo)</dt>
   <dd>Forzare l'eliminazione senza conferma.</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

Elencare i repository di plugin registrati nella CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

<strong>Prerequisiti</strong>:  Nessuno


### bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Aggiungere un nuovo repository di plugin alla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add NOME_REPOSITORY URL_REPOSITORY
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_REPOSITORY (obbligatorio)</dt>
   <dd>Il nome del repository da aggiungere. Puoi definire un tuo nome per ciascun repository.</dd>
   <dt>URL_REPOSITORY (obbligatorio)</dt>
   <dd>L'URL del repository da aggiungere. L'URL del repository deve contenere il protocollo (ad esempio, http://plugins.ng.bluemix.net invece di plugins.ng.bluemix.net). http://plugins.ng.bluemix.net è il repository di plugin ufficiale della CLI Bluemix.</dd>
    </dl>


<strong>Esempi</strong>:

Aggiungere il repository di plug-in ufficiale della CLI Bluemix come `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


### bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Rimuovere un repository di plugin dalla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove NOME_REPOSITORY
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>NOME_REPOSITORY (obbligatorio)</dt>
   <dd>Il nome del repository da rimuovere.</dd>
   </dl>

<strong>Esempi</strong>:

Rimuovere il repository `bluemix-repo` dalla CLI {{site.data.keyword.Bluemix_notm}}:

```
bluemix plugin repo-remove bluemix-repo
```


### bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Elencare tutti i plugin disponibili in tutti i repository aggiunti o in uno specifico repository.

```
bluemix plugin repo-plugins [-r NOME_REPOSITORY]
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-r <i>NOME_REPOSITORY</i> (facoltativo)</dt>
   <dd>Elencare solo i plugin del repository specificato.</dd>
   </dl>

<strong>Esempi</strong>:

Elencare tutti i plugin in tutti i repository aggiunti:

```
bluemix plugin repo-plugins
```

Elencare tutti i plugin nel repository `bluemix-repo`:

```
bluemix plugin repo-plugins -r bluemix-repo
```


### bluemix plugin list
{: #bluemix_plugin_list}

Elencare tutti i plugin installati nella CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

<strong>Prerequisiti</strong>:  Nessuno


### bluemix plugin install
{: #bluemix_plugin_install}

Installare la versione specifica del plugin nella CLI {{site.data.keyword.Bluemix_notm}} dal percorso o repository specificato.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>PERCORSO_PLUGIN|NOME_PLUGIN (obbligatorio)</dt>
   <dd>Se -r <i>NOME_REPOSITORY</i> non viene specificato, il plugin viene installato dal percorso locale o dall'URL remoto specificati.</dd>
   <dt>-r <i>NOME_REPOSITORY</i> (facoltativo)</dt>
   <dd>Il nome del repository in cui si trova il file binario del plugin.</dd>
   <dt>-v <i>VERSIONE</i> (facoltativo)</dt>
   <dd>La versione del plugin da installare. Se non fornita, viene installata l'ultima versione del plugin. Questa opzione è valida solo quando si installa il plugin dal repository.</dd>
    </dl>

<strong>Esempi</strong>:

Installare un plugin dal file locale:

```
bluemix plugin install /downloads/new_plugin
```

Installare un plugin dall'URL remoto:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installare il plugin `container-service` dell'ultima versione dal repository `bluemix-repo`:

```
bluemix plugin install container-service -r bluemix-repo
```
Installare il plugin `container-service` con la versione `0.5.800` dal repository `bluemix-repo`:

```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
```






### bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Disinstallare il plugin specificato dalla CLI {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall NOME_PLUGIN
```

<strong>Prerequisiti</strong>:  Nessuno

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>NOME_PLUGIN (obbligatorio)</dt>
   <dd>Il nome del plugin da disinstallare.</dd>
    </dl>

<strong>Esempi</strong>:

Disinstallare il plugin `container-service` che era stato precedentemente installato:

```
bluemix plugin uninstall container-service
```



# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg)
