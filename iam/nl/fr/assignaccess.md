---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Octroi d'un accès utilisateur 
{: #assignaccess}

Vous accordez un accès aux utilisateurs lorsque vous les invitez, en leur affectant des rôles, des règles, ainsi que les comptes ou les organisations (ou les deux) auxquels ils peuvent accéder. Vous pouvez inviter des utilisateurs et leur accorder un accès dans les instances de compte, d'organisation, d'espace et de service, en fonction des options d'accès que vous êtes habilité à gérer. En tant que propriétaire du compte, vous pouvez affecter des options d'accès à votre compte à un utilisateur lorsque vous et l'utilisateur êtes tous deux membres du compte, sans considération du rôle. Les sections ci-après décrivent les trois types d'accès pouvant être accordés à un utilisateur invité.
{:shortdesc}

## Services avec l'offre Identity and Access activée 

Vous pouvez affecter une règle de service unique lorsque vous invitez un nouvel utilisateur. Une fois que l'utilisateur a accepté l'invitation, vous pouvez ajouter des règles de service supplémentaires. 

1. Dans l'écran **Inviter des utilisateurs**, développez la section **Services avec l'offre Identity and Access activée**. 
2. Sélectionnez **Tous les services avec l'offre Identity and Access activée** ou un service individuel. **Remarque **: si vous sélectionnez l'option **Accorder automatiquement des droits d'accès lorsque de nouveaux services sont ajoutés**, vous n'êtes pas invité à désélectionner chaque nouveau service {{site.data.keyword.Bluemix_notm}} pour cet utilisateur lorsque des services sont ajoutés ultérieurement. 
3. Sélectionnez **Toutes les régions en cours** ou une région spécifique. 
4. Sélectionnez **Toutes les instances de service en cours** ou une instance de service spécifique. 
5. Sélectionnez un rôle afin de définir la portée de l'accès pour la règle. 
6. Facultatif : sélectionnez **Ajouter un rôle** afin de spécifier un rôle supplémentaire pour la règle. 

Voir [Règles de gestion de l'identité et de l'accès et rôles](/docs/iam/users_roles.html#iamusermanpol) pour des informations plus spécifiques sur la définition de règles de service.

## Accès Cloud Foundry

Tous les utilisateurs possèdent le rôle d'organisation Auditeur par défaut. Vous pouvez mettre à jour ce rôle vers le rôle Responsable de la facturation ou Responsable de l'organisation, ou ne définir aucun rôle d'organisation une fois que l'utilisateur a accepté l'invitation. Au cours du processus d'invitation, vous pouvez ajouter plusieurs rôles d'espace (un à la fois). 

1. Dans l'écran **Inviter des utilisateurs**, développez la section **Accès Cloud Foundry**. 
2. Sélectionnez une organisation à laquelle ajouter l'utilisateur. 
3. Sélectionnez **Toutes les régions en cours** ou une région spécifique. 
4. Sélectionnez **Tous les espaces en cours** ou un espace spécifique. 
5. Sélectionnez un rôle afin de définir la portée de l'accès. 
6. Facultatif : sélectionnez **Ajouter un rôle** afin de spécifier un rôle supplémentaire pour la règle. 

Voir [Rôles Cloud Foundry](/docs/iam/users_roles.html#cfroles) pour des informations plus spécifiques sur ces rôles. 

## Accès à l'infrastructure

Si vous disposez du droit approprié, l'option permettant d'accorder des droits d'infrastructure apparaît. Les droits réels accordés sont limités automatiquement au sous-ensemble de droits dont vous disposez. Pour plus d'informations sur les droits et les actions que l'utilisateur peut effectuer avec chaque droit, voir [Droits relatifs à l'infrastructure](/docs/iam/users_roles.html#infrapermissions).

1. Dans l'écran **Inviter des utilisateurs**, développez la section **Accès Infrastructure**.  
2. Sélectionnez un droit afin de définir la portée de l'accès. 

Pour des informations sur la configuration de l'accès pour les utilisateurs après leur ajout à votre compte, voir [Gestion des comptes utilisateur et des accès](/docs/iam/iamusermanage.html).
