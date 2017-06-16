---



copyright:

  years: 2016, 2017
lastupdated: "2017-03-17"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Passage à l'IBMid
Désormais, l'authentification dans SoftLayer utilise un IBMid afin de fournir une connexion unique pour {{site.data.keyword.Bluemix_notm}} dans son intégralité. Les comptes SoftLayer existants sont activés pour passer à l'authentification par IBMid. Un assistant de migration vous aide à effectuer cette opération. 
{:shortdesc}

Lorsque vous entamez le processus permettant de passer à un IBMid, vous pouvez à tout moment annuler l'opération, avant la fin du processus. Cependant, à chaque fois que vous vous connecterez, un message vous invitant à passer à un IBMid s'affichera. Chaque compte SoftLayer que vous prévoyez de lier à un compte {{site.data.keyword.Bluemix_notm}} doit appartenir à un IBMid unique associé à une adresse électronique unique.

Pour passer à un IBMid sur votre compte SoftLayer existant, procédez comme suit : 
1. Connectez-vous à votre compte SoftLayer et cliquez sur **OK** lorsque vous êtes invité à passer à un IBMid. 

   Si vous êtes un utilisateur principal et qu'aucun message vous invitant à passer à un IBMid n'apparaît dans {{site.data.keyword.slportal}}, [prenez contact avec le support IBM](/docs/support/index.html#contacting-support) pour de l'aide. 
  
   Si vous vous êtes déjà connecté et avez cliqué sur **Plus tard** dans l'invite, mais voulez passer à l'authentification par IBMid dans la session en cours, accédez à la page d'édition du profil utilisateur et cliquez sur **Passer à l'IBMid**.

2. Suivez les invites de l'assistant pour créer votre IBMid. 

   Entrez une adresse électronique qui n'est associée à aucun IBMid. Elle servira de nom d'utilisateur pour le nouvel IBMid et le code d'enregistrement sera envoyé à cette adresse une fois l'IBMid créé. Vous pouvez mettre l'adresse électronique à jour ultérieurement mais vous ne pouvez pas changer le nom d'utilisateur. 

3. Une fois que vous avez reçu votre code d'enregistrement, cliquez sur le lien dans le courrier électronique ou copiez l'adresse URL dans un navigateur et entrez votre code d'enregistrement. 

   Le code d'enregistrement est valable pendant sept jours et vous ne pouvez l'utiliser qu'une fois. 
  
4. Après avoir soumis votre code d'enregistrement, utilisez votre IBMid pour vous connecter à {{site.data.keyword.slportal}}.

   A l'invite de connexion au compte, accédez à la section **IBMid Account Login** et cliquez sur **Log in with IBMid**. N'utilisez pas les zones **Username** et **Password** que vous avez précédemment utilisées avec votre ID SoftLayer.

Si vous êtes un nouveau client, vous êtes invité à entrer votre IBMid ou à en créer un lorsque vous êtes sur le point de payer votre commande.  
  * Pour utiliser un IBMid existant, entrez le nom d'utilisateur ou l'adresse électronique de l'IBMid, si unique (c'est-à-dire si l'adresse électronique ou le nom d'utilisateur n'est pas partagé par plusieurs IBMid). 
  
  * Pour créer un IBMid, entrez une adresse électronique qui n'est utilisée par aucun IBMid. Elle servira de nom d'utilisateur pour l'IBMid et votre code d'enregistrement sera envoyé à cette adresse une fois l'IBMid créé. Vous pouvez mettre l'adresse électronique à jour ultérieurement mais vous ne pouvez pas changer le nom d'utilisateur.  
  
Afin de résoudre les problèmes liés à la connexion avec votre IBMid, voir [Traitement des incidents liés à l'accès à Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).

## Activation des comptes utilisateur pour l'authentification par IBMid 
{: #link_accounts_resellers}

Dans certains cas, un revendeur ou un distributeur doit permettre au compte d'utiliser l'authentification par IBMid pour qu'un utilisateur puisse passer à l'IBMid. 

  * L'authentification par IBMid doit être activée pour chaque compte utilisateur existant que vous voulez lier à un compte Bluemix. Ensuite, chaque utilisateur doit suivre le processus permettant de passer à un IBMid à l'aide de l'assistant de migration, comme décrit dans la section précédente. Prenez contact avec le [support IBM](/docs/support/index.html#contacting-support) pour qu'il autorise un compte SoftLayer existant à utiliser l'authentification par IBMid.  
  
  * Pour garantir que les nouveaux comptes utilisateur sont créés avec un IBMid, définissez l'attribut `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` sur le compte de l'utilisateur principal immédiat. Prenez contact avec le [support IBM](/docs/support/index.html#contacting-support) ou avec votre fournisseur afin de définir l'attribut pour vos comptes.   

## Liaison de comptes utilisateur IBMid 
{: #link_user_accounts}

Une fois que vos comptes utilisateur sont passés à l'authentification par IBMid, les revendeurs et les distributeurs peuvent lier les comptes SoftLayer et {{site.data.keyword.Bluemix_notm}} pour combiner des ressources d'infrastructure et de plateforme. 

**Remarque** :
  * L'utilisateur principal du compte qui est lié doit posséder un IBMid. 
  * Chaque compte utilisateur que vous liez à un compte {{site.data.keyword.Bluemix_notm}} doit être détenu par un IBMid unique associé à une adresse électronique unique. Même si un IBMid unique peut être associé à plusieurs comptes SoftLayer, vous devez changer l'utilisateur principal afin qu'il corresponde à un IBMid unique pour chaque compte. Prenez contact avec le [support IBM SoftLayer ![Icône de lien externe](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} pour changer l'utilisateur principal d'un compte SoftLayer. 
  * Lorsque vous ajoutez de nouveaux utilisateurs à un compte lié, vous devez les ajouter au compte SoftLayer et au compte {{site.data.keyword.Bluemix_notm}} pour qu'ils aient accès à toutes les fonctionnalités de la console unifiée.  
  
Pour lier chaque compte à un compte {{site.data.keyword.Bluemix_notm}}, procédez comme suit :
1. Pour établir la liaison à un compte {{site.data.keyword.Bluemix_notm}} existant ou pour créer un nouveau compte, connectez-vous à votre compte SoftLayer en tant qu'utilisateur principal et cliquez sur le lien {{site.data.keyword.Bluemix_notm}}. 

   L'IBMid correspondant à l'utilisateur principal du compte SoftLayer doit être le propriétaire du compte {{site.data.keyword.Bluemix_notm}} auquel vous établissez la liaison.  
   
2. Suivez les invites de l'assistant en ajoutant les utilisateurs du compte SoftLayer au compte {{site.data.keyword.Bluemix_notm}}.
3. Après avoir lié le compte, indiquez à l'utilisateur final de chaque compte qu'il doit migrer vers l'IBMid en suivant la procédure décrite dans la section précédente. 

**Recommandation** : migrez uniquement les comptes d'utilisateur final vers l'IBMid. Ne migrez pas les comptes de marque, qui sont les comptes parent des comptes utilisateur final et qui ne contiennent aucune ressource. Les utilisateurs des comptes de marque qui migrent vers l'IBMid perdent la possibilité de se connecter à Brand Agent Portal (BAP).  
  
