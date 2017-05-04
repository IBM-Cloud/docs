---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Invitation d'utilisateurs, affectation et gestion d'accès
{: #iamuserinv}

Vous pouvez depuis un emplacement unique inviter des utilisateurs dans des services {{site.data.keyword.Bluemix_notm}}, des applications, et l'infrastructure {{site.data.keyword.Bluemix_notm}} . Vous affectez un accès aux utilisateurs lorsque vous les invitez, leur affectez un rôle, des règles, les comptes ou les organisations (ou les deux) auxquels ils peuvent accéder. Vous pouvez inviter et accorder un accès à des utilisateurs à travers le compte ou l'organisation en fonction des options d'accès que vous êtes habilité à gérer. En tant que propriétaire du compte, vous pouvez affecter des options d'accès au compte à un utilisateur lorsque vous et l'utilisateur êtes tous deux membres du compte, sans considération du rôle.
{:shortdesc}

Pour inviter des utilisateurs ou gérer les invitations d'utilisateurs dans votre compte, cliquez dans la barre de menu sur **Gérer** &gt; **Compte** &gt; **Utilisateurs**. La fenêtre Utilisateurs affiche une liste d'utilisateurs avec leur adresse électronique et leur statut actuel dans les comptes que vous gérez. 

Pour inviter des utilisateurs et gérer des invitations en attente, vous devez être propriétaire du compte, responsable de l'organisation ou encore être autorisé dans l'infrastructure à ajouter des utilisateurs.  Vous pouvez inviter des utilisateurs, annuler des invitations, et renvoyer une invitation en attente à un utilisateur invité. Vous pouvez inviter un seul utilisateur ou bien, si vous accordez le même accès à tous les membres d'un groupe d'utilisateurs, inviter simultanément plusieurs utilisateurs.

Pour inviter des utilisateurs, cliquez sur **Inviter des utilisateurs**, spécifiez l'adresse électronique ou l'IBMid de l'utilisateur, puis ajoutez-les à l'une ou plusieurs des options d'accès que vous gérez. Vous devez affecter au moins une option d'accès et configurer les paramètres pour l'utilisateur dans chaque option d'accès que vous lui affectez. Pour les options d'accès supplémentaires que vous n'ajoutez ou ne configurez pas, la valeur par défaut *Aucun accès* lui est affectée. Une ou toutes les options d'accès suivantes peuvent être affichées, selon celles que vous êtes autorisé à gérer :

**Services avec l'offre Identity and Access activée**
Sélectionnez cette option pour affecter les services, les régions, les instances de service, et les rôles pour les utilisateurs que vous invitez.
**Remarque **: si vous sélectionnez l'option **Accorder automatiquement des droits d'accès lorsque de nouveaux services sont ajoutés**, vous n'êtes pas interrogé si chaque nouveau service doit être désélectionné pour cet utilisateur {{site.data.keyword.Bluemix_notm}} quand des services sont ajoutés plus tard.

**Accès Cloud Foundry**
Sélectionnez cette option pour affecter cet accès aux services, régions, espaces, et rôles dans l'espace pour les utilisateurs que vous invitez. Voir [Rôles utilisateur](/docs/admin/users_roles.html#userrolesinfo) pour plus d'informations spécifiques à ces paramètres. Vous pouvez ajouter plusieurs rôles, un à la fois.

**Accès Infrastructure**
Affectez à l'utilisateur l'une des autorisations d'accès suivantes à l'infrastructure : 
<dl>
<dt>Affichage uniquement</dt>
<dd>Les utilisateurs avec cette autorisation peuvent uniquement afficher les éléments dans le système.</dd>
<dt>Utilisateur de base</dt>
<dd>Les utilisateurs avec cette autorisation peuvent effectuer des actions élémentaires dans le système, comme l'ajout d'un ticket et la gestion de périphériques.</dd>
<dt>Superutilisateur</dt>
<dd>Les utilisateurs avec cette autorisation peuvent réaliser toutes les actions disponibles dans le système.</dd>
</dl>
**Remarque **: les autorisations concrètes qui sont affectées sont limitées automatiquement au sous-ensemble d'autorisations dont vous bénéficiez.
Si vous octroyez le même accès à plusieurs utilisateurs, vous pouvez sélectionner **Inviter plusieurs utilisateurs** et entrer une liste d'utilisateurs à inviter. Séparez les entrées d'ID utilisateur par des virgules.  

Si vous déterminez qu'un utilisateur n'a pas besoin d'un accès, vous pouvez aussi annuler l'invitation de n'importe quel utilisateur dont l'état indique **En cours de traitement** ou **En attente** dans la colonne **Statut**. Si un utilisateur invité n'a pas reçu l'invitation, vous pouvez également renvoyer l'invitation à n'importe quel utilisateur dont l'état indique **En attente**. Ces options sont disponibles depuis le menu **Actions** dans la fenêtre Utilisateurs pour les utilisateurs avec l'état approprié.

Pour des informations spécifiques sur la configuration d'un accès pour les utilisateurs, notamment sur les rôles et les règles, voir [Gestion des comptes utilisateurs et des accès](/docs/admin/iamusermanage.html).
