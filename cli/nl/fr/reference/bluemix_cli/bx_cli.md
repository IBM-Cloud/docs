---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Commandes {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

Version : 0.5.2

L'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} fournit un ensemble de commandes qui sont regroupées par espace de nom pour que les utilisateurs puissent interagir avec {{site.data.keyword.Bluemix_notm}}. Certaines commandes {{site.data.keyword.Bluemix_notm}} sont des encapsuleurs de commandes cf existantes, tandis que d'autres fournissent des capacités étendues aux utilisateurs {{site.data.keyword.Bluemix_notm}}. La liste ci-dessous répertorie les commandes prises en charge par l'interface de ligne de commande de {{site.data.keyword.Bluemix_notm}}, en indiquant leurs noms, leurs options, leur syntaxe, leurs prérequis, leurs descriptions, et des exemples.
{:shortdesc}

**Remarque :** la zone *Prérequis* répertorie les actions qui sont requises avant l'utilisation de la commande. Les commandes pour lesquelles aucune action n'est requise indiquent **Aucun**. Sinon, les prérequis peuvent inclure une ou plusieurs des actions suivantes :

<dl>
<dt>Noeud final</dt>
<dd>Un noeud final d'API doit être défini via <code>bluemix api</code> avant l'utilisation de la commande.</dd>
<dt>Connexion</dt>
<dd>La connexion avec la commande <code>bluemix login</code> est requise avant l'utilisation de cette commande.
Si vous vous connectez avec un ID fédéré, utilisez l'option '--sso' pour vous authentifier avec un code d'accès unique ou utilisez l'option '--apikey' pour vous authentifier avec une clé d'API. Dans la console {{site.data.keyword.Bluemix_notm}}, sélectionnez **Gérer** &gt; **Sécurité** &gt; **Clés d'API Bluemix** pour créer des clés d'API.
</dd>
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
 <td>[bluemix help](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target](bx_cli.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](bx_cli.html#bluemix_info) </td>
 <td>[bluemix regions](bx_cli.html#bluemix_regions) </td>
 <td>[bluemix config](bx_cli.html#bluemix_config)</td>
 <td>[bluemix curl](bx_cli.html#bluemix_curl)</td>
 <td>[bluemix update](bx_cli.html#bluemix_update)</td>
 </tr>
 </tbody>
 </table>

<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer des comptes, des organisations, des espaces, des rôles et des clés d'API.">
<caption>Tableau 2. Commandes pour la gestion de comptes, d'organisations, d'espaces, de rôles et de clés d'API</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion de comptes, d'organisations, d'espaces, de rôles et de clés d'API</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](bx_cli.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](bx_cli.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](bx_cli.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](bx_cli.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](bx_cli.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](bx_cli.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](bx_cli.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](bx_cli.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](bx_cli.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](bx_cli.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](bx_cli.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam org-users](bx_cli.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-user-add](bx_cli.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](bx_cli.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-roles](bx_cli.html#bluemix_iam_org_roles)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-role-set](bx_cli.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](bx_cli.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](bx_cli.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-roles](bx_cli.html#bluemix_iam_space_roles)</td>
 <td>[bluemix iam space-role-set](bx_cli.html#bluemix_iam_space_role_set)</td>
</tr>
 <tr>
 <td>[bluemix iam space-role-unset](bx_cli.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix iam accounts](bx_cli.html#bluemix_iam_accounts)</td>
 <td>[bluemix iam org-account](bx_cli.html#bluemix_iam_org_account)</td>
 <td>[bluemix iam account-users](bx_cli.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](bx_cli.html#bluemix_iam_account_users_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam account-user-invite](bx_cli.html#bluemix_iam_account_user_invite)</td>
  <td>[bluemix iam account-user-reinvite](bx_cli.html#bluemix_iam_account_user_reinvite)</td>
  <td>[bluemix iam api-keys](bx_cli.html#bluemix_iam_api_keys)</td>
  <td>[bluemix iam api-key-create](bx_cli.html#bluemix_iam_api_key_create)</td>
  <td>[bluemix iam api-key-delete](bx_cli.html#bluemix_iam_api_key_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam api-key-update](bx_cli.html#bluemix_iam_api_key_update)</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
 </tr>
 </tbody>
 </table>

<table summary="Commandes Bluemix que vous pouvez utiliser pour gérer des applications CF et des domaines, des routes et des certificats liés aux applications.">
<caption>Tableau 3. Commandes pour la gestion d'applications CF et de domaines, de routes et de certificats liés aux applications</caption>
 <thead>
 <th colspan="5">Commandes pour la gestion d'applications CF et de domaines, de routes et de certificats liés aux applications</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](bx_cli.html#bluemix_app_push)</td>
 <td>[bluemix app list](bx_cli.html#bluemix_app_list)</td>
 <td>[bluemix app show](bx_cli.html#bluemix_app_show)</td>
 <td>[bluemix app delete](bx_cli.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](bx_cli.html#bluemix_app_rename)</td>
 </tr>
 <tr>
 <td>[bluemix app start](bx_cli.html#bluemix_app_start)</td>
 <td>[bluemix app stop](bx_cli.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](bx_cli.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](bx_cli.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](bx_cli.html#bluemix_app_instance_restart)</td>
 </tr>
 <tr>
 <td>[bluemix app events](bx_cli.html#bluemix_app_events)</td>
 <td>[bluemix app files](bx_cli.html#bluemix_app_files)</td>
 <td>[bluemix app logs](bx_cli.html#bluemix_app_logs)</td>
 <td>[bluemix app env](bx_cli.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](bx_cli.html#bluemix_app_env_set)</td>
 </tr>
 <tr>
 <td>[bluemix app env-unset](bx_cli.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](bx_cli.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack-show](bx_cli.html#bluemix_app_stack_show)</td>
 <td>[bluemix app manifest-create](bx_cli.html#bluemix_app_manifest_create)</td>
 <td>[bluemix app domain-cert](bx_cli.html#bluemix_app_domain_cert)</td>
 </tr>
 <tr>
  <td>[bluemix app domain-cert-add](bx_cli.html#bluemix_app_domain_cert_add)</td>
  <td>[bluemix app domain-cert-remove](bx_cli.html#bluemix_app_domain_cert_remove)</td>
  <td>[bluemix app domains](bx_cli.html#bluemix_app_domains)</td>
  <td>[bluemix app domain-create](bx_cli.html#bluemix_app_domain_create)</td>
  <td>[bluemix app domain-delete](bx_cli.html#bluemix_app_domain_delete)</td>
 </tr>
 <tr>
  <td>[bluemix app shared-domain-create](bx_cli.html#bluemix_app_shared_domain_create)</td>
  <td>[bluemix app shared-domain-delete](bx_cli.html#bluemix_app_shared_domain_delete)</td>
  <td>[bluemix app routes](bx_cli.html#bluemix_app_routes)</td>
  <td>[bluemix app route-check](bx_cli.html#bluemix_app_route_check)</td>
  <td>[bluemix app route-map](bx_cli.html#bluemix_app_route_map)</td>
 </tr>
 <tr>
  <td>[bluemix app route-unmap](bx_cli.html#bluemix_app_route_unmap)</td>
  <td>[bluemix app route-create](bx_cli.html#bluemix_app_route_create)</td>
  <td>[bluemix app route-delete](bx_cli.html#bluemix_app_route_delete)</td>
  <td>[bluemix app orphaned-routes-delete](bx_cli.html#bluemix_app_orphaned_routes_delete)</td>
  <td></td>
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
 <td>[bluemix service offerings](bx_cli.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](bx_cli.html#bluemix_service_list)</td>
 <td>[bluemix service show](bx_cli.html#bluemix_service_show)</td>
 <td>[bluemix service create](bx_cli.html#bluemix_service_create)</td>
 <td>[bluemix service update](bx_cli.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](bx_cli.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](bx_cli.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](bx_cli.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](bx_cli.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](bx_cli.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](bx_cli.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](bx_cli.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](bx_cli.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](bx_cli.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](bx_cli.html#bluemix_service_user_provided_update)</td>
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
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](bx_cli.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](bx_cli.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](bx_cli.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix plugin update](bx_cli.html#bluemix_plugin_update)</td>
 <td>[bluemix billing account-usage](bx_cli.html#bluemix_billing_account_usage)</td>
 <td>[bluemix billing org-usage](bx_cli.html#bluemix_billing_org_usage)</td>
 <td>[bluemix billing orgs-usage-summary](bx_cli.html#bluemix_billing_orgs_usage_summary)</td>
 <td></td>
 </tr>
 </tbody>
 </table>
 
## bluemix help
{: #bluemix_help}
Affichez l'aide générale pour les commandes intégrées de premier niveau et les espaces de nom pris en charge de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, ou l'aide d'une commande intégrée ou d'un espace de nom spécifique.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>COMMAND|NAMESPACE (facultatif)</dt>
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



## bluemix api
{: #bluemix_api}
Définissez ou affichez le noeud final d'API {{site.data.keyword.Bluemix_notm}}.

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
   <dl>
   <dt>API_ENDPOINT (facultatif)</dt>
   <dd>Noeud final d'API ciblé. Par exemple, `https://api.chinabluemix.net`. Si l'option *NOEUD_FINAL_API* et l'option `--unset` sont toutes les deux spécifiées, le noeud final d'API en cours est affiché.</dd>
   <dt>--unset (facultatif)</dt>
   <dd>Supprimer le paramètre de noeud final d'API.</dd>
   <dt>--skip-ssl-validation (facultatif)</dt>
   <dd>Ignorer la validation SSL des demandes HTTP.</dd>
   </dl>
<strong>Exemples</strong> :

Définissez le noeud final d'API api.chinabluemix.net :

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

Affichez le noeud final d'API en cours :

```
bluemix api
```

Annulez la définition du noeud final d'API :

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

Connectez l'utilisateur. 

```
bluemix login [OPTIONS...]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
<dl>
  <dt>-a <i>API_ENDPOINT</i> (facultatif)</dt>
  <dd> Noeud final de l'API (par exemple : api.ng.bluemix.net)</dd>
  <dt> --apikey <i>API_KEY ou @API_KEY_FILE_PATH</i>
  <dd> Contenu de clé d'API ou chemin d'un fichier de clés d'API indiqué par @</dd>
  <dt> --sso (facultatif) </dt>
  <dd> Utiliser un code d'accès unique pour se connecter </dd>
  <dt> -u <i>USERNAME</i> (facultatif)</dt>
  <dd> Nom d'utilisateur</dd>
  <dt> -p <i>PASSWORD</i> (facultatif)</dt>
  <dd> Mot de passe</dd>
  <dt> -c <i>ACCOUNT_ID</i> (facultatif) </dt>
  <dd> ID du compte cible</dd>
  <dt> -o <i>ORG_NAME</i> (facultatif) </dt>
  <dd> Nom de l'organisation cible </dd>
  <dt> -s <i>SPACE_NAME</i> (facultatif) </dt>
  <dd> Nom de l'espace cible</dd>
  <dt> --skip-ssl-validation (facultatif) </dt>
  <dd> Ignorer la validation SSL des demandes HTTP. Cette option n'est pas recommandée.</dd>
</dl>

<strong>Exemples</strong> :

Connexion en mode interactif :

```
bluemix login
```

Connectez-vous avec un nom d'utilisateur et un mot de passe, puis définissez un compte, une organisation et un espace cible :

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

Connectez-vous avec un code d'accès unique et définissez un compte, une organisation et un espace cible :

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

Connectez-vous avec une clé d'API et définissez des cibles :

* Un compte est associé à une clé d'API

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* Aucun compte n'est associé à une clé d'API

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>Remarque :</strong> si un compte est associé à la clé d'API, le passage à un autre compte n'est pas autorisé.


## bluemix logout
{: #bluemix_logout}

Déconnectez l'utilisateur.

```
bluemix logout
```

<strong>Prérequis</strong> : Aucun


## bluemix target
{: #bluemix_target}


Définissez ou affichez le compte, la région, l'organisation ou l'espace cible :

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>-c <i>ACCOUNT_ID</i> (facultatif)</dt>
   <dd>ID du compte à cibler.</dd>
   <dt>-r <i>REGION</i> (facultatif)</dt>
   <dd>Région vers laquelle basculer.</dd>
   <dt>-o <i>ORG_NAME</i> (facultatif)</dt>
   <dd>Nom de l'organisation à cibler.</dd>
   <dt>-s <i>SPACE_NAME</i> (facultatif)</dt>
   <dd>Nom de l'espace à cibler.</dd>
   </dl>
Si aucune de ces options n'est spécifiée, le compte, la région, l'organisation et l'espace en cours s'affichent.

<strong>Exemples</strong> :

Définissez le compte, l'organisation et l'espace en cours.

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

Basculez vers une nouvelle région

```
bluemix target -r eu-gb
```

Affichez le compte, la région, l'organisation et l'espace en cours :

```
bluemix target
```


## bluemix info
{: #bluemix_info}

Affichez les informations {{site.data.keyword.Bluemix_notm}} de base, notamment la région en cours, la version du contrôleur de cloud et certains noeuds finaux utiles tels que les noeuds finaux pour la connexion et l'échange de jeton d'accès.

```
bluemix info
```

<strong>Prérequis</strong> : Noeud final


## bluemix config
{: #bluemix_config}


Ecrivez les valeurs par défaut dans le fichier de configuration.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>Délai d'attente pour les demandes HTTP. La valeur par défaut est 60 secondes.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>Consigne la trace des demandes HTTP sur le terminal ou dans le fichier spécifié.</dd>
   <dt>--color true|false</dt>
   <dd>Active ou désactive la sortie en couleurs. Elle est activée par défaut.</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
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


## bluemix curl
{: #bluemix_curl}

Exécutez une demande HTTP brute dans {{site.data.keyword.Bluemix_notm}}. *Content-Type* a pour valeur *application/json* par défaut. Cette
commande envoie la demande au proxy de contrôle multi-clouds {{site.data.keyword.Bluemix_notm}}. Pour les chemins pris en charge, reportez-vous aux définitions de chemin d'API dans le document [CloudFoundry API ](http://apidocs.cloudfoundry.org/){: new_window} ![Icône de lien externe](../../../icons/launch-glyph.svg).

```
bluemix curl CHEMIN [OPTIONS...]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt><i>PATH</i> (obligatoire)</dt>
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

## bluemix update
{: #bluemix_update}

Mettez à jour l'interface de ligne de commande vers la version la plus récente

```
bluemix update
```

<strong>Prérequis</strong> : Aucun

## bluemix regions
{: #bluemix_regions}

Affichez les informations pour toutes les régions dans {{site.data.keyword.Bluemix_notm}}.

```
bluemix regions
```

<strong>Prérequis</strong> : Noeud final


## bluemix iam orgs
{: #bluemix_iam_orgs}

Recensement de toutes les organisations

```
bluemix iam orgs [-r REGION] [--guid]
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

## bluemix iam org
{: #bluemix_iam_org}

Affiche des informations sur l'organisation spécifiée.

```
bluemix iam org ORG_NAME [--guid]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation.</dd>
   <dt>--guid (facultatif)</dt>
   <dd>Affiche l'identificateur global unique (GUID) de l'organisation.</dd>
   </dl>

<strong>Exemples</strong> :

Affichage des informations de l'organisation `IBM` en indiquant son identificateur global unique (GUID)

```
bluemix iam org IBM --guid
```


## bluemix iam org-create
{: #bluemix_iam_org_create}

Crée une nouvelle organisation. Cette opération ne peut être effectuée que par le propriétaire du compte.

```
bluemix iam org-create ORG_NAME
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation à créer.</dd>
   </dl>

<strong>Exemples</strong> :

Création d'une organisation nommée `IBM`.

```
bluemix iam org-create IBM
```

## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Répliquez une organisation de la région en cours dans une autre région.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation existante à répliquer.</dd>
   <dt>REGION_NAME (obligatoire)</dt>
   <dd>Nom de la région hébergeant l'organisation répliquée.</dd>
   </dl>

<strong>Exemples</strong> :

Réplication de l'organisation `mon_org` dans la région `eu-gb`:

```
bluemix iam org-replicate mon_org eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Attribue un nouveau nom à une organisation. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>OLD_ORG_NAME (obligatoire)</dt>
   <dd>Ancien nom de l'organisation qui sera renommée.</dd>
   <dt>NEW_ORG_NAME (obligatoire)</dt>
   <dd>Nouveau nom à affecter à l'organisation.</dd>
   </dl>

## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Supprime l'organisation spécifiée dans la région en cours.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation existante à supprimer.</dd>
   <dt>-f (facultatif)</dt>
   <dd>Impose la suppression sans demander de confirmation.</dd>
   <dt>--all (facultatif)</dt>
   <dd>Supprime l'organisation dans toutes les régions.</dd>
   </dl>


## bluemix iam spaces
{: #bluemix_iam_spaces}

Cette commande possède la même fonction et les mêmes options que la commande `cf spaces`.


## bluemix iam space
{: #bluemix_iam_space}

Cette commande possède la même fonction et les mêmes options que la commande `cf space`.


## bluemix iam space-create
{: #bluemix_iam_space_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-space`.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


Cette commande possède la même fonction et les mêmes options que la commande `cf rename-space`.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


Cette commande possède la même fonction et les mêmes options que la commande `cf delete-space`.

## bluemix iam org-users
{: #bluemix_iam_org_users}

Affiche les utilisateurs dans l'organisation spécifiée, par rôle.

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
<dt>ORG_NAME (obligatoire)</dt>
<dd>Nom de l'organisation.</dd>
<dt>-a (facultatif)</dt>
<dd>Recense tous les utilisateurs de l'organisation spécifiés, sans les regrouper par rôle.</dd>
</dl>

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Ajoute un utilisateur dans l'organisation (responsable de l'organisation requis).

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Supprimer un utilisateur de l'organisation (gestionnaire d'organisation ou utilisateur lui-même)

```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Options de commande</strong> :
<dl>
<dt>--force, -f</dt>
<dd>Impose la suppression sans demander de confirmation.</dd>
</dl>

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

Obtenez tous les rôles organisationnels de l'utilisateur en cours

```
bluemix iam org-roles
```

<strong>Prérequis</strong> : Noeud final, Connexion

## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Affecte un rôle de l'organisation à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
  <dl>
   <dt>USER_NAME (obligatoire)</dt>
   <dd>Nom de l'utilisateur à affecter.</dd>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation à laquelle affecter cet utilisateur.</dd>
   <dt>ORG_ROLE (obligatoire)</dt>
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


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Supprime l'affectation d'un rôle d'organisation à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>USER_NAME (obligatoire)</dt>
   <dd>Nom de l'utilisateur à supprimer.</dd>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation dans laquelle supprimer cet utilisateur.</dd>
   <dt>ORG_ROLE (obligatoire)</dt>
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

## bluemix iam space-users
{: #bluemix_iam_space_users}

Affichage des utilisateurs, par rôle, dans l'espace spécifié.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation.</dd>
   <dt>SPACE_NAME (obligatoire)</dt>
   <dd>Nom de l'espace.</dd>
   </dl>


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Affecte un rôle d'espace à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'espace.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

   <dl>
   <dt>USER_NAME (obligatoire)</dt>
   <dd>Nom de l'utilisateur à affecter.</dd>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation à laquelle affecter cet utilisateur.</dd>
   <dt>SPACE_NAME (obligatoire)</dt>
   <dd>Nom de l'espace auquel affecter cet utilisateur.</dd>
   <dt>SPACE_ROLE (obligatoire)</dt>
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

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Suppression de l'affectation d'un rôle d'espace à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'espace.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

   <dl>
   <dt>USER_NAME (obligatoire)</dt>
   <dd>Nom de l'utilisateur à supprimer.</dd>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation dans laquelle supprimer cet utilisateur.</dd>
   <dt>SPACE_NAME (obligatoire)</dt>
   <dd>Nom de l'espace dans lequel supprimer cet utilisateur.</dd>
   <dt>SPACE_ROLE (obligatoire)</dt>
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

## bluemix iam accounts
{: #bluemix_iam_accounts}

Affichez la liste de tous les comptes de l'utilisateur en cours

```
bluemix iam accounts
```

<strong>Prérequis</strong> : Noeud final, Connexion


## bluemix iam org-account
{: #bluemix_iam_org_account}

Affichez le compte de l'organisation spécifiée (utilisateur d'organisation requis)

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
  <dt>--guid (facultatif)</dt>
  <dd>Affichez uniquement l'ID de compte</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

Affiche les utilisateurs associés au compte. Cette opération ne peut être effectuée que par le
propriétaire du compte.

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

Supprimez un utilisateur du compte en cours (propriétaire de compte seulement)

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
<dt>USERNAME (obligatoire)</dt>
<dd>Nom d'utilisateur</dd>
<dt>--force, -f (facultatif)</dt>
<dd>Imposer la suppression sans demander de confirmation.</dd>
</dl>

## bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}

Invite un utilisateur à joindre le compte avec un rôle d'organisation et un rôle d'espace déjà définis. Cette opération ne peut être effectuée que par le
propriétaire du compte.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
   <dt>USER_NAME (obligatoire)</dt>
   <dd>Nom de l'utilisateur à inviter.</dd>
   <dt>ORG_NAME (obligatoire)</dt>
   <dd>Nom de l'organisation dans laquelle inviter cet utilisateur.</dd>
   <dt>ORG_ROLE (obligatoire)</dt>
   <dd>Nom du rôle d'organisation auquel inviter cet utilisateur. Par exemple :
   <ul>
  <li>OrgManager : ce rôle peut inviter et gérer des utilisateurs, sélectionner et changer de plan, et définir des plafonds de dépense.</li>
  <li>BillingManager : ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</li>
  <li>OrgAuditor : ce rôle dispose d'un accès en lecture seule aux informations de l'organisation et aux rapports.</li>
  </ul> </dd>
   <dt>SPACE_NAME (obligatoire)</dt>
   <dd>Nom de l'espace dans lequel inviter cet utilisateur.</dd>
   <dt>SPACE_ROLE (obligatoire)</dt>
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

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Renvoyer l'invitation à un utilisateur (gestionnaire d'organisation ou propriétaire de compte requis)

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

Répertoriez toutes les clés d'API de la plateforme Bluemix

```
bluemix iam api-keys
```

<strong>Prérequis</strong> : Noeud final, Connexion

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

Créez une nouvelle clé d'API pour la plateforme Bluemix

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
<dt>NAME (obligatoire)</dt>
<dd>Nom de la clé d'API à créer.</dd>
<dt>-d <i>DESCRIPTION</i> (facultatif)</dt>
<dd>Description de la clé d'API</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>Sauvegarder les informations de clé d'API dans un fichier spécifié. Si cette option n'est pas spécifiée, le contenu JSON s'affiche.</dd>
</dl>

<strong>Exemples</strong> :

Créez une clé d'API et sauvegardez-la dans un fichier

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

Mettez à jour une clé d'API de la plateforme Bluemix

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
<dt>NAME (obligatoire)</dt>
<dd>Ancien nom de la clé d'API qui doit être mise à jour</dd>
<dt>-n <i>NAME</i> (facultatif)</dt>
<dd>Nouveau nom de la clé d'API</dd>
<dt>-d <i>DESCRIPTION</i> (facultatif)</dt>
<dd>Nouvelle description de la clé d'API</dd>
</dl>

<strong>Exemples</strong> :

Mettre à jour la description d'une clé d'API :

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

Supprimez une clé d'API de la plateforme Bluemix

```
bluemix iam api-key-delete NAME [-f]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
<dt>NAME (obligatoire)</dt>
<dd>Nom de la clé d'API à supprimer.</dd>
<dt>-f (facultatif)</dt>
<dd>Imposer la suppression sans demander de confirmation.</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

Cette commande possède la même fonction et les mêmes options que la commande `cf push`.


## bluemix app list
{: #bluemix_app_list}

Cette commande possède la même fonction et les mêmes options que la commande `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf app`.


## bluemix app delete
{: #bluemix_app_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete`.


## bluemix app rename
{: #bluemix_app_rename}

Cette commande possède la même fonction et les mêmes options que la commande `cf rename`.


## bluemix app start
{: #bluemix_app_start}

Cette commande possède la même fonction et les mêmes options que la commande `cf start`.


## bluemix app stop
{: #bluemix_app_stop}

Cette commande possède la même fonction et les mêmes options que la commande `cf stop`.


## bluemix app restart
{: #bluemix_app_restart}

Cette commande possède la même fonction et les mêmes options que la commande `cf restart`.


## bluemix app restage
{: #bluemix_app_restage}


Cette commande possède la même fonction et les mêmes options que la commande `cf restage`.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


Cette commande possède la même fonction et les mêmes options que la commande `cf restart-app-instance`.


## bluemix app events
{: #bluemix_app_events}

Cette commande possède la même fonction et les mêmes options que la commande `cf events`.


## bluemix app files
{: #bluemix_app_files}

Cette commande possède la même fonction et les mêmes options que la commande `cf files`.


## bluemix app logs
{: #bluemix_app_logs}

Cette commande possède la même fonction et les mêmes options que la commande `cf logs`.


## bluemix app env
{: #bluemix_app_env}

Cette commande possède la même fonction et les mêmes options que la commande `cf env`.


## bluemix app env-set
{: #bluemix_app_env_set}

Cette commande possède la même fonction et les mêmes options que la commande `cf set-env`.


## bluemix app env-unset
{: #bluemix_app_env_unset}

Cette commande possède la même fonction et les mêmes options que la commande `cf unset-env`.


## bluemix app stacks
{: #bluemix_app_stacks}

Cette commande possède la même fonction et les mêmes options que la commande `cf stacks`.


## bluemix app stack-show
{: #bluemix_app_stack_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-app-manifest`.

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

Affichez les informations de certificat d'un domaine.

```
bluemix app domain-cert DOMAIN_NAME
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
<dl>
<dt>DOMAIN_NAME (obligatoire)</dt>
<dd>Domaine hébergeant le certificat.</dd>
</dl>


<strong>Exemples</strong> :

Affichage des informations de certificat du domaine `ibmcxo-eventconnect.com`:

```
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

Ajoutez un certificat au domaine indiqué dans l'organisation en cours.

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
   <dt>DOMAIN (obligatoire)</dt>
   <dd>Domaine auquel ajouter le certificat.</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i> (obligatoire)</dt>
   <dd>Chemin du fichier de clé privée.</dd>
   <dt>-c <i>CERT_FILE</i> (obligatoire)</dt>
   <dd>Chemin du fichier de certificat.</dd>
   <dt>-p <i>PASSWORD</i> (facultatif)</dt>
   <dd>Mot de passe du certificat.</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i> (facultatif)</dt>
   <dd>Chemin du fichier de certificat intermédiaire.</dd>
   <dt>-t <i>TRUST_STORE_FILE</i> (facultatif)</dt>
   <dd>Fichier de clés certifiées.</dd>
   </dl>


<strong>Exemples</strong> :

Ajoutez un certificat au domaine `ibmcxo-eventconnect.com` :

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

Supprimez un certificat du domaine spécifié dans l'organisation en cours.

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>DOMAIN (obligatoire)</dt>
   <dd>Domaine duquel supprimer le certificat.</dd>
   <dt>-f (facultatif)</dt>
   <dd>Imposer la suppression sans demander de confirmation.</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

Cette commande possède la même fonction et les mêmes options que la commande `cf domains`.


## bluemix app domain-create
{: #bluemix_app_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-domain`.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-domain`.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-shared-domain`.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-shared-domain`.

## bluemix app routes
{: #bluemix_app_routes}

Cette commande possède la même fonction et les mêmes options que la commande `cf routes`.


## bluemix app route-check
{: #bluemix_app_route_check}

Cette commande possède la même fonction et les mêmes options que la commande `cf check-route`.


## bluemix app route-map
{: #bluemix_app_route_map}

Mappez une route à une application cf ou un groupe de conteneurs existant associé au domaine et au nom d'hôte spécifiés.

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (obligatoire)</dt>
   <dd>Nom de l'application cf ou du groupe de conteneur à mapper à une route.</dd>
   <dt>DOMAIN (obligatoire)</dt>
   <dd>Domaine de la route. Par exemple, mychinabluemix.net ou chinabluemix.net. </dd>
   <dt>-n <i>HOST_NAME</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du groupe de conteneurs par défaut.</dd>
   </dl>

<strong>Exemples</strong> :

Mappez une route à `mon-app` avec le domaine spécifié :

```
bluemix app route-map my-app mychinabluemix.net
```

Mappez une route à 'mon-groupe-conteneurs' avec le domaine et le nom d'hôte spécifiés :

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

Supprimez le mappage de la route spécifiée à une application cf ou un groupe de conteneurs existant.

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (obligatoire)</dt>
   <dd>Nom de l'application cf ou du groupe de conteneurs.</dd>
   <dt>DOMAIN (obligatoire)</dt>
   <dd>Domaine de la route (par exemple, mychinabluemix.net ou chinabluemix.net).</dd>
   <dt>-n <i>HOST_NAME</i> (facultatif)</dt>
   <dd>Nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du groupe de conteneurs par défaut.</dd>
   </dl>

<strong>Exemples</strong> :

Supprimez le mappage de la route `mon-app.mychinabluemix.net` de `mon-app` :

```
bluemix app route-unmap my-app mychianbluemix.net
```

Supprimez le mappage de la route `abc.chinabluexmix.net` de `mon-groupe-conteneurs` :

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-route`.


## bluemix app route-delete
{: #bluemix_app_route_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-route`.


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-orphaned-routes`.


## bluemix app domains
{: #bluemix_app_domains}

Cette commande possède la même fonction et les mêmes options que la commande `cf domains`.


## bluemix app domain-create
{: #bluemix_app_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-domain`.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-domain`.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-shared-domain`.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-shared-domain`.


## bluemix service offerings
{: #bluemix_service_offerings}


Cette commande possède la même fonction et les mêmes options que la commande `cf marketplace`.


## bluemix service list
{: #bluemix_service_list}

Cette commande possède la même fonction et les mêmes options que la commande `cf services`.


## bluemix service show
{: #bluemix_service_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf service`.


## bluemix service create
{: #bluemix_service_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-service`.


## bluemix service update
{: #bluemix_service_update}

Cette commande possède la même fonction et les mêmes options que la commande `cf update-service`.


## bluemix service delete
{: #bluemix_service_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-service`.


## bluemix service rename
{: #bluemix_service_rename}

Cette commande possède la même fonction et les mêmes options que la commande `cf rename-service`.


## bluemix service bind
{: #bluemix_service_bind}

Cette commande possède la même fonction et les mêmes options que la commande `cf bind-service`.


## bluemix service unbind
{: #bluemix_service_unbind}

Cette commande possède la même fonction et les mêmes options que la commande `cf unbind-service`.


## bluemix service key-create
{: #bluemix_service_key_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-service-key`.


## bluemix service key-delete
{: #bluemix_service_key_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-service-key`.


## bluemix service keys
{: #bluemix_service_keys}

Cette commande possède la même fonction et les mêmes options que la commande `cf service-keys`.


## bluemix service key-show
{: #bluemix_service_key_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf service-key`.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-user-provided-service`.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Cette commande possède la même fonction et les mêmes options que la commande `cf update-user-provided-service`.


## bluemix catalog templates
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


## bluemix catalog template
{: #bluemix_catalog_template}

Affichez les informations détaillées d'un modèle de conteneur boilerplate spécifié.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :
   <dl>
   <dt>TEMPLATE_ID (obligatoire)</dt>
   <dd>ID du modèle de conteneur boilerplate. Utilisez <i>bluemix templates</i> pour afficher tous les ID de modèles.</dd>
   </dl>


<strong>Exemples</strong> :

Affichez les détails du modèle `mobileBackendStarter` :

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

Créez une application cf reposant sur le modèle spécifié avec l'adresse URL et la description indiquées. Par défaut, la nouvelle application est démarrée automatiquement.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Prérequis</strong> : Noeud final, Connexion, Cible

<strong>Options de commande</strong> :
   <dl>
   <dt>TEMPLATE_ID (obligatoire)</dt>
   <dd>Modèle sur lequel sera basée l'application lors de sa création. Utilisez <i>bluemix templates</i> pour voir tous les ID des modèles.</dd>
   <dt>CF_APP_NAME (obligatoire)</dt>
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

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

Affichez l'utilisation mensuelle et les coûts liés à votre compte.

```
bluemix billing account-usage [-d YYYY-MM] [--json]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

<dl>
  <dt>-d MONTH_DATE (facultatif)</dt>
  <dd>Afficher les données relatives au mois et à la date spécifiées en utilisant le format AAAA-MM. Si ces données ne sont pas spécifiées, l'utilisation du mois en cours est affichée.</dd>
  <dt>--json (facultatif)</dt>
  <dd>Afficher le résultat de l'utilisation au format JSON.</dd>
</dl>

<strong>Exemples</strong> :

Affichage du rapport d'utilisation et des coûts de mon compte pour 2016-06 :

```
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

Affichez les détails de l'utilisation mensuelle d'une organisation. Cette opération ne peut être réalisée que par un responsable de la facturation de l'organisation.

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

<dl>
  <dt>ORG_NAME (obligatoire)</dt>
  <dd>Nom de l'organisation.</dd>
  <dt>-d MONTH_DATE (facultatif)</dt>
  <dd>Afficher les données relatives au mois et à la date spécifiés en utilisant le format AAAA-MM. Si ces données ne sont pas spécifiées, l'utilisation du mois en cours est affichée.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nom de la région qui héberge l'organisation. Si ce paramètre a pour valeur 'all', l'utilisation de l'organisation dans toutes les régions est affichée.</dd>
  <dt>--json (facultatif)</dt>
  <dd>Afficher le résultat de l'utilisation au format JSON.</dd>
</dl>



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

Affichez un récapitulatif d'utilisation mensuelle pour les organisations dans mon compte.

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Prérequis</strong> : Noeud final, Connexion

<strong>Options de commande</strong> :

<dl>
  <dt>-d MONTH_DATE (facultatif)</dt>
  <dd>Afficher les données relatives au mois et à la date spécifiés en utilisant le format AAAA-MM. Si ces données ne sont pas spécifiées, l'utilisation du mois en cours est affichée.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nom de la région qui héberge les organisations. Si ce paramètre a pour valeur 'all', le récapitulatif d'utilisation des organisations dans toutes les régions est affiché.</dd>
  <dt>--json (facultatif)</dt>
  <dd>Afficher le résultat de l'utilisation au format JSON.</dd>
</dl>


## bluemix plugin repos
{: #bluemix_plugin_repos}

Répertoriez tous les référentiels de plug-in qui sont enregistrés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

<strong>Prérequis</strong> : Aucun


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Ajoutez un nouveau référentiel de plug-in à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>REPO_NAME (obligatoire)</dt>
   <dd>Nom du référentiel à ajouter. Vous pouvez définir votre propre nom pour chaque référentiel.</dd>
   <dt>REPO_URL (obligatoire)</dt>
   <dd>URL du référentiel à ajouter. Elle doit contenir le protocole (par exemple http://plugins.ng.bluemix.net au lieu de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net est le référentiel de plug-in officiel de l'interface de ligne de commande (CLI) Bluemix.</dd>
    </dl>


<strong>Exemples</strong> :

Ajoutez le référentiel de plug-in officiel de l'interface de ligne de commande Bluemix sous la forme `référentiel-bluemix` :

```
bluemix plugin repo-add référentiel-bluemix http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Retirez un référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove REPO_NAME
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
   <dl>
   <dt>REPO_NAME (obligatoire)</dt>
   <dd>Nom du référentiel à supprimer.</dd>
   </dl>

<strong>Exemples</strong> :

Supprimez `référentiel-bluemix` de l'interface de ligne de commande (CLI) {{site.data.keyword.Bluemix_notm}} :

```
bluemix plugin repo-remove référentiel-bluemix
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Répertoriez tous les plug-in disponibles dans tous les référentiels ajoutés ou dans un référentiel spécifique.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>-r <i>REPO_NAME</i> (facultatif)</dt>
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


## bluemix plugin list
{: #bluemix_plugin_list}

Répertoriez tous les plug-in installés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

<strong>Prérequis</strong> : Aucun


## bluemix plugin install
{: #bluemix_plugin_install}

Installez la version de plug-in spécifique dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} à partir du chemin ou du référentiel spécifié.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (obligatoire)</dt>
   <dd>Si -r <i>REPO_NAME</i> n'est pas spécifié, le plug-in est installé depuis le chemin local spécifié ou depuis l'URL distante.</dd>
   <dt>-r <i>REPO_NAME</i> (facultatif)</dt>
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

## bluemix plugin update
{: #bluemix_plugin_update}

Mettez à niveau le plug-in à partir d'un référentiel

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :
<dl>
 <dt>-r REPO_NAME (obligatoire)</dt>
 <dd>Nom du référentiel hébergeant le fichier binaire du plug-in.</dd>
 <dt><i>PLUGIN_NAME</i> (facultatif)</dt>
 <dd>Si cette option n'est pas spécifiée, tous les plug-ins disponibles pour la mise à jour dans le référentiel indiqué sont répertoriés pour être sélectionnés.</dd>
 <dt>-v <i>VERSION</i> (facultatif)</dt>
 <dd>Version cible du plug-in pour la mise à jour. Si cette option n'est pas spécifiée, mettez à jour le plugin vers la dernière version disponible.</dd>
</dl>

<strong>Exemples</strong> :

Recherchez tous les plug-ins disponibles pour la mise à niveau dans le référentiel "My-Repo" :

```
bluemix plugin update -r My-Repo
```

Mettez à niveau le plug-in "plugin-echo" dans le référentiel "My-Repo" vers la dernière version :

```
bluemix plugin update -r My-Repo plugin-echo
```

Mettez à niveau le plug-in "plugin-echo" dans le référentiel "My-Repo" vers la version "1.0.1" :

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Désinstallez le plug-in spécifié de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>Prérequis</strong> : Aucun

<strong>Options de commande</strong> :

   <dl>
   <dt>PLUGIN_NAME (obligatoire)</dt>
   <dd>Nom du plug-in à désinstaller.</dd>
    </dl>

<strong>Exemples</strong> :

Désinstallez le plug-in `IBM-Containers` installé précédemment :

```
bluemix plugin uninstall IBM-Containers
```
