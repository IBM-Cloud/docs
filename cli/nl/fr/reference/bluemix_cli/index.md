---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}
{: #getting-started}

L'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} vous permet d'interagir avec vos applications, vos serveurs virtuels, vos conteneurs et d'autres services via une interface de ligne de commande. L'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} intègre également des outils de communauté, comme l'interface de ligne de commande Cloud Foundry, l'interface de ligne de commande Docker et l'interface de ligne de commande OpenStack, et initialise des paramètres d'environnement qui vous permettent d'interagir avec différents types de traitement.

**Restriction** : l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} n'est pas prise en charge par Cygwin. Ne l'utilisez donc pas dans la fenêtre de ligne de commande Cygwin.

**Remarque** : si votre réseau comporte un serveur proxy HTTP entre l'hôte qui exécute l'interface de ligne de commande et {{site.data.keyword.Bluemix_notm}}, vous devez spécifier le nom d'hôte ou l'adresse IP du serveur proxy dans la variable d'environnement HTTP_PROXY.

## Installation de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}
{: #install_bluemix_cli}

Avant d'installer l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, installez l'[l'interface de ligne de commande cf ![icône de lien externe](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

Pour Mac OS et Windows, téléchargez le [package de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#downloads) et exécutez le programme d'installation.

Pour Linux, procédez comme suit :

  1. Téléchargez le package, et décompressez-le. Par exemple :

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

  2. Accédez au répertoire `Bluemix_CLI`, puis exécutez la commande `./install_bluemix_cli` avec les droits root. Vous pouvez exécuter la commande en tant qu'utilisateur root ou utiliser la commande `sudo` afin d'obtenir les droits root. Par exemple :

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

Vous pouvez maintenant commencer à utiliser l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} ou installer des plug-in supplémentaires.

## Installation d'un plug-in
{: #install_plug-in}

A l'instar de l'interface de ligne de commande Cloud Foundry, l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} prend en charge une infrastructure d'extension de plug-in permettant d'ajouter des commandes aux commandes intégrées.

Pour installer un plug-in depuis votre environnement local, procédez comme suit :

  1. Téléchargez le plug-in. Par exemple :

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

  2. Pour les systèmes similaires à UNIX, vous devez rendre le fichier téléchargé exécutable avec la commande `chmod`. Par exemple :

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Installez le plug-in à l'aide de la commande `bluemix plugin install`. Par exemple :

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Pour procéder à l'installation depuis un serveur distant,
procédez comme suit :

  1. Installez le plug-in directement depuis une adresse URL
distante à l'aide de la commande `bluemix plugin install`. Par exemple :

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Vous pouvez également installer un plug-in depuis le référentiel. {{site.data.keyword.Bluemix_notm}}
possède des référentiels qui hébergent les plug-in de l'interface de ligne de
commande {{site.data.keyword.Bluemix_notm}} et les plug-in de
l'interface de ligne de commande Cloud Foundry :

  * le [référentiel des plug-in de l'interface de ligne de commande Cloud Foundry ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg), qui héberge les plug-in de l'interface de ligne de commande Cloud Foundry,
  * le [référentiel des plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg), qui héberge les plug-in spécifiques à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

Pour procéder à l'installation depuis les référentiels, procédez comme
suit :

  1. Recherchez le plug-in dans le référentiel. Une fois l'interface
de ligne de commande {{site.data.keyword.Bluemix_notm}} installée, le
référentiel officiel `Bluemix` est ajouté par défaut. Vous
pouvez afficher la liste des plug-in du référentiel `Bluemix`
à l'aide de la commande `bluemix plugin repo-plugins`. Par exemple :

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Installez le plug-in depuis le référentiel `Bluemix` à l'aide de la commande `bluemix plugin install`. Par exemple :

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## Connexion à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}
{: #log_bmcli}

Après avoir installé l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, vous pouvez vous connecter à {{site.data.keyword.Bluemix_notm}} à l'aide de votre IBMid et de votre mot de passe. Par exemple :

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

Vous êtes désormais prêt à utiliser les commandes {{site.data.keyword.Bluemix_notm}} intégrées. Par exemple, exécutez la commande `bluemix catalog templates` pour répertorier tous les modèles de conteneur boilerplate {{site.data.keyword.Bluemix_notm}} disponibles.

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

# Commandes {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

Version : 0.4.6

L'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} fournit un ensemble de commandes qui sont regroupées par espace de nom pour que les utilisateurs puissent interagir avec {{site.data.keyword.Bluemix_notm}}. Certaines commandes {{site.data.keyword.Bluemix_notm}} sont des encapsuleurs de commandes cf existantes, tandis que d'autres fournissent des capacités étendues aux utilisateurs {{site.data.keyword.Bluemix_notm}}. La liste ci-dessous répertorie les commandes prises en charge par l'interface de ligne de commande de {{site.data.keyword.Bluemix_notm}}, en indiquant leurs noms, leurs options, leur syntaxe, leurs prérequis, leurs descriptions, et des exemples.
{:shortdesc}

**Remarque :** la zone *Prérequis* répertorie les actions qui sont requises avant l'utilisation de la commande. Les commandes pour lesquelles aucune action n'est requise indiquent **Aucun**. Sinon, les prérequis peuvent inclure une ou plusieurs des actions suivantes :

<dl>
<dt>Noeud final</dt>
<dd>Un noeud final d'API doit être défini via <code>bluemix api</code> avant l'utilisation de la commande.</dd>
<dt>Connexion</dt>
<dd>La connexion avec la commande <code>bluemix login</code> est requise avant l'utilisation de cette commande. Si vous vous connectez à l'aide d'un ID fédéré, utilisez l'option '--sso' pour vous authentifier avec un code d'accès unique.</dd>
<dt>Cible</dt>
<dd>La commande <code>bluemix target</code> doit être utilisée pour définir une organisation et un espace avant l'utilisation de cette commande.</dd>
<dt>Docker</dt>
<dd>L'interface de ligne de commande Docker (docker) doit être installée pour que vous puissiez exécuter cette commande.</dd>
</dl>

## Index des commandes Bluemix
{: #bx_commands_index}

Utilisez les index des tableaux suivants pour examiner les commandes Bluemix fréquemment utilisées.

**Remarque :** vous pouvez utiliser le format abrégé
des commandes Bluemix. Par exemple, `bx api` est la forme
abrégée de `bluemix api`.


<table summary="Commandes générales Bluemix.">
<caption>Tableau 1. Commandes générales Bluemix</caption>
 <thead>
 <th colspan="5">Commandes générales Bluemix</th>
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


<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer les organisations, les espaces et les utilisateurs.">
<caption>Tableau 2. Commandes pour la gestion d'organisations, d'espaces et d'utilisateurs</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion d'organisations, d'espaces et d'utilisateurs</th>
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


<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer des applications Cloud Foundry.">
<caption>Tableau 3. Commandes pour la gestion d'applications cf</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion d'applications cf</th>
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


<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer des services Bluemix.">
<caption>Tableau 4. Commandes pour la gestion de services Bluemix</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion de services Bluemix</th>
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


<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer un catalogue, des plug-in, la facturation et les paramètres de sécurité Bluemix.">
<caption>Tableau 5. Commandes pour la gestion du catalogue, des plug-in, de la facturation et des paramètres de sécurité Bluemix</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion du catalogue, des plug-in, de la facturation et des paramètres de sécurité Bluemix</th>
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


<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer les paramètres réseau.">
<caption>Tableau 6. Commandes pour la gestion des paramètres réseau</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion des paramètres réseau</th>
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

<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer des conteneurs dans Bluemix.">
<caption>Tableau 7. Commandes pour la gestion de conteneurs dans Bluemix</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion de conteneurs dans Bluemix</th>
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
Affichez l'aide générale pour les commandes intégrées de premier niveau et les espaces de nom pris en charge de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, ou l'aide d'une commande intégrée ou d'un espace de nom spécifique.

```
bluemix help [COMMANDE|ESPACE DE NOM]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>COMMANDE|ESPACE DE NOM (facultatif)</dt>
   <dd>Commande ou espace de nom pour lequel afficher l'aide. Si la commande ou l'espace de nom n'est pas spécifié, l'aide générale de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} est affichée.</dd>
   </dl>



<strong>Exemples</strong> :

Affichez l'aide générale pour l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} :

```
bluemix help
```

Affichez l'aide pour la commande `info` :

```
bluemix help info
```

Affichez l'aide du plug-in `ic` :

```
bluemix help ic
```

ou

```
bluemix ic help
```

Affichez l'aide de la commande `group-create` sous le plug-in `ic` :

```
bluemix ic help group-create
```


### bluemix api
{: #bluemix_api}
Définissez ou affichez le noeud final d'API {{site.data.keyword.Bluemix_notm}}. Cette commande encapsule la commande `cf api`.

```
bluemix api [NOEUD_FINAL_API] [--unset]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
   <dl>
   <dt>NOEUD_FINAL_API (facultatif)</dt>
   <dd>Noeud final d'API ciblé. Par exemple, `https://api.chinabluemix.net`. Si l'option *NOEUD_FINAL_API* et l'option `--unset` sont toutes les deux spécifiées, le noeud final d'API en cours est affiché.</dd>
   <dt>--unset (facultatif)</dt>
   <dd>Supprime le paramètre de noeud final d'API.</dd>
    </dl>
<strong>Exemples</strong> :

Définissez le noeud final d'API api.chinabluemix.net :

```
bluemix api api.chinabluemix.net
```

Affichez le noeud final d'API en cours :

```
bluemix api
```

Annulez la définition du noeud final d'API :

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

Connectez l'utilisateur. Cette commande encapsule la commande `cf login`. Les options de commande sont les mêmes que pour `cf login`.

```
bluemix login [OPTIONS...]
```

<strong>Prérequis</strong> : Noeud final

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>Options de commande</strong> : pour des informations sur les options prises en charge par la commande `login`, voir les informations sur la syntaxe de la commande `cf login` pour les commandes cf de gestion des applications.

<strong>Remarque</strong> :
Si vous vous connectez à l'aide d'un ID fédéré, utilisez l'option '--sso' pour vous authentifier avec un code d'accès unique.

### bluemix logout
{: #bluemix_logout}

Déconnectez l'utilisateur. Cette commande encapsule la commande `cf logout`.

```
bluemix logout
```

<strong>Prérequis</strong> : Aucun


### bluemix target
{: #bluemix_target}


Définissez ou affichez l'organisation ou l'espace cible. Cette commande encapsule la commande `cf target`.

```
bluemix target [-o NOM_ORG] [-s NOM_ESPACE]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>-o <i>NOM_ORG</i> (facultatif)</dt>
   <dd>Nom de l'organisation à cibler.</dd>
   <dt>-s <i>NOM_ESPACE</i> (facultatif)</dt>
   <dd>Nom de l'espace à cibler.</dd>
   </dl>
Si ni -o *NOM_ORG* ni -s *NOM_ESPACE* n'est spécifié, l'organisation et l'espace en cours sont affichés.
<strong>Exemples</strong> :

Définissez l'organisation en cours `MonOrg` et l'espace `MonEspace` :

```
bluemix target -o MonOrg -s MonEspace
```

Affichez l'organisation et l'espace en cours :

```
bluemix target
```


### bluemix info
{: #bluemix_info}

Affichez les informations {{site.data.keyword.Bluemix_notm}} de base, notamment la région en cours, la version du contrôleur de cloud et certains noeuds finaux utiles tels que les noeuds finaux pour la connexion et l'échange de jeton d'accès.

```
bluemix info
```

<strong>Prérequis</strong> : Noeud final


### bluemix config
{: #bluemix_config}


Ecrivez les valeurs par défaut dans le fichier de configuration.

```
bluemix config --http-timeout DELAI_ATTENTE_EN_SECONDES | --trace (true|false|chemin_fichier) | --color (true|false) | --locale (ENV_LOCAL|CLEAR) | --check-version (true|false)
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
   <dl>
   <dt>--http-timeout <i>DELAI_ATTENTE_EN_SECONDES</i></dt>
   <dd>Délai d'attente pour les demandes HTTP. La valeur par défaut est 60 secondes.</dd>
   <dt>--trace true|false|<i>chemin_fichier</i></dt>
   <dd>Consigne la trace des demandes HTTP sur le terminal ou dans le fichier spécifié.</dd>
   <dt>--color true|false</dt>
   <dd>Active ou désactive la sortie en couleurs. Elle est activée par défaut.</dd>
   <dt>--locale <i>ENV_LOCAL|CLEAR</i></dt>
   <dd>Définit un environnement local par défaut. Si ENV_LOCAL spécifie <i>CLEAR</i>, l'environnement local précédent est supprimé.</dd>
   <dt>--check-version true|false</dt>
   <dd>Active ou désactive la vérification de la version de l'interface de ligne de commande</dd>
   </dl>

Une seule de ces options peut être indiquée à la fois.

<strong>Exemples</strong> :

Définissez le délai d'attente des demandes HTTP à 30 secondes :

```
bluemix config --http-timeout 30
```

Activez la sortie de trace pour les demandes HTTP :

```
bluemix config --trace true
```

Consigne la trace des demandes HTTP dans le fichier spécifié */home/usera/my_trace*:

```
bluemix config --trace /home/usera/my_trace
```

Désactivez la sortie couleur :

```
bluemix config --color false
```

Définissez l'environnement local zh_Hans :

```
bluemix config --locale zh_Hans
```

Effacez les paramètres d'environnement local :

```
bluemix config --locale CLEAR
```


### bluemix curl
{: #bluemix_curl}

Exécutez une demande HTTP brute dans {{site.data.keyword.Bluemix_notm}}. *Content-Type* a pour valeur *application/json* par défaut. Cette
commande envoie la demande au proxy de contrôle multi-clouds {{site.data.keyword.Bluemix_notm}}. Pour les chemins pris en charge, reportez-vous aux définitions de chemin d'API dans le document [CloudFoundry API ](http://apidocs.cloudfoundry.org/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg).

```
bluemix curl CHEMIN [OPTIONS...]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt><i>CHEMIN</i> (requis)</dt>
   <dd>Chemin d'URL de la ressource. Par exemple, /v2/apps.</dd>
   <dt><i>OPTIONS</i> (facultatif)</dt>
   <dd>Les options prises en charge par la commande `bluemix curl` sont les mêmes que pour la commande
`cf curl`.</dd>
   </dl>

<strong>Exemples</strong> :

Affichage des informations de toutes les organisations du compte en cours :

```
bluemix curl /v2/organizations
```


### bluemix iam orgs
{: #bluemix_iam_orgs}

Recensement de toutes les organisations

```
bluemix iam orgs [-r REGION --guid]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>-r <i>REGION</i> (facultatif)</dt>
   <dd>Spécifie la région pour laquelle afficher les informations de l'organisation. Si vous spécifiez 'all', toutes les
organisations de toutes les régions sont répertoriées.</dd>
   <dt>--guid (facultatif)</dt>
   <dd>Affiche l'identificateur global unique (GUID) des organisations.</dd>
   </dl>

<strong>Exemples</strong> :

Recensement de toutes les organisations dans la région : `us-south` en affichant leur identificateur global unique (GUID)

```
bluemix iam orgs -r us-south --guid
```

### bluemix iam org
{: #bluemix_iam_org}

Affiche des informations sur l'organisation spécifiée.

```
bluemix iam org NOM_ORG [--guid]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation.</dd>
   <dt>--guid (facultatif)</dt>
   <dd>Affiche l'identificateur global unique (GUID) de l'organisation.</dd>
   </dl>

<strong>Exemples</strong> :

Affichage des informations de l'organisation `IBM` en indiquant son identificateur global unique (GUID)

```
bluemix iam org IBM --guid
```

### bluemix iam org-create
{: #bluemix_iam_org_create}

Crée une nouvelle organisation. Cette opération ne peut être effectuée que par le propriétaire du compte.

```
bluemix iam org-create NOM_ORG
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation à créer.</dd>
   </dl>

<strong>Exemples</strong> :

Création d'une organisation nommée `IBM`.

```
bluemix iam org-create IBM
```


### bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Répliquez une organisation de la région en cours dans une autre région.

```
bluemix iam org-replicate NOM_ORG NOM_REGION
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation existante à répliquer.</dd>
   <dt>NOM_REGION (requis)</dt>
   <dd>Nom de la région hébergeant l'organisation répliquée.</dd>
   </dl>

<strong>Exemples</strong> :

Réplication de l'organisation `mon_org` dans la région `eu-gb`:

```
bluemix iam org-replicate mon_org eu-gb
```


### bluemix iam org-rename
{: #bluemix_iam_org_rename}

Attribue un nouveau nom à une organisation. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-rename ANCIEN_NOM_ORG NOUVEAU_NOM_ORG
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ANCIEN_NOM_ORG (requis)</dt>
   <dd>Ancien nom de l'organisation qui sera renommée.</dd>
   <dt>NOUVEAU_NOM_ORG (requis)</dt>
   <dd>Nouveau nom à affecter à l'organisation.</dd>
   </dl>

### bluemix iam org-delete
{: #bluemix_iam_org_delete}

Supprime l'organisation spécifiée dans la région en cours.

```
bluemix iam org-delete NOM_ORG [-f --all]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation existante à supprimer.</dd>
   <dt>-f (facultatif)</dt>
   <dd>Impose la suppression sans demander de confirmation.</dd>
   <dt>--all (facultatif)</dt>
   <dd>Supprime l'organisation dans toutes les régions.</dd>
   </dl>


### bluemix iam spaces
{: #bluemix_iam_spaces}

Cette commande possède la même fonction et les mêmes options que la commande `cf spaces`.


### bluemix iam space
{: #bluemix_iam_space}

Cette commande possède la même fonction et les mêmes options que la commande `cf space`.


### bluemix iam space-create
{: #bluemix_iam_space_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-space`.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


Cette commande possède la même fonction et les mêmes options que la commande `cf rename-space`.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


Cette commande possède la même fonction et les mêmes options que la commande `cf delete-space`.


### bluemix iam account-users
{: #bluemix_iam_account_users}

Affiche les utilisateurs associés au compte. Cette opération ne peut être effectuée que par le
propriétaire du compte.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}


Invite un utilisateur à joindre le compte avec un rôle d'organisation et un rôle d'espace déjà définis. Cette opération ne peut être effectuée que par le
propriétaire du compte.

```
bluemix iam account-user-invite NOM_UTILISATEUR NOM_ORG ROLE_ORG NOM_ESPACE ROLE_ESPACE
```

<strong>Prérequis</strong> : Noeud final, Connexion


<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_UTILISATEUR (requis)</dt>
   <dd>Nom de l'utilisateur à inviter.</dd>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation dans laquelle inviter cet utilisateur.</dd>
   <dt>ROLE_ORG</dt>
   <dd>Nom du rôle d'organisation auquel inviter cet utilisateur. Par exemple :
   <ul>
  <li>OrgManager : ce rôle peut inviter et gérer des utilisateurs, sélectionner et changer de plan, et définir des plafonds de dépense.</li>
  <li>BillingManager : ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</li>
  <li>OrgAuditor : ce rôle dispose d'un accès en lecture seule aux informations de l'organisation et aux rapports.</li>
  </ul> </dd>
   <dt>NOM_ESPACE (requis)</dt>
   <dd>Nom de l'espace dans lequel inviter cet utilisateur.</dd>
   <dt>ROLE_ESPACE (requis)</dt>
   <dd>Nom de l'espace dans lequel inviter cet utilisateur. Nom du rôle d'espace auquel inviter cet utilisateur. Par exemple :
   <ul>
<li>SpaceManager: ce rôle peut inviter et gérer des utilisateurs, et activer des fonctions dans un espace spécifique.</li>
<li>SpaceDeveloper : ce rôle peut créer et gérer des applications et des services, et consulter les journaux et les rapports.</li>
<li>SpaceAuditor : ce rôle peut consulter les journaux, les rapports, et les paramètres de l'espace.</li>
</ul>
</dd>
</dl>

<strong>Exemples</strong> :

Invitation de l'utilisateur `Mary` dans l'organisation `IBM` sous le rôle `OrgManager` et l'espace
`Cloud` sous le rôle `SpaceAuditor` :

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Renvoyer l'invitation à un utilisateur (gestionnaire d'organisation ou propriétaire de compte requis)
```
 bluemix iam account-user-reinvite EMAIL_UTIL NOM_ORG
```


### bluemix iam org-users
{: #bluemix_iam_org_users}

Affiche les utilisateurs dans l'organisation spécifiée, par rôle.

```
bluemix iam org-users NOM_ORG [-a]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation.</dd>
   <dt>-a (facultatif)</dt>
   <dd>Recense tous les utilisateurs de l'organisation spécifiés, sans les regrouper par rôle.</dd>
    </dl>

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Ajoute un utilisateur dans l'organisation (responsable de l'organisation requis).
```
 bluemix iam org-user-add NOM_UTILISATEUR ORG
```

### bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Supprimer un utilisateur de l'organisation (gestionnaire d'organisation ou utilisateur lui-même)
```
   bluemix iam org-user-remove NOM_UTILISATEUR ORG [-f, --force]
```

<strong>Options de commande</strong> :
  <dl>
   <dt>--force, -f</dt>
   <dd>Impose la suppression sans demander de confirmation.</dd>
 </dl>

### bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Affecte un rôle de l'organisation à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-role-set NOM_UTILISATEUR NOM_ORG ROLE_ORG
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
  <dl>
   <dt>NOM_UTILISATEUR (requis)</dt>
   <dd>Nom de l'utilisateur à affecter.</dd>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation à laquelle affecter cet utilisateur.</dd>
   <dt>ROLE_ORG</dt>
   <dd>Nom du rôle d'organisation auquel affecter cet utilisateur. Par exemple :
   <ul>
   <li>OrgManager : ce rôle peut inviter et gérer des utilisateurs, sélectionner et changer de plan, et définir des plafonds de dépense.</li>
   <li>BillingManager : ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</li>
   <li>OrgAuditor : ce rôle dispose d'un accès en lecture seule aux informations de l'organisation et aux rapports.</li>
   </ul>
   </dd>
    </dl>

<strong>Exemples</strong> :

Affectation de l'utilisateur `Mary` à l'organisation `IBM` sous le rôle `OrgManager` :

```
bluemix iam org-role-set Mary IBM OrgManager
```


### bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Supprime l'affectation d'un rôle d'organisation à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-role-unset NOM_UTILISATEUR NOM_ORG ROLE_ORG
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_UTILISATEUR (requis)</dt>
   <dd>Nom de l'utilisateur à supprimer.</dd>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation dans laquelle supprimer cet utilisateur.</dd>
   <dt>ROLE_ORG</dt>
   <dd>Nom du rôle d'organisation d'où supprimer cet utilisateur. Par exemple :
   <ul>
   <li>OrgManager : ce rôle peut inviter et gérer des utilisateurs, sélectionner et changer de plan, et définir des plafonds de dépense.</li>
   <li>BillingManager : ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</li>
   <li>OrgAuditor : ce rôle dispose d'un accès en lecture seule aux informations de l'organisation et aux rapports.</li>
   </ul>
   </dd>
    </dl>

<strong>Exemples</strong> :

Suppression de l'affectation de l'utilisateur `Mary` dans l'organisation `IBM` au rôle `OrgManager` :

```
bluemix iam org-role-unset Mary IBM OrgManager
```


### bluemix iam space-users
{: #bluemix_iam_space_users}

Affichage des utilisateurs, par rôle, dans l'espace spécifié.

```
bluemix iam space-users NOM_ORG NOM_ESPACE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation.</dd>
   <dt>NOM_ESPACE (requis)</dt>
   <dd>Nom de l'espace.</dd>
   </dl>


### bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Affecte un rôle d'espace à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'espace.

```
bluemix iam space-role-set NOM_UTILISATEUR NOM_ORG NOM_ESPACE ROLE_ESPACE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_UTILISATEUR (requis)</dt>
   <dd>Nom de l'utilisateur à affecter.</dd>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation à laquelle affecter cet utilisateur.</dd>
   <dt>NOM_ESPACE (requis)</dt>
   <dd>Nom de l'espace auquel affecter cet utilisateur.</dd>
   <dt>ROLE_ESPACE (requis)</dt>
   <dd>Nom du rôle d'espace auquel affecter cet utilisateur. Par exemple :
   <ul>
   <li>SpaceManager: ce rôle peut inviter et gérer des utilisateurs, et activer des fonctions dans un espace spécifique.</li>
   <li>SpaceDeveloper : ce rôle peut créer et gérer des applications et des services, et consulter les journaux et les rapports.</li>
   <li>SpaceAuditor : ce rôle peut consulter les journaux, les rapports, et les paramètres de l'espace.</li>
   </ul></dd>
    </dl>

<strong>Exemples</strong> :

Affectation de l'utilisateur `Mary` à l'organisation `IBM` et à l'espace `Cloud` sous le rôle
`SpaceManager` :

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

### bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Suppression de l'affectation d'un rôle d'espace à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'espace.

```
bluemix iam space-role-unset NOM_UTILISATEUR NOM_ORG NOM_ESPACE ROLE_ESPACE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_UTILISATEUR (requis)</dt>
   <dd>Nom de l'utilisateur à supprimer.</dd>
   <dt>NOM_ORG (requis)</dt>
   <dd>Nom de l'organisation dans laquelle supprimer cet utilisateur.</dd>
   <dt>NOM_ESPACE (requis)</dt>
   <dd>Nom de l'espace dans lequel supprimer cet utilisateur.</dd>
   <dt>ROLE_ESPACE (requis)</dt>
   <dd>Nom du rôle d'espace d'où supprimer cet utilisateur. Par exemple :
   <ul>
   <li>SpaceManager: ce rôle peut inviter et gérer des utilisateurs, et activer des fonctions dans un espace spécifique.</li>
   <li>SpaceDeveloper : ce rôle peut créer et gérer des applications et des services, et consulter les journaux et les rapports.</li>
   <li>SpaceAuditor : ce rôle peut consulter les journaux, les rapports, et les paramètres de l'espace.</li>
   </ul></dd>
    </dl>


<strong>Exemples</strong> :

Suppression de l'affectation de l'utilisateur `Mary` dans l'organisation `IBM` et l'espace
`Cloud` au rôle `SpaceManager` :

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


### bluemix app push
{: #bluemix_app_push}

Cette commande possède la même fonction et les mêmes options que la commande `cf push`.


### bluemix app list
{: #bluemix_app_list}

Cette commande possède la même fonction et les mêmes options que la commande `cf apps`.


### bluemix app show
{: #bluemix_app_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf app`.


### bluemix app scale
{: #bluemix_app_scale}

Cette commande possède la même fonction et les mêmes options que la commande `cf scale`.


### bluemix app delete
{: #bluemix_app_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete`.


### bluemix app rename
{: #bluemix_app_rename}

Cette commande possède la même fonction et les mêmes options que la commande `cf rename`.


### bluemix app start
{: #bluemix_app_start}

Cette commande possède la même fonction et les mêmes options que la commande `cf start`.


### bluemix app stop
{: #bluemix_app_stop}

Cette commande possède la même fonction et les mêmes options que la commande `cf stop`.


### bluemix app restart
{: #bluemix_app_restart}

Cette commande possède la même fonction et les mêmes options que la commande `cf restart`.


### bluemix app restage
{: #bluemix_app_restage}


Cette commande possède la même fonction et les mêmes options que la commande `cf restage`.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


Cette commande possède la même fonction et les mêmes options que la commande `cf restart-app-instance`.


### bluemix app events
{: #bluemix_app_events}

Cette commande possède la même fonction et les mêmes options que la commande `cf events`.


### bluemix app files
{: #bluemix_app_files}

Cette commande possède la même fonction et les mêmes options que la commande `cf files`.


### bluemix app logs
{: #bluemix_app_logs}

Cette commande possède la même fonction et les mêmes options que la commande `cf logs`.


### bluemix app env
{: #bluemix_app_env}

Cette commande possède la même fonction et les mêmes options que la commande `cf env`.


### bluemix app env-set
{: #bluemix_app_env_set}

Cette commande possède la même fonction et les mêmes options que la commande `cf set-env`.


### bluemix app env-unset
{: #bluemix_app_env_unset}

Cette commande possède la même fonction et les mêmes options que la commande `cf unset-env`.


### bluemix app stacks
{: #bluemix_app_stacks}

Cette commande possède la même fonction et les mêmes options que la commande `cf stacks`.


### bluemix app stack
{: #bluemix_app_stack}

Cette commande possède la même fonction et les mêmes options que la commande `cf stack`.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-app-manifest`.


### bluemix service offerings
{: #bluemix_service_offerings}


Cette commande possède la même fonction et les mêmes options que la commande `cf marketplace`.


### bluemix service list
{: #bluemix_service_list}

Cette commande possède la même fonction et les mêmes options que la commande `cf services`.


### bluemix service show
{: #bluemix_service_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf service`.


### bluemix service create
{: #bluemix_service_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-service`.


### bluemix service update
{: #bluemix_service_update}

Cette commande possède la même fonction et les mêmes options que la commande `cf update-service`.


### bluemix service delete
{: #bluemix_service_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-service`.


### bluemix service rename
{: #bluemix_service_rename}

Cette commande possède la même fonction et les mêmes options que la commande `cf rename-service`.


### bluemix service bind
{: #bluemix_service_bind}

Cette commande possède la même fonction et les mêmes options que la commande `cf bind-service`.


### bluemix service unbind
{: #bluemix_service_unbind}

Cette commande possède la même fonction et les mêmes options que la commande `cf unbind-service`.


### bluemix service key-create
{: #bluemix_service_key_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-service-key`.


### bluemix service key-delete
{: #bluemix_service_key_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-service-key`.


### bluemix service keys
{: #bluemix_service_keys}

Cette commande possède la même fonction et les mêmes options que la commande `cf service-keys`.


### bluemix service key-show
{: #bluemix_service_key_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf service-key`.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-user-provided-service`.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Cette commande possède la même fonction et les mêmes options que la commande `cf update-user-provided-service`.


### bluemix catalog templates
{: #bluemix_catalog_templates}

Affichez les modèles de conteneur boilerplate dans Bluemix.

```
bluemix catalog templates [-d]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

   <dl>
   <dt>-d (facultatif)</dt>
   <dd>Si l'option <i>-d</i> est spécifiée, la description de chaque modèle est également affichée. Sinon, seul l'ID et le nom des modèles sont affichés.</dd>
   </dl>


### bluemix catalog template
{: #bluemix_catalog_template}

Affichez les informations détaillées d'un modèle de conteneur boilerplate spécifié.

```
bluemix catalog template ID_MODELE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ID_MODELE (requis)</dt>
   <dd>ID du modèle de conteneur boilerplate. Utilisez <i>bluemix templates</i> pour afficher tous les ID de modèles.</dd>
   </dl>


<strong>Exemples</strong> :

Affichez les détails du modèle `mobileBackendStarter` :

```
bluemix catalog template mobileBackendStarter
```


### bluemix catalog template-run
{: #bluemix_catalog_template_run}

Créez une application cf reposant sur le modèle spécifié avec l'adresse URL et la description indiquées. Par défaut, la nouvelle application est démarrée automatiquement.

```
bluemix catalog template-run ID_MODELE NOM_APP_CF [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
   <dt>ID_MODELE (requis)</dt>
   <dd>Modèle sur lequel sera basée l'application lors de sa création. Utilisez <i>bluemix templates</i> pour voir tous les ID des modèles.</dd>
   <dt>NOM_APP_CF (requis)</dt>
   <dd>Nom de l'application cf à créer.</dd>
   <dt>-u <i>URL</i> (facultatif)</dt>
   <dd>Route de l'application. Si elle n'est pas spécifiée, la route est définie automatiquement par Bluemix d'après le nom de votre application et le domaine par défaut.</dd>
   <dt>-d <i>DESCRIPTION</i> (facultatif)</dt>
   <dd>Description de l'application.</dd>
   <dt>--no-start (facultatif)</dt>
   <dd>Indique de ne pas démarrer automatiquement l'application après sa création. Si cette option n'est pas spécifiée, l'application est démarrée automatiquement après sa création.</dd>
   </dl>


<strong>Exemples</strong> :

Créez l'application cf `mon-app` d'après le modèle `javaHelloWorld` :

```
bluemix catalog template-run javaHelloWorld mon-app
```

Créez une application `my-ruby-app` d'après le modèle `rubyHelloWorld` avec la route
`myrubyapp.chinabluemix.net` et la description `Ma première application Ruby dans {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "Ma première application Ruby dans {{site.data.keyword.Bluemix_notm}}."
```

Créez l'application `mon-app-python` d'après le modèle `pythonHelloWorld` sans démarrage automatique :

```
bluemix catalog template-run pythonHelloWorld mon-app-python --no-start
```


### bluemix network regions
{: #bluemix_network_regions}

Affichez les informations pour toutes les régions dans {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

<strong>Prérequis</strong> : Noeud final


### bluemix network region-set
{: #bluemix_network_region_set}

Passez à la région spécifiée. Cette commande vous redirige automatiquement sur la même organisation et le même espace dans la nouvelle région, si possible. Autrement, l'utilisateur est invité à sélectionner une nouvelle organisation et un nouvel espace si l'utilisateur est déjà connecté. Le noeud final d'API est changé en conséquence.

```
bluemix network region-set NOM_REGION
```

<strong>Prérequis</strong> : Noeud final

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_REGION (requis)</dt>
   <dd>Nom de la région sur laquelle basculer. Vous pouvez utiliser la commande <i>bluemix network regions</i> pour afficher tous les noms de région.</dd>
    </dl>

<strong>Exemples</strong> :

Définissez la région en cours `eu-gb` :

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

Cette commande possède la même fonction et les mêmes options que la commande `cf routes`.


### bluemix network route-check
{: #bluemix_network_route_check}

Cette commande possède la même fonction et les mêmes options que la commande `cf check-route`.


### bluemix network route-map
{: #bluemix_network_route_map}

Mappez une route à une application cf ou un groupe de conteneurs existant associé au domaine et au nom d'hôte spécifiés.

```
bluemix network route-map NOM_APP_CF|NOM_GROUPE_CONTENEURS  DOMAINE  [-n NOM_HOTE]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_APP_CF|NOM_GROUPE_CONTENEURS (requis)</dt>
   <dd>Nom de l'application cf ou du groupe de conteneur à mapper à une route.</dd>
   <dt>DOMAINE (requis)</dt>
   <dd>Domaine de la route. Par exemple, mychinabluemix.net ou chinabluemix.net. </dd>
   <dt>-n <i>NOM_HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du groupe de conteneurs par défaut.</dd>
   </dl>

<strong>Exemples</strong> :

Mappez une route à `mon-app` avec le domaine spécifié :

```
bluemix network route-map mon-app mychinabluemix.net
```

Mappez une route à 'mon-groupe-conteneurs' avec le domaine et le nom d'hôte spécifiés :

```
bluemix network route-map mon-groupe-conteneurs chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

Supprimez le mappage de la route spécifiée à une application cf ou un groupe de conteneurs existant.

```
bluemix network route-unmap NOM_APP_CF|NOM_GROUPE_CONTENEURS  DOMAINE  [-n NOM_HOTE]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_APP_CF|NOM_GROUPE_CONTENEURS (requis)</dt>
   <dd>Nom de l'application cf ou du groupe de conteneurs.</dd>
   <dt>DOMAINE (requis)</dt>
   <dd>Domaine de la route (par exemple, mychinabluemix.net ou chinabluemix.net).</dd>
   <dt>-n <i>NOM_HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du groupe de conteneurs par défaut.</dd>
   </dl>

<strong>Exemples</strong> :

Supprimez le mappage de la route `mon-app.mychinabluemix.net` de `mon-app` :

```
bluemix network route-unmap mo-app mychianbluemix.net
```

Supprimez le mappage de la route `abc.chinabluexmix.net` de `mon-groupe-conteneurs` :

```
bluemix network route-unmap mon-groupe-conteneurs chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-route`.


### bluemix network route-delete
{: #bluemix_network_route_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-route`.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-orphaned-routes`.


### bluemix network domains
{: #bluemix_network_domains}

Cette commande possède la même fonction et les mêmes options que la commande `cf domains`.


### bluemix network domain-create
{: #bluemix_network_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-domain`.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-domain`.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-shared-domain`.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-shared-domain`.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

Affichez l'utilisation mensuelle et les coûts liés à votre compte.

```
bluemix bss account-usage [-d AAAA-MM] [--json]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

<dl>
  <dt>-d MOIS_DATE (facultatif)</dt>
  <dd>Afficher les données relatives au mois et à la date spécifiées en utilisant le format AAAA-MM. Si ces données ne sont pas spécifiées, l'utilisation du mois en cours est affichée.</dd>
  <dt>--json (facultatif)</dt>
  <dd>Afficher le résultat de l'utilisation au format JSON.</dd>
</dl>

<strong>Exemples</strong> :

Affichage du rapport d'utilisation et des coûts de mon compte pour 2016-06 :

```
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

Affichez les détails de l'utilisation mensuelle d'une organisation. Cette opération ne peut être réalisée que par un responsable de la facturation de l'organisation.

```
bluemix bss org-usage NOM_ORG [-d AAAA-MM] [-r NOM_REGION] [--json]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

<dl>
  <dt>NOM_ORG (requis)</dt>
  <dd>Nom de l'organisation.</dd>
  <dt>-d MOIS_DATE (facultatif)</dt>
  <dd>Afficher les données relatives au mois et à la date spécifiés en utilisant le format AAAA-MM. Si ces données ne sont pas spécifiées, l'utilisation du mois en cours est affichée.</dd>
  <dt>-r NOM_REGION</dt>
  <dd>Nom de la région qui héberge l'organisation. Si ce paramètre a pour valeur 'all', l'utilisation de l'organisation dans toutes les régions est affichée.</dd>
  <dt>--json (facultatif)</dt>
  <dd>Afficher le résultat de l'utilisation au format JSON.</dd>
</dl>



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

Affichez un récapitulatif d'utilisation mensuelle pour les organisations dans mon compte.

```
bluemix bss orgs-usage-summary [-d AAAA-MM] [-r NOM_REGION] [--json]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

<dl>
  <dt>-d MOIS_DATE (facultatif)</dt>
  <dd>Afficher les données relatives au mois et à la date spécifiés en utilisant le format AAAA-MM. Si ces données ne sont pas spécifiées, l'utilisation du mois en cours est affichée.</dd>
  <dt>-r NOM_REGION</dt>
  <dd>Nom de la région qui héberge les organisations. Si ce paramètre a pour valeur 'all', le récapitulatif d'utilisation des organisations dans toutes les régions est affiché.</dd>
  <dt>--json (facultatif)</dt>
  <dd>Afficher le résultat de l'utilisation au format JSON.</dd>
</dl>



### bluemix security cert
{: #bluemix_security_cert}

Affichage des informations de certificat d'un domaine.

```
bluemix security cert NOM_DOMAINE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_DOMAINE (requis)</dt>
   <dd>Domaine hébergeant le certificat.</dd>
   </dl>



<strong>Exemples</strong> :

Affichage des informations de certificat du domaine `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

Ajoutez un certificat au domaine indiqué dans l'organisation en cours.

```
bluemix security cert-add DOMAINE -k FICHIER_CLE_PRIVEE -c FICHIER_CERT [-p MOT_DE_PASSE] [-i FICHIER_CERT_INTERMEDIAIRE] [--verify-client]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
   <dt>DOMAINE (requis)</dt>
   <dd>Domaine auquel ajouter le certificat.</dd>
   <dt>-k <i>FICHIER_CLE_PRIVEE</i> (requis)</dt>
   <dd>Chemin du fichier de clé privée.</dd>
   <dt>-c <i>FICHIER_CERT</i> (requis)</dt>
   <dd>Chemin du fichier de certificat.</dd>
   <dt>-p <i>MOT_DE_PASSE</i> (facultatif)</dt>
   <dd>Mot de passe du certificat.</dd>
   <dt>-i <i>FICHIER_CERT_INTERMEDIAIRE</i> (facultatif)</dt>
   <dd>Chemin du fichier de certificat intermédiaire.</dd>
   <dt>--verify-client (facultatif)</dt>
   <dd>Indique si la vérification du certificat client doit être activée.</dd>
   </dl>


<strong>Exemples</strong> :

Ajoutez un certificat au domaine `ibmcxo-eventconnect.com` :

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

Supprimez un certificat du domaine spécifié dans l'organisation en cours.

```
bluemix security cert-remove DOMAINE [-f]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>DOMAINE (requis)</dt>
   <dd>Domaine duquel supprimer le certificat.</dd>
   <dt>-f (facultatif)</dt>
   <dd>Impose la suppression sans demander de confirmation.</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

Répertoriez tous les référentiels de plug-in qui sont enregistrés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

<strong>Prérequis</strong> : Aucun


### bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Ajoutez un nouveau référentiel de plug-in à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add NOM_REFERENTIEL URL_REFERENTIEL
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_REFERENTIEL (requis)</dt>
   <dd>Nom du référentiel à ajouter. Vous pouvez définir votre propre nom pour chaque référentiel.</dd>
   <dt>URL_REFERENTIEL (requise)</dt>
   <dd>URL du référentiel à ajouter. Elle doit contenir le protocole (par exemple http://plugins.ng.bluemix.net au lieu de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net est le référentiel de plug-in officiel de l'interface de ligne de commande (CLI) Bluemix.</dd>
    </dl>


<strong>Exemples</strong> :

Ajoutez le référentiel de plug-in officiel de l'interface de ligne de commande Bluemix sous la forme `référentiel-bluemix` :

```
bluemix plugin repo-add référentiel-bluemix http://plugins.ng.bluemix.net
```


### bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Retirez un référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove NOM_REFERENTIEL
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
   <dl>
   <dt>NOM_REFERENTIEL (requis)</dt>
   <dd>Nom du référentiel à supprimer.</dd>
   </dl>

<strong>Exemples</strong> :

Supprimez `référentiel-bluemix` de l'interface de ligne de commande (CLI) {{site.data.keyword.Bluemix_notm}} :

```
bluemix plugin repo-remove référentiel-bluemix
```


### bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Répertoriez tous les plug-in disponibles dans tous les référentiels ajoutés ou dans un référentiel spécifique.

```
bluemix plugin repo-plugins [-r NOM_REFERENTIEL]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>-r <i>NOM_REFERENTIEL</i> (facultatif)</dt>
   <dd>Recense uniquement les plug-in dans le référentiel spécifié.</dd>
   </dl>

<strong>Exemples</strong> :

Répertoriez tous les plug-in dans tous les référentiels ajoutés :

```
bluemix plugin repo-plugins
```

Répertoriez tous les plug-in du référentiel `référentiel-bluemix` :

```
bluemix plugin repo-plugins -r bluemix-repo
```


### bluemix plugin list
{: #bluemix_plugin_list}

Répertoriez tous les plug-in installés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

<strong>Prérequis</strong> : Aucun


### bluemix plugin install
{: #bluemix_plugin_install}

Installez la version de plug-in spécifique dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} à partir du chemin ou du référentiel spécifié.

```
bluemix plugin install CHEMIN_PLUG-IN|NOM_PLUG-IN [-r NOM_REFERENTIEL] [-v VERSION]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>CHEMIN_PLUG-IN|NOM_PLUG-IN (requis)</dt>
   <dd>Si -r <i>NOM_REFERENTIEL</i> n'est pas spécifié, le plug-in est installé depuis le chemin local spécifié ou depuis l'URL distante.</dd>
   <dt>-r <i>NOM_REFERENTIEL</i> (facultatif)</dt>
   <dd>Nom du référentiel hébergeant le fichier binaire du plug-in.</dd>
   <dt>-v <i>VERSION</i> (facultatif)</dt>
   <dd>Version du plug-in à installer. Si elle n'est pas fournie, la dernière version du plug-in est installée. Cette option n'est valide que si vous installez le plug-in à partir du référentiel.</dd>
    </dl>

<strong>Exemples</strong> :

Installez un plug-in depuis le fichier local :

```
bluemix plugin install /downloads/new_plugin
```

Installez un plug-in depuis l'adresse URL distante :

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Installez la dernière version du plug-in `IBM-Containers` à partir du référentiel `référentiel-bluemix` :

```
bluemix plugin install IBM-Containers -r référentiel-bluemix
```
Installez le plug-in `IBM-Containers` avec la version `0.5.800` à partir du référentiel `référentiel-bluemix` :

```
bluemix plugin install IBM-Containers -r référentiel-bluemix -v 0.5.800
```






### bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Désinstallez le plug-in spécifié de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall NOM_PLUG-IN
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>NOM_PLUG-IN (requis)</dt>
   <dd>Nom du plug-in à désinstaller.</dd>
    </dl>

<strong>Exemples</strong> :

Désinstallez le plug-in `IBM-Containers` installé précédemment :

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

Contrôlez un conteneur en cours d'exécution ou affichez sa sortie. Utilisez `CTRL+C` pour quitter et arrêter le conteneur. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [attach ](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>--no-stdin (facultatif)</dt>
   <dd>Indique de ne pas inclure l'entrée standard.</dd>
   <dt>--sig-proxy (facultatif)</dt>
   <dd>Indique d'envoyer par proxy tous les signaux reçus au processus. La valeur
par défaut est <i>true</i>.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
    </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'association au conteneur `mon_conteneur` :
```
bluemix ic attach mon_conteneur
```


### bluemix ic build
{: #bluemix_ic_build}

Appelez le service de génération IBM Containers afin de générer une image Docker localement ou dans votre référentiel {{site.data.keyword.Bluemix_notm}} privé. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [build ](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic build -t ETIQUETTE|--tag ETIQUETTE [--no-cache] [-p|--pull] [-q|--quiet] EMPLACEMENT_DOCKERFILE
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :
   <dl>
   <dt>-t <i>ETIQUETTE</i>|--tag <i>ETIQUETTE</i> (requis)</dt>
   <dd>Nom de référentiel à appliquer à l'image créée.</dd>
   <dt>--no-cache (facultatif)</dt>
   <dd>Indique de ne pas utiliser le cache lorsque l'image est générée. La valeur par défaut est <i>false</i>.</dd>
   <dt>--pull (facultatif)</dt>
   <dd>Indique d'essayer d'extraire l'image de base depuis le registre même si elle est en cache.</dd>
   <dt>-q|--quiet (facultatif)</dt>
   <dd>Supprime la sortie détaillée générée par les conteneurs. La valeur par défaut est <i>false</i>.</dd>
   <dt><i>EMPLACEMENT_DOCKERFILE</i> (requis)</dt>
   <dd>Chemin du fichier Dockerfile et du contexte sur l'hôte local.</dd>
    </dl>

<strong>Exemples</strong> :

L'exemple suivant illustre une demande de génération d'une image nommée *monimage*. Le document Dockerfile et les autres artefacts à utiliser dans la génération se trouvent dans le répertoire depuis lequel la commande est exécutée. Etant donné que le registre et l'espace de nom sont inclus dans le nom de l'image, l'image est générée dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation.
```
bluemix ic build -t registry.ng.bluemix.net/monespacenom/monimage
```


### bluemix ic cp
{: #bluemix_ic_cp}
Copie des fichiers ou des dossiers entre un conteneur et le système de fichiers local. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [cp ](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.


### bluemix ic cpi
{: #bluemix_ic_cpi}

Accédez à une image Docker Hub ou à une image de votre registre local et copiez-la dans votre référentiel {{site.data.keyword.Bluemix_notm}} privé.

```
bluemix ic cpi IMAGE_SOURCE IMAGE_DESTINATION
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
   <dt><i>IMAGE_SOURCE</i> (requis)</dt>
   <dd>Référentiel source et nom de l'image.</dd>
   <dt><i>IMAGE_DESTINATION</i> (requis)</dt>
   <dd>URL du référentiel {{site.data.keyword.Bluemix_notm}} privé, incluant l'espace de nom et le nom de l'image de destination. L'étiquette pour l'image est facultative.</dd>
   </dl>

<strong>Exemples</strong> :

Copiez une image depuis le référentiel source dans votre référentiel privé et ajoutez une étiquette pour l'image :

```
bluemix ic cpi référentiel_source/nom_image_source URL_registre_privé/nom_image_destination:étiquette
```

Copiez l'image `sinatra` depuis le référentiel `training` dans votre référentiel privé `registry.ng.bluemix.net/monespacenom` et nommez l'image `monimagesinatra`. Ajoutez une étiquette `v1` pour l'image `monimagesinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/monespacenom/monimagesinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

Exécutez une commande dans un conteneur. Pour plus d'informations, voir la commande [exec ](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u UTILISATEUR|--user UTILISATEUR] CONTENEUR [CMD]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-d|--detach (facultatif)</dt>
   <dd>Indique d'exécuter en arrière-plan la commande spécifiée.</dd>
   <dt>-it (facultatif)</dt>
   <dd>Mode interactif. L'entrée standard continue d'être affichée. Entrez <i>exit</i> pour quitter.</dd>
   <dt>-u <i>UTILISATEUR</i>|--user <i>UTILISATEUR</i> (facultatif)</dt>
   <dd>Nom de l'utilisateur.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt><i>CMD</i> (facultatif)</dt>
   <dd>Commande à exécuter dans le(s) conteneur(s) spécifié(s).</dd>
   </dl>

<strong>Exemples</strong> :

Exécutez la commande `bash` dans le conteneur `mon_conteneur` en mode interactif :

```
bluemix ic exec -it mon_conteneur bash
```

Exécutez la commande `date` dans le conteneur `mon_conteneur` :

```
bluemix ic exec mon_conteneur date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

Créez un groupe de conteneurs évolutif.

```
bluemix ic group-create [--publish,-p PORT] --name NOM_GROUPE [--memory,-m TAILLE_MEMOIRE] [-n,--hostname NOM_HOTE] [-d,--domain DOMAINE] [--env,-e ENV_KEY=VAL_ENV] [--env-file FICHIER_VARIABLE_ENVIRONNEMENT] [-P false|true] [--volume] [--min NOMBRE_MIN_INSTANCES] [--max NOMBRE_MAX_INSTANCES] [--desired NOMBRE_INSTANCES_SOUHAITE] [--anti false|true] [--auto false|true] NOM_IMAGE [CMD [CMD ...]]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
    <dt><i>NOM_IMAGE</i> (requis)</dt>
   <dd>Image à inclure dans chaque instance de conteneur dans le groupe de conteneurs. Vous pouvez spécifier des commandes après l'image, mais n'indiquez pas d'options. Incluez toutes les options avant de spécifier une image. <br><br>Si vous utilisez une image qui se trouve dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation, spécifiez l'image au format <i>registry.ng.bluemix.net/ESPACE_NOM/IMAGE</i>. <br><br>Si vous utilisez une image fournie par IBM Containers, n'incluez pas l'espace de nom de votre organisation. Spécifiez l'image au format <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>NOM_GROUPE</i> (requis)</dt>
   <dd>Attribue un nom au groupe. <i>-n</i> est obsolète.<br>
   <strong>Astuce :</strong> le nom de conteneur doit commencer par une lettre. Il peut inclure des lettres majuscules, des
lettres minuscules, des chiffres, des points, des traits de soulignement (_) ou des traits d'union (-).</dd>
   <dt>-m <i>TAILLE_MEMOIRE</i>|--memory <i>TAILLE_MEMOIRE</i> (facultatif)</dt>
   <dd>Affecte une limite de mémoire, en Mo, au groupe. Lorsque vous créez un groupe de conteneurs depuis l'interface de ligne de commande, la valeur par défaut pour chaque instance de conteneur est <i>64</i> Mo. Lorsque vous créez un groupe de conteneurs depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}, la valeur par défaut pour chaque instance de conteneur est <i>256</i> Mo. Les valeurs admises sont <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> et <i>2048</i>. Une fois que vous avez affecté une limite de mémoire, vous ne pouvez plus la modifier.</dd>
   <dt>-n <i>NOM_HOTE</i>|--hostname <i>NOM_HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte, tel que <i>monhôteconteneur</i>. L'hôte et le domaine sont combinés pour former l'adresse URL de route publique complète, par exemple <i>http://monhôteconteneur.mybluemix.net</i>. Lorsque vous passez en revue les détails d'un groupe de conteneurs avec la commande <i>bluemix ic group-inspect</i>, l'hôte et le domaine sont affichés ensemble et constituent la route.</dd>
   <dt>-d <i>DOMAINE</i>|--domain <i>DOMAINE</i> (facultatif)</dt>
   <dd>Généralement, le domaine est <i>.mybluemix.net</i>. L'hôte et le domaine sont combinés pour former l'adresse URL de route publique complète, par exemple <i>http://monhôteconteneur.mybluemix.net</i>. Lorsque vous passez en revue les détails d'un groupe de conteneurs avec la commande <i>bluemix ic group-inspect</i>, l'hôte et le domaine sont affichés ensemble et constituent la route.</dd>
   <dt>-e <i>CLE_ENV=VAL_ENV</i>|--env <i>CLE_ENV=VAL_ENV</i> (facultatif)</dt>
   <dd>Définissez la variable d'environnement. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Par exemple : `-e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3"`.  Le tableau suivant répertorie certaines variables d'environnement couramment utilisées que vous pouvez spécifier :</dd>
    </dl>


|  Variable d'environnement                              |     Description                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nom_app&gt;*       | Liez un service à un conteneur. Utilisez la variable d'environnement `CCS_BIND_APP` pour lier
une application au conteneur. L'application est liée au service cible et sert de pont qui permet à {{site.data.keyword.Bluemix_notm}} de fournir les informations contenues dans la variable `VCAP_SERVICES` de votre application pont à votre instance de conteneur en cours d'exécution.|
| CCS_BIND_SRV=*&lt;nom_instance_service1&gt;*,*&lt;nom_instance_service2&gt;* | Pour lier un service Bluemix directement à un
conteneur sans utiliser d'application de pont, utilisez CCS_BIND_SRV. Cette liaison permet à Bluemix d'injecter les informations VCAP_SERVICES dans
l'instance de conteneur en cours d'exécution. Pour répertorier plusieurs services Bluemix, incluez-les dans la même variable d'environnement. |
| LOG_LOCATIONS=*&lt;chemin_fichier&gt;* | Ajoutez un fichier journal à surveiller dans le conteneur. Incluez la variable d'environnement `LOG_LOCATIONS` avec un chemin d'accès au fichier journal. |
{: caption="Table 8. Commonly used environment variables" caption-side="top"}


 <dl>
   <dt>--env-file <i>FICHIER_VARIABLE_ENVIRONNEMENT</i> (facultatif)</dt>
   <dd> Importe les variables d'environnement d'un fichier, env-file étant le chemin d'accès au fichier sur le répertoire local. Chaque ligne du fichier représente une paire clé=valeur. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CHEMIN_CONTENEUR</i>[:ro] (facultatif)</dt>
   <dd>Rattache un volume à un conteneur en spécifiant ses détails sous le format <i>ID_volume:Chemin_conteneur[:ro]</i>.
   <ul>
   <li><i>VOLUME</i> : ID ou nom du volume.</li>
   <li><i>CHEMIN_CONTENEUR</i> : Chemin absolu du volume dans le conteneur.</li>
   <li>ro (facultatif) : La spécification de <i>ro</i> rend le volume accessible en lecture seule, au lieu de le laisser accessible par défaut en lecture/écriture.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (facultatif)</dt>
   <dd>Expose le port pour le trafic HTTP. Les conteneurs qui se trouvent dans votre groupe doivent être à l'écoute sur le port HTTP. Il n'est pas possible d'envoyer des demandes HTTPS. Vous ne pouvez pas inclure plusieurs ports pour les groupes de conteneurs. <br><br>Lorsque vous spécifiez un port, vous mettez l'application à disposition dans l'équilibreur de charge {{site.data.keyword.Bluemix_notm}} ou dans les conteneurs qui tentent d'accéder à l'hôte dans le même espace {{site.data.keyword.Bluemix_notm}}. L'équilibreur de charge ou les conteneurs {{site.data.keyword.Bluemix_notm}} peuvent alors utiliser le port pour joindre l'hôte et l'application dans le même espace {{site.data.keyword.Bluemix_notm}}. Si un port est spécifié dans le document Dockerfile pour l'image que vous utilisez, incluez ce port. <br>
   <strong>Conseils </strong>: <ul>
   <li>Pour l'image Liberty Server certifiée IBM, ou une version modifiée de cette image, entrez le port 9080.</li>
   <li>Pour l'image Node.js certifiée IBM, ou une version modifiée de cette image, entrez le port 8000.</li>
   </ul>
   </dd>
   <dt>-P (facultatif)</dt>
   <dd>Publie tous les ports</dd>
   <dt>--min <i>NOMBRE_MIN_INSTANCES</i> (facultatif)</dt>
   <dd>Nombre minimal d'instances. La valeur par défaut est 1. Si vous définissez un nombre minimum d'instances, cette valeur ne peut plus être modifiée après la création du groupe de conteneurs.</dd>
   <dt>--max <i>NOMBRE_MAX_INSTANCES</i> (facultatif)</dt>
   <dd>Nombre maximal d'instances. La valeur par défaut est 2. Si vous définissez un nombre maximum d'instances, cette valeur ne peut plus être modifiée après la création du groupe de conteneurs.</dd>
   <dt>--desired <i>NOMBRE_INSTANCES_SOUHAITE</i> (facultatif)</dt>
   <dd>Nombre d'instances dont vous avez besoin. La valeur par défaut est 2.</dd>
   <dt>--auto (facultatif)</dt>
   <dd>Lorsque le groupe de conteneurs est créé et que la reprise automatique est activée, IBM Containers vérifie la santé de chaque instance en envoyant une demande HTTP au port affecté.<br>
   Si aucune réponse n'est reçue d'une instance de conteneur aux cours de deux intervalles consécutifs de 90 secondes, l'instance est supprimée et remplacée par une nouvelle instance. Aucune action n'est effectuée si le conteneur répond. Ce processus est répété en permanence. Au cours d'une fenêtre de 30 minutes, si le nombre total de conteneurs différents qui sont membres du groupe est égal ou supérieur à trois fois la taille maximale observée pour le groupe, la reprise automatique est désactivée définitivement pour le groupe de conteneurs. Pour l'activer à nouveau, vous devez recréer le groupe de conteneurs.</dd>
  <dt>--anti (facultatif)</dt>
  <dd> Utilisez l'anti-affinité pour élever le niveau de haute disponibilité de votre groupe de conteneurs. L'option --anti force chaque instance de conteneur de votre groupe à être placée sur un noeud de traitement physique distinct, ce qui réduit les chances que tous les conteneurs d'un groupe tombent en panne en même temps en cas de défaillance matérielle. Il se peut que vous ne puissiez pas utiliser cette option avec des tailles de groupe plus importantes car chaque région et organisation Bluemix possède un ensemble limité de noeuds de traitement disponibles pour déploiement. Si votre déploiement échoue, vous pouvez soit réduire le nombre d'instances de conteneur dans le groupe, soit retirer l'option --anti. </dd>
   <dt><i>CMD</i> (facultatif)</dt>
   <dd>Commande et arguments transmis au groupe de conteneurs pour exécution. Cette commande doit être une commande à exécution longue. N'utilisez pas de commande à exécution courte, c'est-à-dire qui ne s'exécute pas très longtemps, comme <i>/bin/date</i>, car elle pourrait entraîner la panne du conteneur.  <br> <strong>Remarques :</strong> <ul>
   <li>La commande et les arguments doivent être spécifiés à la fin de la ligne de commande <i>bluemix ic run</i>.</li>
   <li>Si les arguments de commande incluent un trait d'union (-), comme dans <i>-c</i> dans l'exemple de commande précédent, la commande doit être précédée par deux traits d'union (--).</li>
   </ul></dd>
   </dl>


<strong>Exemples</strong> :

Créez un groupe de conteneurs `mon_groupe_conteneurs` en utilisant l'image `registry.ng.bluemix.net/ibmnode` fournie par IBM Containers, puis exécutez la commande à exécution longue `ping localhost` sur ce groupe de conteneurs :

```
bluemix ic group-create --name mon_groupe_conteneurs registry.ng.bluemix.net/ibmnode ping localhost
```

Créez un groupe de conteneurs `mon_groupe_conteneurs` en utilisant l'image `registry.ng.bluemix.net/ibmnode` fournie par IBM Containers, puis exécutez la commande à exécution longue `tail -f /dev/null` sur ce groupe de conteneurs :

```
bluemix ic group-create --name mon_groupe_conteneurs registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Créez un groupe évolutif `mongroupe` pour lequel la reprise automatique est activée en utilisant l'image `registry.ng.bluemix.net/ibmliberty`. Le port est `9080`, le nom d'hôte est `monhôteconteneur` et le nom de domaine est `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n monhôteconteneur -d mybluemix.net --name mongroupe registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Affichez les informations détaillées, comme les variables d'environnement, les ports ou la mémoire, qui sont spécifiées pour un groupe de conteneurs lors de sa création.

```
bluemix ic group-inspect GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'inspection du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-inspect mon_groupe
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

Répertoriez les instances d'un groupe de conteneurs spécifié.

```
bluemix ic group-instances GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

Répertoriez toutes les instances du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-instances mon_groupe
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

Retirez un groupe de conteneurs d'un espace.

```
bluemix ic group-remove [-f|--force] NOM_GROUPE [GROUP_NAME2 [...]]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-f|--force (facultatif)</dt>
   <dd>Force le retrait d'un conteneur en exécution ou défaillant.</dd>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait d'un groupe de conteneurs dont le nom est `mon_groupe` :
```
bluemix ic group-remove mon_groupe
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

Mettez à jour un groupe de conteneurs.


```
bluemix ic group-update [--anti] [--desired NOMBRE_INSTANCES_SOUHAITE] [-e ENV_KEY=VAL_ENV] NOM_GROUPE
```

**Astuce :** afin de mettre à jour le nom d'hôte ou le domaine pour un groupe de conteneurs, utilisez `bluemix ic route-map [-n HOTE][-d DOMAIN] GROUPE_CONTENEURS`.

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
 <dl>
   <dt>--anti (facultatif)</dt>
   <dd>Utilisez l'anti-affinité pour élever le niveau de haute disponibilité de votre groupe de conteneurs. L'option --anti force chaque instance de conteneur de votre groupe à être placée sur un noeud de traitement physique distinct, ce qui réduit les probabilités que tous les conteneurs d'un groupe tombent en panne en même temps en cas de défaillance matérielle. Il se peut que vous ne puissiez pas utiliser cette option avec des tailles de groupe plus importantes car chaque région et organisation Bluemix possède un ensemble limité de noeuds de traitement disponibles pour déploiement. Si votre déploiement échoue, vous pouvez soit réduire le nombre d'instances de conteneur dans le groupe, soit retirer l'option --anti.</dd>
   <dt>--desired <i>NOMBRE_INSTANCES_SOUHAITE</i> (facultatif)</dt>
   <dd>Nombre d'instances dont vous avez besoin. La valeur par défaut est <i>2</i>.</dd>
   <dt>-e <i>CLE_ENV=VAL_ENV</i>(facultatif)</dt>
   <dd>Définissez la variable d'environnement. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Par exemple : `-e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3"`.</dd>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de mise à jour du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-update --desired 5 mon_groupe
```


### bluemix ic groups
{: #bluemix_ic_groups}

Répertoriez les groupes de conteneurs qui existent dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation.

```
bluemix ic groups [-q]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
	<dl>
	<dt>-q (facultatif)</dt>
   	<dd>Affiche uniquement les ID groupe</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

Affichez la liste de toutes les images disponibles dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation. Pour plus d'informations, voir la commande [images ](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker. La liste inclut l'ID de l'image, la date de création et le nom de l'image.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-a|--all (facultatif)</dt>
   <dd>Indique d'inclure toutes les couches d'image pour chaque image dans le référentiel de votre organisation, et non pas seulement la couche la plus récente.</dd>
   <dt>-f (facultatif)</dt>
   <dd>Filtre la liste des images en fonction de la condition fournie.</dd>
   <dt>--no-trunc (facultatif)</dt>
   <dd>Indique de ne pas tronquer la sortie.</dd>
   <dt>-q|--quiet (facultatif)</dt>
   <dd>Indique d'afficher uniquement les ID numériques.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de réception de la liste des images disponibles pour l'organisation :
```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

Affichez un ensemble d'informations décrivant l'état de l'instance de service cloud de conteneur. Les informations incluent la limite relative aux conteneurs, l'utilisation des conteneurs, les conteneurs en cours d'exécution, la limite de mémoire, l'utilisation de la mémoire, la limite relative aux adresses IP flottantes, l'utilisation des adresses IP flottantes, l'adresse URL de l'hôte CCS, l'adresse URL de l'hôte du registre et le statut du mode débogage.

```
bluemix ic info
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


### bluemix ic init
{: #bluemix_ic_init}

Initialisez l'environnement des conteneurs sur votre machine locale afin d'utiliser l'ensemble des capacités du service IBM Containers.

```
bluemix ic init
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

**Remarque :** avant l'initialisation, assurez-vous que l'interface de ligne de commande Docker (docker) est installée et configurée dans votre variable d'environnement PATH. Pour passer dans une autre région, utilisez la commande `bluemix region-set`.

<strong>Exemples</strong> :

Passez dans la région `us-south` :

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

Affichez les informations sur un conteneur. Pour plus d'informations,
voir la commande
[inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window}
dans l'aide de Docker.

```
bluemix ic inspect [IMAGE|images|CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>IMAGE</i> (requis)</dt>
   <dd>Affiche des informations détaillées sur une image spécifique en indiquant son nom ou son ID.</dd>
   <dt>images (requis)</dt>
   <dd>Affiche des informations détaillées sur toutes les images de votre référentiel.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Affiche des informations détaillées sur un conteneur spécifique en indiquant son nom ou son ID.</dd>
   </dl>

**Remarque :** vous ne pouvez spécifier qu'un seul des arguments suivants à la fois : *IMAGE*, *images* ou *CONTENEUR*.

<strong>Exemples</strong> :

L'exemple suivant est une demande d'inspection d'un conteneur dont le nom est `proxy` :
```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Liez une adresse IP flottante disponible à un conteneur.

```
bluemix ic ip-bind ADRESSE_IP CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>ADRESSE_IP</i> (requis)</dt>
   <dd>Adresse IP à lier.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur à lier.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de liaison de l'adresse IP `192.123.12.12` au conteneur `proxy` :
```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

Libérez une adresse IP flottante de l'instance de service cloud de conteneur.

```
bluemix ic ip-release ADRESSE_IP [ADRESSE2_IP [...]]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>ADRESSE_IP</i> (requis)</dt>
   <dd>Adresse IP à libérer.</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
Demandez une nouvelle adresse IP flottante.

```
bluemix ic ip-request [-q]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-q (facultatif)</dt>
   <dd>Répertorie uniquement les adresses IP, sans les ID des conteneurs qui sont liés à ces adresses IP.</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Annulez la liaison d'une adresse IP flottante à son conteneur.

Les adresses IP publiques constituent une ressource limitée dans IBM Containers. Par conséquent, les adresses IP publiques qui sont allouées à un espace et qui ne sont pas liées à un conteneur sont régulièrement récupérées auprès des utilisateurs de l'essai gratuit, environ toutes les semaines. Les adresses IP publiques non liées ne sont jamais récupérées auprès des utilisateurs facturés ponctuellement ou disposant d'un abonnement.

```
bluemix ic ip-unbind ADRESSE_IP CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>ADRESSE_IP</i> (requis)</dt>
   <dd>Adresse IP pour laquelle annuler la liaison.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>ID ou nom du conteneur pour lequel annuler la liaison.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'annulation de la liaison de l'adresse IP `192.123.12.12` au conteneur `proxy` :
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

Répertoriez les adresses IP flottantes disponibles pour l'utilisateur connecté. La liste répertorie les adresses IP et l'ID de conteneur auquel les adresses IP sont liées. Si l'adresse IP n'est pas utilisée, aucun ID de conteneur n'est affiché.

```
bluemix ic ips [-q]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-q (facultatif)</dt>
   <dd>Répertorie uniquement les adresses IP, sans les ID des conteneurs qui sont liés à ces adresses IP.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant illustre une demande de réception de la liste de toutes les adresses IP disponibles pour l'organisation :
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

Arrêtez un processus en cours dans un conteneur sans arrêter le conteneur. Pour plus d'informations, voir la commande [kill ](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (facultatif)</dt>
   <dd>Envoie une commande au processus s'exécutant dans le conteneur.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>ID ou nom du conteneur.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande d'arrêt du processus dans un conteneur dont le nom est `proxy` :
```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

Affiche les journaux de sortie ou d'erreur d'un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [logs ](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.
```
bluemix ic logs [OPTIONS] CONTENEUR
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Affichez le nom du référentiel d'images {{site.data.keyword.Bluemix_notm}} privé pour l'organisation à laquelle vous êtes connecté.

```
bluemix ic namespace-get
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Définissez le nom du référentiel d'images {{site.data.keyword.Bluemix_notm}} privé pour l'organisation à laquelle vous êtes connecté.

*Restriction* : vous ne pouvez pas utiliser de trait d'union (`-`) dans le nom d'espace de nom de votre référentiel.

```
bluemix ic namespace-set NOM
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM</i> (requis)</dt>
   <dd>Fonction exécutée une seule fois pour définir l'espace de nom du référentiel de votre organisation, si ce n'est déjà fait. Une fois l'espace de nom défini, réinitialisez IBM Containers avec la commande `bluemix ic init` avant de continuer.</dd>
   </dl>


### bluemix ic pause
{: #pause}

Interrompez tous les processus d'un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [pause ](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker. Pour arrêter un conteneur, voir la commande [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :
   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Paused container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande d'interruption d'un conteneur dont le nom est `proxy` :
```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

Répertoriez les mappages de port ou un mappage spécifique pour le conteneur. Cette commande encapsule la commande `docker port`. Pour plus d'informations, voir la commande [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.


### bluemix ic ps
{: #bluemix_ic_ps}
Affichez la liste des conteneurs en cours d'exécution dans l'espace de nom de l'utilisateur connecté. Par défaut, cette commande affiche seulement les conteneurs en cours d'exécution. Pour plus d'informations, voir la commande [ps ](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic ps [-a|--all] [--filter env=CRITERES_RECHERCHE] [-s|--size] [-l NOMBRE|--limit NOMBRE] [-q|--quiet]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-a|--all (facultatif)</dt>
   <dd>Affiche tous les conteneurs, qu'ils soient en exécution ou arrêtés.</dd>
   <dt>--filter env=<i>CRITERES_RECHERCHE</i> (facultatif)</dt>
   <dd>Recherche les conteneurs possédant une valeur de variable d'environnement spécifique. Vous pouvez filtrer vos conteneurs en fonction d'une clé de variable d'environnement ou d'une valeur répertoriée dans la section Env de votre réponse d'interface de ligne de commande lorsque vous inspectez un conteneur. Remplacez CRITERES_RECHERCHE par la clé ou la valeur recherchée. Vos critères de recherche n'ont pas besoin de renvoyer une correspondance exacte. </dd>
   <dt>-s|--size (facultatif)</dt>
   <dd>Répertorie les tailles des conteneurs.</dd>
   <dt>-l <i>NOMBRE</i>|--limit <i>NOMBRE</i> (facultatif)</dt>
   <dd>Répertorie les conteneurs les plus récemment créés, où <i>NOMBRE</i> est le nombre de ces conteneurs que vous désirez renvoyer. <br><br> Par exemple, si vous
avez créé séquentiellement les conteneurs <i>node1</i> à <i>node5</i>, la commande <i>bluemix ic ps --limit 2</i> renvoie node4 et node5 puisqu'il s'agit des
deux derniers conteneurs créés. </dd>
   <dt>-q|--quiet (facultatif)</dt>
   <dd>Indique d'afficher uniquement les ID des conteneurs.</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande d'affichage de tous les conteneurs en cours d'exécution et arrêtés :
```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
Renomme un conteneur. Pour plus d'informations, voir la commande [rename ](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic rename ANCIEN_NOM NOUVEAU_NOM
```
<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

<dl>
   <dt><i>ANCIEN_NOM</i> (requis)</dt>
   <dd>Ancien nom du conteneur.</dd>
   <dt><i>NOUVEAU_NOM</i> (requis)</dt>
   <dd>Nouveau nom du conteneur.</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

Recrée le service IBM Containers dans l'espace Bluemix auquel vous êtes connecté. Le quota d'origine pour l'espace est conservé.

<strong>Important</strong> : lorsque vous exécutez cette commande, aucun de vos conteneurs et groupes de conteneurs contenus dans cet espace ne sera
migrés vers l'espace qui est remis à disposition et vos conteneurs et groupes seront retirés lors du processus de migration.

```
bluemix ic reprovision [--force|-f] [ZONE_DISPONIBILITE]
```
<strong>Options de commande</strong> :

<dl>
   <dt>--force|-f (facultatif)</dt>
   <dd>Force la recréation du service IBM Containers dans l'espace Bluemix.</dd>
   <dt><i>ZONE_DISPONIBILITE</i> (facultatif)</dt>
   <dd>Nom de la zone de disponibilité IBM Containers dans laquelle vos conteneurs sont déployés. Si aucune zone de disponibilité n'est spécifiée, la zone de disponibilité par défaut définie pour la région est utilisée.</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

Redémarrer un conteneur. Pour plus d'informations, voir la commande [restart ](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic restart CONTENEUR [-t SECS|--time SECS]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (facultatif)</dt>
   <dd>Nombre de secondes pendant lesquelles patienter avant le redémarrage du conteneur.</dd>
   </dl>


<strong>Réponses</strong> :

- Restarted container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande de redémarrage d'un conteneur dont le nom est `proxy` :
```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

Supprimez un conteneur. Pour plus d'informations, voir la commande [rm ](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic rm [-f|--force] CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-f|--force (facultatif)</dt>
   <dd>Force le retrait d'un conteneur en exécution ou défaillant.</dd>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Removed container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service.

<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait d'un conteneur dont le nom est `proxy` :
```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

Supprimez une image de l'espace de nom de l'utilisateur connecté. Pour plus d'informations, voir la commande [rmi ](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic rmi [-R REGISTRE|--registry REGISTRE] IMAGE
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-R <i>REGISTRE</i>|--registry <i>REGISTRE</i> (facultatif)</dt>
   <dd>Changer l'hôte de registre. Par défaut, le registre que vous spécifiez dans la commande <i>bluemix ic init</i> est utilisé.</dd>
   <dt><i>IMAGE</i> (requis)</dt>
   <dd>Nom de l'image à supprimer. Si aucune étiquette n'est spécifiée dans le nom de l'image, l'image associée à l'étiquette <i>latest</i> est supprimée par défaut.</dd>
   </dl>

<strong>Réponses</strong> :

- Removed: `{IMAGE}`

 Où `{IMAGE}` est le nom de l'image qui a été supprimée.

- Error! No registry host specified.

- Image remove failed - Could not connect to container cloud registry

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait de l'image `monespacenom/monimage:latest` :
```
bluemix ic rmi registry.ng.bluemix.net/monespacenom/monimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

Etablissez la route pour le trafic Internet à utiliser pour accéder au groupe de conteneurs. Vous pouvez utiliser cette commande pour établir une nouvelle route ou mettre à jour une route existante.

```
bluemix ic route-map [-n HOTE|--hostname HOTE] [-d DOMAINE|--domain DOMAINE] GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-n <i>HOTE</i>|--hostname <i>HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route. Il s'agit de la première partie de l'adresse URL de route publique complète, par exemple <i>monhôteconteneur</i> dans l'adresse URL <i>monhôteconteneur.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAINE</i>|--domain <i>DOMAINE</i> (facultatif)</dt>
   <dd>Nom de domaine pour la route, qui constitue la seconde partie de l'URL complète de route publique. Dans la plupart des cas, le domaine est
<i>mybluemix.net</i>. Vous pouvez aussi utiliser ce paramètre pour spécifier un domaine privé.</dd>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple ci-dessous illustre une demande de mappage de la route du groupe appelé `GROUPE1`, où `mon_hôte` est le
nom de l'hôte et `mybluemix.net` est le domaine.
```
bluemix ic route-map -n mon_hôte -d mybluemix.net GROUPE1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Etablissez la route pour le trafic Internet à utiliser pour accéder au groupe de conteneurs. Vous pouvez utiliser cette commande pour établir une nouvelle route ou mettre à jour une route existante.

```
bluemix ic route-unmap [-n HOTE|--hostname HOTE] [-d DOMAINE|--domain DOMAINE] GROUPE_CONTENEURS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>-n <i>HOTE</i>|--hostname <i>HOTE</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route.</dd>
   <dt>-d <i>DOMAINE</i>|--domain <i>DOMAINE</i> (facultatif)</dt>
   <dd>Nom de domaine de la route.</dd>
   <dt><i>GROUPE_CONTENEURS</i> (requis)</dt>
   <dd>ID ou nom du groupe de conteneurs.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant illustre une demande d'annulation du mappage de la route du groupe intitulé `GROUPE1`, où `mon_hôte` est le
nom de  l'hôte et `organization.com`, le domaine.
```
bluemix ic route-unmap -n mon_hôte -d organisation.com GROUPE1
```


### bluemix ic run
{: #bluemix_ic_run}

Démarrez un nouveau conteneur dans le service cloud de conteneur depuis un nom d'image. Pour plus d'informations, voir la commande [run ](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMOIRE|--memory MEMOIRE] [-e ENV|--env ENV] [-volume VOLUME:CHEMIN_CONTENEUR] -n NOM|--name NOM [--link
NOM:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Remarque :** vérifiez que l'outil de commandes Cloud Foundry est installé et que vous disposez d'un jeton Cloud Foundry. L'aboutissement
d'une connexion à l'aide de `bluemix login` et de `bluemix ic init` génère le jeton et les certificats requis.


<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (facultatif)</dt>
   <dd>Expose le port pour le trafic HTTP. Incluez tous les ports spécifiés dans le document Dockerfile pour l'image que vous utilisez. Vous pouvez inclure plusieurs ports avec plusieurs options <i>-p</i>. L'exposition d'un port lie automatiquement une adresse IP publique au conteneur si une telle adresse est disponible. <br><br>Si une adresse IP existe dans l'espace à lier au conteneur, vous pouvez la spécifier plutôt que de procéder à la liaison ultérieurement. L'adresse IP doit être spécifiée au format &lt;adresse_ip&gt;:&lt;port_conteneur&gt;:&lt;port_conteneur&gt; <br><br>Pour plus d'informations sur la demande d'adresses IP pour un espace, voir la commande <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Lorsque vous spécifiez un port, vous rendez l'application disponible dans l'équilibreur de charge {{site.data.keyword.Bluemix_notm}} ou dans les conteneurs du même espace {{site.data.keyword.Bluemix_notm}} qui tentent d'accéder à l'hôte. Si un port est spécifié dans le document Dockerfile pour l'image que vous utilisez, incluez ce port. <br><br><strong>Conseils :</strong><ul><li>Pour l'image Liberty Server certifiée IBM, ou une version modifiée de cette image, entrez le port 9080.</li><li>Pour l'image Node.js certifiée IBM, ou une version modifiée de cette image, entrez le port 8000.</li></ul></dd>
   <dt>-P (facultatif)</dt>
   <dd>Expose automatiquement au trafic HTTP les ports spécifiés dans le fichier Dockerfile de l'image.</dd>
   <dt>-m <i>MEMOIRE</i>|--memory <i>MEMOIRE </i> (facultatif)</dt>
   <dd>Affecte une limite de mémoire, en Mo, au groupe. Lorsque vous créez un groupe de conteneurs depuis l'interface de ligne de commande, la valeur par défaut pour chaque instance de conteneur est 64 Mo.  Lorsque vous créez un groupe de conteneurs depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}, la valeur par défaut est 256 Mo. Les valeurs admises sont : 64, 256, 512, 1024 et 2048 Mo. Une fois que vous avez affecté une limite de mémoire, vous ne pouvez plus la modifier.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (facultatif)</dt>
   <dd>Définit la variable d'environnement, où <i>ENV</i> représente une paire clé=valeur. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Par exemple : -e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3". Le tableau suivant répertorie certaines variables d'environnement couramment utilisées que vous pouvez spécifier :</dd>
   </dl>


|      Variable d'environnement                          |   Description                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nom_app&gt;*       | Liez un service à un conteneur. Utilisez la variable d'environnement `CCS_BIND_APP` pour lier
une application au conteneur. L'application est liée au service cible et sert de pont qui permet à {{site.data.keyword.Bluemix_notm}} de fournir les informations contenues dans la variable `VCAP_SERVICES` de votre application pont dans votre instance de conteneur en cours d'exécution. Pour plus d'informations sur la création d'une application pont, voir
[Liaison d'un service à un conteneur](/docs/containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nom_instance_service1&gt;*,*&lt;nom_instance_service2&gt;* | Pour lier un service Bluemix directement à un
conteneur sans utiliser d'application de pont, utilisez CCS_BIND_SRV. Cette liaison permet à Bluemix d'injecter les informations VCAP_SERVICES dans
l'instance de conteneur en cours d'exécution. Pour répertorier plusieurs services Bluemix, incluez-les dans la même variable d'environnement. |
| LOG_LOCATIONS=*&lt;chemin_fichier&gt;* | Ajoutez un fichier journal à surveiller dans le conteneur. Incluez la variable d'environnement `LOG_LOCATIONS` avec un chemin d'accès au fichier journal. |
{: caption="Table 9. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CHEMIN_CONTENEUR</i>[:ro] (facultatif)</dt>
   <dd>Rattache un volume à un conteneur en spécifiant ses détails sous le format <i>ID_volume:Chemin_conteneur[:ro]</i>.
   <ul>
   <li><i>VOLUME</i> : ID ou nom du volume.</li>
   <li><i>CHEMIN_CONTENEUR</i> : Chemin absolu du volume dans le conteneur.</li>
   <li>ro (facultatif) : La spécification de <i>ro</i> rend le volume accessible en lecture seule, au lieu de le laisser accessible par défaut en lecture/écriture.</li></ul>
   </dd>
   <dt>-n <i>NOM</i>|--name <i>NOM</i> (requis)</dt>
   <dd>Attribue un nom au conteneur. <br> <strong>Astuce :</strong> le nom de conteneur doit commencer par une lettre. Il peut inclure des lettres majuscules, des
lettres minuscules, des chiffres, des points, des traits de soulignement (_) ou des traits d'union (-).</dd>
   <dt>--link <i>NOM</i>:<i>ALIAS</i> (facultatif)</dt>
   <dd>Chaque fois que vous désirez qu'un conteneur communique avec un autre en exécution, vous pouvez le désigner en utilisant un alias pour le nom d'hôte.</dd>
   <dt>-it (facultatif)</dt>
   <dd>Indique d'exécuter le conteneur en mode interactif. Une fois le conteneur créé, l'entrée standard continue d'être affichée. Entrez <i>exit</i> pour quitter.</dd>
   <dt><i>IMAGE</i> (requis)</dt>
   <dd>Image à inclure dans le conteneur. Vous pouvez spécifier des commandes après l'image, mais n'indiquez pas d'options. Incluez toutes les options avant de spécifier une image. Incluez toutes les options avant de spécifier une image. <br><br>Si vous utilisez une image qui se trouve dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation, spécifiez l'image au format <i>registry.ng.bluemix.net/ESPACE_NOM/IMAGE</i>. <br><br>Si
vous utilisez une image fournie par IBM Containers, spécifiez-la sous le format : <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (facultatif)</dt>
   <dd>Commande et arguments transmis au groupe de conteneurs pour exécution. Cette commande doit être une commande à exécution longue. N'utilisez pas de commande à exécution courte, c'est-à-dire qui ne s'exécute pas très longtemps, comme <i>/bin/date</i>, car elle pourrait entraîner la panne du conteneur.</dd>
   </dl>


<strong>Exemples</strong> :

Exécutez la commande à exécution longue `sh -c "while true; do date; sleep 20; done"` sur le conteneur `mon_conteneur` construit sur l'image `registry.ng.bluemix.net/ibmnode`.
```
bluemix ic run --name mon_conteneur registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Créez et démarrez un conteneur `proxy` avec une limite de mémoire de `1024` Mo en utilisant l'image `mon_espace_nom/nginx`, où `mon_espace_nom` est l'espace de nom associé aux utilisateurs connectés.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/mon_espace_nom/nginx
```

Créez et démarrez un conteneur en utilisant l'image `mon_espace_nom/blog` et transmettez les données d'identification sous forme de variables d'environnement. `mon_espace_nom` est l'espace de nom associé aux utilisateurs connectés.
```
bluemix ic run -n mon_conteneur -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/mon_espace_nom/blog
```

Ajoutez un volume au conteneur en utilisant l'image `mon_espace_nom/blog`, où `mon_espace_nom` est l'espace de nom associé aux utilisateurs connectés.
```
bluemix ic run -n mon_conteneur -v IDVol1:/premier/chemin -v IDVol2:/deuxième/chemin registry.ng.bluemix.net/mon_espace_nom/blog
```


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

Ajoutez un service à un groupe de conteneurs en cours d'exécution. Cette commande est disponible uniquement pour les groupes de conteneurs. Les conteneurs doivent être liés à un service via la commande bluemix ic run.

```
bluemix ic service-bind NOM_GROUPE INSTANCE_SERVICE
```
<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe.</dd>
   <dt><i>INSTANCE_SERVICE</i> (requis)</dt>
   <dd>Nom de l'instance de service qui doit être ajouté au groupe de conteneurs.</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Suppression d'un service dans un groupe de conteneurs en exécution. Cette commande est disponible uniquement pour les groupes de conteneurs. Pour les conteneurs
uniques, vous devez supprimer le conteneur et en créer un nouveau sans le service.

```
bluemix ic service-unbind NOM_GROUPE INSTANCE_SERVICE
```
<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_GROUPE</i> (requis)</dt>
   <dd>ID ou nom du groupe.</dd>
   <dt><i>INSTANCE_SERVICE</i> (requis)</dt>
   <dd>Nom de l'instance de service qui doit être ajouté au groupe de conteneurs.</dd>
   </dl>


### bluemix ic start
{: #ic_start}
Démarrez un conteneur arrêté. Pour plus d'informations, voir la commande [start ](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker. Pour arrêter un conteneur, voir la commande [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>


<strong>Réponses</strong> :

- Started container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande de démarrage d'un conteneur dont le nom est `proxy` :
```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

Affichez les statistiques d'utilisation actuelles d'un ou de plusieurs conteneurs. Utilisez `CTRL+C` pour quitter. Pour plus d'informations, voir la commande
[stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window}
dans l'aide de Docker.

```
bluemix ic stats [--no-stream] CONTENEUR [CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt>--no-stream (facultatif)</dt>
   <dd>Indique d'afficher uniquement le dernier résultat, sans inclure les informations qui le précédent.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'affichage des statistiques les plus récentes sur un conteneur :
```
bluemix ic stats --no-stream mon_conteneur
```


### bluemix ic stop
{: #ic_stop}
Arrêtez un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [stop ](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker. Pour démarrer un conteneur, voir la commande [bluemix ic start](#ic_start).

```
bluemix ic stop CONTENEUR [-t SECS|--time SECS]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (facultatif)</dt>
   <dd>Nombre de secondes avant l'arrêt du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Stopped container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande d'arrêt d'un conteneur dont le nom est `proxy` :
```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

Affichez les processus en cours d'exécution dans le conteneur. Pour plus d'informations, voir la commande [top ](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic top CONTENEUR [CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'affichage des processus d'un conteneur dont le nom est `mon_conteneur`.
```
bluemix ic top mon_conteneur
```


### bluemix ic unpause
{: #unpause}

Reprenez l'exécution de tous les processus dans un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [unpause ](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker. Pour interrompre un conteneur, voir la commande [bluemix ic pause](#pause).

```
bluemix ic unpause CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Réponses</strong> :

- Unpaused container successfully.

- Command failed with container cloud service

 `{message}`

 Où `{message}` est l'erreur connexe.

- Command failed - Could not connect to container cloud service

<strong>Exemples</strong> :

L'exemple suivant est une demande de reprise d'un conteneur dont le nom est `proxy` :
```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

Supprime le service IBM Containers de l'espace Bluemix auquel vous êtes connecté.

<strong>Attention</strong> : lorsque vous exécutez cette commande, tous vos conteneurs et groupes de conteneurs sont perdus. Votre espace est toujours disponible dans Bluemix. Pour recommencer à utiliser le service IBM Containers, vous devez exécuter `bluemix ic reprovision` pour remettre le service IBM
Containers à disposition.

```
bluemix ic reprovision [--force|-f]
```
<strong>Options de commande</strong> :

<dl>
   <dt>--force|-f (facultatif)</dt>
   <dd>Force la suppression de Bluemix dans l'espace Bluemix.</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

Affichez la version de Docker et de l'API IBM Containers.

```
bluemix ic version
```

<strong>Prérequis</strong> : Docker

Pour afficher la version d'IBM Containers, exécutez `bluemix ic info`. Pour plus d'informations, voir la commande [version ](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

Créez un volume.

```
bluemix ic volume-create NOM_VOLUME NOM_PF
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_PF</i> (facultatif)</dt>
   <dd>Nom du partage de fichiers. Si aucun partage de fichiers n'est disponible ou indiqué, le volume sera généré sur le partage de fichiers par défaut
de l'espace.</dd>
   <dt><i>NOM_VOLUME</i> (requis)</dt>
   <dd>Nom du volume. Ce nom peut comporter des lettres en minuscules, des chiffres, des traits de soulignement (_) et des traits d'union (-).</dd>
   </dl>


<strong>Exemples</strong> :

L'exemple suivant est une demande de création d'un volume :
```
bluemix ic volume-create nom_volume nom_partage_fichiers
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Répertoriez les partages de fichiers.

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Crée un partage de fichiers.

```
bluemix ic volume-fs-create NOM_PARTAGE_FICHIERS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_PARTAGE_FICHIERS</i> (requis)</dt>
   <dd>Nom du partage de fichiers. Ce nom peut comporter des lettres en minuscules, des chiffres, des traits de soulignement (_) et des traits d'union (-).</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant illustre une demande de création d'un partage de fichiers.
```
bluemix ic volume-fs-create mon_partage_fichiers
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Répertorie toutes les versions de partage de fichiers.

```
bluemix ic volume-fs-flavors
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspectez un partage de fichiers.

```
bluemix ic volume-fs-inspect NOM_PARTAGE_FICHIERS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

  <dl>
  <dt><i>NOM_PARTAGE_FICHIERS</i> (requis)</dt>
   <dd>Nom du partage de fichiers.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple ci-dessous illustre une demande d'inspection d'un partage de fichiers, où `mon_partage_fichiers` est le nom du partage de
fichiers.
```
bluemix ic volume-fs-inspect mon_partage_fichiers
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Supprime un partage de fichiers.

```
bluemix ic volume-fs-remove NOM_PARTAGE_FICHIERS
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_PARTAGE_FICHIERS</i> (requis)</dt>
   <dd>Nom du partage de fichiers.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple ci-dessous illustre une demande de retrait d'un partage de fichiers, où `mon_partage_fichiers` est le nom du partage
de
fichiers.
```
bluemix ic volume-fs-remove mon_partage_fichiers
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspectez un volume.

```
bluemix ic volume-inspect NOM_VOLUME
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_VOLUME</i> (requis)</dt>
   <dd>Nom du volume.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande d'inspection d'un volume, où `nom_volume` est le nom du volume :
```
bluemix ic volume-inspect nom_volume
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Retirez un volume.

```
bluemix ic volume-remove NOM_VOLUME
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt><i>NOM_VOLUME</i> (requis)</dt>
   <dd>Nom du volume.</dd>
    </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de retrait d'un volume, où `nom_volume` est le nom du volume :
```
bluemix ic volume-remove nom_volume
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

Répertoriez les volumes.

```
bluemix ic volumes
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible


### bluemix ic wait
{: #bluemix_ic_wait}

Quittez un conteneur et affichez le code de sortie comme confirmation. Pour plus d'informations, voir la commande [wait ](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg) dans l'aide de Docker.

```
bluemix ic wait CONTENEUR [CONTENEUR]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de sortie d'un conteneur dont le nom est `mon_conteneur` :
```
bluemix ic wait mon_conteneur
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

Indique d'attendre qu'un conteneur unique ou un groupe de conteneurs passe à un état non transitoire. Pendant cette attente, la ligne de commande ne renvoie pas de résultat et vous ne pouvez pas entrer de
commandes. Dès que le conteneur passe à un état non transitoire, un message OK s'affiche. Pour les conteneurs uniques, les états non transitoires sont notamment les suivants : En cours d'exécution, Arrêt, En panne, En pause ou Suspendu. Pour les groupes de conteneurs, les états non transitoires sont notamment les suivants : CREATE_COMPLETE, UPDATE_COMPLETE ou FAILED

```
bluemix ic wait-status CONTENEUR
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible, Docker

<strong>Options de commande</strong> :

   <dl>
   <dt><i>CONTENEUR</i> (requis)</dt>
   <dd>Nom ou ID du conteneur.</dd>
   </dl>

<strong>Exemples</strong> :

L'exemple suivant est une demande de sortie d'un conteneur dont le nom est `mon_conteneur` :
```
bluemix ic wait mon_conteneur
```



# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

* [Outil bx ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg)
