---

copyright:

  years: 2015, 2017

lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des utilisateurs et de l'accès 
{: #iamusermanage}

Vous pouvez afficher et gérer les utilisateurs au niveau du compte ou de l'organisation en fonction des options d'accès que vous êtes habilité à gérer. En tant que propriétaire du compte, vous pouvez gérer les utilisateurs au niveau des options d'accès que vous administrez et pour lesquelles l'accès a été accordé à l'utilisateur sur le compte en cours. {:shortdesc}

Pour gérer des utilisateurs sur votre compte, procédez comme suit : 

1. Dans la barre de menu, cliquez sur **Gérer** &gt; **Compte** &gt; **Utilisateurs**. La fenêtre Utilisateurs affiche une liste d'utilisateurs avec leur adresse électronique et leur statut en cours sur les comptes que vous gérez. 
2. Sélectionnez le nom d'utilisateur ou cliquez sur **Gérer un utilisateur** dans le menu **Actions**.  
3. Ensuite, selon l'accès que vous pouvez gérer, mettez à jour l'accès pour l'utilisateur dans les sections Règles de service ou Rôles Cloud Foundry, ou cliquez sur le lien d'accès à la page Affecter l'accès Infrastructure. 

Lisez les sections suivantes pour des informations supplémentaires sur la gestion de chaque type d'accès et pour des informations sur l'utilisation du répertoire d'équipe. 

Si vous devez vérifier l'accès qui vous a été affecté sur un compte auquel vous avez ajouté, procédez comme suit :

1. Dans la barre de menu, cliquez sur **Gérer** &gt; **Sécurité** &gt; **Identity & Access** &gt; **Utilisateurs**. 
2. Sélectionnez votre nom.  
3. Passez en revue les rôles qui vous ont été affectés. 

Si vous devez changer votre rôle ou votre règle de service, prenez contact avec le responsable de l'organisation ou le propriétaire du compte pour qu'il mette à jour le rôle ou avec l'administrateur du service ou de l'instance de service pour qu'il mette à jour la règle de service. 

## Accès Cloud Foundry
{: #iammancfser}

Pour pouvoir gérer l'accès à des organisations et des espaces de compte, vous devez être le propriétaire du compte, le responsable de l'organisation ou le responsable de l'espace :

1. Dans la barre de menu, cliquez sur **Gérer** &gt; **Sécurité** &gt; **Identity & Access** &gt; **Utilisateurs**. 
2. Sélectionnez le nom d'utilisateur pour lequel éditer les rôles. 
3. Depuis le menu **Actions** de la section Cloud Foundry, vous pouvez : 

  * Retirer l'utilisateur de l'organisation 
  * Editer le rôle d'organisation 
  * Editer le rôle d'espace 

Vous pouvez aussi ajouter un utilisateur à une autre organisation en cliquant sur **Affecter une organisation**, si vous êtes le responsable d'une organisation dont l'utilisateur n'est pas encore membre.  


## Services avec l'offre Identity and Access activée 
{: #iammanidaccser}

Pour pouvoir gérer les règles de service ou affecter de nouvelles règles de service à des utilisateurs, vous devez être l'administrateur des accès au compte ou l'administrateur désigné pour le service ou l'instance de service spécifique. 

1. Dans la barre de menu, cliquez sur **Gérer** &gt; **Sécurité** &gt; **Identity & Access** &gt; **Utilisateurs**. 
2. Sélectionnez le nom d'utilisateur auquel affecter des règles de service. 
3. Sélectionnez **Affecter des règles de service** pour créer une règle de service ou depuis le menu **Actions** de la section Règles de service : 
  
  * Editez la règle
  * Retirez la règle 

Pour plus d'informations sur les règles de service et les rôles, voir [Règles de gestion de l'identité et de l'accès et rôles](/docs/iam/users_roles.html#iamusermanpol).

## Services d'infrastructure 

Si vous pouvez affecter des droits d'infrastructure, vous pouvez définir les rôles suivants pour l'utilisateur : Affichage uniquement, Utilisateur de base ou Superutilisateur. Cliquez sur le lien **Affecter l'accès Infrastructure** pour mettre à jour des droits ou en affecter de nouveaux. 

Pour plus d'informations sur les droits, voir [Droits relatifs à l'infrastructure](/docs/iam/users_roles.html#infrapermissions).

## Gestion des rôles Cloud Foundry dans le répertoire d'équipe 
{: #editinguserroles}

Dans la page Répertoire d'équipe, les propriétaires de compte peuvent gérer les utilisateurs de plateforme uniquement. Toutefois, si vous pouvez sélectionner la page **Gérer** &gt; **Compte** &gt; **Utilisateurs**, vous pouvez gérer tous les utilisateurs des services de plateforme et d'infrastructure à un seul endroit. 

Les responsables de l'organisation peuvent éditer les rôles d'organisation et d'espace pour les utilisateurs existants dans la page Répertoire d'équipe. 

1. Localisez et sélectionnez le membre d'équipe dont vous voulez éditer les rôles.
2. Cliquez sur **Afficher les rôles**.
3. Sélectionnez ou désélectionnez les rôles d'espace afin de modifier l'accès du membre d'équipe aux espaces.
4. Cliquez sur **Sauvegarder**.

Les responsables de l'espace peuvent éditer les rôles des membres d'équipe dans leur espace.

1. Localisez et sélectionnez le membre d'équipe dont vous désirez éditer les rôles.
2. Cliquez sur **Afficher les rôles**.
3. Cliquez sur **Afficher les espaces**.
4. Sélectionnez ou désélectionnez l'option de rôle d'espace pour le rôle à ajouter ou retirer pour le membre d'équipe.
5. Ensuite, cliquez sur **Sauvegarder**.
