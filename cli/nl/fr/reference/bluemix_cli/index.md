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

Installez la version la plus récente du plug-in `container-service` depuis le référentiel `bluemix-repo` :

```
bluemix plugin install container-service -r bluemix-repo
```
Installez le plug-in `container-service` avec la version `0.5.800` depuis le référentiel `bluemix-repo` :

```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
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

Désinstallez le plug-in `container-service` installé auparavant :

```
bluemix plugin uninstall container-service
```



# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

* [Outil bx ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![icône de lien externe](../../../icons/launch-glyph.svg)
