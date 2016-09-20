---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Interface de ligne de commande pour l'administration de {{site.data.keyword.Bluemix_notm}}
{: #bluemixadmincli}

Dernière mise à jour 17 août 2016
{: .last-updated}


Vous pouvez gérer les utilisateurs pour votre environnement
{{site.data.keyword.Bluemix_notm}} local ou {{site.data.keyword.Bluemix_notm}} dédié en utilisant l'interface de ligne de commande Cloud Foundry avec le plug-in
d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}. Par exemple, vous pouvez ajouter des utilisateurs depuis
un registre LDAP. Pour des informations sur la gestion de votre compte {{site.data.keyword.Bluemix_notm}} public, voir [Administration](../../../admin/adminpublic.html#administer).

Avant de commencer, installez l'interface de ligne de commande cf. Le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}} requiert cf version 6.11.2 ou ultérieure. [Télécharger l'interface de ligne de commande Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restriction :** l'interface de ligne de commande Cloud Foundry n'est pas prise en charge par Cygwin. Utilisez-la dans une fenêtre de ligne de commande autre que Cygwin.

## Ajout du plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}

Une fois l'interface de ligne de commande cf installée, vous pouvez ajouter le plug-in d'interface de ligne de commande d'administration
{{site.data.keyword.Bluemix_notm}}.

**Remarque** : si vous avez déjà installé le plug-in d'administration {{site.data.keyword.Bluemix_notm}}, il peut être
nécessaire de le désinstaller, de supprimer le référentiel, puis de réinstaller le plug-in afin de bénéficier des mises à jour les plus récentes.

Procédez comme suit pour ajouter le référentiel et installer le plug-in :

<ol>
<li>Pour ajouter le référentiel de plug-in d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante : <br/><br/> <code>
cf add-plugin-repo BluemixAdmin https://console.&lt;sous-domaine&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;sous-domaine&gt;</dt>
<dd class="pd">Sous-domaine de l'adresse URL pour votre instance {{site.data.keyword.Bluemix_notm}}. Par exemple, <code>https://console.mycompany.bluemix.net/cli</code>.</dd>
</dl>
</li>
<li>Pour installer le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Si vous devez désinstaller le plug-in, vous pouvez utiliser les commandes suivantes, puis vous pouvez ajouter le référentiel mis à jour et installer la dernière version du plug-in :

* Désinstallez le plug-in : `cf uninstall-plugin-repo BluemixAdminCLI`
* Retirez le référentiel de plug-in : `cf remove-plugin-repo BluemixAdmin`


## Utilisation du plug-in d'interface de ligne de commande
d'administration {{site.data.keyword.Bluemix_notm}}

Vous pouvez utiliser le plug-in d'interface de ligne de commande d'administration
{{site.data.keyword.Bluemix_notm}} pour ajouter ou retirer des utilisateurs, affecter des
utilisateurs à des organisations ou annuler leur affectation, et effectuer d'autres tâches de gestion. Pour afficher la liste des commandes, exécutez la
commande suivante :

```
cf plugins
```
{: codeblock}

Pour obtenir de l'aide supplémentaire sur une commande, utilisez l'option `-help`.

### Connexion à {{site.data.keyword.Bluemix_notm}} et ouverture de session

Pour pouvoir utiliser le plug-in d'interface de ligne de commande d'administration afin de gérer les utilisateurs, vous devez vous connecter et
ouvrir une session, si ce n'est pas déjà fait.

<ol>
<li>Pour vous connecter au noeud final d'API {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante : <br/><br/> <code>
cf ba api https://console.&lt;sous-domaine&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;sous-domaine&gt;</dt>
<dd class="pd">Sous-domaine de l'adresse URL pour votre instance {{site.data.keyword.Bluemix_notm}}.<br />
</dd>
</dl>
<p>Vous trouverez l'adresse URL correcte dans la page Resources Information de la console d'administration. L'adresse URL est affichée dans la section API Information, dans la zone **API
URL**.</p>
</li>
<li>Connectez-vous à {{site.data.keyword.Bluemix_notm}} avec la commande suivante :<br/><br/>
<code>
cf login
</code>
</li>
</ol>

### Ajout d'un utilisateur

Vous pouvez ajouter un utilisateur à votre environnement {{site.data.keyword.Bluemix_notm}} depuis le registre d'utilisateurs pour votre environnement.
Entrez la commande suivante :

```
cf ba add-user <nom_utilisateur> <organisation>
```
{: codeblock}

**Remarque** : pour ajouter un utilisateur à une organisation spécifique, vous devez être le responsable de l'organisation ou vous devez disposez des droits**Admin** (l'alternative disponible est **Superutilisateur**) ou **Utilisateur** avec un accès **Ecriture**. 

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans le registre LDAP.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à laquelle ajouter l'utilisateur.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba au** comme alias pour le nom de commande plus long
**ba add-user**.

<!-- staging-only commands start. Live for interconnect -->

### Recherche d'un utilisateur

Vous pouvez rechercher un utilisateur. Entrez la commande suivante :

```
cf ba search-users <nom_utilisateur>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Astuce :** vous pouvez aussi utiliser **ba su** comme alias pour le nom de commande plus long **ba
search-users**.

### Définition des droits d'un utilisateur

Vous pouvez définir les droits d'un utilisateur spécifié. Entrez la commande suivante :

```
cf ba set-permissions <nom_utilisateur> <droit> <accès>
```
{: codeblock}

**Remarque** : vous ne pouvez définir qu'un droit à la fois.

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;droit&gt;</dt>
<dd class="pd">Définissez les droits pour l'utilisateur : Admin (l'alternative disponible est Superutilisateur), Connexion (l'alternative disponible est De base), Catalogue (accès en lecture ou en écriture), Rapports (accès en lecture ou en
écriture) ou Utilisateurs (accès en lecture ou en écriture).</dd>
<dt class="pt dlterm">&lt;accès&gt;</dt>
<dd class="pd">Pour les droits Catalogue, Rapports ou Utilisateurs, vous devez aussi définir le niveau d'accès <code>read</code> (lecture) ou
<code>write</code> (écriture).</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sp** comme alias pour le nom de commande plus long **ba
set-permissions**.

<!-- staging-only commands end -->

### Retrait d'un utilisateur

Vous pouvez retirer un utilisateur de votre environnement {{site.data.keyword.Bluemix_notm}} avec la commande suivante :

```
cf ba remove-user <nom_utilisateur>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Astuce :** vous pouvez aussi utiliser **ba ru** comme alias pour le nom de commande plus long **ba
remove-user**.

### Ajout et suppression d'une organisation

Vous pouvez ajouter et supprimer une organisation.

* Pour ajouter une organisation, entrez la commande suivante :

```
cf ba create-organization <organisation> <responsable>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à ajouter.</dd>
<dt class="pt dlterm">&lt;responsable&gt;</dt>
<dd class="pd">Nom d'utilisateur du responsable de l'organisation.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba co** comme alias pour le nom de commande plus long **ba
create-organization**.

* Pour supprimer une organisation, entrez la commande suivante :

```
cf ba delete-organization <organisation>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à supprimer.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba do** comme alias pour le nom de commande plus long **ba
delete-organization**.

### Affectation d'un utilisateur à une organisation

Vous pouvez affecter un utilisateur dans votre environnement {{site.data.keyword.Bluemix_notm}} à une organisation particulière. Entrez la commande suivante :

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
<dd class="pd">Voir [Rôles](../../../admin/users_roles.html) pour prendre connaissance des rôles utilisateur
{{site.data.keyword.Bluemix_notm}} et pour des descriptions.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba so** comme alias pour le nom de commande plus long **ba
set-org**.

### Annulation de l'affectation d'un utilisateur à une organisation

Vous pouvez annuler l'affectation d'un utilisateur dans votre environnement {{site.data.keyword.Bluemix_notm}} à une organisation
particulière. Entrez la commande suivante :

```
cf ba unset-org <nom_utilisateur> <organisation> [<rôle>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nom_utilisateur&gt;</dt>
<dd class="pd">Nom de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organisation&gt;</dt>
<dd class="pd">Nom ou identificateur global unique de l'organisation {{site.data.keyword.Bluemix_notm}}
à laquelle affecter l'utilisateur.</dd>
<dt class="pt dlterm">&lt;rôle&gt;</dt>
<dd class="pd">Voir [Rôles](../../../admin/users_roles.html) pour prendre connaissance des rôles utilisateur
{{site.data.keyword.Bluemix_notm}} et pour des descriptions.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba uo** comme alias pour le nom de commande plus long **ba
unset-org**.

### Rôles

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
<dd class="pd">Responsable de la facturation. Un responsable de la facturation peut afficher des informations sur l'utilisation des contextes d'exécution et des
services pour l'organisation.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Auditeur de l'organisation. Un auditeur de l'organisation peut afficher le contenu des applications et des services dans l'espace.</dd>
</dl>

### Définition d'un quota pour une organisation

Vous pouvez définir le quota d'usage pour une organisation particulière.

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

**Astuce :** vous pouvez aussi utiliser **ba sq** comme alias pour le nom de commande plus long **ba
set-quota**.

### Ajout, suppression et extraction de rapports

Vous pouvez ajouter, supprimer et extraire des rapports de sécurité.
* Pour ajouter un rapport, entrez la commande suivante :

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

* Pour supprimer un rapport, entrez la commande suivante :

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

* Pour extraire un rapport, entrez la commande suivante :

```
cf ba retrieve-report <catégorie> <date> <nom>
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

**Astuce :** vous pouvez aussi utiliser **ba rr** comme alias pour le nom de commande plus long **ba
retrieve-report**.

### Activation et désactivation des services pour toutes les organisations

Vous pouvez activer ou désactiver l'affichage d'un service dans le catalogue
{{site.data.keyword.Bluemix_notm}} pour toutes les organisations.

* Pour rendre un service visible dans le catalogue
{{site.data.keyword.Bluemix_notm}} pour
toutes les organisations, entrez la commande suivante :

```
cf ba enable-service-plan <identificateur_plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificateur_plan&gt;</dt>
<dd class="pd">Nom ou identificateur global unique (GUID) du plan de service à activer. Si vous entrez un nom de plan de service qui n'est pas unique, par exemple, "Standard" ou "Basic", vous êtes invité à choisir
parmi plusieurs plans de service. Pour identifier un nom de plan de service, sélectionnez la catégorie du service dans la page d'accueil, puis
**Ajouter** pour afficher les services de cette catégorie. Cliquez sur le nom du service pour ouvrir la vue détaillée, depuis laquelle vous pourrez examiner les noms des plans de service disponibles pour ce service. </dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba esp** comme alias pour le nom de commande plus long **ba
enable-service-plan**.

* Afin qu'un service ne soit pas visible dans le catalogue
{{site.data.keyword.Bluemix_notm}} pour toutes les organisations, entrez la commande suivante
:

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

### Ajout, suppression et édition de la visibilité d'un service pour les organisations

Vous pouvez ajouter ou supprimer une organisation dans la liste des organisations pouvant afficher un service spécifique dans le catalogue
{{site.data.keyword.Bluemix_notm}}. Vous pouvez aussi éditer et remplacer la liste des
services que des organisations spécifiques peuvent afficher dans le catalogue
{{site.data.keyword.Bluemix_notm}}.

* Pour permettre à une organisation d'afficher un service spécifique dans le catalogue
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

* Afin de supprimer la visibilité d'un service dans le catalogue
{{site.data.keyword.Bluemix_notm}} pour une organisation, entrez la commande suivante :

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

* Afin de remplacer tous les services visibles existants pour une organisation ou plusieurs organisations, entrez la commande suivante :

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

### Utilisation de courtiers de services

Utilisez les commandes ci-après pour répertorier tous les courtiers de services, ajouter ou supprimer un courtier de services, ou mettre à jour un
courtier de services.

* Vous pouvez répertorier un courtier de services en entrant la commande suivante :

```
cf ba service-brokers <nom_courtier>
```
{: codeblock}

**Remarque** : pour répertorier tous les courtiers de services, entrez la commande sans le paramètre
`nom_courtier`.

<dl class="parml">
<dt class="pt dlterm">&lt;nom_courtier&gt;</dt>
<dd class="pd">Facultatif : nom du courtier de services personnalisé. Utilisez ce paramètre pour obtenir des informations sur un courtier de services
spécifique.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sb** comme alias pour le nom de commande plus long **ba
service-brokers**.

* Vous pouvez ajouter un courtier de services pour pouvoir ajouter un service personnalisé à votre catalogue
{{site.data.keyword.Bluemix_notm}} avec la commande suivante :

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

**Astuce :** vous pouvez aussi utiliser **ba asb** comme alias pour le nom de commande plus long **ba
add-service-broker**.

* Vous pouvez supprimer un courtier de services pour retirer le service personnalisé de votre catalogue
{{site.data.keyword.Bluemix_notm}} avec la commande suivante :

```
cf ba delete-service-broker <courtier_services>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;courtier_services&gt;</dt>
<dd class="pd">Nom ou identificateur global unique du courtier de services personnalisé.</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba dsb** comme alias pour le nom de commande plus long **ba
delete-service-broker**.

* Vous pouvez mettre à jour un courtier de services avec la commande suivante :

`cf ba update-service-broker <nom_courtier> <nom_utilisateur> <mot_de_passe> <url_courtier>`
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

**Astuce :** vous pouvez aussi utiliser **ba usb** comme alias pour le nom de commande plus long **ba
update-service-broker**.


### Utilisation de groupes de sécurité d'application

Pour utiliser des groupes de sécurité d'application, vous devez être un administrateur avec accès complet pour l'environnement local ou dédié. Tous les utilisateurs de l'environnement peuvent répertorier les groupes de sécurité d'application disponibles pour l'organisation ciblée par la commande. En revanche, pour créer, mettre à jour ou lier des groupes de sécurité d'application, vous devez être un administrateur de l'environnement {{site.data.keyword.Bluemix_notm}}. 

Les groupes de sécurité d'application fonctionnent comme des pare-feu virtuels qui contrôlent le trafic sortant des applications de votre environnement {{site.data.keyword.Bluemix_notm}}. Chaque groupe de sécurité d'application comprend une liste de règles autorisant un trafic et des communications spécifiques vers et depuis le réseau externe. Vous pouvez lier un ou plusieurs groupes de sécurité d'application à un ensemble de groupes donné, par exemple, un ensemble de groupes utilisé pour l'application d'un accès global, ou vous pouvez effectuer une liaison à des espaces d'une organisation dans votre environnement {{site.data.keyword.Bluemix_notm}}. 

A l'origine, {{site.data.keyword.Bluemix_notm}} est configuré avec un accès global restreint au réseau externe. Deux groupes de sécurité créés par IBM, `public_networks` et `dns`, permettent un accès global au réseau externe lorsque vous liez ces deux groupes aux ensembles de groupes de sécurité Cloud Foundry. Les deux ensembles de groupes de sécurité Cloud Foundry qui sont utilisés pour appliquer un accès global sont **Default Staging** et **Default Running**. Ces ensembles de groupes appliquent les règles autorisant le trafic vers toutes les applications en cours d'exécution ou toutes les applications en cours de constitution. Si vous ne souhaitez pas établir de liaison à ces deux ensembles de groupes de sécurité, vous pouvez annuler la liaison à ces ensembles de groupes Cloud Foundry, puis lier le groupe de sécurité à un espace donné. Pour plus d'informations, voir [Binding Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Remarque** : les commandes suivantes qui vous permettent de gérer des groupes de sécurité sont basées sur la version 1.6 de Cloud Foundry. 

#### Recensement, création, mise à jour et suppression des groupes de sécurité

Pour plus d'informations sur la création de groupes de sécurité et des règles qui définissent le trafic sortant, voir [Creating Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

* Vous pouvez répertorier tous les groupes de sécurité en entrant la commande suivante :

```
cf ba security-groups
```
{: codeblock}

**Astuce :** vous pouvez aussi utiliser **ba sgs** comme alias pour le nom de commande plus long **ba security-groups**.

* Vous pouvez afficher les détails d'un groupe de sécurité donné en entrant la commande suivante :


```
cf ba security-groups <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom du groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba sg** comme alias pour le nom de commande plus long
**ba security-groups** avec le paramètre `security-group`. 


* Vous pouvez créer un groupe de sécurité en entrant la commande ci-après.
Le préfixe `adminconsole_` est ajouté au nom de chaque groupe de sécurité que vous créez afin de le distinguer des groupes de sécurité créés par IBM. 

```
cf ba create-security-group <groupe-sécurité> <chemin-vers-fichier-règles>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
<dt class="pt dlterm">&lt;Chemin vers fichier de règles&gt;</dt>
<dd class="pd">Chemin d'accès relatif ou absolu à un fichier de règles</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba csg** comme alias pour le nom de commande plus long **ba create-security-group**.

* Vous pouvez mettre à jour un groupe de sécurité en entrant la commande suivante :

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

* Vous pouvez supprimer un groupe de sécurité en entrant la commande suivante :

```
cf ba delete-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba dsg** comme alias pour le nom de commande plus long **ba delete-security-group**.


#### Liaison, annulation de liaison et recensement des groupes de sécurité liés

Pour plus d'informations sur la liaison et l'annulation de liaison des groupes de sécurité, voir [Binding Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window} et [Unbinding Application Security Groups](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* Vous pouvez établir une liaison à l'ensemble de groupes de sécurité Default Staging en entrant la commande suivante :


```
cf ba bind-staging-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba bssg** comme alias pour le nom de commande plus long **ba bind-staging-security-group**.

* Vous pouvez établir une liaison à l'ensemble de groupes de sécurité Default Running en entrant la commande suivante :


```
cf ba bind-running-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba brsg** comme alias pour le nom de commande plus long **ba bind-running-security-group**.

* Vous pouvez annuler la liaison à un ensemble de groupes de sécurité Default Staging en entrant la commande suivante :


```
cf ba cf ba unbind-staging-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba ussg** comme alias pour le nom de commande plus long **ba unbind-staging-security-group**.

* Vous pouvez annuler la liaison à un ensemble de groupes de sécurité Default Running en entrant la commande suivante :


```
cf ba unbind-running-security-group <groupe-sécurité>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;groupe de sécurité&gt;</dt>
<dd class="pd">Nom de votre groupe de sécurité</dd>
</dl>

**Astuce :** vous pouvez aussi utiliser **ba brsg** comme alias pour le nom de commande plus long **ba bind-running-security-group**.

* Vous pouvez lier un groupe de sécurité à un espace en entrant la commande suivante :

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

* Vous pouvez annuler la liaison d'un groupe de sécurité à un espace en entrant la commande suivante :

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

