---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Création d'organisations et d'espaces
{: #orgsspacesusers}

En tant que propriétaire de compte, vous pouvez gérer vos organisations et vos espaces depuis la page Gérer les organisations. Un responsable de l'organisation peut également utiliser la page Gérer les organisations afin de gérer les organisations dont il est responsable.
{:shortdesc}

Pour gérer des organisations et les espaces, clique dans la barre de menu {{site.data.keyword.Bluemix_notm}} sur **Gérer** &gt; **Compte** &gt; **Organisations**. 

**Remarque** : vous devez être propriétaire d'un compte Paiement à la carte pour pouvoir créer une organisation.

## Création d'organisations
{: #createorg}

Les organisations peuvent couvrir plusieurs régions et sont définies par les éléments suivants :

<dl>
<dt>Les membres d'équipe</dt>
<dd>Rôle disposant du droit de base dans les organisations et les espaces. Vous devez être affecté à une organisation pour pouvoir obtenir d'autres droits dans les espaces de l'organisation. Pour des informations détaillées, voir [Utilisateurs et rôles](/docs/iam/users_roles.html#userrolesinfo).</dd>
<dt>Les domaines</dt>
<dd>Indiquez la route Internet allouée à l'organisation. Une route possède un sous-domaine et un domaine. En général, le sous-domaine est le nom de l'application. Un domaine peut être un domaine de système ou un domaine personnalisé que vous avez enregistré pour votre application. Voir [Gestion des domaines personnalisés](/docs/admin/manageorg.html#managedomains).<br/>
<p>**Remarque :** si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS afin de résoudre votre domaine personnalisé de sorte qu'il désigne le domaine de système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque {{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre application.</p></dd>
<dt>Le quota</dt>
<dd>Il représente les ressources disponibles pour une organisation, notamment le nombre de services et la quantité de mémoire pouvant être alloués à l'organisation. Les quotas sont affectés lorsque les organisations sont créées. Toute application ou tout service dans un espace d'une organisation contribue à l'utilisation du quota. Avec les plans Paiement à la carte ou Abonnement, vous pouvez ajuster votre quota pour les applications et les conteneurs Cloud Foundry au fur et à mesure que les besoins de votre organisation changent. Voir [Gestion du quota](/docs/admin/manageorg.html#managequota).
<p>**Remarque :** Dans un compte d'abonnement, le quota est une limite définie par l'utilisateur qui déclenche l'envoi des notifications relatives aux dépenses.</p></dd>
</dl>

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser des organisations afin de permettre la collaboration entre les membres d'équipe et de faciliter le regroupement logique des ressources de projet comme suit :

<ul>
<li>Vous pouvez regrouper un ensemble d'espaces, d'applications, de services, de domaines, de routes et de membres d'équipe dans des organisations.</li>
<li>Vous pouvez gérer l'accès aux espaces et aux organisations pour chaque utilisateur.</li>
</ul>

Lorsque vous créez une organisation, le nom de l'organisation doit être unique dans {{site.data.keyword.Bluemix_notm}}. Si le nom d'organisation est déjà utilisé par un autre utilisateur d'environnement {{site.data.keyword.Bluemix_notm}} public, dédié ou local, vous devez spécifier un autre nom. Une fois que vous avez créé l'organisation, le droit *Responsable de l'organisation*, qui vous permet d'éditer le nom de l'organisation, d'ajouter des membres d'équipe et de créer ou de supprimer des espaces dans l'organisation, vous est attribué automatiquement.

Vous pouvez utiliser la commande [`bx iam org-delete`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_org_delete) pour supprimer des organisations. Lorsque vous supprimez une organisation, tous les espaces, toutes les applications et tous les services au sein de l'organisation sont supprimés.

Les [rôles utilisateur](/docs/iam/users_roles.html#userrolesinfo) suivants peuvent être affectés aux membres d'équipe dans une organisation :

<ul>
<li>Responsable de l'organisation</li>
<li>Responsable de la facturation de l'organisation</li>
<li>Auditeur de l'organisation</li>
</ul>

Seuls les propriétaires de compte de type Paiement à la carte peuvent créer une organisation. Vous pouvez créer une organisation comme suit :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Cliquez sur **Ajouter une nouvelle organisation**.
3. Entrez le nom de l'organisation.
4. Cliquez sur **Ajouter**.

<!-- Add info on Manage infrastructure option under a space -->

## Création d'espaces
{: #spaceinfo}

Dans une organisation, vous pouvez utiliser des espaces pour regrouper un ensemble d'applications, de services et de membres d'équipe. Les espaces sont liés à une région spécifique dans {{site.data.keyword.Bluemix_notm}}.

Une fois que vous avez ajouté des membres d'équipe à une organisation, vous pouvez leur attribuer des droits pour les espaces. A l'instar des organisations, les espaces possèdent également un ensemble de [rôles utilisateur](/docs/iam/users_roles.html#userrolesinfo) associés à des droits spécifiques pouvant être attribués aux membres d'équipe :

<ul>
<li>Responsable de l'espace</li>
<li>Développeur de l'espace</li>
<li>Auditeur de l'espace</li>
</ul>

**Remarque** : un membre d'équipe doit disposer d'au moins l'un des droits dans l'espace.

Vous pouvez créer des espaces dans votre organisation, par exemple un espace *dev* comme environnement de développement, un espace *test* comme environnement de test et un espace *production* comme environnement de production. Ensuite, vous pouvez associer vos applications à des espaces. Procédez comme suit pour créer un espace :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation à laquelle vous désirez ajouter un espace, puis sélectionnez **Afficher les détails**.
4. Cliquez sur **Ajouter un espace**.
5. Entrez le nom de l'espace.
6. Cliquez sur **Ajouter**.
