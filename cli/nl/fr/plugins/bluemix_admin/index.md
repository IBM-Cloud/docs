---

copyright:

  years: 2015, 2017

lastupdated: "2017-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Interface de ligne de commande pour l'administration de {{site.data.keyword.Bluemix_notm}}
{: #bluemixadmincli}


Vous pouvez gérer votre environnement {{site.data.keyword.Bluemix_notm}} local ou {{site.data.keyword.Bluemix_notm}} dédié en utilisant l'interface de ligne de commande Cloud Foundry avec le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}. Par exemple, vous pouvez ajouter des utilisateurs depuis un registre LDAP. Pour des informations sur la gestion de votre compte {{site.data.keyword.Bluemix_notm}} public, voir [Administration](/docs/admin/adminpublic.html#administer).

Avant de commencer, installez l'interface de ligne de commande cf. Le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}} requiert cf version 6.11.2 ou ultérieure. [Télécharger l'interface de ligne de commande Cloud Foundry ![icône de lien externe](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restriction :** l'interface de ligne de commande Cloud Foundry n'est pas prise en charge par Cygwin. Utilisez-la dans une fenêtre de ligne de commande autre que Cygwin.

**Remarque** : l'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}} n'est utilisée que pour l'environnement {{site.data.keyword.Bluemix_notm}} local et l'environnement {{site.data.keyword.Bluemix_notm}} dédié. Elle n'est pas prise en charge par l'environnement {{site.data.keyword.Bluemix_notm}} public.

## Ajout du plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}

Une fois l'interface de ligne de commande cf installée, vous pouvez ajouter le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}.

**Remarque** : si vous avez déjà installé le plug-in d'administration {{site.data.keyword.Bluemix_notm}}, il peut être nécessaire de le désinstaller, de supprimer le référentiel, puis de réinstaller le plug-in afin de bénéficier des mises à jour les plus récentes.

Procédez comme suit pour ajouter le référentiel et installer le plug-in :

<ol>
<li>Pour ajouter le plug-in d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin http://plugins.ng.bluemix.net
</code><br/><br/>
</li>
<li>Pour installer le plug-in de l'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

Si vous devez désinstaller le plug-in, vous pouvez utiliser les commandes suivantes, puis vous pouvez ajouter le référentiel mis à jour et installer la dernière version du plug-in :

* Désinstallez le plug-in : `cf uninstall-plugin BluemixAdminCLI`
* Retirez le référentiel de plug-in : `cf remove-plugin-repo BluemixAdmin`


## Utilisation du plug-in d'interface de ligne de commande
d'administration {{site.data.keyword.Bluemix_notm}}

Vous pouvez utiliser le plug-in d'interface de ligne de commande d'administration
{{site.data.keyword.Bluemix_notm}} pour ajouter ou retirer des utilisateurs, affecter des
utilisateurs à des organisations ou annuler leur affectation, et effectuer d'autres tâches de gestion.

Pour afficher la liste des commandes, exécutez la
commande suivante :

```
cf plugins
```
{: codeblock}

Pour obtenir de l'aide supplémentaire sur une commande, utilisez l'option `-help`.

### Connexion à {{site.data.keyword.Bluemix_notm}} et ouverture de session

Pour pouvoir utiliser le plug-in d'interface de ligne de commande d'administration, vous devez vous connecter et ouvrir une session, si ce n'est pas déjà fait.

<ol>
<li>Pour vous connecter au noeud final d'API {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;sous-domaine&gt;</dt>
<dd class="pd">Sous-domaine de l'adresse URL pour votre instance {{site.data.keyword.Bluemix_notm}}.<br />
</dd>
</dl>
<p>Vous trouverez l'adresse URL correcte dans la page des informations sur les ressources de la console d'administration. L'adresse URL est affichée dans la section API Information, dans la zone **API
URL**.</p>
</li>
<li>Connectez-vous à {{site.data.keyword.Bluemix_notm}} à l'aide de la commande suivante :<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## Administration des utilisateurs
{: #admin_users}

### Ajout d'un utilisateur
{: #admin_add_user}

Pour ajouter un utilisateur à votre environnement {{site.data.keyword.Bluemix_notm}} à partir du registre d'utilisateurs
de votre environnement, utilisez la commande suivante :

```
cf ba add-user <nom_utilisateur> <organisation> <prénom> <nom>
```
{: codeblock}

**Remarque** : pour ajouter un utilisateur à une organisation spécifique, vous devez être un **administrateur** disposant du droit **users.write** (ou **Superutilisateur**). Si vous êtes un responsable de l'organisation, vous pouvez aussi disposer de la capacité d'ajouter des utilisateurs à votre organisation via un superutilisateur qui exécute la commande **enable-managers-add-users**. Voir [Permettre aux responsables d'ajouter des utilisateurs](index.html#clius_emau) pour plus d'informations.

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans le registre LDAP.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à laquelle ajouter l'utilisateur.</dd>
<dt class="pt dlterm">&lt;prénom&gt;</dt>
<dd class="pd">Prénom de l'utilisateur à ajouter à l'organisation. </dd>
<dt class="pt dlterm">&lt;nom&gt;</dt>
<dd class="pd">Nom de l'utilisateur à ajouter à l'organisation. </dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba au** comme alias pour le nom de commande plus long **ba add-user**.

<!-- staging-only commands start. Live for interconnect -->

### Recherche d'un utilisateur
{: #admin_search_user}

Pour rechercher un utilisateur, entrez la commande suivante en conjonction avec les paramètres de filtre de recherche facultatifs (name, permission, organization et role) :

```
cf ba search-users -name=<valeur_nom_utilisateur> -permission=<valeur_droit> -organization=<valeur_organisation>
-role=<valeur_rôle>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;valeur_nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}. </dd>
<dt class="pt dlterm">&lt;valeur_droit&gt;</dt>
<dd class="pd">Droit accordé à l'utilisateur. Exemple : Superutilisateur, Accès de base, Catalogue, Utilisateur et Rapports. Pour plus d'informations sur les droits pouvant être affectés aux utilisateurs, voir [Droits](/docs/admin/index.html#permissions). Vous ne pouvez pas utiliser ce paramètre avec le paramètre organization dans une même requête. </dd>
<dt class="pt dlterm">&lt;valeur_organisation&gt;</dt>
<dd class="pd">Nom de l'organisation à laquelle appartient l'utilisateur. Vous ne pouvez pas utiliser ce paramètre avec le paramètre permission dans une même requête.</dd>
<dt class="pt dlterm">&lt;valeur_rôle&gt;</dt>
<dd class="pd">Rôle de l'organisation affecté à l'utilisateur. Exemple : responsable, responsable de la facturation ou auditeur de l'organisation. Vous devez spécifier l'organisation avec ce paramètre. Pour plus d'informations sur les rôles, voir [Rôles utilisateur](/docs/admin/users_roles.html#userrolesinfo).</dd>

</dl>

**Astuce :** vous pouvez aussi utiliser **ba su** comme alias pour le nom de commande plus long **ba search-users**.

### Définition des droits d'un utilisateur
{: #admin_setperm_user}

Pour définir les droits d'un utilisateur indiqué, entrez la commande suivante :

```
cf ba set-permissions <nom_utilisateur> <droit> <accès>
```
{: codeblock}

**Remarque** : vous ne pouvez définir qu'un droit à la fois.

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;droit&gt;</dt>
<dd class="pd">Définissez les droits pour l'utilisateur : Admin (l'alternative disponible est Superutilisateur), Connexion (l'alternative disponible est De base), Catalogue (accès en lecture ou en écriture), Rapports (accès en lecture ou en écriture) ou Utilisateurs (accès en lecture ou en écriture).</dd>
<dt class="pt dlterm">&lt;accès&gt;</dt>
<dd class="pd">Pour les droits Catalogue, Rapports ou Utilisateurs, vous devez aussi définir le niveau d'accès <code>read</code> (lecture) ou <code>write</code> (écriture).</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sp** comme alias pour le nom de commande plus long **ba set-permissions**.

<!-- staging-only commands end -->

### Retrait d'un utilisateur
{: #admin_remov_user}

Pour retirer un utilisateur de votre environnement {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante :

```
cf ba remove-user <nom_utilisateur>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Astuce :** vous pouvez aussi utiliser **ba ru** comme alias pour le nom de commande plus long **ba remove-user**.

### Permettre aux responsables d'ajouter des utilisateurs
{: #clius_emau}

Si vous disposez du droit **Superutilisateur** dans votre environnement {{site.data.keyword.Bluemix_notm}}, vous pouvez permettre aux responsables de l'organisation d'ajouter des utilisateurs aux organisations qu'ils gèrent. Pour permettre aux responsables d'ajouter des utilisateurs, entrez la commande suivante :

```
cf ba enable-managers-add-users
```
{: codeblock}

**Astuce :** vous pouvez aussi utiliser **ba emau** comme alias pour le nom de commande plus long **ba enable-managers-add-users**.

### Empêcher les responsables d'ajouter des utilisateurs
{: #clius_dmau}

Si des responsables de l'organisation ont été autorisés à ajouter des utilisateurs aux organisations qu'ils gèrent dans votre environnement {{site.data.keyword.Bluemix_notm}} avec la commande **enable-managers-add-users** et que vous disposez du droit **Superutilisateur**, vous pouvez supprimer cette capacité. Pour empêcher les responsables d'ajouter des utilisateurs, utilisez la commande suivante :

```
cf ba disable-managers-add-users
```
{: codeblock}

**Astuce :** vous pouvez aussi utiliser **ba dmau** comme alias pour le nom de commande plus long **ba disable-managers-add-users**.

## Administration des organisations
{: #admin_orgs}

### Ajout d'une organisation
{: #admin_add_org}

Pour ajouter une organisation, utilisez la commande suivante :

```
cf ba create-org <organisation> <responsable>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à ajouter.</dd>
<dt class="pt dlterm">&lt;responsable&gt;</dt>
<dd class="pd">Nom d'utilisateur du responsable de l'organisation.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba co** comme alias pour le nom de commande plus long **ba create-org**. 

### Suppression d'une organisation
{: #admin_delete_org}

Pour supprimer une organisation, utilisez la commande suivante :

```
cf ba delete-org <organisation>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à supprimer.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba do** comme alias pour le nom de commande plus long **ba delete-org**. 

### Affectation d'un utilisateur à une organisation
{: #admin_ass_user_org}

Pour affecter un utilisateur de votre environnement {{site.data.keyword.Bluemix_notm}} à une organisation particulière, utilisez la commande suivante :

```
cf ba set-org <nom_utilisateur> <organisation> [<rôle>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à laquelle affecter l'utilisateur.</dd>
<dt class="pt dlterm">&lt;rôle&gt;</dt>
<dd class="pd">Voir [Rôles](/docs/admin/users_roles.html) pour prendre connaissance des rôles utilisateur
{{site.data.keyword.Bluemix_notm}} et pour des descriptions.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba so** comme alias pour le nom de commande plus long **ba set-org**.

### Annulation de l'affectation d'un utilisateur à une organisation
{: #admin_unass_user_org}

Pour annuler l'affectation d'un utilisateur de votre environnement {{site.data.keyword.Bluemix_notm}} à une organisation particulière, entrez la commande suivante :

```
cf ba unset-org <nom_utilisateur> <organisation> [<rôle>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle affecter l'utilisateur.</dd>
<dt class="pt dlterm">&lt;rôle&gt;</dt>
<dd class="pd">Pour connaître les rôles utilisateur {{site.data.keyword.Bluemix_notm}} ainsi que leur description, voir [Affectation de rôles](/docs/admin/users_roles.html).</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba uo** comme alias pour le nom de commande plus long **ba unset-org**.

#### Affectation de rôles

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Responsable de l'organisation. Un responsable de l'organisation peut effectuer les opérations suivantes :
<ul>
<li>Créer ou supprimer des espaces dans l'organisation.</li>
<li>Inviter des utilisateurs dans l'organisation et gérer les utilisateurs.</li>
<li>Gérer les domaines de l'organisation.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Responsable de la facturation. Un responsable de la facturation peut afficher des informations sur l'utilisation des contextes d'exécution et des services pour l'organisation.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Auditeur de l'organisation. Un auditeur de l'organisation peut afficher le contenu des applications et des services dans l'espace.</dd>
</dl>

### Définition d'un quota pour une organisation
{: #admin_set_org_quota}

Pour définir le quota d'utilisation d'une organisation donnée, entrez la commande suivante :

```
cf ba set-quota <organisation> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
pour laquelle définir le quota.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">Plan d'établissement des quotas pour une organisation.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sq** comme alias pour le nom de commande plus long **ba set-quota**.


### Recherche des quotas de conteneur d'une organisation
{: #admin_find_containquotas}

Pour rechercher le quota de conteneur d'une organisation, utilisez la commande suivante :

```
cf bluemix-admin containers-quota <organisation>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou ID de l'organisation dans Bluemix. Ce paramètre est obligatoire.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba cq** comme alias pour le nom de commande plus long **bluemix-admin containers-quota**.

### Définition des quotas de conteneur pour une organisation
{: #admin_set_containquotas}

Pour définir le quota de conteneur d'une organisation, utilisez la commande suivante avec au moins une des options :

```
cf bluemix-admin set-containers-quota <organisation> <options>
```
{: codeblock}

**Remarque** : Vous pouvez inclure plusieurs options, mais vous devez en indiquer au moins une.

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou ID de l'organisation dans Bluemix. Ce paramètre est obligatoire.</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">Incluez au moins l'une des options suivantes, dont la valeur doit être un entier :
<ul>
<li>floating-ips-max &lt;valeur&gt;</li>
<li>floating-ips-space-default &lt;valeur&gt;</li>
<li>memory-max &lt;valeur&gt;</li>
<li>memory-space-default &lt;valeur&gt;</li>
<li>image-limit &lt;valeur&gt;</li>
</ul>
</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser les noms abrégés suivants comme alias des noms d'option plus longs :
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;valeur&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;valeur&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;valeur&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;valeur&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;valeur&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

Vous pouvez, si vous le souhaitez, fournir un fichier contenant des paramètres de configuration spécifiques dans un objet JSON valide. Si vous utilisez l'option **-file**, elle prévaut sur les autres options qui sont ignorées. Pour indiquer un fichier au lieu des options, entrez la commande suivante :

```
cf bluemix-admin set-containers-quota <organisation> <-file chemin_fichier_JSON>
```
{: codeblock}

Le fichier JSON doit être au format indiqué dans l'exemple suivant :

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**Astuce :** vous pouvez aussi utiliser **ba scq** comme alias pour le nom de commande plus long **bluemix-admin set-containers-quota**.

## Administration d'espaces
{: #admin_spaces}

### Ajout d'un espace à l'organisation

Pour ajouter un espace à l'organisation, utilisez la commande suivante :

```
cf bluemix-admin create-space <organisation> <nom_espace>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) de l'organisation à laquelle l'espace doit être ajouté. </dd>
<dt class="pt dlterm">&lt;nom_espace&gt;</dt>
<dd class="pd">Nom de l'espace qui doit être créé dans l'organisation. </dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba cs** comme alias pour le nom de commande plus long **ba create-space**. 

### Suppression d'un espace dans l'organisation

Pour retirer un espace de l'organisation, utilisez la commande suivante :

```
cf bluemix-admin delete-space <organisation> <nom_espace>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) de l'organisation dont l'espace doit être retiré. </dd>
<dt class="pt dlterm">&lt;nom_espace&gt;</dt>
<dd class="pd">Nom de l'espace qui doit être retiré de l'organisation. </dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba cs** comme alias pour le nom de commande plus long **ba delete-space**. 

### Ajout d'un utilisateur à un espace avec un rôle

Pour créer un utilisateur dans un espace en le dotant d'un rôle spécifié, utilisez le commande suivante :

```
cf bluemix-admin set-space <organisation> <nom_espace> <nom_utilisateur> <rôle>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) de l'organisation à laquelle l'utilisateur doit être ajouté. </dd>
<dt class="pt dlterm">&lt;nom_espace&gt;</dt>
<dd class="pd">Nom de l'espace auquel l'utilisateur doit être ajouté. </dd>
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur qui doit être ajouté. </dd>
<dt class="pt dlterm">&lt;rôle&gt;</dt>
<dd class="pd">Rôle de l'utilisateur qui doit être affecté. La valeur peut être Responsable, Développeur ou Auditeur. Pour connaître les rôles utilisateur et les descriptions {{site.data.keyword.Bluemix_notm}} dans un espace, voir [Affectation de rôles](/docs/admin/users_roles.html).
</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba ss** comme alias pour le nom de commande plus long **ba set-space**.


### Retrait du rôle d'un utilisateur dans un espace 

Pour retirer le rôle d'un utilisateur dans un espace, utilisez la commande suivante :

```
cf bluemix-admin unset-space <organisation> <nom_espace> <nom_utilisateur> <rôle>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) de l'organisation à laquelle l'utilisateur doit être ajouté. </dd>
<dt class="pt dlterm">&lt;nom_espace&gt;</dt>
<dd class="pd">Nom de l'espace auquel l'utilisateur doit être ajouté. </dd>
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur qui doit être ajouté. </dd>
<dt class="pt dlterm">&lt;rôle&gt;</dt>
<dd class="pd">Rôle de l'utilisateur qui doit être affecté. La valeur peut être Responsable, Développeur ou Auditeur. Pour connaître les rôles utilisateur et les descriptions {{site.data.keyword.Bluemix_notm}} dans un espace, voir [Affectation de rôles](/docs/admin/users_roles.html).
</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba us** comme alias pour le nom de commande plus long **ba unset-space**. 

## Administration de catalogue
{: #admin_catalog}

### Activation des services pour toutes les organisations
{: #admin_ena_service_org}

Pour activer l'affichage d'un service dans le catalogue {{site.data.keyword.Bluemix_notm}} pour toutes les organisations, entrez la commande suivante :

```
cf ba enable-service-plan <identificateur_plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificateur_plan&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) du plan de service à activer. Si vous entrez un nom de plan de service qui n'est pas unique, par exemple, "Standard" ou "Basic", vous êtes invité à choisir parmi plusieurs plans de service. Pour identifier un nom de plan de service, sélectionnez la catégorie du service dans la page d'accueil, puis **Ajouter** pour afficher les services de cette catégorie. Cliquez sur le nom du service pour ouvrir la vue détaillée, depuis laquelle vous pourrez examiner les noms des plans de service disponibles pour ce service. </dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba esp** comme alias pour le nom de commande plus long **ba enable-service-plan**.

### Désactivation des services pour toutes les organisations
{: #admin_dis_service_org}

Pour désactiver l'affichage d'un service dans le catalogue {{site.data.keyword.Bluemix_notm}} pour toutes les organisations, utilisez la commande suivante :

```
cf ba disable-service-plan <identificateur_plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificateur_plan&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) du plan de service à activer. Si vous entrez un nom de plan de service qui n'est pas unique, par exemple, "Standard" ou "Basic", vous êtes invité à choisir
parmi plusieurs plans de service. Pour identifier un nom de plan de service, sélectionnez la catégorie du service dans la page d'accueil, puis
**Ajouter** pour afficher les services de cette catégorie. Cliquez sur le nom du service pour ouvrir la vue détaillée, depuis laquelle vous pourrez examiner les noms des plans de service disponibles pour ce service.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba dsp** comme alias pour le nom de commande plus long **ba
disable-service-plan**.

### Ajout de la visibilité d'un service pour les organisations
{: #admin_addvis_service_org}

Vous pouvez ajouter une organisation dans la liste des organisations pouvant afficher un service spécifique dans le catalogue
{{site.data.keyword.Bluemix_notm}}. Pour permettre à une organisation
d'afficher un service spécifique dans le catalogue
{{site.data.keyword.Bluemix_notm}}, entrez la commande suivante :

```
cf ba add-service-plan-visibility <identificateur_plan> <organisation>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificateur_plan&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) du plan de service à activer. Si vous entrez un nom de plan de service qui n'est pas unique, par exemple, "Standard" ou "Basic", vous êtes invité à choisir
parmi plusieurs plans de service. Pour identifier un nom de plan de service, sélectionnez la catégorie du service dans la page d'accueil, puis
**Ajouter** pour afficher les services de cette catégorie. Cliquez sur le nom du service pour ouvrir la vue détaillée, depuis laquelle vous pourrez examiner les noms des plans de service disponibles pour ce service.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à ajouter à la liste de visibilité du service.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba aspv** comme alias pour le nom de commande plus long **ba
add-service-plan-visibility**.

### Suppression de la visibilité d'un service pour les organisations
{: #admin_remvis_service_org}

Vous pouvez supprimer une organisation de la liste des
organisations pouvant afficher un service spécifique dans le catalogue
{{site.data.keyword.Bluemix_notm}}. Afin de supprimer la visibilité
d'un service dans le catalogue {{site.data.keyword.Bluemix_notm}} pour
une organisation, entrez la commande suivante :

```
cf ba remove-service-plan-visibility <identificateur_plan> <organisation>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificateur_plan&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) du plan de service à activer. Si vous entrez un nom de plan de service qui n'est pas unique, par exemple, "Standard" ou "Basic", vous êtes invité à choisir
parmi plusieurs plans de service. Pour identifier un nom de plan de service, sélectionnez la catégorie du service dans la page d'accueil, puis
**Ajouter** pour afficher les services de cette catégorie. Cliquez sur le nom du service pour ouvrir la vue détaillée, depuis laquelle vous pourrez examiner les noms des plans de service disponibles pour ce service.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à retirer de la liste de visibilité du service.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba rspv** comme alias pour le nom de commande plus long **ba
remove-service-plan-visibility**.

### Edition de la visibilité d'un service pour les organisations
{: #admin_editvis_service_org}

Vous pouvez éditer et remplacer la liste des services que des
organisations spécifiques peuvent afficher dans le catalogue
{{site.data.keyword.Bluemix_notm}}. Afin de remplacer tous les services visibles existants pour une organisation ou plusieurs organisations, entrez la commande suivante :

```
cf ba edit-service-plan-visibilities <identificateur_plan> <organisation_1> <organisation_2_facultative>
```
{: codeblock}

**Remarque :** cette commande remplace les services visibles existants pour les organisations spécifiées par le service que vous
indiquez dans la commande.

<dl class="parml">
<dt class="pt dlterm">&lt;identificateur_plan&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) du plan de service à activer. Si vous entrez un nom de plan de service qui n'est pas unique, par exemple, "Standard" ou "Basic", vous êtes invité à choisir
parmi plusieurs plans de service. Pour identifier un nom de plan de service, sélectionnez la catégorie du service dans la page d'accueil, puis
**Ajouter** pour afficher les services de cette catégorie. Cliquez sur le nom du service pour ouvrir la vue détaillée, depuis laquelle vous pourrez examiner les noms des plans de service disponibles pour ce service.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
pour laquelle ajouter la visibilité. Vous pouvez activer la visibilité du service pour plusieurs organisations en entrant des noms ou des identificateurs
globaux uniques supplémentaires dans la commande.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba espv** comme alias pour le nom de commande plus long **ba
edit-service-plan-visibility**.

## Administration des rapports
{: #admin_add_report}

### Ajout de rapports
{: #admin_add_report}

Pour ajouter un rapport de sécurité, entrez la commande suivante :

```
cf ba add-report <catégorie> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**Remarque **: si vous disposez de droits d'accès en écriture pour les rapports, vous pouvez créer une nouvelle catégorie et ajouter un
rapport sous l'un des formats admis pour vos utilisateurs. Entrez le nom de la nouvelle catégorie pour le paramètre
`catégorie` ou ajoutez votre nouveau rapport à une catégorie existante.

<dl class="parml">
<dt class="pt dlterm">&lt;catégorie&gt;</dt>
<dd class="pd">Catégorie du rapport. Si le nom comporte un espace, placez-le entre guillemets.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">Date du rapport au format <samp class="ph codeph">AAAAMMJJ</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">Chemin d'accès au rapport au format PDF, au fichier texte ou au fichier journal à télécharger.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Option permettant d'inclure une version RTF (Rich Text Format) du document PDF. Elle ne s'applique que si vous avez inclus un chemin d'accès au rapport
au format PDF. La version RTF est utilisée pour l'indexation et la recherche.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba ar** comme alias pour le nom de commande plus long **ba
add-report**.

### Suppression de rapports
{: #admin_del_report}

Pour supprimer un rapport de sécurité, entrez la commande suivante :

```
cf ba delete-report <catégorie> <date> <nom>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;catégorie&gt;</dt>
<dd class="pd">Catégorie du rapport. Si le nom comporte un espace, placez-le entre guillemets.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">Date du rapport au format <samp class="ph codeph">AAAAMMJJ</samp>.</dd>
<dt class="pt dlterm">&lt;nom&gt;</dt>
<dd class="pd">Nom du rapport.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba dr** comme alias pour le nom de commande plus long **ba
delete-report**.

### Extraction de rapports
{: #admin_retr_report}

Pour extraire un rapport de sécurité, utilisez la commande suivante :

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">Nom de fichier du rapport. Si le nom comporte un espace, placez-le entre guillemets.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba rr** comme alias pour le nom de commande plus long **ba retrieve-report**.

## Affichage des informations relatives aux mesures des ressources
{: #cliresourceusage}

Vous pouvez afficher des informations sur les mesures des ressources,
notamment sur l'utilisation de la mémoire, du disque et de l'unité centrale. Vous
pouvez consulter un récapitulatif des ressources physiques et réservées disponibles, ainsi que l'utilisation des ressources physiques et réservées. Vous pouvez également afficher les données d'utilisation et l'utilisation historique de la mémoire et du disque des agents DEA (Droplet Execution Agent) et des cellules (architecture Diego). Les données d'historique pour l'utilisation de la mémoire et du disque sont affichées par défaut par semaine et par ordre décroissant. Pour afficher les informations sur les mesures des ressources, entrez la commande suivante :

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">Affichez les données d'historique pour la mémoire et l'espace disque un mois à la fois.</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">Affichez les données d'historique pour la mémoire et l'espace disque une semaine à la fois. Il s'agit de la valeur par défaut.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba rsm** comme alias pour le nom de commande plus long **ba resource-metrics**.


## Administration des courtiers de services
{: #admin_servbro}

### Liste des courtiers de services
{: #clilistservbro}

Pour dresser la liste de tous les courtiers de services, utilisez la
commande suivante :

```
cf ba service-brokers <nom_courtier>
```
{: codeblock}

**Remarque** : pour répertorier tous les courtiers de services, entrez la commande sans le paramètre
`nom_courtier`.

<dl class="parml">
<dt class="pt dlterm">&lt;nom_courtier&gt;</dt>
<dd class="pd">Facultatif : nom du courtier de services personnalisé. Utilisez ce paramètre pour obtenir des informations sur un courtier de services spécifique.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sb** comme alias pour le nom de commande plus long **ba service-brokers**.

### Ajout d'un courtier de services
{: #cliaddservbro}

Pour ajouter un courtier de services afin de pouvoir ajouter un service personnalisé à votre catalogue {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante :

```
cf ba add-service-broker <nom_courtier> <nom_utilisateur> <mot_de_passe> <url_courtier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_courtier&gt;</dt>
<dd class="pd">Nom du courtier de services personnalisé.</dd>
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom d'utilisateur du compte ayant accès au courtier de services.</dd>
<dt class="pt dlterm">&lt;mot_de_passe&gt;</dt>
<dd class="pd">Mot de passe du compte ayant accès au courtier de services.</dd>
<dt class="pt dlterm">&lt;url_courtier&gt;</dt>
<dd class="pd">Adresse URL du courtier de services.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba asb** comme alias pour le nom de commande plus long **ba add-service-broker**.

### Suppression d'un courtier de services
{: #clidelservbro}

Pour supprimer un courtier de services afin de retirer un service personnalisé de votre catalogue {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante :

```
cf ba delete-service-broker <courtier_services>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;courtier_services&gt;</dt>
<dd class="pd">Nom ou identificateur global unique du courtier de services personnalisé.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba dsb** comme alias pour le nom de commande plus long **ba delete-service-broker**.

### Mise à jour d'un courtier de services
{: #cliupdservbro}

Pour mettre à jour un courtier de services, utilisez la commande suivante :

```
cf ba update-service-broker <nom_courtier> <nom_utilisateur> <mot_de_passe> <url_courtier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_courtier&gt;</dt>
<dd class="pd">Nom du courtier de services personnalisé.</dd>
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom d'utilisateur du compte ayant accès au courtier de services.</dd>
<dt class="pt dlterm">&lt;mot_de_passe&gt;</dt>
<dd class="pd">Mot de passe du compte ayant accès au courtier de services.</dd>
<dt class="pt dlterm">&lt;url_courtier&gt;</dt>
<dd class="pd">Adresse URL du courtier de services.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba usb** comme alias pour le nom de commande plus long **ba update-service-broker**.


## Administration des groupes de sécurité d'application
{: #admin_secgro}

Pour utiliser des groupes de sécurité d'application, vous devez être un administrateur avec accès complet pour l'environnement local ou dédié. Tous les utilisateurs de l'environnement peuvent répertorier les groupes de sécurité d'application disponibles pour l'organisation ciblée par la commande. En revanche, pour créer, mettre à jour ou lier des groupes de sécurité d'application, vous devez être un administrateur de l'environnement {{site.data.keyword.Bluemix_notm}}.

Les groupes de sécurité d'application fonctionnent comme des pare-feux virtuels qui contrôlent le trafic sortant des applications de votre environnement {{site.data.keyword.Bluemix_notm}}. Chaque groupe de sécurité d'application comprend une liste de règles autorisant un trafic et des communications spécifiques vers et depuis le réseau externe. Vous pouvez lier un ou plusieurs groupes de sécurité d'application à un ensemble de groupes donné, par exemple, un ensemble de groupes utilisé pour l'application d'un accès global, ou vous pouvez effectuer une liaison à des espaces d'une organisation dans votre environnement {{site.data.keyword.Bluemix_notm}}.

A l'origine, {{site.data.keyword.Bluemix_notm}} est configuré avec un accès global restreint au réseau externe. Deux groupes de sécurité créés par IBM, `public_networks` et `dns`, permettent un accès global au réseau externe lorsque vous liez ces deux groupes aux ensembles de groupes de sécurité Cloud Foundry. Les deux ensembles de groupes de sécurité Cloud Foundry qui sont utilisés pour appliquer un accès global sont **Default Staging** et **Default Running**. Ces ensembles de groupes appliquent les règles autorisant le trafic vers toutes les applications en cours d'exécution ou toutes les applications en cours de constitution. Si vous ne souhaitez pas établir de liaison à ces deux ensembles de groupes de sécurité, vous pouvez annuler la liaison à ces ensembles de groupes Cloud Foundry, puis lier le groupe de sécurité à un espace donné. Pour plus d'informations, voir [Binding Application Security Groups ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Remarque** : les commandes suivantes qui vous permettent de gérer des groupes de sécurité sont basées sur la version 1.6 de Cloud Foundry. Pour plus d'informations, y compris sur les zones obligatoires et facultatives, reportez-vous aux informations relatives à Cloud Foundry concernant la [création de groupes de sécurité d'application ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

### Liste des groupes de sécurité
{: #clilissecgro}

* Pour dresser la liste de tous les groupes de sécurité, utilisez la commande suivante :

```
cf ba security-groups
```
{: codeblock}

**Astuce :** vous pouvez aussi utiliser **ba sgs** comme alias pour le nom de commande plus long **ba security-groups**.

* Pour afficher les détails d'un groupe de sécurité donné, utilisez la commande suivante :

```
cf ba security-groups <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom du groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sg** comme alias pour le nom de commande plus long **ba security-groups** avec le paramètre `security-group`.


### Création d'un groupe de sécurité
{: #clicreasecgro}

Pour plus d'informations sur la création de groupes de sécurité et des règles qui définissent le trafic sortant, voir [Creating Application Security Groups ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

Pour créer un groupe de sécurité, utilisez la commande suivante :

```
cf ba create-security-group <groupe-sécurité> <chemin-vers-fichier-règles>
```
{: codeblock}

Le préfixe `adminconsole_` est ajouté au nom de chaque groupe de sécurité que vous créez afin de le distinguer des groupes de sécurité créés par IBM.

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
<dt class="pt dlterm">&lt;Chemin vers fichier de règles&gt;</dt>
<dd class="pd">Chemin d'accès relatif ou absolu à un fichier de règles</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba csg** comme alias pour le nom de commande plus long **ba create-security-group**.

### Mise à jour d'un groupe de sécurité
{: #cliupdsecgro}

Pour mettre à jour un groupe de sécurité, utilisez la commande suivante :

```
cf ba update-security-group <groupe-sécurité> <chemin-vers-fichier-règles>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
<dt class="pt dlterm">&lt;Chemin vers fichier de règles&gt;</dt>
<dd class="pd">Chemin d'accès relatif ou absolu à un fichier de règles</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba usg** comme alias pour le nom de commande plus long **ba update-security-group**.

### Suppression d'un groupe de sécurité
{: #clidelsecgro}

Pour supprimer un groupe de sécurité, utilisez la commande suivante :

```
cf ba delete-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba dsg** comme alias pour le nom de commande plus long **ba delete-security-group**.


### Liaison de groupes de sécurité
{: #clibindsecgro}

Pour plus d'informations sur la liaison des groupes de sécurité, voir [Binding Application Security Groups ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

* Pour établir une liaison vers l'ensemble de groupes de sécurité Default Staging, utilisez la commande suivante :

```
cf ba bind-staging-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba bssg** comme alias pour le nom de commande plus long **ba bind-staging-security-group**.

* Pour établir une liaison vers l'ensemble de groupes de sécurité Default Running, utilisez la commande suivante :

```
cf ba bind-running-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba brsg** comme alias pour le nom de commande plus long **ba bind-running-security-group**.

* Pour lier un groupe de sécurité à un espace, utilisez la commande suivante :

```
cf ba bind-security-group <groupe-sécurité> <org> <espace>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
<dt class="pt dlterm">&lt;org&gt;</dt>
<dd class="pd">Nom de l'organisation à laquelle associer le groupe de sécurité</dd>
<dt class="pt dlterm">&lt;espace&gt;</dt>
<dd class="pd">Nom de l'espace dans l'organisation à laquelle associer le groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba bsg** comme alias pour le nom de commande plus long **ba bind-security-group**.

### Annulation de la liaison de groupes de sécurité
{: #cliunbindsecgro}

Pour plus d'informations sur l'annulation de la liaison de groupes de sécurité, voir [Unbinding Application Security Groups ![icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* Pour annuler la liaison vers l'ensemble de groupes de sécurité Default Staging, utilisez la commande suivante :

```
cf ba unbind-staging-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba ussg** comme alias pour le nom de commande plus long **ba unbind-staging-security-group**.

* Pour annuler la liaison vers l'ensemble de groupes de sécurité Default Running, utilisez la commande suivante :

```
cf ba unbind-running-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba brsg** comme alias pour le nom de commande plus long **ba bind-running-security-group**.

* Pour annuler la liaison d'un groupe de sécurité à un espace, utilisez la commande suivante :

```
cf ba unbind-security-group <groupe-sécurité> <org> <espace>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
<dt class="pt dlterm">&lt;org&gt;</dt>
<dd class="pd">Nom de l'organisation à laquelle associer le groupe de sécurité</dd>
<dt class="pt dlterm">&lt;espace&gt;</dt>
<dd class="pd">Nom de l'espace dans l'organisation à laquelle associer le groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba usg** comme alias pour le nom de commande plus long **ba unbind-staging-security-group**.

## Administration des packs de construction
{: #admin_buildpack}

### Liste des packs de construction
{: #clilistbuildpack}

Si vous disposez des droits en écriture dans le catalogue des applications, vous pouvez répertorier les packs de construction. Pour répertorier tous les packs de construction ou visualiser un pack de construction spécifique, utilisez la commande suivante :

```
cf ba buildpacks <nom_pack_construction>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_pack_construction&gt;</dt>
<dd class="pd">Paramètre facultatif permettant de spécifier un pack de construction particulier à afficher.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba lb** comme alias pour le nom de commande plus long **ba buildpacks**.

### Création et téléchargement d'un pack de construction
{: #clicreupbuildpack}

Si vous disposez des droits en écriture dans le catalogue des applications, vous pouvez créer et télécharger un pack de construction. Vous pouvez télécharger tout fichier compressé dont le type est .zip. Pour télécharger un pack de construction, utilisez la commande suivante :

```
cf ba create-buildpack <nom_pack_construction> <chemin_fichier> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_pack_construction&gt;</dt>
<dd class="pd">Nom du pack de construction à télécharger.</dd>
<dt class="pt dlterm">&lt;chemin_fichier&gt;</dt>
<dd class="pd">Chemin du fichier compressé du pack de construction.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">Ordre dans lequel les packs de construction sont recherchés au cours de la détection automatique des packs de construction.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba cb** comme alias pour le nom de commande plus long **ba create-buildpack**.

### Mise à jour d'un pack de construction
{: #cliupdabuildpack}

Si vous disposez des droits en écriture dans le catalogue des applications, vous pouvez mettre à jour un pack de construction existant.  Pour mettre à jour un pack de construction, utilisez la commande suivante :

```
cf ba update-buildpack <nom_pack_construction> <position> <activé> <verrouillé>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_pack_construction&gt;</dt>
<dd class="pd">Nom du pack de construction à mettre à jour.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">Ordre dans lequel les packs de construction sont recherchés au cours de la détection automatique des packs de construction.</dd>
<dt class="pt dlterm">&lt;activé&gt;</dt>
<dd class="pd">Indique si le pack de construction est utilisé pour la constitution.</dd>
<dt class="pt dlterm">&lt;verrouillé&gt;</dt>
<dd class="pd">Indique si le pack de construction est verrouillé pour empêcher les mises à jour.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba ub** comme alias pour le nom de commande plus long **ba update-buildpack**.

### Suppression d'un pack de construction
{: #clidelbuildpack}

Si vous disposez des droits en écriture dans le catalogue des applications, vous pouvez supprimer un pack de construction existant.  Pour supprimer un pack de construction, utilisez la commande suivante :

```
cf ba delete-buildpack <nom_pack_construction>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_pack_construction&gt;</dt>
<dd class="pd">Nom du pack de construction à supprimer.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba db** comme alias pour le nom de commande plus long **ba delete-buildpack**.
