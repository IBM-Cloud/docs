---

copyright:

  years: 2015, 2016
lastupdated: "2017-03-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des accès utilisateur aux services Cloud Foundry et des rôles dans la page Répertoire d'équipe
{: #userroles}

Vous pouvez gérer les utilisateurs de la plateforme auxquels a été alloué un accès aux services Cloud Foundry depuis la page Répertoire d'équipe de votre compte. Vous pouvez gérer les membres d'équipe existants et leurs rôles dans votre organisation et ses espaces.
{:shortdesc}

Vous pouvez accéder au Répertoire d'équipe de votre compte depuis un lien situé en haut de la page Nouveaux utilisateurs. Pour accéder à la page Utilisateurs, depuis le menu {{site.data.keyword.Bluemix_notm}}, cliquez sur **Gérer** &gt; **Compte** &gt; **Utilisateurs**.

Les propriétaires de compte peuvent effectuer toutes les opérations sur les organisations et les espaces, notamment gérer les membres d'équipe et les rôles qui leur sont affectés. Les autorisations d'accès des responsables de l'organisation leur permettent de gérer les rôles. Un responsable de l'espace
peut utiliser la page **Gérer les organisations** pour ajouter des membres de compte existants à l'espace et ajuster leurs rôles. Lisez
les informations ci-après pour en savoir plus sur les rôles.

## Rôles utilisateur
{: #userrolesinfo}

Au niveau du compte, deux rôles permettent l'accès à différentes fonctions de gestion des comptes :

| Rôle de compte | Droits |
|----------------|---------|
|Propriétaire | Un propriétaire de compte peut accéder à son profil, au répertoire d'équipe, aux informations de facturation, aux notifications relatives aux dépenses et au tableau de bord de l'utilisation. Dans la page Répertoire d'équipe, le propriétaire peut inviter de nouveaux membres d'équipe et ajuster les rôles. Il peut également ajouter des offres promotionnelles, définir ou changer la limite de facturation, définir l'accès aux services et gérer les organisations et les espaces. |
|Membre | Un membre peut accéder à son profil, au répertoire d'équipe, aux crédits du compte et aux limites de facturation dans l'en-tête {{site.data.keyword.Bluemix_notm}}. Toutefois, dans la page Répertoire d'équipe, un membre ne peut afficher que les membres d'équipe existants sur le compte. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

Les nouveaux membres d'équipe sont ajoutés en tant que membre du compte. Vous pouvez affecter des rôles d'organisation et d'espace aux invités afin
d'activer des vues et des droits spécifiques dans {{site.data.keyword.Bluemix_notm}}. Les nouveaux membres d'équipe ajoutés à une organisation, sauf dans un
environnement local ou dédié, possèdent le rôle Auditeur de l'organisation par défaut. Pour un espace spécifique, vous pouvez choisir d'affecter le rôle Développeur ou Auditeur aux invités. Une fois que vos invités ont accepté l'invitation et ont rejoint {{site.data.keyword.Bluemix_notm}}, vous pouvez éditer leurs rôles depuis la page Répertoire d'équipe.

Les rôles suivants peuvent être affectés au niveau de l'organisation :

| Rôle d'organisation | Droits |
|-------------------|-------------|
|Responsable | Un responsable de l'organisation peut créer, éditer ou supprimer des espaces dans l'organisation, afficher l'utilisation et le quota de l'organisation, inviter des membres d'équipe dans l'organisation, définir quels sont les membres qui ont accès à l'organisation ainsi que les rôles de ces membres dans l'organisation, et gérer des domaines personnalisés pour l'organisation. |
|Responsable de la facturation | Un responsable de la facturation peut afficher des informations sur l'utilisation des contextes d'exécution et des services pour l'organisation dans la page Tableau de bord de l'utilisation.  |
|Auditeur | Un auditeur de l'organisation peut afficher le contenu des applications et des services dans l'organisation. Il peut également afficher les membres d'équipe dans l'organisation et les rôles qui leur sont affectés, ainsi que le quota pour l'organisation. Ce rôle est affecté à tous les invités par défaut, sauf dans un environnement
local ou dédié. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

Les rôles suivants peuvent être affectés au niveau de l'espace :

| Rôle d'espace | Droits |
|------------|-------------|
|Responsable | Un responsable de l'espace peut ajouter des membres d'équipe existants et gérer les rôles dans l'espace. Il peut également afficher le nombre d'instances, les liaisons de service et l'utilisation des ressources pour chaque application dans l'espace. |
|Développeur | Un développeur de l'espace peut créer, supprimer et gérer des applications et des services dans l'espace. Certaines tâches de gestion impliquent le déploiement d'applications, le démarrage ou l'arrêt d'applications, le changement de nom d'une application, la suppression d'une application, le changement de nom d'un espace, la liaison d'un service ou l'annulation de la liaison d'un service à une application ainsi que l'affichage du nombre d'instances, des liaisons de service et de l'utilisation des ressources pour chaque application dans l'espace. De plus, le développeur de l'espace peut associer une adresse URL interne ou externe à une application dans l'espace.   |
|Auditeur | Un auditeur de l'espace dispose de l'accès en lecture à toutes les informations sur l'espace, telles que le nombre d'instances, les liaisons de service et l'utilisation des ressources pour chaque application dans l'espace. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Remarque** : les membres d'équipe qui possèdent le rôle de responsable ou de développeur de l'espace peuvent accéder à la
variable
d'environnement VCAP_SERVICES. Toutefois, un membre d'équipe possédant le rôle d'auditeur ne peut pas y accéder.

## Edition des rôles
{: #editinguserroles}

Les propriétaires de compte et les responsables de l'organisation peuvent modifier les rôles dans l'organisation et les espaces des membres d'équipe existants depuis la page Répertoire d'équipe.

1. Localisez et sélectionnez le membre d'équipe dont vous désirez éditer les rôles.
2. Cliquez sur **Afficher les rôles**.
3. Sélectionnez ou désélectionner les rôles d'espace afin de modifier l'accès du membre d'équipe aux espaces.
4. Cliquez sur **Sauvegarder**.

Les responsables de l'espace peuvent éditer les rôles des membres d'équipe dans leur espace.

1. Localisez et sélectionnez le membre d'équipe dont vous désirez éditer les rôles.
2. Cliquez sur **Afficher les rôles**.
3. Cliquez sur **Afficher les espaces**.
4. Sélectionnez ou désélectionnez l'option de rôle d'espace pour le rôle à ajouter ou retirer pour le membre d'équipe.
5. Ensuite, cliquez sur **Sauvegarder**.

## Invitation de membres d'équipe
{: #inviteteammembers}

Vous pouvez ajouter un utilisateur depuis la fenêtre Répertoire d'équipe si son ID utilisateur n'est pas un compte lié et que vous êtes le propriétaire du compte ou un gestionnaire de l'organisation. Lorsque vous ajoutez de nouveaux membres d'équipe, le
rôle Auditeur leur est affecté automatiquement, sauf dans un environnement
local ou dédié. Vous pouvez changer les rôles
ultérieurement dans la page Répertoire d'équipe. Pour inviter un membre d'équipe, procédez comme suit :

<ol>
<li>Cliquez sur **Inviter un utilisateur**.</li>
<li>Entrez l'adresse électronique de l'utilisateur que vous invitez.</li>
<li>Sélectionnez le rôle à lui affecter dans l'organisation.</li>
<li>Sélectionnez le rôle à lui affecter dans l'espace ou les espaces de l'organisation.</li>
<li>Sélectionnez l'option permettant de confirmer que vous prenez en charge tous les frais liés au compte.</li>
<li>Cliquez sur **Inviter**.</li>
</ol>

L'utilisateur est ajouté à liste des membres d'équipe affichée pour le compte.

## Retrait de membres d'équipe
{: #removingteammembers}

Si l'utilisateur a été ajouté depuis le Répertoire d'équipe et qu'il ne s'agit pas d'un compte lié, les propriétaires du compte et les gestionnaires de l'organisation peuvent retirer des membres de l'équipe depuis la page Répertoire d'équipe. Pour retirer un membre d'équipe, procédez comme suit :

1. Localisez l'utilisateur que vous comptez retirer et cliquez sur l'icône **Retirer l'utilisateur** ![Icône Retirer](../icons/icon_remove_teamuser.svg).
2. Cliquez sur **Retirer** pour confirmer que vous désirez retirer du compte l'utilisateur spécifié.

L'utilisateur est retiré de la liste affichée des membres d'équipe pour le compte.
