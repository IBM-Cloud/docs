---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des organisations et des espaces 
{: #orgsspacesusers}
*Dernière mise à jour : 16 mai 2016*

En tant que propriétaire de compte, vous pouvez gérer vos organisations en cliquant sur l'icône **Compte et support**
![Icône Compte et support](../admin/images/account_support.svg) &gt; page **Gérer les organisations**. Un
responsable de l'organisation peut également utiliser la page Gérer les organisations afin de gérer les organisations dont il est responsable.
{:shortdesc}

Les tâches de gestion sont les suivantes : 

* Création d'une organisation ou d'un espace 
* Changement de nom d'une organisation
* Suppression d'une organisation ou d'un espace existant 
* Affichage de la liste des membres d'équipe ajoutés à votre compte ou organisation 
* Gestion ou affichage du quota 
* Gestion des domaines personnalisés 

## Organisations
{: #orginfo}

Les organisations peuvent couvrir plusieurs régions et sont définies par les éléments suivants :


<dl>
<dt>Les membres d'équipe</dt>
<dd>Rôle disposant du droit de base dans les organisations et les espaces. Vous devez être affecté à une organisation pour pouvoir obtenir d'autres
droits dans les espaces de l'organisation. Pour des informations détaillées, voir
[Utilisateurs et rôles](users_roles.html#userrolesinfo).</dd>
<dt>Les domaines</dt>
<dd>Indiquez la route Internet allouée à l'organisation. Une route possède un sous-domaine et un domaine. En général, le sous-domaine est le nom de l'application. Un domaine peut être un domaine de système ou un
domaine personnalisé que vous avez enregistré pour votre application. Voir [Gestion des domaines personnalisés](orgs_spaces.html#managedomains).<br/>
<p>**Remarque** : si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS afin de résoudre votre domaine
personnalisé de sorte qu'il désigne le domaine de système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque
{{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre
application.</p></dd>
<dt>Le quota</dt>
<dd>Il représente les limites de ressources pour l'organisation, notamment le nombre de services et la quantité de mémoire pouvant être alloués à
l'organisation. Les quotas sont affectés lorsque les organisations sont
créées. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota. Avec les plans Paiement à la carte ou
Abonnement, vous pouvez ajuster votre quota pour les applications et les conteneurs Cloud Foundry au fur et à mesure que les besoins de votre organisation
changent. Voir [Gestion du quota](orgs_spaces.html#managequota).</dd>
</dl>

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser des organisations afin de permettre la collaboration entre les
membres d'équipe et
de faciliter le regroupement logique des ressources de projet comme suit :

<ul>
<li>Vous pouvez regrouper un ensemble d'espaces, d'applications, de services, de domaines, de routes et de membres d'équipe dans des
organisations.</li>
<li>Vous pouvez gérer l'accès aux espaces et aux organisations pour chaque utilisateur.</li>
</ul>

Lorsque vous créez une organisation, le nom de l'organisation doit être unique dans {{site.data.keyword.Bluemix_notm}}. Si le nom
d'organisation est déjà utilisé par un autre utilisateur d'environnement {{site.data.keyword.Bluemix_notm}} public, dédié ou local, vous devez
spécifier un autre nom.
Une fois que vous avez créé l'organisation, le droit *Responsable de l'organisation*, qui vous permet d'éditer le nom de l'organisation,
d'ajouter des membres d'équipe et de créer ou de supprimer des espaces dans l'organisation, vous est attribué automatiquement.

Vous devez prendre contact avec le [support {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} pour
supprimer une organisation. Lorsque vous demandez à l'équipe de support de supprimer une organisation, tous les espaces, toutes les applications et tous les
services dans l'organisation
sont supprimés.

Les [rôles utilisateur](users_roles.html#userrolesinfo) suivants peuvent être affectés aux membres d'équipe dans une organisation :


<ul>
<li>Responsable de l'organisation</li>
<li>Responsable de la facturation de l'organisation</li>
<li>Auditeur de l'organisation</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Espaces
{: #spaceinfo}

Dans une organisation, vous pouvez utiliser des espaces pour regrouper un ensemble d'applications, de services et de membres d'équipe. Les espaces
sont liés à une région spécifique dans {{site.data.keyword.Bluemix_notm}}.

Une fois que vous avez ajouté des membres d'équipe à une organisation, vous pouvez leur attribuer des droits pour les espaces. A l'instar des
organisations, les espaces possèdent également un ensemble de [rôles utilisateur](users_roles.html#userrolesinfo) associés à des droits
spécifiques pouvant être attribués aux membres d'équipe :


<ul>
<li>Responsable de l'espace</li>
<li>Développeur de l'espace</li>
<li>Auditeur de l'espace</li>
</ul>

**Remarque** : un membre d'équipe doit disposer d'au moins l'un des droits dans l'espace.

## Création d'organisations et d'espaces 
{: #createorg}

Seuls les propriétaires de compte de type Paiement à la carte peuvent créer une organisation. Vous pouvez créer une organisation comme suit :


1. Cliquez sur l'icône **Compte et support**
![Icône Compte et support](../admin/images/account_support.svg) &gt; page **Gérer les organisations**. 
2. Cliquez sur **Ajouter une nouvelle organisation**.
3. Entrez le nom de l'organisation. 
4. Cliquez sur **Ajouter**.

Vous pouvez créer des espaces dans votre organisation, par exemple un espace *dev* comme environnement de développement, un espace
*test* comme environnement de test et un espace *production* comme environnement de production. Ensuite, vous pouvez
associer vos applications à des espaces. Procédez comme suit pour créer un espace : 

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; page **Gérer les organisations**. 
2. Identifiez l'organisation à laquelle ajouter un espace, puis sélectionnez **Afficher les détails**.
3. Cliquez sur **Editer**.
4. Cliquez sur **Ajouter un espace**.
5. Entrez le nom de l'espace. 
6. Cliquez sur **Ajouter**.


## Changement de nom d'une organisation
{: #orgrename}

Procédez comme suit pour renommer votre organisation :

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; page **Gérer les organisations**. 
2. Identifiez l'organisation à éditer, puis sélectionnez **Afficher les détails**.
3. Sélectionnez **Editer**.
4. Sélectionnez **Editer** pour le titre de l'organisation. 
5. Entrez le nouveau nom d'organisation. 
6. Cliquez sur **Sauvegarder**.

## Suppression d'une organisation ou d'un espace existant 
{: #deleteorgs}

En tant que propriétaire de compte, vous pouvez prendre contact avec le
[support {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} pour supprimer une organisation.  

**Remarque** : les opérations de suppression sont irréversibles. Vous perdez toutes vos applications et tous les services qui sont
associés à l'organisation.

Vous pouvez supprimer un espace depuis la page **Gérer les organisations** : 

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; page **Gérer les organisations**. 
2. Identifiez l'organisation à éditer, puis sélectionnez **Afficher les détails**.
3. Identifiez l'espace à supprimer, puis sélectionnez **Editer**.
4. Cliquez sur **Supprimer un espace**.

## Liste des membres
{: #listmembers}

Procédez comme suit pour répertorier les membres d'une organisation spécifique :


1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; **Gérer les organisations**. 
2. Identifiez l'organisation dont vous voulez afficher les membres, puis cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer**.
4. Vous pouvez afficher les membres de votre organisation et leurs rôles dans l'onglet
**Utilisateurs**.

Procédez comme suit pour répertorier les membres d'un espace spécifique :


1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; page **Gérer les organisations**. 
2. Identifiez l'organisation dont vous voulez afficher les membres, puis cliquez sur **Afficher les détails**.
3. Identifiez l'espace dont vous voulez afficher les membres, puis cliquez sur **Editer**.
4. Les membres de votre espace et leurs rôles s'affichent dans l'onglet **Utilisateurs**. 

## Gestion du quota 
{: #managequota}

En tant que propriétaire de compte ou responsable de l'organisation, vous pouvez afficher le quota alloué et le quota utilisé pour votre organisation.
Le quota représente les limites de ressources pour l'organisation et est affecté lorsque l'organisation est créée. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota.

Pour afficher le quota de votre organisation, procédez comme suit : 

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; page **Gérer les organisations**. 
2. Identifiez l'organisation pour laquelle afficher le quota, puis cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer**.
4. Sélectionnez l'onglet **Quota**. 

Afin de mettre à jour le quota pour votre organisation, vous devez ouvrir un ticket de demande de service.
Pour plus d'informations sur l'ouverture d'un ticket de demande de service, voir [Support
client](../support/index.html#contacting-support). Pour plus d'informations sur le quota pour les conteneurs, voir
[Quota](../containers/container_creating_ov.html#container_quota) dans la documentation relative aux conteneurs. 

## Gestion des domaines 
{: #managedomains}

En tant que propriétaire de compte ou responsable de l'organisation, vous pouvez afficher le domaine de système et ajouter des
données personnalisés pour les applications construites dans une organisation et ses espaces. Si vous êtes responsable de l'espace, l'onglet
**Domaines** d'un espace est une liste en lecture seule des domaines affectés à l'espace.
 

1. Cliquez sur l'icône **Compte et support** ![Icône Compte et support](../admin/images/account_support.svg)
&gt; page **Gérer les organisations**. 
2. Identifiez l'organisation pour laquelle afficher ou éditer les domaines. 
3. Sélectionnez **Afficher les détails** pour cette organisation. 
4. Cliquez sur **Editer**.
5. Cliquez sur **Domaines**.

Si vous ajoutez un domaine personnalisé, vous devez configurer
votre serveur DNS pour qu'il résolve votre domaine personnalisé, de telle sorte qu'il désigne le domaine de système
{{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque
{{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre
application. Le domaine de système est toujours disponible dans un espace, et des domaines personnalisés peuvent également être alloués à un espace. Les
applications créées dans un espace peuvent utiliser tout domaine répertorié pour cet espace. Pour plus d'informations sur la création et l'utilisation de
domaines personnalisés, voir [Création et utilisation d'un domaine personnalisé](../manageapps/updapps.html#domain).
