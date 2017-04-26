---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des organisations et des espaces
{: #orgsspacesusers}

En tant que propriétaire de compte, vous pouvez gérer vos organisations et vos espaces depuis la page Gérer les organisations. Un responsable de l'organisation peut également utiliser la page Gérer les organisations afin de gérer les organisations dont il est responsable.
{:shortdesc}

Pour gérer des organisations et les espaces, clique dans la barre de menu {{site.data.keyword.Bluemix_notm}} sur **Gérer** &gt; **Compte** &gt; **Organisations**. 

**Remarque** : vous devez être propriétaire d'un compte Paiement à la carte pour pouvoir créer une organisation.

## Gestion des organisations
{: #orginfo}

Les organisations peuvent couvrir plusieurs régions et sont définies par les éléments suivants :

<dl>
<dt>Les membres d'équipe</dt>
<dd>Rôle disposant du droit de base dans les organisations et les espaces. Vous devez être affecté à une organisation pour pouvoir obtenir d'autres droits dans les espaces de l'organisation. Pour des informations détaillées, voir [Utilisateurs et rôles](/docs/admin/users_roles.html#userrolesinfo).</dd>
<dt>Les domaines</dt>
<dd>Indiquez la route Internet allouée à l'organisation. Une route possède un sous-domaine et un domaine. En général, le sous-domaine est le nom de l'application. Un domaine peut être un domaine de système ou un domaine personnalisé que vous avez enregistré pour votre application. Voir [Gestion des domaines personnalisés](/docs/admin/orgs_spaces.html#managedomains).<br/>
<p>**Remarque** : si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS afin de résoudre votre domaine personnalisé de sorte qu'il désigne le domaine de système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque {{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre application.</p></dd>
<dt>Le quota</dt>
<dd>Il représente les limites de ressources pour l'organisation, notamment le nombre de services et la quantité de mémoire pouvant être alloués à l'organisation. Les quotas sont affectés lorsque les organisations sont créées. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota. Avec les plans Paiement à la carte ou Abonnement, vous pouvez ajuster votre quota pour les applications et les conteneurs Cloud Foundry au fur et à mesure que les besoins de votre organisation changent. Voir [Gestion du quota](/docs/admin/orgs_spaces.html#managequota).</dd>
</dl>

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser des organisations afin de permettre la collaboration entre les membres d'équipe et de faciliter le regroupement logique des ressources de projet comme suit :

<ul>
<li>Vous pouvez regrouper un ensemble d'espaces, d'applications, de services, de domaines, de routes et de membres d'équipe dans des organisations.</li>
<li>Vous pouvez gérer l'accès aux espaces et aux organisations pour chaque utilisateur.</li>
</ul>

Lorsque vous créez une organisation, le nom de l'organisation doit être unique dans {{site.data.keyword.Bluemix_notm}}. Si le nom d'organisation est déjà utilisé par un autre utilisateur d'environnement {{site.data.keyword.Bluemix_notm}} public, dédié ou local, vous devez spécifier un autre nom. Une fois que vous avez créé l'organisation, le droit *Responsable de l'organisation*, qui vous permet d'éditer le nom de l'organisation, d'ajouter des membres d'équipe et de créer ou de supprimer des espaces dans l'organisation, vous est attribué automatiquement.

Vous devez prendre contact avec le [support {{site.data.keyword.Bluemix_notm}} ![icône de lien externe](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} pour supprimer une organisation. Lorsque vous demandez à l'équipe de support de supprimer une organisation, tous les espaces, toutes les applications et tous les services dans l'organisation sont supprimés.

Les [rôles utilisateur](/docs/admin/users_roles.html#userrolesinfo) suivants peuvent être affectés aux membres d'équipe dans une organisation :

<ul>
<li>Responsable de l'organisation</li>
<li>Responsable de la facturation de l'organisation</li>
<li>Auditeur de l'organisation</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Utilisation des espaces
{: #spaceinfo}

Dans une organisation, vous pouvez utiliser des espaces pour regrouper un ensemble d'applications, de services et de membres d'équipe. Les espaces sont liés à une région spécifique dans {{site.data.keyword.Bluemix_notm}}.

Une fois que vous avez ajouté des membres d'équipe à une organisation, vous pouvez leur attribuer des droits pour les espaces. A l'instar des organisations, les espaces possèdent également un ensemble de [rôles utilisateur](/docs/admin/users_roles.html#userrolesinfo) associés à des droits spécifiques pouvant être attribués aux membres d'équipe :

<ul>
<li>Responsable de l'espace</li>
<li>Développeur de l'espace</li>
<li>Auditeur de l'espace</li>
</ul>

**Remarque** : un membre d'équipe doit disposer d'au moins l'un des droits dans l'espace.

## Création d'organisations et d'espaces
{: #createorg}

Seuls les propriétaires de compte de type Paiement à la carte peuvent créer une organisation. Vous pouvez créer une organisation comme suit :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Cliquez sur **Ajouter une nouvelle organisation**.
3. Entrez le nom de l'organisation.
4. Cliquez sur **Ajouter**.

Vous pouvez créer des espaces dans votre organisation, par exemple un espace *dev* comme environnement de développement, un espace *test* comme environnement de test et un espace *production* comme environnement de production. Ensuite, vous pouvez associer vos applications à des espaces. Procédez comme suit pour créer un espace :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation à laquelle vous désirez ajouter un espace, puis sélectionnez **Afficher les détails**.
4. Cliquez sur **Ajouter un espace**.
5. Entrez le nom de l'espace.
6. Cliquez sur **Ajouter**.

## Changement de nom d'une organisation
{: #orgrename}

Procédez comme suit pour renommer votre organisation :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation que vous désirez éditer, puis sélectionnez **Afficher les détails**.
3. Sélectionnez **Editer l'organisation**.
4. Sélectionnez **Editer** pour le titre de l'organisation.
5. Entrez le nouveau nom d'organisation.
6. Cliquez sur **SAUVEGARDER**.

## Suppression d'une organisation ou d'un espace existant
{: #deleteorgs}

En tant que propriétaire de compte, vous pouvez prendre contact avec le [support {{site.data.keyword.Bluemix_notm}} ![icône de lien externe](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} pour supprimer une organisation.

**Remarque** : les opérations de suppression sont irréversibles. Vous perdez toutes vos applications et tous les services qui sont associés à l'organisation.

Vous pouvez supprimer un espace depuis la page **Gérer les organisations** :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation que vous désirez éditer, puis sélectionnez **Afficher les détails**.
3. Identifiez l'espace à supprimer, puis sélectionnez **Editer l'espace**.
4. Cliquez sur **Supprimer l'espace**.

## Liste des membres
{: #listmembers}

Procédez comme suit pour répertorier les membres d'une organisation spécifique :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation dont vous voulez afficher les membres, puis cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer l'organisation**.
4. Les membres de votre organisation et leurs rôles s'affichent dans l'onglet **UTILISATEURS**.

Procédez comme suit pour répertorier les membres d'un espace spécifique :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation dont vous voulez afficher les membres, puis cliquez sur **Afficher les détails**.
3. Identifiez l'espace dont vous voulez afficher les membres, puis cliquez sur **Editer l'espace**.
4. Les membres de votre espace et leurs rôles s'affichent dans l'onglet **UTILISATEURS**.

## Gestion du quota
{: #managequota}

En tant que propriétaire de compte {{site.data.keyword.Bluemix_notm}} ou responsable de l'organisation, vous pouvez afficher le quota alloué et le quota utilisé pour une organisation. Le quota représente les limites de ressources pour l'organisation et est affecté lorsque l'organisation est créée. Selon que vous disposez d'un compte d'essai ou d'un compte facturable, les ressources disponibles pour une organisation varient. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota alloué.

Pour afficher le quota utilisé et le quota alloué d'une organisation, procédez comme suit :

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation pour laquelle afficher le quota, puis cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer l'organisation**.
4. Si des espaces sont définis dans plusieurs régions, sélectionnez la région que vous souhaitez visualiser.
5. Cliquez sur **QUOTA**. 
6. Par défaut, la page du quota **Cloud Foundry** s'ouvre. Vous pouvez afficher les détails de quota des ressources suivantes :
 * MEMOIRE
 * Services
 * PLAN
 * PRIX
7. Cliquez sur **Conteneurs** pour afficher l'allocation des quotas de conteneur utilisé et disponible. L'allocation de conteneur varie en fonction du plan de tarification. Vous pouvez afficher les détails de quota des ressources suivantes :
 * MEMOIRE
 * Adresse IP publique
 * PARTAGE DE FICHIERS
8. Cliquez sur **Serveurs virtuels** pour visualiser les machines virtuelles.

**Remarque :** Les conteneurs ne sont pas disponibles dans la région {{site.data.keyword.Bluemix_notm}} Sydney. 

Pour plus d'informations sur les conteneurs, reportez-vous à la rubrique [Quota](/docs/containers/container_planning_org_ov.html#container_planning_quota) dans la documentation sur les conteneurs.
Pour modifier le quota alloué à une organisation, vous devez ouvrir un ticket de demande de service. Pour plus d'informations sur l'ouverture d'un ticket de demande de service, voir [Support client](/docs/support/index.html#contacting-support). 

## Gestion des domaines
{: #managedomains}

En tant que propriétaire de compte ou responsable de l'organisation, vous pouvez afficher le domaine de système et ajouter des données personnalisés pour les applications construites dans une organisation et ses espaces. Si vous êtes responsable de l'espace, l'onglet **Domaines** d'un espace est une liste en lecture seule des domaines affectés à l'espace.

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation que vous désirez éditer ou éditer les domaines.
3. Sélectionnez **Afficher les détails** pour cette organisation.
4. Cliquez sur **Editer l'organisation**.
5. Cliquez sur **DOMAINES**.

Si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS pour qu'il résolve votre domaine personnalisé, de telle sorte qu'il désigne le domaine de système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque {{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre application. Le domaine de système est toujours disponible dans un espace, et des domaines personnalisés peuvent également être alloués à un espace. Les applications créées dans un espace peuvent utiliser tout domaine répertorié pour cet espace. Pour plus d'informations sur la création et l'utilisation de domaines personnalisés, voir [Création et utilisation d'un domaine personnalisé](/docs/manageapps/updapps.html#domain).
