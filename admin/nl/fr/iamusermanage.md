---

copyright:

  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des comptes utilisateur et des accès
{: #iamusermanage}

Vous pouvez examiner et gérer les utilisateurs au niveau du compte ou de l'organisation en fonction des options d'accès que vous êtes habilité à gérer. En tant que propriétaire du compte, vous pouvez gérer les utilisateurs au niveau des options d'accès que vous administrez et pour lesquelles l'accès a été accordé à l'utilisateur, quel que soit le rôle, dans le compte actuel. Vous pouvez affecter, modifier ou supprimer l'accès d'utilisateurs dans n'importe quelle option d'accès que vous gérez. 
{:shortdesc}

Pour gérer des utilisateurs de votre compte, cliquez dans la barre de menu sur **Gérer** &gt; **Compte** &gt; **Utilisateurs**. La fenêtre Utilisateurs affiche une liste d'utilisateurs avec leur adresse électronique et leur statut actuel dans les comptes que vous gérez. Dans la fenêtre Utilisateurs, sélectionnez l'utilisateur que vous désirez gérer ou cliquez sur **Gérer un utilisateur** dans le menu **Actions**. Des tables de règles pour les options d'accès que vous pouvez gérer pour cet utilisateur s'affichent.

## Gestion des services de l'offre l'offre Identity and Access activée
{: #iammanidaccser}

Si un accès à un **service de l'offre l'offre Identity and Access activée** a été accordé à un utilisateur, des informations sur les règles en vigueur sont affichées dans la fenêtre Gérer un utilisateur.  Les informations affichées pour cet utilisateur ou ce groupe dépendent des règles qui ont été affectées. Si aucune règle n'a été affectée, un message vous demande si vous désirez en affecter une. Si des règles ont déjà été affectées, leur liste est affichée, ainsi que le rôle de l'utilisateur ou du groupe et la description des attributs de ressource pour chaque règle. Vous pouvez affecter des règles depuis la page Affecter des règles en cliquant sur **Affecter des règles de service**. L'option **Affecter des règles de service** est activée si vous êtes habilité à créer des règles. Vous pouvez gérer des règles existantes en cliquant sur la règle concernée dans la liste ou en cliquant sur **Editer la règle** sous **Actions** dans la ligne de la règle que vous désirez modifier.

## Gestion de l'accès aux services Cloud Foundry
{: #iammancfser}

Si un accès à **Cloud Foundry** a été accordé à l'utilisateur, les organisations et les espaces auxquels est affecté l'utilisateur sont indiqués dans la fenêtre Gérer un utilisateur. Vous pouvez retirer d'une organisation l'utilisateur ou changer le rôle qui lui est attribué dans une organisation ou un espace. Vous pouvez ajouter un utilisateur à une autre organisation en cliquant sur **Affecter une organisation** si vous gérez une organisation dont n'est pas encore membre l'utilisateur. Vous pouvez gérer les rôles dans une organisation ou un espace existants en cliquant sur **Editer un rôle d'espace** ou sur **Editer un rôle d'organisation** dans la ligne du rôle que vous désirez modifier.

## Gestion des règles
{: #iamusermanpol}

Vous pouvez affecter et gérer des règles pour un utilisateur ayant accès aux **Services avec l'offre Identity and Access activée**. Une règle affecte à un utilisateur un rôle ou plusieurs rôles sur un ensemble de ressources en utilisant une combinaison d'attributs pour définir l'ensemble de ressources applicable.

Lorsque vous affectez une règle à un utilisateur, vous devez d'abord spécifier le service à affecter. La liste **Services** permet de sélectionner des services spécifiques, et comporte également une option pour affecter tous les services disponibles. Vous devez également sélectionner un rôle, ou plusieurs, à lui affecter.

Des options de configuration supplémentaires sont disponibles, en fonction du service sélectionné. Vous pouvez sélectionner un service pour examiner les options pour ce service.

Vous pouvez restreindre la liste des options de service affichées. Cliquez sur **Spécifier un contexte de service facultatif** pour sélectionner des options supplémentaires, comme la région et des instances de service.  Vous ne voudrez peut-être pas spécifier toutes les options affichées, mais vous pouvez choisir lesquelles configurer.

Vous pouvez affecter et gérer des règles si le rôle approprié vous a été attribué. Le tableau suivant décrit les tâches de gestion de règles et le rôle requis pour chacune.


{: #iamui_table1}

| Action | Rôle requis |
|----------|---------|
| Créer une règle sur un compte | Administrateur du compte |
| Créer une règle sur tous les services d'un compte | Administrateur du compte |
| Créer une règle sur toutes les instances de service d'un compte | Administrateur du compte |
| Créer une règle sur un service dans un compte | Administrateur du compte ou administrateur du service dans le compte |
| Créer une instance de service | Administrateur ou éditeur du compte ou administrateur ou éditeur du service dans le compte |
| Créer une règle sur une instance de service | Administrateur du compte ou administrateur du servie dans le compte ou administrateur de l'instance de service |
{: caption="Tableau 1. Tâches d'administration pour la gestion des règles **Services avec l'offre Identity and Access activée**" caption-side="top"}

## Affectation et gestion des rôles
{: #iamusermanrol}

Les rôles sont un assortiment d'actions ; les actions mappées à ces rôles sont spécifiques au service concerné. 
Vu que les actions sont regroupées en rôles, vous pouvez utiliser un petit ensemble de rôles prédéfinis pour couvrir toutes les actions sur n'importe quel service et ressource. Par exemple, si vous avez besoin d'un administrateur de machines virtuelles, du stockage et de l'opération en réseau, vous pouvez désigner l'utilisateur comme administrateur de ces trois ressources en modifiant la cible de la règle. Vous configureriez alors la règle en incluant l'administrateur des machines virtuelles, l'administrateur du stockage et l'administrateur de l'opération réseau.

Les ressources ne sont pas intégrées dans les rôles, par conséquent de nouveaux noms de rôles ne sont pas créés pour chaque type de ressource introduit dans le système. Par exemple, vous n'avez pas besoin d'un rôle d'administrateur de machine virtuelle, d'un rôle d'administrateur du stockage et d'un rôle d'administrateur réseau pour gérer les ressources de machines virtuelles, de stockage et réseau.

En complément des descriptions des rôles disponibles dans l'interface utilisateur, le tableau suivant fournit des exemples de diverses tâches que les utilisateurs affectés à chaque rôle peuvent réaliser.

{: #iamui_table2}

| Rôle | Description d'actions | Exemples d'actions|
|:-----------------|:-----------------|:-----------------|
| Visualiseur | Exécute des actions qui ne modifient pas l'état ; actions en lecture seule | <ul><li>Recensement des unités</li><li>Lecture d'objet de stockage</li><li>Exécution de requêtes</li><li>Exécution de recherches</li></ul>|
| Editeur | Exécute des actions qui modifient l'état et créent ou suppriment des sous-ressources |<ul><li>Création ou suppression de machines virtuelles</li><li>Rattachement de stockage</li><li>Réamorçage</li><li>Démarrage ou arrêt</li><li>Attribution d'un nouveau nom</li></ul> |
| Administrateur | Peut effectuer toutes les actions, notamment de gestion du contrôle d'accès |<ul><li>Invitation d'utilisateurs</li><li>Création ou suppression de machines virtuelles</li><li>Mise à jour des règles d'accès utilisateur</li><li>Recensement des unités</li><li>Rattachement de stockage</li><li>Réamorçage</li><li>Démarrage ou arrêt</li><li>Attribution d'un nouveau nom</li><li>Sauvegarde et restauration</li></ul>|
{: caption="Tableau 2. Tâches d'administration pour la gestion des règles **Services avec l'offre Identity and Access activée**" caption-side="top"}

Pour plus d'informations spécifiques sur les rôles des utilisateurs jouissant d'un accès à Cloud Foundry, voir [Rôles utilisateur](/docs/admin/users_roles.html#userrolesinfo).

Lorsque vous ajoutez des utilisateurs, vous devez sélectionner au moins un rôle et vous pouvez lui en ajouter plusieurs. Lorsque vous sélectionnez un rôle, sa définition est affichée pour vous aider à déterminer le rôle ou les rôles à affecter à l'utilisateur.  Les rôles que vous affectez ont des options d'accès différentes mais concernent les mêmes attributs de ressource que vous spécifiez.

Si vous avez sélectionné le service **Cloud Foundry**, les rôles que vous affectez sont associés aux organisations et aux espaces que vous sélectionnez.
