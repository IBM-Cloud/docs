---

copyright:

  years: 2015, 2016
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Rôles utilisateur et droits 
{: #userroles}

Vous pouvez gérer les utilisateurs dans les services de plateforme et d'infrastructure {{site.data.keyword.Bluemix_notm}} depuis la page **Utilisateurs** de votre compte. Celle-ci comporte également un lien vers la page Répertoire d'équipe, si vous ne voulez gérer que l'accès Cloud Foundry des utilisateurs de plateforme aux organisations et aux espaces. Toutefois, il n'est pas nécessaire de quitter la page Utilisateurs pour gérer l'accès Cloud Foundry.
{:shortdesc}

Pour accéder à la page Utilisateurs, depuis le menu {{site.data.keyword.Bluemix_notm}}, cliquez sur **Gérer** &gt; **Compte** &gt; **Utilisateurs**. Les propriétaires de compte peuvent effectuer toutes les opérations sur les organisations et les espaces, notamment gérer les utilisateurs et les rôles qui leur sont affectés. Les responsables de l'organisation et les responsables de l'espace ont également le droit de gérer les rôles.  

Si, en tant qu'utilisateur, vous avez été ajouté au compte d'une autre personne et voulez consulter les rôles et les droits qui vous sont affectés, sélectionnez **Gérer** &gt; **Sécurité** &gt; **Identity & Access** &gt; **Utilisateurs**, et cliquez sur votre nom. 

## Rôles de compte 
{: #userrolesinfo}

Au niveau du compte, deux rôles permettent l'accès à différentes fonctions de gestion des comptes :

| Rôle de compte | Droits |
|----------------|---------|
|Propriétaire | Un propriétaire de compte peut accéder à son profil, au répertoire d'équipe, aux informations de facturation, aux notifications relatives aux dépenses et au tableau de bord de l'utilisation. Depuis la page Répertoire d'équipe ou Utilisateurs, le propriétaire peut inviter de nouveaux membres d'équipe et ajuster les rôles. Il peut également ajouter des offres promotionnelles, définir ou changer la limite de facturation, définir l'accès aux services et gérer les organisations et les espaces. |
|Membre | Un membre peut accéder à son profil, au répertoire d'équipe, aux crédits du compte et aux limites de facturation dans l'en-tête {{site.data.keyword.Bluemix_notm}}. Toutefois, dans la page Répertoire d'équipe, un membre ne peut afficher que les membres d'équipe existants sur le compte. |
{:caption="Tableau 1. Rôles de compte et droits" caption-side="top"}

Tous les nouveaux utilisateurs sont ajoutés en tant que membre du compte. Vous pouvez affecter des rôles d'organisation et d'espace aux invités afin
d'activer des vues et des droits spécifiques dans {{site.data.keyword.Bluemix_notm}}. Les nouveaux membres d'équipe ajoutés à une organisation, sauf dans un
environnement local ou dédié, possèdent le rôle Auditeur de l'organisation par défaut. Pour un espace spécifique, vous pouvez choisir d'affecter le rôle Développeur ou Auditeur aux invités. Une fois que vos invités ont accepté l'invitation et ont rejoint {{site.data.keyword.Bluemix_notm}}, vous pouvez éditer leurs rôles dans la page Utilisateurs ou Répertoire d'équipe. 

## Rôles Cloud Foundry
{: #cfroles}

Les rôles Cloud Foundry incluent les droits d'accès pour les organisations et les espaces définis sur le compte. Les rôles suivants peuvent être affectés au niveau de l'organisation :

| Rôle d'organisation | Droits |
|-------------------|-------------|
|Responsable | Un responsable de l'organisation peut créer, éditer ou supprimer des espaces dans l'organisation, afficher l'utilisation et le quota de l'organisation, inviter des membres d'équipe dans l'organisation, définir quels sont les membres qui ont accès à l'organisation ainsi que les rôles de ces membres dans l'organisation, et gérer des domaines personnalisés pour l'organisation. |
|Responsable de la facturation | Un responsable de la facturation peut afficher des informations sur l'utilisation des contextes d'exécution et des services pour l'organisation dans la page Tableau de bord de l'utilisation.  |
|Auditeur | Un auditeur de l'organisation peut afficher le contenu des applications et des services dans l'organisation. Il peut également afficher les utilisateurs dans l'organisation et les rôles qui leur sont affectés, ainsi que le quota pour l'organisation. Ce rôle est affecté à tous les invités par défaut, sauf dans un environnement
local ou dédié. |
{:caption="Tableau 2. Rôles d'organisation et droits" caption-side="top"}

Les rôles suivants peuvent être affectés au niveau de l'espace :

| Rôle d'espace | Droits |
|------------|-------------|
|Responsable | Un responsable de l'espace peut ajouter des utilisateurs existants et gérer les rôles dans l'espace. Il peut également afficher le nombre d'instances, les liaisons de service et l'utilisation des ressources pour chaque application dans l'espace. |
|Développeur | Un développeur de l'espace peut créer, supprimer et gérer des applications et des services dans l'espace. Certaines tâches de gestion impliquent le déploiement d'applications, le démarrage ou l'arrêt d'applications, le changement de nom d'une application, la suppression d'une application, le changement de nom d'un espace, la liaison d'un service ou l'annulation de la liaison d'un service à une application ainsi que l'affichage du nombre d'instances, des liaisons de service et de l'utilisation des ressources pour chaque application dans l'espace. De plus, le développeur de l'espace peut associer une adresse URL interne ou externe à une application dans l'espace.   |
|Auditeur | Un auditeur de l'espace dispose de l'accès en lecture à toutes les informations sur l'espace, telles que le nombre d'instances, les liaisons de service et l'utilisation des ressources pour chaque application dans l'espace. |
{:caption="Tableau 3. Rôles d'espace et droits" caption-side="top"}

**Remarque** : les utilisateurs qui possèdent le rôle de responsable ou de développeur de l'espace peuvent accéder à la
variable
d'environnement VCAP_SERVICES. Toutefois, un utilisateur possédant le rôle d'auditeur ne peut pas y accéder.

## Règles de gestion de l'identité et de l'accès et rôles 
{: #iamusermanpol}

Les propriétaires de compte sont affectés automatiquement au rôle d'administrateur des accès au compte pour la gestion de l'identité et de l'accès, qui permet d'affecter et de gérer des règles de service. Ce type de contrôle d'accès permet l'affectation de règles par service ou instance de service afin d'accorder des niveaux d'accès pour la gestion des ressources et des utilisateurs dans le contexte affecté. 

### Règles de service

Une règle affecte à un utilisateur un rôle ou plusieurs rôles sur un ensemble de ressources en utilisant une combinaison d'attributs pour définir l'ensemble de ressources applicable. Lorsque vous affectez une règle à un utilisateur, vous devez d'abord spécifier le service à affecter ; il existe notamment une option permettant d'affecter tous les services disponibles. Ensuite, vous pouvez aussi sélectionner un ou plusieurs rôles à affecter. D'autres options de configuration peuvent être disponibles, selon le service que vous sélectionnez. 

Vous pouvez affecter et gérer des règles si le rôle approprié vous a été attribué. Le tableau ci-dessous décrit les tâches de gestion de règles et le rôle requis pour chacune.

{: #iamui_table1}

| Action | Rôle requis |
|----------|---------|
| Créer une règle sur un compte | Administrateur des accès au compte  |
| Créer une règle sur tous les services d'un compte | Administrateur des accès au compte  |
| Créer une règle sur toutes les instances de service d'un compte | Administrateur des accès au compte  |
| Créer une règle sur un service dans un compte | Administrateur des accès au compte ou administrateur du service sur le compte |
| Créer une instance de service | Administrateur des accès au compte ou administrateur ou éditeur du service sur le compte |
| Créer une règle sur une instance de service | Administrateur des accès au compte ou administrateur du service sur le compte ou administrateur dans l'instance de service |
{: caption="Tableau 4. Tâches d'administration pour la gestion des règles de service avec l'offre Identity and Access activée " caption-side="top"}

### Rôles de règle de service 
{: #iamusermanrol}

Les rôles sont un assortiment d'actions ; les actions mappées à ces rôles sont spécifiques au service concerné. Voir la documentation du service sélectionné pour des détails supplémentaires sur les types d'action que chaque rôle autorise. 

En complément des descriptions des rôles disponibles dans la console, le tableau ci-dessous présente des exemples de diverses tâches que les utilisateurs affectés à chaque rôle peuvent effectuer, selon le service sélectionné.  

{: #iamui_table2}

| Rôle | Description d'actions | Exemples d'actions|
|:-----------------|:-----------------|:-----------------|
| Visualiseur | Exécute des actions qui ne modifient pas l'état ; actions en lecture seule | <ul><li>Recensement des unités</li><li>Lecture d'objet de stockage</li><li>Exécution de requêtes</li><li>Exécution de recherches</li></ul>|
| Editeur | Exécute des actions qui modifient l'état et créent ou suppriment des sous-ressources |<ul><li>Création ou suppression de machines virtuelles</li><li>Rattachement de stockage</li><li>Réamorçage</li><li>Démarrage ou arrêt</li><li>Attribution d'un nouveau nom</li></ul> |
| Administrateur | Peut effectuer toutes les actions, notamment de gestion du contrôle d'accès |<ul><li>Invitation d'utilisateurs</li><li>Création ou suppression de machines virtuelles</li><li>Mise à jour des règles d'accès utilisateur</li><li>Recensement des unités</li><li>Rattachement de stockage</li><li>Réamorçage</li><li>Démarrage ou arrêt</li><li>Attribution d'un nouveau nom</li><li>Sauvegarde et restauration</li></ul>|
{: caption="Tableau 5. Tâches d'administration pour la gestion des règles de service avec l'offre Identity and Access activée " caption-side="top"}

## Droits relatifs à l'infrastructure 
{: #infrapermissions}

Si vous pouvez affecter des rôles d'infrastructure, vous pouvez définir les droits suivants pour l'utilisateur :  

| Droits relatifs à l'infrastructure  | Description des actions |
|---------------------------|------------------------|
|Affichage uniquement | Les utilisateurs avec cette autorisation peuvent uniquement afficher les éléments dans le système.|
|Utilisateur de base | Les utilisateurs avec cette autorisation peuvent effectuer des actions élémentaires dans le système, comme l'ajout d'un ticket et la gestion de périphériques. |
|Superutilisateur | Les utilisateurs avec cette autorisation peuvent effectuer toutes les actions disponibles dans le système. |
{:caption="Tableau 6. Droits relatifs à l'infrastructure" caption-side="top"}

