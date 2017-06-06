---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Invitation d'utilisateurs
{: #iamuserinv}

Vous pouvez depuis un emplacement unique inviter des utilisateurs dans des services {{site.data.keyword.Bluemix_notm}}, des applications, et l'infrastructure {{site.data.keyword.Bluemix_notm}}. Pour inviter des utilisateurs et gérer des invitations en attente, vous devez être propriétaire du compte, responsable de l'organisation ou encore disposer des droits d'infrastructure permettant d'ajouter des utilisateurs. Vous pouvez inviter des utilisateurs, annuler des invitations, et renvoyer une invitation en attente à un utilisateur invité. Vous pouvez inviter un seul utilisateur ou bien, si vous accordez le même accès à tous les membres d'un groupe d'utilisateurs, inviter simultanément plusieurs utilisateurs.
{:shortdesc}

Pour inviter des utilisateurs ou gérer les invitations d'utilisateur sur votre compte, procédez comme suit : 

1. Dans la barre de menu, cliquez sur **Gérer** &gt; **Sécurité** &gt; **Identity & Access** &gt; **Utilisateurs**.La fenêtre Utilisateurs affiche une liste d'utilisateurs avec leur adresse électronique et leur statut actuel dans les comptes que vous gérez. 
2. Cliquez sur **Inviter des utilisateurs**. 
3. Spécifiez l'adresse électronique ou l'IBMid de l'utilisateur. Si vous octroyez le même accès à plusieurs utilisateurs, vous pouvez sélectionner **Inviter plusieurs utilisateurs** et entrer une liste d'utilisateurs à inviter. Séparez les entrées d'ID utilisateur par des virgules. 
4. Ajoutez une ou plusieurs options d'accès que vous gérez. Vous devez affecter au moins une option d'accès et configurer les paramètres pour l'utilisateur dans chaque option d'accès que vous lui affectez. Pour les options d'accès supplémentaires que vous n'ajoutez ou ne configurez pas, la valeur par défaut *Aucun accès* lui est affectée. L'une des options suivantes ou toutes les options d'accès suivantes peuvent s'afficher, selon celles que vous êtes autorisé à gérer : **Services avec l'offre Identity and Access activée**, **Accès Cloud Foundry**, **Accès Infrastructure**. Voir [Octroi d'un accès utilisateur](/docs/iam/assignaccess.html) pour plus d'informations. 

Si vous déterminez qu'un utilisateur n'a pas besoin d'un accès, vous pouvez annuler l'invitation de n'importe quel utilisateur dont l'état indique **En cours de traitement** ou **En attente** dans la colonne **Statut**. Si un utilisateur invité n'a pas reçu d'invitation, vous pouvez renvoyer l'invitation à n'importe quel utilisateur dont l'état indique **En attente**. 
