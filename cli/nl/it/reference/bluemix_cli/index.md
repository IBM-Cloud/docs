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

  1. Trova il plug-in nel repository. Dop oaver installato la CLI {{site.data.keyword.Bluemix_notm}}, il repository ufficiale `Bluemix` viene aggiunto per impostazione predefinita. Puoi elencare i plugin nel repository `Bluemix` utilizzando il comando `bluemix plugin repo-plugins`. Ad
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

<table summary="Comandi bluemix che puoi utilizzare per la gestione dei contenitori in Bluemix.">
<caption>Tabella 7. Comandi per la gestione dei contenitori in Bluemix</caption>
 <thead>
 <th colspan="5">Comandi per la gestione dei contenitori in Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](index.html#bluemix_ic_service-bind)</td>
 <td>[bluemix ic service-unbind](index.html#bluemix_ic_service-unbind)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](index.html#unpause)</td>
 <td>[bluemix ic unprovision](index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
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

Visualizzare la guida per il plug-in `ic`:

```
bluemix help ic
```

o

```
bluemix ic help
```

Visualizzare la guida per il comando `group-create` sotto il plug-in `ic`:

```
bluemix ic help group-create
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

Installare il plugin `IBM-Containers` dell'ultima versione dal repository `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Installare il plugin `IBM-Containers` con la versione `0.5.800` dal repository `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
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

Disinstallare il plugin `IBM-Containers` che era stato precedentemente installato:

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

Controllare un contenitore in esecuzione o visualizzarne l'output. Utilizza `CTRL+C` per uscire e arrestare il contenitore. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [attach ](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>--no-stdin (facoltativo)</dt>
   <dd>Non includere l'input standard.</dd>
   <dt>--sig-proxy (facoltativo)</dt>
   <dd>Eseguire il proxy di tutti i segnali ricevuti nel processo. Il
valore predefinito è <i>true</i>.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
    </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di collegamento al contenitore `my_container`:
```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

Richiamare il servizio di build IBM Containers per creare un'immagine Docker in locale o nel tuo repository {{site.data.keyword.Bluemix_notm}} privato. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [build ](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (obbligatorio)</dt>
   <dd>Il nome repository da applicare all'immagine in fase di creazione.</dd>
   <dt>--no-cache (facoltativo)</dt>
   <dd>Non utilizzare la cache quando viene creata l'immagine. Il valore predefinito è <i>false</i>.</dd>
   <dt>--pull (facoltativo)</dt>
   <dd>Provare a estrarre l'immagine di base dal registro anche se è memorizzata nella cache.</dd>
   <dt>-q|--quiet (facoltativo)</dt>
   <dd>Sopprimere l'output dettagliato generato dai contenitori. Il valore predefinito è <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (obbligatorio)</dt>
   <dd>Il percorso verso Dockerfile e contesto sull'host locale.</dd>
    </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di creazione di un'immagine denominata *myimage*. Il Dockerfile e altre risorse utente da utilizzare nella creazione si trovano nella stessa directory da cui viene eseguito il comando. Poiché il registro e lo spazio dei nomi sono inclusi nel nome dell'immagine, l'immagine viene creata nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


### bluemix ic cp
{: #bluemix_ic_cp}
Copia file o cartelle tra un contenitore e il file system locale. Questo comando richiama la CLI Docker. Per ulteriori informazioni, vedi il comando [cp ](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.


### bluemix ic cpi
{: #bluemix_ic_cpi}

Accedere a un'immagine Docker Hub o a un'immagine dal tuo registro locale e copiarla nel tuo repository {{site.data.keyword.Bluemix_notm}} privato.

```
bluemix ic cpi IMMAGINE_DI_ORIGINE IMMAGINE_DI_DESTINAZIONE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
   <dl>
   <dt><i>IMMAGINE_DI_ORIGINE</i> (obbligatorio)</dt>
   <dd>Il nome del repository e dell'immagine di origine.</dd>
   <dt><i>IMMAGINE_DI_DESTINAZIONE</i> (obbligatorio)</dt>
   <dd>L'URL del repository {{site.data.keyword.Bluemix_notm}} privato, che include lo spazio dei nomi e il nome dell'immagine di destinazione. Una tag per l'immagine è facoltativa.</dd>
   </dl>

<strong>Esempi</strong>:

Copiare un'immagine dal repository di origine nel repository privato ed aggiungere una tag per l'immagine:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copiare l'immagine `sinatra` dal repository `training` nel repository privato `registry.ng.bluemix.net/mynamespace` e il nome dell'immagine `mysinatra`. Aggiungere una tag `v1` per l'immagine `mysinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

Eseguire un comando all'interno di un contenitore. Per ulteriori informazioni, vedi il comando [exec ](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-d|--detach (facoltativo)</dt>
   <dd>Eseguire il comando specificato in background.</dd>
   <dt>-it (facoltativo)</dt>
   <dd>Modalità interattiva. L'input standard rimane visualizzato. Immetti <i>exit</i> per uscire.</dd>
   <dt>-u <i>UTENTE</i>|--user <i>UTENTE</i> (facoltativo)</dt>
   <dd>Il nome utente.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt><i>CMD</i> (facoltativo)</dt>
   <dd>Il comando da eseguire all'interno del contenitore o dei contenitori specificati.</dd>
   </dl>

<strong>Esempi</strong>:

Eseguire il comando `bash` all'interno del contenitore `my_container` nella modalità interattiva:

```
bluemix ic exec -it my_container bash
```

Eseguire il comando `date` all'interno del contenitore `my_container`:

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

Creare un gruppo di contenitori scalabile.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (obbligatorio)</dt>
   <dd>L'immagine da includere in ciascuna istanza del contenitore del gruppo di contenitori. L'immagine può essere seguita da un elenco di comandi, ma non da opzioni. Includi tutte le opzioni prima di specificare l'immagine. <br><br>Se utilizzi un'immagine nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione, specificala con il seguente formato: <i>registry.ng.bluemix.net/SPAZIO_NOMI/IMMAGINE</i>. <br><br>Se utilizzi un'immagine fornita da IBM Containers, non includere lo spazio dei nomi della tua organizzazione. Specifica l'immagine con il seguente formato: <i>registry.ng.bluemix.net/IMMAGINE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (obbligatorio)</dt>
   <dd>Assegnare un nome al gruppo. <i>-n</i> è stato dichiarato obsoleto.<br>
   <strong>Suggerimento:</strong> il nome del contenitore deve iniziare con una lettera. Il nome può includere lettere maiuscole, lettere minuscole, numeri, punti., caratteri di sottolineatura _, o trattini -.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (facoltativo)</dt>
   <dd>Assegnare un limite di memoria al gruppo in MB. Quando crei un gruppo di contenitori dalla CLI, il valore predefinito per ogni istanza del contenitore è <i>64</i> MB. Quando crei un gruppo di contenitori dal Dashboard {{site.data.keyword.Bluemix_notm}}, il valore predefinito per ogni istanza del contenitore è <i>256</i> MB. I valori accettati sono <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> e <i>2048</i>. Una volta assegnato, il limite di memoria non può essere modificato.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (facoltativo)</dt>
   <dd>Il nome host, quale ad esempio <i>mycontainerhost</i>. L'host e il dominio si combinano per formare l'URL completo della rotta pubblica, quale ad esempio <i>http://mycontainerhost.mybluemix.net</i>. Quando esamini i dettagli di un gruppo di contenitori con il comando <i>bluemix ic group-inspect</i>, l'host e il dominio vengono elencati insieme come rotta.</dd>
   <dt>-d <i>DOMINIO</i>|--domain <i>DOMINIO</i> (facoltativo)</dt>
   <dd>Di solito, il dominio è <i>.mybluemix.net</i>. L'host e il dominio vengono combinati per formare l'URL completo della rotta pubblica, quale ad esempio <i>http://mycontainerhost.mybluemix.net</i>. Quando esamini i dettagli di un gruppo di contenitori con il comando <i>bluemix ic group-inspect</i>, l'host e il dominio vengono elencati insieme come rotta.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (facoltativo)</dt>
   <dd>Imposta la variabile di ambiente. In caso di più chiavi, elencale separatamente. Se sono incluse virgolette, includile racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  La seguente tabella mostra alcune variabili di ambiente comunemente utilizzate che puoi specificare:</dd>
    </dl>


|  Variabile di ambiente                              |     Descrizione                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nome_applicazione&gt;*       | Eseguire il bind di un servizio a un contenitore. Utilizza la variabile di ambiente `CCS_BIND_APP` per eseguire il bind di un'applicazione al contenitore. L'applicazione viene associata tramite bind al servizio di destinazione e funge da ponte che consente a {{site.data.keyword.Bluemix_notm}} di portare le informazioni `VCAP_SERVICES` dell'applicazione ponte all'istanza del contenitore in esecuzione.|
| CCS_BIND_SRV=*&lt;nome_istanza_servizio1&gt;*,*&lt;nome_istanza_servizio2&gt;* | Per eseguire direttamente il bind di un servizio Bluemix a un contenitore senza utilizzare un'applicazione ponte, utilizza CCS_BIND_SRV. Questo bind consente a Bluemix di inserire le informazioni VCAP_SERVICES nell'istanza del contenitore in esecuzione. Per elencare più servizi Bluemix, puoi includerli come parte della stessa variabile di ambiente. |
| LOG_LOCATIONS=*&lt;&gt;percorso_verso_file* | Aggiungere un file di log da monitorare nel contenitore. Includi la variabile di ambiente `LOG_LOCATIONS` in un percorso verso il file di log. |
{: caption="Table 8. Commonly used environment variables" caption-side="top"}


 <dl>
   <dt>--env-file <i>FILE_VARIABILE_AMBIENTE</i> (facoltativo)</dt>
   <dd> Importa variabili di ambiente da un file dove ENVFILE è il percorso del tuo file nella directory locale. Ogni riga nel file rappresenta una coppia key=value. </dd>
   <dt>--volume <i>VOLUME</i>:<i>PERCORSO_CONTENITORE</i>[:ro] (facoltativo)</dt>
   <dd>Collegare un volume a un contenitore, specificando i dettagli nel formato <i>IDVolume:PercorsoContenitore[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: l'ID o nome del volume.</li>
   <li><i>PERCORSO_CONTENITORE</i>: il percorso assoluto per il volume del contenitore.</li>
   <li>ro: facoltativo. La specifica di <i>ro</i> rende il volume di sola lettura invece della lettura/scrittura predefinita.</li></ul>
   </dd>
   <dt>-p <i>PORTA</i>|--publish <i>PORTA</i> (facoltativo)</dt>
   <dd>Esporre la porta per il traffico HTTP. I contenitori del tuo gruppo devono essere in ascolto sulla porta HTTP. Non possono essere effettuate richieste HTTPS. Per i gruppi di contenitori, non puoi includere più porte. <br><br>Quando specifichi una porta, stai rendendo l'applicazione disponibile al programma di bilanciamento del carico {{site.data.keyword.Bluemix_notm}} o ai contenitori che stanno provando a raggiungere l'host nello stesso spazio {{site.data.keyword.Bluemix_notm}}. Quindi i contenitori o il bilanciamento del carico {{site.data.keyword.Bluemix_notm}} possono utilizzare la porta per raggiungere l'host e l'applicazione nello stesso spazio {{site.data.keyword.Bluemix_notm}}. Se nel Dockerfile è specificata una porta per l'immagine che stai utilizzando, includila. <br>
   <strong>Suggerimenti</strong>: <ul>
   <li>Per l'immagine Liberty Server certificata da IBM o una versione modificata di questa immagine, immetti la porta 9080.</li>
   <li>Per l'immagine Node.js certificata da IBM o una versione modificata di questa immagine, immetti la porta 8000.</li>
   </ul>
   </dd>
   <dt>-P (facoltativo)</dt>
   <dd>Pubblica tutte le porte</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero minimo di istanze. Il valore predefinito è 1. Se imposti un numero minimo di istanze, una volta creato il gruppo di contenitori non è più possibile modificare questo valore.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero massimo di istanze. Il valore predefinito è 2. Se imposti un numero massimo di istanze, una volta creato il gruppo di contenitori non è più possibile modificare questo valore.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero di istanze da te richiesto. Il valore predefinito è 2.</dd>
   <dt>--auto (facoltativo)</dt>
   <dd>Quando si crea il gruppo di contenitori e il ripristino automatico è abilitato, IBM Containers verifica l'integrità di ciascuna istanza con una richiesta HTTP alla porta assegnata.<br>
   Se non viene ricevuta alcuna risposta da un'istanza del contenitore entro 2 intervalli consecutivi di 90 secondi, l'istanza viene rimossa e sostituita con una nuova istanza. Se il contenitore risponde non viene effettuata alcuna azione. Questo processo viene ripetuto continuamente. In una finestra di 30 minuti, se il numero totale di differenti contenitori membri del gruppo è uguale o 3 volte maggiore della dimensione massima osservata per il gruppo stesso, il ripristino automatico viene disabilitato in modo permanente per il gruppo di contenitori. Per abilitare di nuovo il ripristino automatico, devi ricreare il gruppo di contenitori.</dd>
  <dt>--anti (facoltativo)</dt>
  <dd> Utilizza l'opzione anti-affinity per rendere il tuo gruppo di contenitori molto più disponibile. L'opzione --anti forza l'inserimento di ogni istanza di contenitore del tuo gruppo in un nodo di elaborazione fisico separato, riducendo così la possibilità che si verifichi un arresto anomalo di tutti i contenitori nel gruppo a causa di un errore hardware. Potresti non essere in grado di utilizzare questa opzione con gruppi di dimensione maggiore in quanto ogni regione e organizzazione Bluemix ha a disposizione una serie di nodi di elaborazione limitata per la distribuzione. Se la distribuzione non riesce, riduci il numero di istanze del contenitore nel gruppo o rimuovi l'opzione --anti. </dd>
   <dt><i>CMD</i> (facoltativo)</dt>
   <dd>Il comando e gli argomenti trasmessi al gruppo di contenitori per l'esecuzione. Questo comando deve essere un comando a esecuzione prolungata. Non utilizzare un comando di breve durata che non viene eseguito per molto tempo, quale ad esempio <i>/bin/date</i>, poiché tale comando potrebbe provocare un arresto anomalo del contenitore.  <br> <strong>Note:</strong> <ul>
   <li>Il comando e i relativi argomenti devono trovarsi alla fine della riga di comando <i>bluemix ic run</i>.</li>
   <li>Se gli argomenti del comando includono il trattino -, come in <i>-c</i> nel comando di esempio precedente, il comando deve essere preceduto da due trattini (--).</li>
   </ul></dd>
   </dl>


<strong>Esempi</strong>:

Creare un gruppo di contenitori `my_container_group` utilizzando l'immagine `registry.ng.bluemix.net/ibmnode` fornita da IBM Containers, quindi eseguire il comando di lunga durata `ping localhost` su tale gruppo di contenitori:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Creare un gruppo di contenitori `my_container_group` utilizzando l'immagine `registry.ng.bluemix.net/ibmnode` fornita da IBM Containers, quindi eseguire il comando di lunga durata `tail -f /dev/null` su tale gruppo di contenitori:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Creare un gruppo scalabile `mygroup` con il ripristino automatico abilitato, utilizzando l'immagine `registry.ng.bluemix.net/ibmliberty`. La porta è `9080`, il nome host è `mycontainerhost`, il nome dominio è `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Visualizzare informazioni dettagliate, quali le variabili di ambiente, le porte o la memoria, specificate per un gruppo di contenitori al momento della creazione.

```
bluemix ic group-inspect GRUPPO_CONTENITORI
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di controllo del gruppo di contenitori `my_group`:
```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

Elencare istanze di un gruppo di contenitori specificato.

```
bluemix ic group-instances GRUPPO_CONTENITORI
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Elencare tutte le istanze del gruppo di contenitori `my_group`:
```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

Rimuovere un gruppo di contenitori da uno spazio.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-f|--force (facoltativo)</dt>
   <dd>Forza la rimozione di un contenitore in esecuzione o in errore.</dd>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di un gruppo di contenitori, dove `my_group` è il nome del gruppo di contenitori.
```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

Aggiornare un gruppo di contenitori.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Suggerimento:** per aggiornare il nome host o il dominio di un gruppo di contenitori, utilizza `bluemix ic route-map [-n HOST][-d DOMAIN] GRUPPO_CONTENITORI`.

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
 <dl>
   <dt>--anti (facoltativo)</dt>
   <dd>Utilizza l'opzione anti-affinity per rendere il tuo gruppo di contenitori molto più disponibile. L'opzione --anti forza l'inserimento di ogni istanza di contenitore del tuo gruppo in un nodo di elaborazione fisico separato, riducendo così la possibilità che si verifichi un arresto anomalo di tutti i contenitori nel gruppo a causa di un errore hardware. Potresti non essere in grado di utilizzare questa opzione con gruppi di dimensione maggiore in quanto ogni regione e organizzazione Bluemix ha a disposizione una serie di nodi di elaborazione limitata per la distribuzione. Se la distribuzione non riesce, riduci il numero di istanze del contenitore nel gruppo o rimuovi l'opzione --anti.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (facoltativo)</dt>
   <dd>Il numero di istanze da te richiesto. Il valore predefinito è <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(facoltativo)</dt>
   <dd>Imposta la variabile di ambiente. In caso di più chiavi, elencale separatamente. Se sono incluse virgolette, includile racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di aggiornamento del gruppo di contenitori `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

Elencare i gruppi di contenitori nel repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione.

```
bluemix ic groups [-q]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:
	<dl>
	<dt>-q (facoltativo)</dt>
   	<dd>Visualizza solo gli ID gruppo</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

Visualizzare un elenco di tutte le immagini disponibili nel repository {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione. Per ulteriori informazioni, vedi il comando [images ](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker. L'elenco include l'ID immagine, la data di creazione e il nome dell'immagine.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-a|--all (facoltativo)</dt>
   <dd>Includere tutti i livelli di immagine per ciascuna immagine del repository dell'organizzazione e non solo il più recente.</dd>
   <dt>-f (facoltativo)</dt>
   <dd>Filtrare l'elenco di immagini in base alla condizione fornita.</dd>
   <dt>--no-trunc (facoltativo)</dt>
   <dd>Non troncare l'output.</dd>
   <dt>-q|--quiet (facoltativo)</dt>
   <dd>Visualizzare solo gli ID numerici.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di elenco delle immagini disponibili per l'organizzazione:
```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

Visualizzare un insieme di informazioni che descrivono lo stato dell'istanza del servizio cloud del contenitore. Le informazioni includono limite dei contenitori, utilizzo dei contenitori, contenitori in esecuzione, limite di memoria, utilizzo della memoria, limite dell'indirizzo IP mobile, utilizzo dell'indirizzo IP mobile, URL host CCS, URL host del registro e stato della modalità di debug.

```
bluemix ic info
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


### bluemix ic init
{: #bluemix_ic_init}

Inizializzare l'ambiente dei contenitori sulla macchina locale in uso per sfruttare appieno le funzioni del servizio IBM Containers.

```
bluemix ic init
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

**Nota:** prima dell'inizializzazione, accertati che la CLI Docker (docker) sia installata e configurato nella tua variabile di ambiente PATH. Per passare a un'altra regione, utilizza il comando `bluemix region-set`.

<strong>Esempi</strong>:

Passare alla regione `us-south`:

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

Visualizzare le informazioni su un contenitore. Per ulteriori informazioni, vedi il comando [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} nella guida di Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IMAGE</i> (obbligatorio)</dt>
   <dd>Visualizzare informazioni dettagliate su un'immagine specifica indicando l'ID o il nome dell'immagine.</dd>
   <dt>images (obbligatorio)</dt>
   <dd>Visualizzare informazioni dettagliate su tutte le immagini del tuo repository.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Visualizzare informazioni dettagliate su un contenitore specifico, indicando l'ID o il nome del contenitore.</dd>
   </dl>

**Suggerimento:** non è possibile specificare *IMMAGINE*, *images* o il *CONTENITORE* contemporaneamente.

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di controllo di un contenitore denominato `proxy`:
```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Eseguire il bind di un indirizzo IP a virgola mobile disponibile a un contenitore.

```
bluemix ic ip-bind CONTENITORE INDIRIZZO_IP
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obbligatorio)</dt>
   <dd>L'indirizzo IP da associare mediante bind.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore da associare mediante bind.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di bind dell'indirizzo IP `192.123.12.12 al` contenitore `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

Rilasciare un indirizzo IP a virgola mobile dall'istanza del servizio cloud del contenitore.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obbligatorio)</dt>
   <dd>L'indirizzo IP da rilasciare.</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
Richiedere un nuovo indirizzo IP mobile.

```
bluemix ic ip-request [-q]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-q (facoltativo)</dt>
   <dd>Elenca solo gli indirizzi IP, senza l'ID per i contenitori associati a tali indirizzi IP.</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Annullare il bind di un indirizzo IP a virgola mobile dal relativo contenitore.

Gli indirizzi IP pubblici sono una risorsa limitata di IBM Containers. Pertanto, gli indirizzi IP pubblici assegnati a uno spazio e non associati mediante bind a un contenitore vengono recuperati periodicamente dagli utenti della versione di prova, approssimativamente su base settimanale. Gli indirizzi IP non associati non sono mai recuperati dai clienti con pagamento a consumo o con una sottoscrizione.

```
bluemix ic ip-unbind INDIRIZZO_IP CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obbligatorio)</dt>
   <dd>L'indirizzo IP da scollegare.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore da scollegare.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di annullamento del bind dell'indirizzo IP `192.123.12.12` dal contenitore `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

Elencare gli indirizzi IP a virgola mobile disponibili per l'utente che ha effettuato l'accesso. L'elenco include gli indirizzi IP e l'ID contenitore a cui sono collegati gli indirizzi IP. Se l'indirizzo IP non è in uso, non verrà visualizzato alcun ID contenitore.

```
bluemix ic ips [-q]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-q (facoltativo)</dt>
   <dd>Elenca solo gli indirizzi IP, senza l'ID per i contenitori associati a tali indirizzi IP.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta per ricevere un elenco di tutti gli indirizzi IP per l'organizzazione.
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

Arrestare un processo in esecuzione in un contenitore senza arrestare il contenitore. Per ulteriori informazioni, vedi il comando [kill ](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (facoltativo)</dt>
   <dd>Inviare un comando al processo in esecuzione nel contenitore.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di terminazione di un contenitore denominato `proxy`:
```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

Mostra i log di output o di errore per un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [logs ](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Visualizzare il nome del repository di immagini {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione a cui sei collegato.

```
bluemix ic namespace-get
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Impostare il nome del repository di immagini {{site.data.keyword.Bluemix_notm}} privato dell'organizzazione a cui sei collegato.

*Limitazione*: non puoi utilizzare un trattino `-` nel nome del tuo spazio dei nomi del repository.

```
bluemix ic namespace-set NOME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME</i> (obbligatorio)</dt>
   <dd>Una funzione da eseguire una sola volta per impostare lo spazio dei nomi del repository per la tua organizzazione, se non già impostato. Una volta impostato lo spazio dei nomi, reinizializza IBM Containers attraverso il comando `bluemix ic init` prima di continuare.</dd>
   </dl>


### bluemix ic pause
{: #pause}

Mettere in pausa tutti i processi all'interno di un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [pause ](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker. Per arrestare un contenitore, vedi il comando [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:
   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Risposte</strong>:

- Contenitore correttamente in pausa.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di messa in pausa di un contenitore denominato `proxy`:
```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

Elenca le associazioni delle porte o un'associazione specifica del contenitore. Questo comando include il comando `docker port`. Per ulteriori informazioni, vedi il comando [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.


### bluemix ic ps
{: #bluemix_ic_ps}
Visualizzare un elenco di contenitori in esecuzione nello spazio dei nomi dell'utente che ha effettuato l'accesso. Per impostazione predefinita, questo comando mostra solo i contenitori in esecuzione. Per ulteriori informazioni, vedi il comando [ps ](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-a|--all (facoltativo)</dt>
   <dd>Visualizzare tutti i contenitori, sia quelli in esecuzione sia quelli arrestati.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (facoltativo)</dt>
   <dd>Cerca i contenitori che hanno uno specifico valore di variabile di ambiente. Puoi filtrare i tuoi contenitori in base a qualsiasi chiave o valore di variabile di ambiente elencato nella sezione Env della tua risposta CLI quando ispezioni un contenitore. Sostituisci SEARCH_CRITERIA con la chiave o valore che stai cercando. I tuoi criteri di ricerca non devono necessariamente essere una corrispondenza esatta. </dd>
   <dt>-s|--size (facoltativo)</dt>
   <dd>Elencare le dimensioni dei contenitori.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (facoltativo)</dt>
   <dd>Elencare i contenitori creati più di recente, dove <i>NUM</i> è il numero dei contenitori creati più di recente che desideri restituire. <br><br> Ad esempio, se hai creato i contenitori da <i>node1</i> a <i>node5</i> in modo sequenziale, il comando <i>bluemix ic ps --limit 2</i> restituisce node4 e node5 perché sono gli ultimi due contenitori creati. </dd>
   <dt>-q|--quiet (facoltativo)</dt>
   <dd>Visualizzare solo gli ID contenitore.</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di visualizzazione di tutti i contenitori in esecuzione e arrestati:
```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
Rinomina un contenitore. Per ulteriori informazioni, vedi il comando [rename ](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

<dl>
   <dt><i>OLD_NAME</i> (obbligatorio)</dt>
   <dd>Il vecchio nome del contenitore.</dd>
   <dt><i>NEW_NAME</i> (obbligatorio)</dt>
   <dd>Il nuovo nome del contenitore.</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

Ricrea il servizio IBM Containers nello spazio Bluemix a cui sei collegato. La quota originale per lo spazio viene mantenuta.

<strong>Importante</strong>: quando esegui questo comando, nessuno dei tuoi singoli contenitori e gruppi in questo spazio verrà migrato nello spazio di cui è stato eseguito di nuovo il provisioning e verranno rimossi durante il processo di migrazione.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Opzioni del comando</strong>:

<dl>
   <dt>--force|-f (facoltativo)</dt>
   <dd>Forza la nuova creazione del servizio IBM Containers nello spazio Bluemix.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (facoltativo)</dt>
   <dd>Il nome della zona di disponibilità IBM Containers in cui vengono distribuiti i tuoi contenitori. Se non si specifica alcuna zona di disponibilità, viene utilizzata la zona predefinita impostata per la regione.</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

Riavviare un contenitore. Per ulteriori informazioni, vedi il comando [restart ](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt>-t <i>SECONDI</i>|--time <i>SECONDI</i> (facoltativo)</dt>
   <dd>Il numero di secondi di attesa prima che il contenitore venga riavviato.</dd>
   </dl>


<strong>Risposte</strong>:

- Contenitore riavviato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di riavvio di un contenitore denominato `proxy`:
```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

Rimuovere un contenitore. Per ulteriori informazioni, vedi il comando [rm ](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-f|--force (facoltativo)</dt>
   <dd>Forza la rimozione di un contenitore in esecuzione o in errore.</dd>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Risposte</strong>:

- Contenitore rimosso correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore.

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di un contenitore denominato `proxy`:
```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

Rimuovere un'immagine dallo spazio dei nomi dell'utente che ha effettuato l'accesso. Per ulteriori informazioni, vedi il comando [rmi ](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-R <i>REGISTRO</i>|--registry <i>REGISTRO</i> (facoltativo)</dt>
   <dd>Modificare l'host del registro. Per impostazione predefinita verrà utilizzato il registro che hai specificato nel comando <i>bluemix ic init</i>.</dd>
   <dt><i>IMAGE</i> (obbligatorio)</dt>
   <dd>Il nome dell'immagine che desideri rimuovere. Se non viene specificata
una tag nel nome immagine, per impostazione predefinita viene eliminata
l'immagine contrassegnata come <i>latest</i>.</dd>
   </dl>

<strong>Risposte</strong>:

- Rimozione di: `{IMMAGINE}`

 Dove `{IMMAGINE}` è il
nome dell'immagine che è stata rimossa.

- Errore. Nessun host registro specificato.

- Rimozione dell'immagine non riuscita - Impossibile connettersi al registro cloud del contenitore

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione dell'immagine `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

Stabilire la rotta per il traffico internet da utilizzare per accedere al gruppo di contenitori. Puoi utilizzare questo comando per stabilire una nuova rotta o aggiornarne una esistente.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (facoltativo)</dt>
   <dd>Il nome host della rotta. Il nome host costituisce la prima parte dell'URL completo della rotta pubblica, quale ad esempio <i>mycontainerhost</i> nell'URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMINIO</i>|--domain <i>DOMINIO</i> (facoltativo)</dt>
   <dd>Il nome dominio della rotta, che costituisce la seconda parte dell'URL completo della rotta pubblica. Nella maggior parte dei casi, il dominio è <i>mybluemix.net</i>. Puoi anche utilizzare questo parametro per specificare un dominio privato.</dd>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di associazione della rotta del gruppo denominato `GROUP1`, dove `my_host` è il nome host e `mybluemix.net` è il dominio.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Stabilire la rotta per il traffico internet da utilizzare per accedere al gruppo di contenitori. Puoi utilizzare questo comando per stabilire una nuova rotta o aggiornarne una esistente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (facoltativo)</dt>
   <dd>Il nome host della rotta.</dd>
   <dt>-d <i>DOMINIO</i>|--domain <i>DOMINIO</i> (facoltativo)</dt>
   <dd>Il nome dominio della rotta.</dd>
   <dt><i>GRUPPO_CONTENITORI</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del gruppo di contenitori.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di annullamento dell'associazione della rotta del gruppo denominato `GRUPPO1`, dove `mio_host` è il nome dell'host e `organization.com` è il dominio.
```
bluemix ic route-unmap -n mio_host -d organization.com GRUPPO1
```


### bluemix ic run
{: #bluemix_ic_run}

Avviare un nuovo contenitore nel servizio cloud del contenitore da
un nome immagine. Per ulteriori informazioni, vedi il comando [run ](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.


```
bluemix ic run [-p PORT|--publish PORTA] [-P] [-m MEMORIA|--memory MEMORIA] [-e ENV|--env ENV] [--volume VOLUME:PERCORSO_CONTENITORE] -n NOME|--name NOME [--link NOME:ALIAS] [-it] IMMAGINE [CMD [CMD ...]]
```
**Nota:** accertati che lo strumento di comando Cloud Foundry sia installato e di disporre di un token Cloud Foundry. Se si accede correttamente tramite `bluemix login` e `bluemix ic init` vengono creati i certificati e i token richiesti.


<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt>-p <i>PORTA</i>|--publish <i>PORTA</i> (facoltativo)</dt>
   <dd>Esporre la porta per il traffico HTTP. Includi le eventuali porte specificate nel Dockerfile per l'immagine che stai utilizzando. Puoi includere più porte con più opzioni <i>-p</i>. L'esposizione di una porta comporta automaticamente il bind di un indirizzo IP pubblico, se disponibile, al contenitore. <br><br>Se disponi già di un indirizzo IP nello spazio che desideri associare mediante bind al contenitore, puoi specificare l'indirizzo IP invece di eseguirne il bind successivamente. L'indirizzo IP deve essere specificato nel seguente formato: &lt;indirizzo_IP&gt;:&lt;porta_contenitore&gt;:&lt;porta_contenitore&gt; <br><br>Per ulteriori informazioni sulla richiesta di indirizzi IP per uno spazio, vedi il comando <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Quando specifichi una porta, stai rendendo l'applicazione disponibile al programma di bilanciamento del carico {{site.data.keyword.Bluemix_notm}} o ai contenitori dello stesso spazio {{site.data.keyword.Bluemix_notm}} che stanno provando a raggiungere l'host. Se nel Dockerfile è specificata una porta per l'immagine che stai utilizzando, includila. <br><br><strong>Suggerimenti:</strong><ul><li>Per l'immagine Liberty Server certificata da IBM o una versione modificata di questa immagine, immetti la porta 9080.</li><li>Per l'immagine Node.js certificata da IBM o una versione modificata di questa immagine, immetti la porta 8000.</li></ul></dd>
   <dt>-P (facoltativo)</dt>
   <dd>Esporre automaticamente le porte specificate nel Dockerfile dell'immagine per il traffico HTTP.</dd>
   <dt>-m <i>MEMORIA</i>|--memory <i>MEMORIA</i> (facoltativo)</dt>
   <dd>Assegnare un limite di memoria al gruppo in MB. Quando crei un gruppo di contenitori dalla CLI, il valore predefinito per ogni istanza del contenitore è 64 MB.  Quando crei un gruppo di contenitori dal Dashboard {{site.data.keyword.Bluemix_notm}}, il valore predefinito per ciascuna istanza è 256 MB. I valori accettati sono 64, 256, 512, 1024 e 2048. Una volta assegnato, il limite di memoria non può essere modificato.</dd>
   <dt>-e <i>AMB</i>|--env <i>AMB</i> (facoltativo)</dt>
   <dd>Impostare la variabile di ambiente, dove <i>AMB</i> è una coppia chiave=valore. In caso di più chiavi, elencale separatamente. Se includi virgolette, fallo racchiudendo sia il valore che il nome della variabile di ambiente. Ad esempio: -e "key1=value1" -e "key2=value2" -e "key3=value3". La seguente tabella mostra alcune variabili di ambiente comunemente utilizzate che puoi specificare:</dd>
   </dl>


|      Variabile di ambiente                          |   Descrizione                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nome_applicazione&gt;*       | Eseguire il bind di un servizio a un contenitore. Utilizza la variabile di ambiente `CCS_BIND_APP` per eseguire il bind di un'applicazione al contenitore. L'applicazione viene associata mediante bind al servizio di destinazione e funge da ponte che consente a {{site.data.keyword.Bluemix_notm}} di portare le informazioni `VCAP_SERVICES` dell'applicazione ponte nell'istanza del contenitore in esecuzione. Per ulteriori informazioni sulla creazione di un'applicazione ponte, vedi [Esecuzione del bind di un servizio a un contenitore](/docs/containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nome_istanza_servizio1&gt;*,*&lt;nome_istanza_servizio2&gt;* | Per eseguire direttamente il bind di un servizio Bluemix a un contenitore senza utilizzare un'applicazione ponte, utilizza CCS_BIND_SRV. Questo bind consente a Bluemix di inserire le informazioni VCAP_SERVICES nell'istanza del contenitore in esecuzione. Per elencare più servizi Bluemix, puoi includerli come parte della stessa variabile di ambiente. |
| LOG_LOCATIONS=*&lt;&gt;percorso_verso_file* | Aggiungere un file di log da monitorare nel contenitore. Includi la variabile di ambiente `LOG_LOCATIONS` in un percorso verso il file di log. |
{: caption="Table 9. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>PERCORSO_CONTENITORE</i>[:ro] (facoltativo)</dt>
   <dd>Collegare un volume a un contenitore, specificando i dettagli nel formato <i>IDVolume:PercorsoContenitore[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: l'ID o nome del volume.</li>
   <li><i>PERCORSO_CONTENITORE</i>: il percorso assoluto per il volume del contenitore.</li>
   <li>ro: facoltativo. La specifica di <i>ro</i> rende il volume di sola lettura invece della lettura/scrittura predefinita.</li></ul>
   </dd>
   <dt>-n <i>NOME</i>|--name <i>NOME</i> (facoltativo)</dt>
   <dd>Assegnare un nome al contenitore. <br> <strong>Suggerimento:</strong> il nome del contenitore deve iniziare con una lettera. Il nome può includere lettere maiuscole, lettere minuscole, numeri, punti., caratteri di sottolineatura _, o trattini -.</dd>
   <dt>--link <i>NOME</i>:<i>ALIAS</i> (facoltativo)</dt>
   <dd>Ogni volta che desideri che un contenitore comunichi con un altro contenitore in esecuzione, puoi farvi riferimento utilizzando un alias del nome host.</dd>
   <dt>-it (facoltativo)</dt>
   <dd>Eseguire il contenitore in modalità interattiva. Una volta creato il contenitore, mantieni l'input standard visualizzato. Immetti <i>exit</i> per uscire.</dd>
   <dt><i>IMAGE</i> (obbligatorio)</dt>
   <dd>L'immagine da includere nel contenitore. L'immagine può essere seguita da un elenco di comandi, ma non da opzioni. Includi tutte le opzioni prima di specificare un'immagine. Includi tutte le opzioni prima di specificare l'immagine. <br><br>Se utilizzi un'immagine nel repository {{site.data.keyword.Bluemix_notm}} privato della tua organizzazione, specificala con il seguente formato: <i>registry.ng.bluemix.net/SPAZIO_NOMI/IMMAGINE</i>. <br><br>Se utilizzi un'immagine fornita da IBM Containers, specificala nel seguente formato: <i>registry.ng.bluemix.net/IMMAGINE</i>. </dd>
   <dt><i>CMD</i> (facoltativo)</dt>
   <dd>Il comando e gli argomenti trasmessi al gruppo di contenitori per l'esecuzione. Questo comando deve essere un comando a esecuzione prolungata. Non utilizzare un comando di breve durata che non viene eseguito per molto tempo, quale ad esempio <i>/bin/date</i>, poiché tale comando potrebbe provocare un arresto anomalo del contenitore.</dd>
   </dl>


<strong>Esempi</strong>:

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


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

Aggiungi un servizio a un gruppo di contenitori in esecuzione. Questo comando è disponibile solo per i gruppi di contenitori. I singoli contenitori devono essere associati tramite bind a un servizio come parte del comando bluemix ic run.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>L'ID o il nome del gruppo.</dd>
   <dt><i>ISTANZA_SERVIZIO</i> (obbligatorio)</dt>
   <dd>Il nome dell'istanza del servizio da aggiungere al gruppo di contenitori.</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Rimuovi un servizio da un gruppo di contenitori in esecuzione. Questo comando è disponibile solo per i gruppi di contenitori. I singoli contenitori devono rimuovere il contenitore e crearne uno nuovo senza il servizio.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME GRUPPO</i> (obbligatorio)</dt>
   <dd>L'ID o il nome del gruppo.</dd>
   <dt><i>ISTANZA_SERVIZIO</i> (obbligatorio)</dt>
   <dd>Il nome dell'istanza del servizio da aggiungere al gruppo di contenitori.</dd>
   </dl>


### bluemix ic start
{: #ic_start}
Avviare un contenitore arrestato. Per ulteriori informazioni, vedi il comando [start ](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker. Per arrestare un contenitore, vedi il comando [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>


<strong>Risposte</strong>:

- Contenitore avviato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di avvio di un contenitore denominato `proxy`.
```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

Visualizzare le statistiche di utilizzo in tempo reale per uno o più contenitori. Utilizza `CTRL+C` per chiudere. Per ulteriori informazioni, vedi il comando [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} nella guida di Docker.

```
bluemix ic stats [--no-stream] CONTENITORE [CONTENITORE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt>--no-stream (facoltativo)</dt>
   <dd>Visualizzare solo il risultato più recente, senza includere informazioni precedenti.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di visualizzazione delle statistiche più recenti su un contenitore:
```
bluemix ic stats --no-stream mio_contenitore
```


### bluemix ic stop
{: #ic_stop}
Arrestare un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [stop ](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker. Per avviare un contenitore, vedi il comando [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   <dt>-t <i>SECONDI</i>|--time <i>SECONDI</i> (facoltativo)</dt>
   <dd>Il numero di secondi di attesa prima che il contenitore venga arrestato.</dd>
   </dl>

<strong>Risposte</strong>:

- Contenitore arrestato correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di arresto di un contenitore denominato `proxy`.
```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

Mostrare i processi in esecuzione nel contenitore. Per ulteriori informazioni, vedi il comando [top ](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic top CONTENITORE [CONTENITORE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di visualizzazione dei processi di un contenitore denominato `mio_contenitore`.
```
bluemix ic top mio_contenitore
```


### bluemix ic unpause
{: #unpause}

Riprendere tutti i processi all'interno di un contenitore in esecuzione. Per ulteriori informazioni, vedi il comando [unpause ](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker. Per mettere in pausa un contenitore, vedi il comando [bluemix ic pause](#pause).

```
bluemix ic unpause CONTENITORE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Risposte</strong>:

- Esecuzione del contenitore ripresa correttamente.

- Comando non riuscito con il servizio cloud del contenitore

 `{messaggio}`

 Dove `{messaggio}` è
l'errore correlato.

- Comando non riuscito - Impossibile connettersi al servizio cloud del contenitore

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di ripresa dell'esecuzione di un contenitore denominato `proxy`:
```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

Elimina il servizio IBM Containers dallo spazio Bluemix a cui sei collegato.

<strong>Attenzione</strong>: quando esegui questo comando, tutti i tuoi singoli contenitori e gruppi di contenitori vengono persi. Il tuo spazio sarà ancora disponibile in Bluemix. Per iniziare a utilizzare di nuovo IBM Containers, devi eseguire `bluemix ic reprovision` per effettuare nuovamente il provisioning del servizio IBM Containers.

```
bluemix ic reprovision [--force|-f]
```
<strong>Opzioni del comando</strong>:

<dl>
   <dt>--force|-f (facoltativo)</dt>
   <dd>Forza l'eliminazione di Bluemix dallo spazio Bluemix.</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

Mostrare la versione di Docker e dell'API IBM Containers.

```
bluemix ic version
```

<strong>Prerequisiti</strong>:  Docker

Per visualizzare la versione di IBM Containers, eseguire `bluemix ic info`. Per ulteriori informazioni, vedi il comando [version ](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

Creare un volume.

```
bluemix ic volume-create NOME_VOLUME NOME_FS
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_FS</i> (facoltativo)</dt>
   <dd>Il nome della condivisione file. Se non viene denominata o non è disponibile alcuna condivisione file, il volume sarà creato nella condivisione file predefinita dello spazio.</dd>
   <dt><i>NOME_VOLUME</i> (obbligatorio)</dt>
   <dd>Il nome del volume. Il nome può contenere lettere minuscole, numeri, caratteri di sottolineatura (_) e trattini (-).</dd>
   </dl>


<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di creazione di un volume.
```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Elencare le condivisioni file.

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Creare una condivisione file.

```
bluemix ic volume-fs-create NOME_CONDIVISIONE_FILE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_CONDIVISIONE_FILE</i> (obbligatorio)</dt>
   <dd>Il nome della condivisione file. Il nome può contenere lettere minuscole, numeri, caratteri di sottolineatura (_) e trattini (-).</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di creazione di una condivisione file.
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Elencare tutte le caratteristiche della condivisione file.

```
bluemix ic volume-fs-flavors
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Ispezionare una condivisione file.

```
bluemix ic volume-fs-inspect NOME_CONDIVISIONE_FILE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

  <dl>
  <dt><i>NOME_CONDIVISIONE_FILE</i> (obbligatorio)</dt>
   <dd>Il nome della condivisione file.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio è una richiesta di ispezione di una condivisione file, dove `my_file_share` è il nome della condivisione file.
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Rimuovere una condivisione file.

```
bluemix ic volume-fs-remove NOME_CONDIVISIONE_FILE
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_CONDIVISIONE_FILE</i> (obbligatorio)</dt>
   <dd>Il nome della condivisione file.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di una condivisione file, dove `my_file_share` è il nome della condivisione file.
```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Ispezionare un volume.

```
bluemix ic volume-inspect NOME_VOLUME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_VOLUME</i> (obbligatorio)</dt>
   <dd>Il nome del volume.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio è una richiesta di ispezione di un volume, dove `nome_volume` è il nome del volume.
```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Rimuovere un volume.

```
bluemix ic volume-remove NOME_VOLUME
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>NOME_VOLUME</i> (obbligatorio)</dt>
   <dd>Il nome del volume.</dd>
    </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di rimozione di un volume, dove `nome_volume` è il nome del volume.
```
bluemix ic volume-remove nome_volume
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

Elencare i volumi.

```
bluemix ic volumes
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione


### bluemix ic wait
{: #bluemix_ic_wait}

Chiudere un contenitore e visualizzare il codice di uscita come conferma. Per ulteriori informazioni, vedi il comando [wait ](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg) nella guida di Docker.

```
bluemix ic wait CONTENITORE [CONTENITORE]
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di chiusura di un contenitore denominato `mio_contenitore`:
```
bluemix ic wait mio_contenitore
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

Attendere che un singolo contenitore o gruppo di contenitori raggiunga lo stato non temporaneo. Durante questo tempo di attesa, la riga di comando non viene restituita e non puoi immettere i comandi. Non appena il contenitore raggiunge lo stato non temporaneo, viene visualizzato il messaggio OK. Per i singoli contenitori, gli stati non temporanei includono In esecuzione, Arresto, Arresto anomalo, In pausa o Sospeso. Per i gruppi di contenitori, gli stati non temporanei includono CREATE_COMPLETE, UPDATE_COMPLETE o FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Prerequisiti</strong>:  Endpoint, Accesso, Destinazione, Docker

<strong>Opzioni del comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obbligatorio)</dt>
   <dd>Il nome o l'ID del contenitore.</dd>
   </dl>

<strong>Esempi</strong>:

Il seguente esempio mostra una richiesta di chiusura di un contenitore denominato `mio_contenitore`:
```
bluemix ic wait mio_contenitore
```



# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![icona link esterno](../../../icons/launch-glyph.svg)
