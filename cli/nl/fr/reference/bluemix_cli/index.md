---

 

copyright:

  années : 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Commandes {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

*Dernière mise à jour : 15 avril 2016*

L'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} fournit un ensemble de commandes qui sont regroupées par espace de nom pour que les utilisateurs puissent interagir avec {{site.data.keyword.Bluemix_notm}}. Certaines commandes {{site.data.keyword.Bluemix_notm}} sont des encapsuleurs de commandes cf existantes, alors que d'autres fournissent des capacités étendues aux utilisateurs {{site.data.keyword.Bluemix_notm}}. Vous trouverez ci-après la liste de toutes les commandes qui sont prises en charge par l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, ainsi que leurs noms, leurs options, leur syntaxe, les prérequis, leurs descriptions et des exemples.
{:shortdesc}
 
**Remarque :** la zone *Prérequis* répertorie les actions qui sont requises avant l'utilisation de la commande. Les commandes pour lesquelles aucune action n'est requise indiquent **Aucun**. Sinon, les prérequis peuvent inclure une ou plusieurs des actions suivantes :
<dl>
<dt>Noeud final</dt>
<dd>Un noeud final d'API doit être défini via <code>bluemix api</code> avant l'utilisation de la commande.</dd>
<dt>Connexion</dt>
<dd>La connexion avec la commande <code>bluemix login</code> est requise avant l'utilisation de cette commande.</dd>
<dt>Cible</dt>
<dd>La commande <code>bluemix target</code> doit être utilisée pour définir une organisation et un espace avant l'utilisation de cette commande.</dd>
<dt>Docker</dt>
<dd>L'interface de ligne de commande Docker (docker) doit être installée pour que vous puissiez exécuter cette commande.</dd>
</dl>

Vous pouvez utiliser les commandes {{site.data.keyword.Bluemix_notm}} suivantes :

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
Affichez l'aide générale pour les commandes intégrées de premier niveau et les espaces de nom pris en charge de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, ou l'aide d'une commande intégrée ou d'un espace de nom spécifique.

```
bluemix help [COMMANDE|ESPACE DE NOM]
```

**Prérequis** : Aucun

**Options de commande** :

*COMMANDE*|*ESPACE DE NOM* (facultatif) : commande ou espace de nom pour laquelle ou lequel l'aide est affichée. Si la commande ou l'espace de nom n'est pas spécifié, l'aide générale de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} est affichée.

**Exemples** :

Affichez l'aide générale pour l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} :

```
bluemix help
```

Affichez l'aide pour la commande `info` :

```
bluemix help info
```

Affichez l'aide pour l'espace de nom `ic` :

```
bluemix help ic
```

ou 

```
bluemix ic help
```

Affichez l'aide de la commande `group-create` sous l'espace de nom `ic` :

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
Définissez ou affichez le noeud final d'API {{site.data.keyword.Bluemix_notm}}. Cette commande encapsule la commande `cf api`.

```
bluemix api [NOEUD_FINAL_API][--unset]
```

**Prérequis** : Aucun

**Options de commande** :

*NOEUD_FINAL_API* (facultatif) : noeud final d'API ciblé, par exemple https://api.ng.bluemix.net.  Si l'option *NOEUD_FINAL_API* et l'option `--unset` sont toutes les deux spécifiées, le noeud final d'API en cours est affiché.

`--unset` (facultatif) : retirez le paramètre de noeud final d'API.

**Exemples** :

Définissez le noeud final d'API api.ng.bluemix.net :

```
bluemix api api.ng.bluemix.net
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

Connectez l'utilisateur. Cette commande encapsule la commande `cf login`. Les options de commande sont les mêmes que pour `cf login`.

```
bluemix login [OPTIONS...]
```

**Prérequis** : Noeud final

**Options de commande** : pour des informations sur les options prises en charge par la commande `login`, voir les informations sur la syntaxe de la commande `cf login` pour les commandes cf de gestion des applications.


## bluemix logout
{: #bluemix_logout}

Déconnectez l'utilisateur. Cette commande encapsule la commande `cf logout`.

```
bluemix logout
```

**Prérequis** : Aucun


## bluemix target
{: #bluemix_target}


Définissez ou affichez l'organisation ou l'espace cible. Cette commande encapsule la commande `cf target`.

```
bluemix target [-o NOM_ORG] [-s NOM_ESPACE]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

-o *NOM_ORG* (facultatif) : nom de l'organisation à cibler.

-s *NOM_ESPACE* (facultatif) : nom de l'espace à cibler.

Si ni -o *NOM_ORG* ni -s *NOM_ESPACE* n'est spécifié, l'organisation et l'espace en cours sont affichés.

**Exemples** :

Définissez l'organisation en cours `MonOrg` et l'espace `MonEspace` :

```
bluemix target -o MonOrg -s MonEspace
```

Affichez l'organisation et l'espace en cours :

```
bluemix target
```


## bluemix info
{: #bluemix_info}

Affichez les informations {{site.data.keyword.Bluemix_notm}} de base, notamment la région en cours, la version du contrôleur de cloud et certains noeuds finaux utiles tels que les noeuds finaux pour la connexion et l'échange de jeton d'accès.

```
bluemix info
```

**Prérequis** : Noeud final


## bluemix config
{: #bluemix_config}


Ecrivez les valeurs par défaut dans le fichier de configuration.

```
bluemix config --http-timeout DELAI_ATTENTE_EN_SECONDES | --trace (true|false|chemin/fichier) | --color (true|false) | --locale (ENVIRONNEMENT_LOCAL|CLEAR)
```

**Prérequis** : Aucun

**Options de commande** :

--http-timeout *DELAI_ATTENTE_EN_SECONDES* : valeur du délai d'attente pour les demandes HTTP. La valeur par défaut est 60 secondes.

--trace true|false|*chemin/fichier* : tracez les demandes HTTP jusqu'au terminal ou au fichier spécifié.

--color true|false : activez ou désactivez la sortie couleur. Elle est activée par défaut.

--locale *ENVIRONNEMENT_LOCAL* : définissez un environnement local par défaut. Si ENVIRONNEMENT_LOCAL a pour valeur *CLEAR*, l'environnement local précédent est supprimé.

Une seule de ces options peut être indiquée à la fois.

**Exemples** :

Définissez le délai d'attente des demandes HTTP à 30 secondes :

```
bluemix config --http-timeout 30
```

Activez la sortie de trace pour les demandes HTTP :

```
bluemix config --trace true
```

Tracez les demandes HTTP vers le fichier nommé */home/usera/my_trace* :

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


## bluemix list
{: #bluemix_list}

Répertoriez toutes les applications cf, les conteneurs, les groupes de conteneurs et les groupes de machines virtuelles dans l'espace en cours.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

apps (facultatif) : affichez uniquement les informations sur les applications.

containers (facultatif) : affichez uniquement les informations sur les conteneurs.

container-groups (facultatif) : affichez uniquement les informations sur les groupes de conteneurs.

vm-groups (facultatif) : affichez uniquement les informations sur les groupes de machines virtuelles.

Vous ne pouvez spécifier qu'un argument à la fois : `apps`, `containers`, `container-groups` ou `vm-groups`. Si vous ne spécifiez rien, toutes les applications cf, tous les conteneurs, tous les groupes de conteneurs et tous les groupes de machines virtuelles sont répertoriés.

**Exemples** :

Répertoriez toutes les applications cf :

```
bluemix list apps
```

Répertoriez toutes les instances de conteneur :

```
bluemix list containers
```

Répertoriez toutes les applications, tous les conteneurs, tous les groupes de conteneurs et tous les groupes de machines virtuelles :

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

Réduisez ou augmentez le nombre d'instances, le quota de disque et la taille de mémoire spécifiés pour l'application cf ou le groupe de conteneurs.

**Remarque :** seul un nombre d'instances peut être indiqué pour la mise à l'échelle d'un groupe de conteneurs. Si aucune option n'est spécifiée, cette commande répertorie le nombre d'instances en cours pour le groupe de conteneurs, ainsi que le quota de disque et la taille de mémoire pour l'application cf.

```
bluemix scale NOM_APP_CF|NOM_GROUPE_CONTENEURS [-i NOMBRE_INSTANCES][-k QUOTA_DISQUE] [-m TAILLE_MEMOIRE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (obligatoire) : nom de l'application cf ou du groupe de conteneurs à mettre à l'échelle.

-i *NOMBRE_INSTANCES*  (facultatif) : nouveau nombre d'instances pour l'application cf ou le groupe de conteneurs à mettre à l'échelle. Il s'agit de la seule option valide pour la mise à l'échelle d'un groupe de conteneurs.

-k *QUOTA_DISQUE* (facultatif) : nouveau quota de disque de l'application cf. Non valide pour la mise à l'échelle d'un groupe de conteneurs.

-m *TAILLE_MEMOIRE* (facultatif) : nouvelle taille de mémoire pour l'application cf. Non valide pour la mise à l'échelle d'un groupe de conteneurs.

**Exemples** :

Affichez le nombre d'instances actuel pour `mon-groupe-conteneurs` :

```
bluemix scale mon-groupe-conteneurs
```

Mettez à l'échelle `mon-groupe-conteneurs` avec 2 instances :

```
bluemix scale mon-groupe-conteneurs -i 2
```

Mettez à l'échelle `mon-app-java` avec 3 instances, 8 Go de quota de disque et 1024 Mo de taille de mémoire :

```
bluemix scale mon-app-java -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

Exécutez une demande HTTP brute dans {{site.data.keyword.Bluemix_notm}}. *Content-Type* a pour valeur *application/json* par défaut. Cette
commande envoie la demande au proxy de contrôle multi-clouds {{site.data.keyword.Bluemix_notm}}. Pour les chemins pris en charge, reportez-vous aux
définitions de chemin d'API dans le document [CloudFoundry API](http://apidocs.cloudfoundry.org/){: new_window}.

```
bluemix curl CHEMIN [OPTIONS...]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*CHEMIN* (obligatoire) : chemin URL de la ressource. Par exemple, /v2/apps.

*OPTIONS* (facultatif) : les options prises en charge par la commande `bluemix curl` sont les mêmes que pour la commande `cf curl`.

**Exemples** :

Affichage des informations de toutes les organisations du compte en cours :

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

Recensement de toutes les organisations

```
bluemix iam orgs [-r REGION --guid]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*-r REGION*  (Facultatif) : région pour laquelle les informations d'organisation sont présentées. Si vous spécifiez 'all', toutes les
organisations de toutes les régions sont répertoriées.

*--guid* (facultatif) : affiche l'identificateur global unique des organisations.

**Exemples** :
recensement de toutes les organisations dans la région : `us-south`, avec affichage de l'identificateur global unique

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

Affiche des informations sur l'organisation spécifiée.

```
bluemix iam org NOM_ORG [--guid]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (requis) : nom de l'organisation.

*--guid* (facultatif) : affiche l'identificateur global unique de l'organisation.


**Exemples** :
Affichage des informations de l'organisation `IBM`, avec affichage de l'identificateur global unique

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

Crée une nouvelle organisation. Cette opération ne peut être effectuée que par le propriétaire du compte.

```
bluemix iam org-create NOM_ORG
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (requis) : nom de l'organisation à créer.

**Exemples** :
création d'une organisation nommée `IBM`.

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Répliquez une organisation de la région en cours dans une autre région.

```
bluemix iam org-replicate NOM_ORG NOM_REGION
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (obligatoire) : nom de l'organisation existante à répliquer.

*NOM_REGION* (obligatoire) : nom de la région hébergeant l'organisation répliquée.

**Exemples** :

Réplication de l'organisation `myorg` dans la région `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Attribue un nouveau nom à une organisation. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-rename ANCIEN_NOM_ORG NOUVEAU_NOM_ORG
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*ANCIEN_NOM_ORG* (requis) :  ancien nom de l'organisation à renommer.

*NOUVEAU_NOM_ORG* (requis) :  nouveau nom de l'organisation à renommer.


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Supprime l'organisation spécifiée dans la région en cours.

```
bluemix iam org-delete NOM_ORG [-f --all]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (requis) :  nom de l'organisation existante à supprimer.

*-f* (facultatif) : force la suppression sans demander de confirmation.

*--all* (facultatif) : supprime l'organisation de toutes les régions.


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


## bluemix iam account-users
{: #bluemix_iam_account_users}

Affiche les utilisateurs associés au compte. Cette opération ne peut être effectuée que par le propriétaire du compte.

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


Invite un utilisateur à joindre le compte avec un rôle d'organisation et un rôle d'espace déjà définis. Cette opération ne peut être effectuée que par le
propriétaire du compte.

```
bluemix iam account-user-invite NOM_UTILISATEUR NOM_ORG ROLE_ORG NOM_ESPACE ROLE_ESPACE
```

**Prérequis** : Noeud final, Connexion


**Options de commande** :

*NOM_UTILISATEUR* (requis) : nom de l'utilisateur invité.

*NOM_ORG* (requis) : nom de l'organisation à laquelle est invité l'utilisateur.

*ROLE_ORG* (requis): nom du rôle d'organisation auquel est invité l'utilisateur. Par exemple :

<dl>
<dt>OrgManager</dt>
<dd>Ce rôle peut inviter et gérer des utilisateurs, sélectionner et modifier des plans, et définir des plafonds de dépense.</dd>
<dt>BillingManager</dt>
<dd>Ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</dd>
<dt>OrgAuditor</dt>
<dd>Ce rôle dispose d'un accès en lecture seule aux informations et aux rapports de l'organisation.</dd>
</dl> 

*NOM_ESPACE* (requis) : nom de l'espace auquel est invité l'utilisateur.

*ROLE_ESPACE* (requis) : nom du rôle d'espace auquel est invité l'utilisateur. Par exemple :

<dl>
<dt>SpaceManager</dt>
<dd>Ce rôle peut inviter et gérer des utilisateurs, et activer des fonctions dans un espace spécifique.</dd>
<dt>SpaceDeveloper</dt>
<dd>Ce rôle peut créer et gérer des applications et des services, et consulter les journaux et les rapports.</dd>
<dt>SpaceAuditor</dt>
<dd>Ce rôle peut consulter les journaux, les rapports, et les paramètres de l'espace.</dd>
</dl> 

**Exemples** :

Invitation de l'utilisateur `Mary` dans l'organisation `IBM` sous le rôle `OrgManager` et l'espace
`Cloud` sous le rôle `SpaceAuditor` :

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

Affiche les utilisateurs dans l'organisation spécifiée, par rôle.

```
bluemix iam org-users NOM_ORG [-a]
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (requis) : nom de l'organisation.

*-a* (facultatif) : répertorie tous les utilisateurs de l'organisation spécifiée, sans les classer par rôle.


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Affecte un rôle de l'organisation à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-role-set NOM_UTILISATEUR NOM_ORG ROLE_ORG
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_UTILISATEUR* (requis) : nom de l'utilisateur affecté.

*NOM_ORG* (requis) : nom de l'organisation à laquelle est affecté l'utilisateur.

*ROLE_ORG* (requis): nom du rôle d'organisation auquel est affecté l'utilisateur. Par exemple :

<dl>
<dt>OrgManager</dt>
<dd>Ce rôle peut inviter et gérer des utilisateurs, sélectionner et modifier des plans, et définir des plafonds de dépense.</dd>
<dt>BillingManager</dt>
<dd>Ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</dd>
<dt>OrgAuditor</dt>
<dd>Ce rôle dispose d'un accès en lecture seule aux informations et aux rapports de l'organisation.</dd>
</dl> 

**Exemples** :

Affectation de l'utilisateur `Mary` à l'organisation `IBM` sous le rôle `OrgManager` :

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Supprime l'affectation d'un rôle d'organisation à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'organisation.

```
bluemix iam org-role-unset NOM_UTILISATEUR NOM_ORG ROLE_ORG
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_UTILISATEUR* (requis) : nom de l'utilisateur à supprimer.

*NOM_ORG* (requis) : nom de l'organisation d'où est supprimé l'utilisateur.

*ROLE_ORG* (requis): nom du rôle d'organisation où est supprimé l'utilisateur. Par exemple :

<dl>
<dt>OrgManager</dt>
<dd>Ce rôle peut inviter et gérer des utilisateurs, sélectionner et modifier des plans, et définir des plafonds de dépense.</dd>
<dt>BillingManager</dt>
<dd>Ce rôle peut créer et gérer le compte de facturation et les informations de paiement.</dd>
<dt>OrgAuditor</dt>
<dd>Ce rôle dispose d'un accès en lecture seule aux informations et aux rapports de l'organisation.</dd>
</dl> 

**Exemples** :

Suppression de l'affectation de l'utilisateur `Mary` dans l'organisation `IBM` au rôle `OrgManager` :

```
bluemix iam org-role-unset Mary IBM OrgManager
```


## bluemix iam space-users
{: #bluemix_iam_space_users}

Affichage des utilisateurs, par rôle, dans l'espace spécifié.

```
bluemix iam space-users NOM_ORG NOM_ESPACE
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_ORG* (requis) : nom de l'organisation.

*NOM_ESPACE* (requis) : nom de l'espace.


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Affecte un rôle d'espace à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'espace.

```
bluemix iam space-role-set NOM_UTILISATEUR NOM_ORG NOM_ESPACE ROLE_ESPACE
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_UTILISATEUR* (requis) : nom de l'utilisateur affecté.

*NOM_ORG* (requis) : nom de l'organisation à laquelle est affecté l'utilisateur.

*NOM_ESPACE* (requis) : nom de l'espace auquel est affecté l'utilisateur.

*ROLE_ESPACE* (requis) : nom du rôle d'espace auquel est affecté l'utilisateur. Par exemple :

<dl>
<dt>SpaceManager</dt>
<dd>Ce rôle peut inviter et gérer des utilisateurs, et activer des fonctions dans un espace spécifique.</dd>
<dt>SpaceDeveloper</dt>
<dd>Ce rôle peut créer et gérer des applications et des services, et consulter les journaux et les rapports.</dd>
<dt>SpaceAuditor</dt>
<dd>Ce rôle peut consulter les journaux, les rapports, et les paramètres de l'espace.</dd>
</dl> 


**Exemples** :

Affectation de l'utilisateur `Mary` à l'organisation `IBM` et à l'espace `Cloud` sous le rôle
`SpaceManager` :

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Suppression de l'affectation d'un rôle d'espace à un utilisateur. Cette opération ne peut être réalisée que par un responsable de l'espace.

```
bluemix iam space-role-unset NOM_UTILISATEUR NOM_ORG NOM_ESPACE ROLE_ESPACE
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_UTILISATEUR* (requis) : nom de l'utilisateur dont supprimer l'affectation.

*NOM_ORG* (requis) : nom de l'organisation d'où est supprimé l'utilisateur.

*NOM_ESPACE* (requis) : nom de l'espace d'où est supprimé l'utilisateur.

*ROLE_ESPACE* (requis) : nom du rôle d'espace d'où est supprimé l'utilisateur. Par exemple :

<dl>
<dt>SpaceManager</dt>
<dd>Ce rôle peut inviter et gérer des utilisateurs, et activer des fonctions dans un espace spécifique.</dd>
<dt>SpaceDeveloper</dt>
<dd>Ce rôle peut créer et gérer des applications et des services, et consulter les journaux et les rapports.</dd>
<dt>SpaceAuditor</dt>
<dd>Ce rôle peut consulter les journaux, les rapports, et les paramètres de l'espace.</dd>
</dl> 

**Exemples** :

Suppression de l'affectation de l'utilisateur `Mary` dans l'organisation `IBM` et l'espace
`Cloud` au rôle `SpaceManager` :

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

Cette commande possède la même fonction et les mêmes options que la commande `cf push`.


## bluemix app list
{: #bluemix_app_list}

Cette commande possède la même fonction et les mêmes options que la commande `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Cette commande possède la même fonction et les mêmes options que la commande `cf app`.


## bluemix app scale
{: #bluemix_app_scale}

Cette commande possède la même fonction et les mêmes options que la commande `cf scale`.


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


## bluemix app stack
{: #bluemix_app_stack}

Cette commande possède la même fonction et les mêmes options que la commande `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-app-manifest`.


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

**Prérequis** : Noeud final, Connexion

**Options de commande** :

-d (facultatif) : si l'option `-d` est spécifiée, la description de chaque modèle est également affichée. Sinon, seul l'ID et le nom des modèles sont affichés.


## bluemix catalog template
{: #bluemix_catalog_template}

Affichez les informations détaillées d'un modèle de conteneur boilerplate spécifié.

```
bluemix catalog template ID_MODELE
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*ID_MODELE* (requis) : ID du modèle de conteneur boilerplate. Utilisez 'bluemix templates' pour afficher les ID de tous les modèles.

**Exemples** :

Affichez les détails du modèle `mobileBackendStarter` :

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

Créez une application cf reposant sur le modèle spécifié avec l'adresse URL et la description indiquées. Par défaut, la nouvelle application est démarrée automatiquement.

```
bluemix catalog template-run ID_MODELE NOM_APP_CF [-u URL] [-d DESCRIPTION] [--no-start]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*ID_MODELE* (obligatoire) : modèle sur lequel doit s'appuyer l'application lorsqu'elle est créée. Utilisez `bluemix templates` pour voir tous les ID des modèles.

*NOM_APP_CF* (obligatoire) : nom de l'application cf à créer.

-u *URL* (facultatif) : route de l'application. Si elle n'est pas spécifiée, la route est définie par
{{site.data.keyword.Bluemix_notm}} automatiquement en fonction du nom de votre application et du domaine par défaut.

-d *DESCRIPTION* (facultatif) : description de l'application.

--no-start (facultatif) : permet de ne pas démarrer l'application automatiquement après sa création. Si cette option n'est pas spécifiée, l'application est démarrée automatiquement après sa création.

**Exemples** :

Créez l'application cf `mon-app` d'après le modèle `javaHelloWorld` :

```
bluemix catalog template-run javaHelloWorld mon-app
```

Créez l'application `mon-app-ruby` d'après le modèle `rubyHelloWorld` avec la route `mon-app-ruby.ng.bluemix.net` et la description `Ma première application Ruby dans {{site.data.keyword.Bluemix_notm}}.` :

```
bluemix catalog template-run rubyHelloWorld mon-app-ruby -u mon-app-ruby.ng.bluemix.net -d "Ma première application Ruby dans {{site.data.keyword.Bluemix_notm}}."
```

Créez l'application `mon-app-python` d'après le modèle `pythonHelloWorld` sans démarrage automatique :

```
bluemix catalog template-run pythonHelloWorld mon-app-python --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

Affichez les informations pour toutes les régions dans {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

**Prérequis** : Noeud final


## bluemix network region-set
{: #bluemix_network_region_set}

Passez à la région spécifiée. Cette commande vous redirige automatiquement sur la même organisation et le même espace dans la nouvelle région, si possible. Autrement, l'utilisateur est invité à sélectionner une nouvelle organisation et un nouvel espace si l'utilisateur est déjà connecté. Le noeud final d'API est changé en conséquence.

```
bluemix network region-set NOM_REGION
```

**Prérequis** : Noeud final

**Options de commande** :

*NOM_REGION* (obligatoire) : nom de la région à laquelle vous voulez accéder. Vous pouvez utiliser la commande `bluemix network regions` pour afficher tous les noms de région.

**Exemples** :

Définissez la région en cours `eu-gb` :

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

Cette commande possède la même fonction et les mêmes options que la commande `cf routes`.


## bluemix network route-check
{: #bluemix_network_route_check}

Cette commande possède la même fonction et les mêmes options que la commande `cf check-route`.


## bluemix network route-map
{: #bluemix_network_route_map}

Mappez une route à une application cf ou un groupe de conteneurs existant associé au domaine et au nom d'hôte spécifiés.

```
bluemix network route-map NOM_APP_CF|NOM_GROUPE_CONTENEURS  DOMAINE  [-n NOM_HOTE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (obligatoire) : nom de l'application cf ou du groupe de conteneurs à mapper à une route.

*DOMAINE* (obligatoire) : domaine de la route. Exemple : mybluemix.net ou ng.bluemix.net. 

-n *NOM_HOTE* (facultatif) : nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du groupe de conteneurs par défaut.

**Exemples** :

Mappez une route à `mon-app` avec le domaine spécifié :

```
bluemix network route-map mon-app mybluemix.net
```

Mappez une route à 'mon-groupe-conteneurs' avec le domaine et le nom d'hôte spécifiés :

```
bluemix network route-map mon-groupe-conteneurs ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

Supprimez le mappage de la route spécifiée à une application cf ou un groupe de conteneurs existant.

```
bluemix network route-unmap NOM_APP_CF|NOM_GROUPE_CONTENEURS  DOMAINE  [-n NOM_HOTE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_APP_CF*|*NOM_GROUPE_CONTENEURS* (obligatoire) : nom de l'application cf ou du groupe de conteneurs.

*DOMAINE* (obligatoire) : domaine de la route (par exemple mybluemix.net ou ng.bluemix.net). 

-n *NOM_HOTE* (facultatif) : nom d'hôte de la route. S'il n'est pas spécifié, le nom d'hôte est le nom de l'application ou le nom du groupe de conteneurs par défaut.

**Exemples** :

Supprimez le mappage de la route `mon-app.mybluemix.net` de `mon-app` :

```
bluemix network route-unmap mon-app mybluemix.net
```

Supprimez le mappage de la route `abc.ng.bluexmix.net` de `mon-groupe-conteneurs` :

```
bluemix network route-unmap mon-groupe-conteneurs ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-route`.


## bluemix network route-delete
{: #bluemix_network_route_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-route`.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-orphaned-routes`.


## bluemix network domains
{: #bluemix_network_domains}

Cette commande possède la même fonction et les mêmes options que la commande `cf domains`.


## bluemix network domain-create
{: #bluemix_network_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-domain`.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-domain`.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Cette commande possède la même fonction et les mêmes options que la commande `cf create-shared-domain`.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Cette commande possède la même fonction et les mêmes options que la commande `cf delete-shared-domain`.


## bluemix security cert
{: #bluemix_security_cert}

Affichage des informations de certificat d'un domaine.

```
bluemix security cert NOM_DOMAIN
```

**Prérequis** : Noeud final, Connexion

**Options de commande** :

*NOM_DOMAINE* (requis) :  nom du domaine hébergeant le certificat.

**Exemples** :

Affichage des informations de certificat du domaine `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

Ajoutez un certificat au domaine indiqué dans l'organisation en cours.

```
bluemix security cert-add DOMAINE -k FICHIER_CLE_PRIVEE -c FICHIER_CERT [-p MOT_DE_PASSE][-i FICHIER_CERT_INTERMEDIAIRE] [--verify-client]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*DOMAINE* (obligatoire) : domaine auquel est ajouté le certificat.

-k *FICHIER_CLE_PRIVEE* (obligatoire) : chemin d'accès au fichier de clé privée.

-c *FICHIER_CERT* (obligatoire) : chemin d'accès au fichier de certificat.

-p *MOT_DE_PASSE* (facultatif) : mot de passe du certificat.

-i *FICHIER_CERT_INTERMEDIAIRE* (facultatif) : chemin d'accès au fichier de certificat intermédiaire.

--verify-client (facultatif) : indique s'il faut activer la vérification du certificat client.

**Exemples** :

Ajoutez un certificat au domaine `ibmcxo-eventconnect.com` :

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

Supprimez un certificat du domaine spécifié dans l'organisation en cours.

```
bluemix security cert-remove DOMAINE [-f]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*DOMAINE* (obligatoire) : domaine duquel supprimer le certificat.

-f (facultatif) : forcer la suppression sans confirmation.







## bluemix plugin repos
{: #bluemix_plugin_repos}

Répertoriez tous les référentiels de plug-in qui sont enregistrés dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

**Prérequis** : Aucun


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Ajoutez un nouveau référentiel de plug-in à l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add NOM_REFERENTIEL URL_REFERENTIEL
```

**Prérequis** : Aucun

**Options de commande** :

*NOM_REFERENTIEL* (obligatoire) : nom du référentiel à ajouter. Vous pouvez définir votre propre nom pour chaque référentiel.

*URL_REFERENTIEL* (obligatoire) : adresse URL du référentiel à ajouter. Elle doit contenir le protocole (par exemple http://plugins.ng.bluemix.net au lieu de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net est le référentiel de plug-in officiel de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

**Exemples** :

Ajoutez le référentiel de plug-in officiel de l'interface de ligne de commande Bluemix sous la forme `référentiel-bluemix` :

```
bluemix plugin repo-add référentiel-bluemix http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Retirez un référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove NOM_REFERENTIEL
```

**Prérequis** : Aucun

**Options de commande** :

*NOM_REFERENTIEL* (obligatoire) : nom du référentiel à retirer.

**Exemples** :

Supprimez `référentiel-bluemix` de l'interface de ligne de commande (CLI) {{site.data.keyword.Bluemix_notm}} :

```
bluemix plugin repo-remove référentiel-bluemix
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Répertoriez tous les plug-in disponibles dans tous les référentiels ajoutés ou dans un référentiel spécifique.

```
bluemix plugin repo-plugins [-r NOM_REFERENTIEL]
```

**Prérequis** : Aucun

**Options de commande** :

-r *NOM_REFERENTIEL* (facultatif) : répertoriez uniquement les plug-in dans le référentiel spécifié.

**Exemples** :

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

**Prérequis** : Aucun


## bluemix plugin install
{: #bluemix_plugin_install}

Installez la version de plug-in spécifique dans l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} à partir du chemin ou du référentiel spécifié.

```
bluemix plugin install CHEMIN_PLUG-IN|NOM_PLUG-IN [-r NOM_REFERENTIEL][-v VERSION]
```

**Prérequis** : aucun

**Options de commande** :

*CHEMIN_PLUG-IN*|*NOM_PLUG-IN* (obligatoire) : si `-r *NOM_REFERENTIEL*` n'est pas indiqué, le plug-in est installé à partir de l'URL distante ou du chemin local indiqué.

-r *NOM_REFERENTIEL* (facultatif) : nom du référentiel dans lequel se trouve le fichier binaire du plug-in.
-v *VERSION*  (facultatif) : version de plug-in à installer. Si elle n'est pas fournie, la dernière version du plug-in est installée. Cette option n'est valide que si vous installez le plug-in à partir du référentiel.

**Exemples** :

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






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Désinstallez le plug-in spécifié de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall NOM_PLUG-IN
```

**Prérequis** : Aucun

**Options de commande** :

*NOM_PLUG-IN* (obligatoire) : nom du plug-in à désinstaller.

**Exemples** :

Désinstallez le plug-in `IBM-Containers` installé précédemment :

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

Initialisez l'environnement des conteneurs sur votre machine locale afin d'utiliser l'ensemble des capacités du service IBM Containers.

```
bluemix ic init
```

**Prérequis** : Noeud final, Connexion, Cible

**Remarque :** avant l'initialisation, assurez-vous que l'interface de ligne de commande Docker (docker) est installée et configurée dans votre variable d'environnement PATH. Pour passer dans une autre région, utilisez la commande `bluemix region-set`. 

**Exemples** :

Passez dans la région `us-south` :

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

Contrôlez un conteneur en cours d'exécution ou affichez sa sortie. Utilisez `CTRL+C` pour quitter et arrêter le conteneur. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} dans l'aide de Docker. 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

--no-stdin (facultatif) : permet de ne pas inclure l'entrée standard.

--sig-proxy (facultatif) : envoyer par proxy tous les signaux reçus au processus. La valeur par défaut est **true**.

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Exemples** :

L'exemple suivant est une demande d'association au conteneur `mon_conteneur` :
```
bluemix ic attach mon_conteneur
```


## bluemix ic build
{: #bluemix_ic_build}

Appelez le service de génération IBM Containers afin de générer une image Docker localement ou dans votre référentiel {{site.data.keyword.Bluemix_notm}} privé. Cette commande appelle l'interface de ligne de commande Docker. Pour plus d'informations, voir la commande [build](https://docs.docker.com/reference/commandline/build/){: new_window} dans l'aide de Docker. 

```
bluemix ic build -t ETIQUETTE|--tag ETIQUETTE [--no-cache][-p|--pull] [-q|--quiet] EMPLACEMENT_DOCKERFILE
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-t *ETIQUETTE*|--tag *ETIQUETTE* (requis) : nom du référentiel à appliquer à l'image qui est créée.

--no-cache (facultatif) : permet de ne pas utiliser le cache lorsque l'image est générée. La valeur par défaut est **false**.

-p|--pull (facultatif) : tenter d'extraire l'image de base depuis le registre même si elle est en cache.

-q|--quiet (facultatif) : supprimer la sortie prolixe qui est générée par les conteneurs. La valeur par défaut est **false**.

*EMPLACEMENT_DOCKERFILE* (requis) : chemin d'accès au document Dockerfile et au contexte sur l'hôte local.

**Exemples** :

L'exemple ci-après est une demande de génération d'une image appelée *monimage*. Le document Dockerfile et les autres artefacts à utiliser dans la génération se trouvent dans le répertoire depuis lequel la commande est exécutée. Etant donné que le registre et l'espace de nom sont inclus dans le nom de l'image, l'image est générée dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation.
```
bluemix ic build -t registry.ng.bluemix.net/monespacenom/monimage
```


## bluemix ic create
{: #bluemix_ic_create}

Créez un conteneur dans votre référentiel {{site.data.keyword.Bluemix_notm}}. Cette commande encapsule la commande `docker create`. Pour plus d'informations, voir la commande [create](https://docs.docker.com/reference/commandline/create/){: new_window} dans l'aide de Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Accédez à une image Docker Hub ou à une image de votre registre local et copiez-la dans votre référentiel {{site.data.keyword.Bluemix_notm}} privé.

```
bluemix ic cpi IMAGE_SOURCE IMAGE_DESTINATION
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*IMAGE_SOURCE* (requis) : référentiel source et nom de l'image.

*IMAGE_DESTINATION* (requis) : adresse URL du référentiel {{site.data.keyword.Bluemix_notm}} privé, qui inclut l'espace de nom et le nom de l'image de destination. L'étiquette pour l'image est facultative.

**Exemples** :

Copiez une image depuis le référentiel source dans votre référentiel privé et ajoutez une étiquette pour l'image :

```
bluemix ic cpi référentiel_source/nom_image_source URL_registre_privé/nom_image_destination:étiquette
```

Copiez l'image `sinatra` depuis le référentiel `training` dans votre référentiel privé `registry.ng.bluemix.net/monespacenom` et nommez l'image `monimagesinatra`. Ajoutez une étiquette `v1`
pour l'image `monimagesinatra`. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/monespacenom/monimagesinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


Exécutez une commande dans un conteneur. Pour plus d'informations, voir la commande [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} dans l'aide de Docker.

```
bluemix ic exec [-d|--detach][-it] [-u UTILISATEUR|--user UTILISATEUR] CONTENEUR [CMD]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-d|--detach (facultatif) : exécuter la commande spécifiée en arrière-plan.

-it (facultatif) : mode interactif. L'entrée standard continue d'être affichée. Entrer `exit` pour quitter.

-u *UTILISATEUR*|--user *UTILISATEUR* (facultatif) : nom de l'utilisateur.

*CONTENEUR* (requis) : nom ou ID du conteneur.

*CMD* (facultatif) : commande à exécuter dans le ou les conteneurs spécifiés.

**Exemples** :

Exécutez la commande `bash` dans le conteneur `mon_conteneur` en mode interactif :

```
bluemix ic exec -it mon_conteneur bash
```

Exécutez la commande `date` dans le conteneur `mon_conteneur` :

```
bluemix ic exec mon_conteneur date
```


## bluemix ic groups
{: #bluemix_ic_groups}

Répertoriez les groupes de conteneurs qui existent dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation.

```
bluemix ic groups
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Affichez les informations détaillées, comme les variables d'environnement, les ports ou la mémoire, qui sont spécifiées pour un groupe de conteneurs lors de sa création.

```
bluemix ic group-inspect GROUPE_CONTENEURS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*GROUPE_CONTENEURS* (requis) : nom ou ID du groupe de conteneurs.

**Exemples** :

L'exemple suivant est une demande d'inspection du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-inspect mon_groupe
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Répertoriez les instances d'un groupe de conteneurs spécifié.

```
bluemix ic group-instances GROUPE_CONTENEURS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*GROUPE_CONTENEURS* (requis) : nom ou ID du groupe de conteneurs.

**Exemples** :

Répertoriez toutes les instances du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-instances mon_groupe
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Créez un groupe de conteneurs évolutif.

```
bluemix ic group-create [-p PORT|--publish port][-m MEMOIRE|--memory MEMOIRE] [-e ENV|--env ENV][-v VOLUME:CHEMIN_CONTENEUR] [--min MIN][--max MAX] [--desired SOUHAITE][--auto] [-n HOTE|--hostname HOTE][-d DOMAINE|--domain DOMAINE] [--name NOM] IMAGE [CMD]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

-m *MEMOIRE*|--memory *MEMOIRE* (facultatif) : affectez une limite de mémoire au groupe en mégaoctets. Lorsque vous créez un groupe de conteneurs depuis l'interface de ligne de commande, la valeur par défaut pour chaque instance de conteneur est `64` Mo. Lorsque vous créez un groupe de conteneurs depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}, la valeur par défaut pour chaque instance de conteneur est `256` Mo. Les valeurs admises sont `64`, `256`, `512`, `1024` et `2048`. Une fois que vous avez affecté une limite de mémoire, vous ne pouvez plus la modifier.

-e *ENV*|--env *ENV* (facultatif) : définissez la variable d'environnement, où **ENV** est une paire `clé=valeur`. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Exemple : `-e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3"`.  Le tableau suivant répertorie certaines variables d'environnement couramment utilisées que vous pouvez spécifier :

|  Variable d'environnement                              |     Description                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nom_app&gt;*       | Liez un service à un conteneur. Utilisez la variable d'environnement `CCS_BIND_APP` pour lier une application à un conteneur. L'application est liée au service cible et sert de pont qui permet à {{site.data.keyword.Bluemix_notm}} de fournir les informations contenues dans la variable `VCAP_SERVICES` de votre application pont à votre instance de conteneur en cours d'exécution. Pour plus d'informations sur la création d'une application pont, voir
[Liaison d'un service à un conteneur](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;clé_ssh_publique&gt;* | Ajoutez une clé SSH à un conteneur lorsque vous créez le conteneur. Vous pouvez ajouter la clé SSH à l'aide de la variable d'environnement lorsque vous créez un conteneur depuis le tableau de bord {{site.data.keyword.Bluemix_notm}} ou depuis l'interface de ligne de commande. Pour plus d'informations sur les clés SSH, voir [Connexion à un conteneur](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;chemin_fichier&gt;* | Ajoutez un fichier journal à surveiller dans le conteneur. Incluez la variable d'environnement `LOG_LOCATIONS` avec un chemin d'accès au fichier journal. |
*Tableau 1. Variables d'environnement couramment utilisées*

-v VOLUME:CHEMIN_CONTENEUR[:ro]|--volume VOLUME:CHEMIN_CONTENEUR[:ro](facultatif) :  associez un volume à un conteneur en spécifiant les détails au format `ID_volume:chemin_conteneur[:ro]`.

- *VOLUME* : nom ou ID du volume.
- *CHEMIN_CONTENEUR* : chemin d'accès absolu au volume dans le conteneur.
- ro (facultatif) : la spécification de `ro` rend le volume accessible en lecture seule au lieu d'être accessible par défaut en lecture/écriture.

-p *PORT*|--publish *PORT* (facultatif) : exposez le port pour le trafic HTTP. Les conteneurs qui se trouvent dans votre groupe doivent être à l'écoute sur le port HTTP. Il n'est pas possible d'envoyer des demandes HTTPS. Vous ne pouvez pas inclure plusieurs ports pour les groupes de conteneurs.

Lorsque vous spécifiez un port, vous mettez l'application à disposition dans l'équilibreur de charge {{site.data.keyword.Bluemix_notm}} ou dans les conteneurs qui tentent d'accéder à l'hôte dans le même espace {{site.data.keyword.Bluemix_notm}}. L'équilibreur
de charge ou les conteneurs {{site.data.keyword.Bluemix_notm}} peuvent alors utiliser le port pour joindre l'hôte et l'application dans le même espace {{site.data.keyword.Bluemix_notm}}. Si un port est spécifié dans le document Dockerfile pour l'image que vous utilisez, incluez ce port.

**Astuce :**

- Pour l'image Liberty Server certifiée IBM, ou une version modifiée de cette image, entrez le port 9080.
- Pour l'image Node.js certifiée IBM, ou une version modifiée de cette image, entrez le port 8000.

--min *MIN* (facultatif) : nombre minimal d'instances. La valeur par défaut est **1**. Si vous définissez un nombre minimal d'instances, la valeur ne peut pas être changée une fois le groupe de conteneurs créé.

--max *MAX* (facultatif) : nombre maximal d'instances. La valeur par défaut est **2**. Si vous définissez un nombre maximal d'instances, la valeur ne peut pas être changée une fois le groupe de conteneurs créé.

--desired *SOUHAITE* (facultatif) : nombre d'instances requises. La valeur par défaut est **2**.

--auto (facultatif) : lorsque le groupe de conteneurs est créé et que la reprise automatique est activée, IBM Containers vérifie la santé de chaque instance en envoyant une demande HTTP au port affecté.

Si aucune réponse n'est reçue d'une instance de conteneur aux cours de deux intervalles consécutifs de 90 secondes, l'instance est supprimée et remplacée par une nouvelle instance. Aucune action n'est effectuée si le conteneur répond. Ce processus est répété en permanence. Au cours d'une fenêtre de 30 minutes, si le nombre total de conteneurs différents qui sont membres du groupe est égal ou supérieur à trois fois la taille maximale observée pour le groupe, la reprise automatique est désactivée définitivement pour le groupe de conteneurs. Pour l'activer à nouveau, vous devez recréer le groupe de conteneurs.

-n *HOTE*|--hostname *HOTE* (facultatif) : nom d'hôte, par exemple `monhôteconteneur`. L'hôte et le domaine sont combinés pour former l'adresse URL de route publique complète, par exemple `http://monhôteconteneur.mybluemix.net`. Lorsque vous passez en revue les détails d'un groupe de conteneurs avec la commande `bluemix ic group-inspect`, l'hôte et le domaine sont affichés ensemble et constituent la route.

-d *DOMAINE*|--domain *DOMAINE* (facultatif) : en général, le domaine est `.mybluemix.net`. L'hôte et le domaine sont combinés pour former l'adresse URL de route publique complète, par exemple `http://monhôteconteneur.mybluemix.net`. Lorsque vous passez en revue les détails d'un groupe de conteneurs avec la commande `bluemix ic group-inspect`, l'hôte et le domaine sont affichés ensemble et constituent la route.

--name *NOM* (requis) : affectez un nom au groupe. `-n` est obsolète.

**Astuce :** le nom de conteneur doit commencer par une lettre. Il peut inclure des lettres majuscules, des lettres minuscules, des chiffres, des points (`.`), des traits de soulignement (`_`) et des traits d'union (`-`).

*IMAGE* (requis) : image à inclure dans chaque instance de conteneur dans le groupe de conteneurs. Vous pouvez spécifier des commandes après l'image, mais n'indiquez pas d'options. Incluez toutes les options avant de spécifier une image.

Si vous utilisez une image qui se trouve dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation, spécifiez l'image au format `registry.ng.bluemix.net/ESPACE_NOM/IMAGE`.

Si vous utilisez une image fournie par IBM Containers, n'incluez pas l'espace de nom de votre organisation. Spécifiez l'image au format `registry.ng.bluemix.net/IMAGE`.

*CMD* (facultatif) : commande et arguments qui sont transmis au groupe de conteneurs pour leur exécution. Cette commande doit être une commande à exécution longue. N'utilisez pas de commande à exécution courte, c'est-à-dire qui ne s'exécute pas très longtemps, comme **/bin/date**, car elle pourrait entraîner la panne du conteneur.

**Remarque :**
- La commande et les arguments doivent être spécifiés à la fin de la ligne de commande `bluemix ic run`.
- Si les arguments de commande incluent un trait d'union (`-`), comme `-c` dans l'exemple de commande précédent, la commande doit être précédée de deux traits d'union (`--`).



**Exemples** :

Créez un groupe de conteneurs `mon_groupe_conteneurs` en utilisant l'image `registry.ng.bluemix.net/ibmnode` fournie par IBM Containers, puis exécutez la commande à exécution longue `ping localhost` sur ce groupe de conteneurs :

```
bluemix ic group-create --name mon_groupe_conteneurs registry.ng.bluemix.net/ibmnode ping localhost
```

Créez un groupe de conteneurs `mon_groupe_conteneurs` en utilisant l'image `registry.ng.bluemix.net/ibmnode` fournie par IBM Containers, puis exécutez la commande à exécution longue `tail -f /dev/null` sur ce groupe de conteneurs :

```
bluemix ic group-create --name mon_groupe_conteneurs registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Créez un groupe évolutif `mongroupe` pour lequel la reprise automatique est activée en utilisant l'image `registry.ng.bluemix.net/ibmliberty`. Le port est `9080`, le nom d'hôte est `monhôteconteneur`, le nom de domaine est `.mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n monhôteconteneur -d .mybluemix.net --name mongroupe registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Mettez à jour un groupe de conteneurs.


```
bluemix ic group-update [--min MIN][--max MAX] [--desired SOUHAITE][--auto] GROUPE_CONTENEURS
```

**Astuce :** afin de mettre à jour le nom d'hôte ou le domaine pour un groupe de conteneurs, utilisez `bluemix ic route-map [-n
HOTE][-d DOMAINE] GROUPE_CONTENEURS.

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

--min *MIN* (facultatif) : nombre minimal d'instances. La valeur par défaut est **1**. Une fois le nombre d'instances minimal défini, il ne peut pas être changé.

--max *MAX* (facultatif) : nombre maximal d'instances. La valeur par défaut est **2**. Une fois le nombre d'instances maximal défini, il ne peut pas être changé.

--desired *SOUHAITE* (facultatif) : nombre d'instances requises. La valeur par défaut est **2**.

**Astuce :** vous ne pouvez pas spécifier `--min MIN`, `--max MAX` et `--desired SOUHAITE` simultanément.

--auto (facultatif) : redémarrez automatiquement les instances défaillantes en activant la reprise automatique.

*GROUPE_CONTENEURS* (requis) : nom ou ID du groupe de conteneurs.

**Exemples** :

L'exemple suivant est une demande de mise à jour du groupe de conteneurs `mon_groupe` :
```
bluemix ic group-update --max 5 mon_groupe
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Supprime un groupe de conteneurs dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation.

```
bluemix ic group-remove [-f|--force] GROUPE_CONTENEURS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

-f|--force (facultatif) : force le retrait d'un conteneur en cours d'exécution ou ayant échoué.

*GROUPE_CONTENEURS* (requis) : nom ou ID du groupe de conteneurs.

**Exemples** :

L'exemple suivant est une demande de retrait d'un groupe de conteneurs dont le nom est `mon_groupe` :
```
bluemix ic group-remove mon_groupe
```


## bluemix ic images
{: #bluemix_ic_images}

Affichez la liste de toutes les images disponibles dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de l'organisation. Pour plus d'informations, voir la commande [images](https://docs.docker.com/reference/commandline/images){: new_window} dans l'aide de Docker. La liste inclut l'ID de l'image, la date de création et le nom de l'image.

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-a|--all (facultatif) : incluez toutes les couches d'image pour chaque image se trouvant dans le référentiel de votre organisation, et pas seulement la couche la plus récente.

--no-trunc (facultatif) : permet de ne pas tronquer la sortie.

-q|--quiet (facultatif) : affichez seulement les ID numériques.

**Exemples** :

L'exemple suivant est une demande de réception de la liste des images disponibles pour l'organisation :
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Affichez les informations sur un conteneur. Pour plus d'informations, voir la commande [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} dans l'aide de Docker.

```
bluemix ic inspect [IMAGE|images|CONTENEUR]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*IMAGE* (requis) : affichez des informations détaillées sur une image spécifique en indiquant son nom ou son ID.

images (requis) : affichez des informations détaillées sur toutes les images qui se trouvent dans votre référentiel.

*CONTENEUR* (requis) : affichez des informations détaillées sur un conteneur spécifique en indiquant son nom ou son ID.

**Astuce :** vous ne pouvez pas spécifier *IMAGE*, images ou *CONTENEUR* simultanément. 

**Exemples** :

L'exemple suivant est une demande d'inspection d'un conteneur dont le nom est `proxy` : 
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

Affichez un ensemble d'informations décrivant l'état de l'instance de service cloud de conteneur. Les informations incluent la limite relative aux conteneurs, l'utilisation des conteneurs, les conteneurs en cours d'exécution, la limite de mémoire, l'utilisation de la mémoire, la limite relative aux adresses IP flottantes, l'utilisation des adresses IP flottantes, l'adresse URL de l'hôte CCS, l'adresse URL de l'hôte du registre et le statut du mode
débogage.

```
bluemix ic info
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix ic ips
{: #bluemix_ic_ips}

Répertoriez les adresses IP flottantes disponibles pour l'utilisateur connecté. La liste répertorie les adresses IP et l'ID de conteneur auquel les adresses IP sont liées. Si l'adresse IP n'est pas utilisée, aucun ID de conteneur n'est affiché.

```
bluemix ic ips [-a|--all]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

-a|--all (facultatif) : répertoriez toutes les adresses IP. Par défaut, seules les adresses IP disponibles sont renvoyées.

**Exemples** :

L'exemple suivant est une demande de réception de la liste de toutes les adresses IP pour l'organisation, qu'elles soient disponibles ou non :
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
Demandez une nouvelle adresse IP flottante.

```
bluemix ic ip-request
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Libérez une adresse IP flottante de l'instance de service cloud de conteneur.

```
bluemix ic ip-release ADRESSE_IP
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*ADRESSE_IP* (requis) : adresse IP à publier.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Liez une adresse IP flottante disponible à un conteneur.

```
bluemix ic ip-bind ADRESSE_IP CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*ADRESSE_IP* (requis) : adresse IP à lier.

*CONTENEUR* (requis) : nom ou ID du conteneur à lier.

**Exemples** :

L'exemple suivant est une demande de liaison de l'adresse IP `192.123.12.12` au conteneur `proxy` :
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Annulez la liaison d'une adresse IP flottante à son conteneur.

Les adresses IP publiques constituent une ressource limitée dans IBM Containers. Par conséquent, les adresses IP publiques qui sont allouées à un espace et qui ne sont pas liées à un conteneur sont régulièrement récupérées auprès des utilisateurs de l'essai gratuit, environ toutes les semaines. Les adresses IP publiques non liées ne sont jamais récupérées auprès des utilisateurs facturés ponctuellement ou disposant d'un abonnement.

```
bluemix ic ip-unbind ADRESSE_IP CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*ADRESSE_IP* (requis) : adresse IP pour laquelle annuler la liaison.

*CONTENEUR* (requis) : nom ou ID du conteneur pour lequel annuler la liaison.

**Exemples** :

L'exemple suivant est une demande d'annulation de la liaison de l'adresse IP `192.123.12.12` au conteneur `proxy` :
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

Arrêtez un processus en cours dans un conteneur sans arrêter le conteneur. Pour plus d'informations, voir la commande [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} dans l'aide de Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-s *CMD*|--signal *CMD* (facultatif) : envoyez une commande au processus en cours dans le conteneur.

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Exemples** :

L'exemple suivant est une demande d'arrêt du processus dans un conteneur dont le nom est `proxy` :
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Affichez le nom du référentiel d'images {{site.data.keyword.Bluemix_notm}} privé pour l'organisation à laquelle vous vous connectez.

```
bluemix ic namespace-get
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Définissez le nom du référentiel d'images {{site.data.keyword.Bluemix_notm}} privé pour l'organisation à laquelle vous vous connectez.

*Restriction* : vous ne pouvez pas utiliser de trait d'union (`-`) dans le nom d'espace de nom de votre référentiel.

```
bluemix ic namespace-set NOM
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM* (requis) : fonction exécutée une fois seulement afin de définir l'espace de nom de référentiel pour votre organisation, s'il n'est pas déjà défini. Une fois l'espace de nom défini, réinitialisez IBM Containers avec la commande `bluemix ic init` avant de continuer.


## bluemix ic pause
{: #pause}

Interrompez tous les processus d'un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} dans l'aide de Docker. Pour arrêter un conteneur, voir la commande [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Réponses** :

- Paused container successfully.

- Command failed with container cloud service

 `{message}`
  
 Où `{message}` est l'erreur connexe.
 
- Command failed - Could not connect to container cloud service

**Exemples** :

L'exemple suivant est une demande d'interruption d'un conteneur dont le nom est `proxy` :
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

Reprenez l'exécution de tous les processus dans un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} dans l'aide de Docker. Pour interrompre un conteneur, voir la commande [bluemix ic pause](#pause).

```
bluemix ic unpause CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Réponses** :

- Unpaused container successfully.

- Command failed with container cloud service 

 `{message}` 
 
 Où `{message}` est l'erreur connexe.
 
- Command failed - Could not connect to container cloud service

**Exemples** :

L'exemple suivant est une demande de reprise d'un conteneur dont le nom est `proxy` :
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Répertoriez les mappages de port ou un mappage spécifique pour le conteneur. Cette commande encapsule la commande `docker port`. Pour plus d'informations, voir la commande [port](https://docs.docker.com/reference/commandline/port/){: new_window} dans l'aide de Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Affichez la liste des conteneurs en cours d'exécution dans l'espace de nom de l'utilisateur connecté. Par défaut, cette commande affiche seulement les conteneurs en cours d'exécution. Pour plus d'informations, voir la commande [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} dans l'aide de Docker.

```
bluemix ic ps [-a|--all][-s|--size] [-l NOMBRE|--limit NOMBRE][-q|--quiet]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-a|--all (facultatif) : affichez tous les conteneurs, en cours d'exécution et arrêtés.

-s|--size (facultatif) : répertoriez les tailles des conteneurs.

-l *NOMBRE*|--limit *NOMBRE* (facultatif) : répertoriez les conteneurs créés le plus récemment, où *NOMBRE* est le nombre de conteneurs créés le plus récemment à renvoyer.

Par exemple, si vous avez créé les conteneurs `noeud1` à `noeud5` séquentiellement, la commande `bluemix ic ps --limit 2` renvoie noeud4 et noeud5 car il s'agit des deux derniers conteneurs créés.

-q|--quiet (facultatif) : affichez les ID de conteneur seulement.

**Exemples** :

L'exemple suivant est une demande d'affichage de tous les conteneurs en cours d'exécution et arrêtés :
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

Redémarrer un conteneur. Pour plus d'informations, voir la commande [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} dans l'aide de Docker.

```
bluemix ic restart CONTENEUR [-t SECONDES|--time SECONDES]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

-t *SECONDES*|--time *SECONDES* (facultatif) : délai d'attente en secondes avant le redémarrage du conteneur.

**Réponses** :

- Restarted container successfully.

- Command failed with container cloud service 

 `{message}` 
 
 Où `{message}` est l'erreur connexe.
 
- Command failed - Could not connect to container cloud service

**Exemples** :

L'exemple suivant est une demande de redémarrage d'un conteneur dont le nom est `proxy` :
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Supprimez un conteneur. Pour plus d'informations, voir la commande [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} dans l'aide de Docker.

```
bluemix ic rm [-f|--force] CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-f|--force (facultatif) : force le retrait d'un conteneur en cours d'exécution ou ayant échoué.

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Réponses** :

- Removed container successfully.

- Command failed with container cloud service 

 `{message}` 
 
 Où `{message}` est l'erreur connexe.
 
- Command failed - Could not connect to container cloud service.

**Exemples** :

L'exemple suivant est une demande de retrait d'un conteneur dont le nom est `proxy` :
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Supprimez une image de l'espace de nom de l'utilisateur connecté. Pour plus d'informations, voir la commande [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} dans l'aide de Docker.

```
bluemix ic rmi [-R REGISTRE|--registry REGISTRE] IMAGE
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-R *REGISTRE*|--registry *REGISTRE* (facultatif) : changez l'hôte du registre. Par défaut, le registre que vous spécifiez dans la commande `bluemix ic init` est utilisé.

*IMAGE* (requis) : nom de l'image à retirer. Si aucune étiquette n'est spécifiée dans le nom de l'image, l'image associée à l'étiquette `latest` est supprimée par défaut.

**Réponses** :

- Removed: `{IMAGE}`

 Où `{IMAGE}` est le nom de l'image qui a été supprimée.
 
- Error! No registry host specified.

- Image remove failed - Could not connect to container cloud registry

- Command failed with container cloud service 

 `{message}`
 
 Où `{message}` est l'erreur connexe.

**Exemples** :

L'exemple suivant est une demande de retrait de l'image `monespacenom/monimage:latest` :
```
bluemix ic rmi registry.ng.bluemix.net/monespacenom/monimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

Démarrez un nouveau conteneur dans le service cloud de conteneur depuis un nom d'image. Pour plus d'informations, voir la commande [run](https://docs.docker.com/reference/commandline/run/){: new_window} dans l'aide de Docker.



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMOIRE|--memory MEMOIRE][-e ENV|--env ENV] [-v VOLUME:CHEMIN_CONTENEUR] -n NOM|--name NOM [--link NOM:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**Remarque :** assurez-vous que l'outil de commande Cloud Foundry est installé et que vous disposez d'un jeton Cloud Foundry. Une connexion réussie avec `bluemix login` et `bluemix ic init` génère le jeton et les certificats requis. 


**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

-p *PORT*|--publish *PORT* (facultatif) : exposez le port pour le trafic HTTP. Incluez tous les ports spécifiés dans le document Dockerfile pour l'image que vous utilisez. Vous pouvez inclure plusieurs ports avec plusieurs options `-p`. L'exposition d'un port lie automatiquement une adresse IP publique au conteneur si une telle adresse est disponible.

Si une adresse IP existe dans l'espace à lier au conteneur, vous pouvez la spécifier plutôt que de procéder à la liaison ultérieurement. L'adresse IP doit être spécifiée au format *&lt;adresse_ip&gt;:&lt;port_conteneur&gt;:&lt;port_conteneur&gt;*

Pour plus d'informations sur la demande d'adresses IP pour un espace, voir la commande [bluemix ic ip-request](#ip_request).

Lorsque vous spécifiez un port, vous rendez l'application disponible dans l'équilibreur de charge {{site.data.keyword.Bluemix_notm}} ou dans les conteneurs du même espace {{site.data.keyword.Bluemix_notm}} qui tentent d'accéder à l'hôte. Si un port est spécifié dans le document Dockerfile pour l'image que vous utilisez, incluez ce port.

**Astuce :**

- Pour l'image Liberty Server certifiée IBM, ou une version modifiée de cette image, entrez le port 9080.
- Pour l'image Node.js certifiée IBM, ou une version modifiée de cette image, entrez le port 8000.

-P (facultatif) : exposez automatiquement les ports qui sont spécifiés dans le document Dockerfile de l'image pour le trafic HTTP.

-m *MEMOIRE*|--memory *MEMOIRE* (facultatif) : affectez une limite de mémoire au groupe en mégaoctets. Lorsque vous créez un groupe de conteneurs depuis l'interface de ligne de commande, la valeur par défaut pour chaque instance de conteneur est `64` Mo.  Lorsque vous créez un groupe de conteneurs depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}, la valeur par défaut pour chaque instance est `256` Mo. Les valeurs admises sont `64`, `256`, `512`, `1024` et `2048`. Une fois que vous avez affecté une limite de mémoire, vous ne pouvez plus la modifier.

-e *ENV*|--env *ENV* (facultatif) : définissez la variable d'environnement, où **ENV** est une paire `clé=valeur`. Répertoriez plusieurs clés séparément. Si vous incluez des guillemets, placez-les autour du nom et de la valeur de la variable d'environnement. Exemple : `-e "clé1=valeur1" -e "clé2=valeur2" -e "clé3=valeur3"`. Le tableau suivant répertorie certaines variables d'environnement couramment utilisées que vous pouvez spécifier :

|      Variable d'environnement                          |   Description                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nom_app&gt;*       | Liez un service à un conteneur. Utilisez la variable d'environnement `CCS_BIND_APP` pour lier une application à un conteneur. L'application est liée au service cible et sert de pont qui permet à {{site.data.keyword.Bluemix_notm}} de fournir les informations contenues dans la variable `VCAP_SERVICES` de votre application pont dans votre instance de conteneur en cours d'exécution. Pour plus d'informations sur la création d'une application pont, voir
[Liaison d'un service à un conteneur](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;clé_ssh_publique&gt;* | Ajoutez une clé SSH à un conteneur lorsque vous créez le conteneur. Vous pouvez ajouter la clé SSH à l'aide d'une variable d'environnement lorsque vous créez un conteneur depuis le tableau de bord {{site.data.keyword.Bluemix_notm}} ou depuis l'interface de ligne de commande. Pour plus d'informations sur les clés SSH, voir [Connexion à un conteneur](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;chemin_fichier&gt;* | Ajoutez un fichier journal à surveiller dans le conteneur. Incluez la variable d'environnement `LOG_LOCATIONS` avec un chemin d'accès au fichier journal. |
*Tableau 2. Variables d'environnement couramment utilisées*

-v VOLUME:CHEMIN_CONTENEUR[:ro]|--volume VOLUME:CHEMIN_CONTENEUR[:ro](facultatif) : associez un volume à un conteneur en spécifiant les détails au format `ID_volume:chemin_conteneur[:ro]`.

- *VOLUME* : nom ou ID du volume.
- *CHEMIN_CONTENEUR* : chemin d'accès absolu au volume dans le conteneur.
- ro (facultatif) : la spécification de `ro` rend le volume accessible en lecture seule au lieu d'être accessible par défaut en lecture/écriture.

-n *NOM*|--name *NOM* (requis) : affectez un nom au conteneur.

*Astuce :* le nom de conteneur doit commencer par une lettre. Il peut inclure des lettres majuscules, des lettres minuscules, des chiffres, des points (`.`), des traits de soulignement (`_`) et des traits d'union (`-`).

--link *NOM*:*ALIAS* (facultatif) : à chaque fois que vous voulez qu'un conteneur communique avec un autre conteneur en cours d'exécution, vous pouvez le désigner en utilisant un alias pour le nom d'hôte.

-it (facultatif) : exécutez le conteneur en mode interactif. Une fois le conteneur créé, l'entrée standard continue d'être affichée. Entrez `exit` pour quitter.

*IMAGE* (requis) : image à inclure dans le conteneur. Vous pouvez spécifier des commandes après l'image, mais n'indiquez pas d'options. Incluez toutes les options avant de spécifier une image.

Si vous utilisez une image qui se trouve dans le référentiel {{site.data.keyword.Bluemix_notm}} privé de votre organisation, spécifiez l'image au format *registry.ng.bluemix.net/ESPACE_NOM/IMAGE*.

Si vous utilisez une image fournie par IBM Containers, spécifiez l'image au format *registry.ng.bluemix.net/IMAGE*.

*CMD* (facultatif) : commande et arguments transmis au conteneur en vue de leur exécution. Cette commande doit être une commande à exécution longue. N'utilisez pas de commande à exécution courte, comme `/bin/date`, car elle pourrait entraîner la panne du conteneur.



**Exemples** :

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


## bluemix ic route-map
{: #bluemix_ic_route_map}

Etablissez la route pour le trafic Internet à utiliser pour accéder au groupe de conteneurs. Vous pouvez utiliser cette commande pour établir une nouvelle route ou mettre à jour une route existante.

```
bluemix ic route-map [-n HOTE|--hostname HOTE][-d DOMAINE|--domain DOMAINE] GROUPE_CONTENEURS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

-n *HOTE*|--hostname *HOTE* (facultatif) : nom d'hôte pour la route. Il s'agit de la première partie de l'adresse URL de route publique complète, par exemple `monhôteconteneur` dans l'adresse URL `monhôteconteneur.mybluemix.net`.

-d *DOMAINE*|--domain *DOMAINE* (facultatif) : nom de domaine pour la route, qui constitue la deuxième partie de l'adresse URL de route publique complète. Dans la plupart des cas, le domaine est `mybluemix.net`. Vous pouvez aussi utiliser ce paramètre pour spécifier un domaine privé.

*GROUPE_CONTENEURS* (requis) : nom ou ID du groupe de conteneurs.

**Exemples** :

L'exemple suivant est une demande de mappage de route pour le groupe dont le nom est `GROUPE1`, où `mon_hôte` est le nom d'hôte et `organisation.com` est le domaine.
```
bluemix ic route-map -n mon_hôte -d organisation.com GROUPE1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Etablissez la route pour le trafic Internet à utiliser pour accéder au groupe de conteneurs. Vous pouvez utiliser cette commande pour établir une nouvelle route ou mettre à jour une route existante.

```
bluemix ic route-unmap [-n HOTE|--hostname HOTE][-d DOMAINE|--domain DOMAINE] GROUPE_CONTENEURS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

-n *HOTE*|--hostname *HOTE* (facultatif) : nom d'hôte pour la route.

-d *DOMAINE*|--domain *DOMAINE* (facultatif) : nom de domaine pour la route.

*GROUPE_CONTENEURS* (requis) : nom ou ID du groupe de conteneurs.

**Exemples** :

L'exemple suivant est une demande d'annulation de mappage de route pour le groupe dont le nom est `GROUPE1`, où `mon_hôte` est le nom d'hôte et `organisation.com` est le domaine.
```
bluemix ic route-unmap -n mon_hôte -d organisation.com GROUPE1
```


## bluemix ic start
{: #ic_start}
Démarrez un conteneur arrêté. Pour plus d'informations, voir la commande [start](https://docs.docker.com/reference/commandline/start/){: new_window} dans l'aide de Docker. Pour arrêter un conteneur, voir la commande [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTENEUR
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Réponses** :

- Started container successfully.

- Command failed with container cloud service

 `{message}`
  
 Où `{message}` est l'erreur connexe.
 
- Command failed - Could not connect to container cloud service

**Exemples** :

L'exemple suivant est une demande de démarrage d'un conteneur dont le nom est `proxy` :
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
Arrêtez un conteneur en cours d'exécution. Pour plus d'informations, voir la commande [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} dans l'aide de Docker. Pour démarrer un conteneur, voir la commande [bluemix ic start](#ic_start).

```
bluemix ic stop CONTENEUR [-t SECONDES|--time SECONDES]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

-t *SECONDES*|--time *SECONDES* (facultatif) : délai d'attente en secondes avant l'arrêt du conteneur.

**Réponses** :

- Stopped container successfully.

- Command failed with container cloud service

 `{message}`
  
 Où `{message}` est l'erreur connexe.
 
- Command failed - Could not connect to container cloud service

**Exemples** :

L'exemple suivant est une demande d'arrêt d'un conteneur dont le nom est `proxy` :
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Affichez les statistiques d'utilisation actuelles d'un ou de plusieurs conteneurs. Utilisez `CTRL+C` pour quitter. Pour plus d'informations, voir la commande [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} dans l'aide de Docker.

```
bluemix ic stats [--no-stream] CONTENEUR [CONTENEUR]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

--no-stream (facultatif) : affichez seulement le résultat le plus récent et n'incluez aucune information précédente.

**Exemples** :

L'exemple suivant est une demande d'affichage des statistiques les plus récentes sur un conteneur :
```
bluemix ic stats --no-stream mon_conteneur
```


## bluemix ic top
{: #bluemix_ic_top}

Affichez les processus en cours d'exécution dans le conteneur. Pour plus d'informations, voir la commande [top](https://docs.docker.com/reference/commandline/top/){: new_window} dans l'aide de Docker.

```
bluemix ic top CONTENEUR [CONTENEUR]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Exemples** :

L'exemple suivant est une demande d'affichage des processus d'un conteneur dont le nom est `mon_conteneur`.
```
bluemix ic top mon_conteneur
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Répertoriez les volumes.

```
bluemix ic volumes
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspectez un volume.

```
bluemix ic volume-inspect NOM_VOLUME
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_VOLUME* (requis) : nom du volume.

**Exemples** :

L'exemple suivant est une demande d'inspection d'un volume, où `nom_volume` est le nom du volume :
```
bluemix ic volume-inspect nom_volume
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Créez un volume.

```
bluemix ic volume-create NOM_VOLUME
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_VOLUME* (requis) : nom du volume. Il peut comporter des lettres minuscules, des chiffres, des traits de soulignement (`_`) et des traits d'union (`-`).

**Exemples** :

L'exemple suivant est une demande de création d'un volume :
```
bluemix ic volume-create nom_volume 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Retirez un volume.

```
bluemix ic volume-remove NOM_VOLUME
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_VOLUME* (requis) : nom du volume.

**Exemples** :

L'exemple suivant est une demande de retrait d'un volume, où `nom_volume` est le nom du volume :
```
bluemix ic volume-remove nom_volume
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Répertorie les systèmes de fichiers.

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Crée un nouveau système de fichiers.

```
bluemix ic volume-fs-create NOM_SYSTEME_FICHIERS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_SYSTEME_FICHIERS* (requis) : nom du système de fichiers. Il peut comporter des lettres minuscules, des chiffres, des traits de soulignement (`_`) et des traits d'union (`-`).

**Exemples** :

L'exemple suivant illustre une demande de création d'un système de fichiers.
```
bluemix ic volume-fs-create mon_système_fichiers
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Supprime un espace de fichiers.

```
bluemix ic volume-fs-remove NOM_SYSTEME_FICHIERS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_SYSTEME_FICHIERS* (requis) : nom du système de fichiers. 

**Exemples** :

L'exemple suivant illustre une demande de suppression d'un système de fichiers, où
`mon_système_fichiers` est le nom du système de fichiers.
```
bluemix ic volume-fs-remove mon_système_fichiers
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspecte un système de fichiers.

```
bluemix ic volume-fs-inspect NOM_SYSTEME_FICHIERS
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_SYSTEME_FICHIERS* (requis) : nom du système de fichiers. 

**Exemples** :

L'exemple suivant illustre une demande d'inspection d'un système de fichiers, où `mon_système_fichiers` est le nom du volume.
```
bluemix ic volume-fs-inspect mon_système_fichiers
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Répertorie toutes les versions de système de fichiers.

```
bluemix ic volume-fs-flavors
```

**Prérequis** : Noeud final, Connexion, Cible

## bluemix ic wait
{: #bluemix_ic_wait}

Quittez un conteneur et affichez le code de sortie comme confirmation. Pour plus d'informations, voir la commande [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} dans l'aide de Docker.

```
bluemix ic wait CONTENEUR [CONTENEUR]
```

**Prérequis** : Noeud final, Connexion, Cible, Docker

**Options de commande** :

*CONTENEUR* (requis) : nom ou ID du conteneur.

**Exemples** :

L'exemple suivant est une demande de sortie d'un conteneur dont le nom est `mon_conteneur` :
```
bluemix ic wait mon_conteneur
```


## bluemix ic version
{: #bluemix_ic_version}

Affichez la version de Docker. 

```
bluemix ic version
```

**Prérequis** : Docker

Pour afficher la version d'IBM Containers, exécutez `bluemix ic info`. Pour plus d'informations, voir la commande [version](https://docs.docker.com/reference/commandline/version/){: new_window} dans l'aide de Docker.
