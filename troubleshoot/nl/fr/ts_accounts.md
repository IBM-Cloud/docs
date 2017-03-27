---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Traitement des incidents liés à la gestion des comptes
{: #managingaccounts}

Vous pouvez rencontrer des problèmes d'ordre général lorsque vous gérez votre compte, par exemple, différentes applications partagent le même nom de domaine ou les administrateurs ne peuvent pas afficher toutes les organisations. Dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}


## Le compte est inactif
{: #ts_accnt_inactive}

Vous ne pouvez pas créer d'application dans {{site.data.keyword.Bluemix_notm}} si votre compte est inactif. Vous devez prendre contact avec l'équipe de support pour résoudre ce problème.

Lorsque vous tentez de créer une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms} 

`BXNUI0096E: L'application n'a pas été créée. Votre compte est inactif car il a été annulé ou suspendu.`

Le statut de votre compte {{site.data.keyword.Bluemix_notm}} devient inactif lorsque le compte est annulé ou suspendu.
{: tsCauses}


Pour réactiver votre compte, contactez le [support {{site.data.keyword.Bluemix_notm}} ![](../icons/launch-glyph.svg "")](http://ibm.biz/bluemixsupport.com){: new_window}. Indiquez les informations suivantes dans votre courrier électronique :
{: tsResolve}

  * L'IBMid que vous utilisez pour vous connecter à {{site.data.keyword.Bluemix_notm}}.
  * Le nom de l'organisation dans laquelle votre application est créée. Ces informations peuvent être utiles à l'équipe de support pour déterminer si l'appartenance ou les rôles appropriés vous ont été affectés dans votre organisation.


## Aucun espace n'est associé à votre organisation en cours
{: #ts_no_space}

Vous ne pouvez pas créer d'application si aucun espace n'est associé à votre organisation en cours.

Lorsque vous tentez de créer une application dans {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms} 

`BXNUI0097E: Pour qu'une application puisse être ajoutée, un espace au moins doit être associé à votre organisation et à votre région. Dans le tableau de bord, cliquez sur Créer un espace. Une fois l'espace créé, essayez à nouveau.`

Les applications dans {{site.data.keyword.Bluemix_notm}} doivent être créées dans un espace sous votre organisation.
{: tsCauses} 

Pour créer un espace, appliquez l'une des méthodes suivantes : 
{: tsResolve}
 
  * Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, sélectionnez l'organisation dans laquelle créer l'espace, puis cliquez sur **Créer un espace**.
  * Dans l'interface de ligne de commande cf, tapez `cf create-space <nom_espace> -o <nom_organisation>`.

  
## Les applications partagent le même nom de domaine
{: #ts_domain_diff}

Il se peut que plusieurs applications partagent la même adresse URL dans {{site.data.keyword.Bluemix_notm}}.

Ce problème peut se produire lorsque vous affectez la même route d'adresse URL à plusieurs applications dans un espace.
{: tsCauses}

Par exemple, vous envoyez par commande push l'application myApp1 dans {{site.data.keyword.Bluemix_notm}} et définissez le nom de domaine "mynewapp.stage1.mybluemix.net". Puis, vous envoyez par commande push une autre application myApp2 dans le même espace et affectez "mynewapp.mybluemix.net" à l'une de ses routes d'URL. La route est désormais mappée aux deux applications.

Il s'agit du comportement de {{site.data.keyword.Bluemix_notm}} pris en charge ; il permet d'obtenir un temps d'indisponibilité nul pour la mise à niveau de votre application. Pour plus d'informations, voir [Using Blue-Green Deployment to Reduce Downtime and Risk ![](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}.
{: tsResolve}
  

## Les administrateurs ne peuvent pas visualiser toutes les organisations à l'aide de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}
{: #ts_ui_org}

En tant qu'administrateur, lorsque vous utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, vous ne pouvez pas afficher chaque organisation à des fins d'administration. Vous pouvez afficher et administrer uniquement les organisations auxquelles vous appartenez.

En tant qu'administrateur, vous ne pouvez pas afficher toutes les organisations à l'aide de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Il s'agit d'une limitation de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Vous pouvez utiliser des commandes telles que `cf orgs`, `cf create-org` et `cf delete-org` à partir de l'interface de ligne de commande cf pour gérer toutes les organisations. Pour obtenir une liste complète des commandes cf, entrez `cf help`.
{: tsResolve}
	
## La carte de crédit ne peut pas être ajoutée
{: #ts_addcc}

Vous ne pouvez pas soumettre vos informations de carte de crédit pour convertir votre compte d'essai en compte Paiement à la carte.

Le bouton **Soumettre** sur la page Ajout d'une carte de crédit est désactivé.
{: tsSymptoms}

Ce problème survient lorsque vos informations ne sont pas remplies correctement sur la page Ajout d'une carte de crédit.
{: tsCauses}


Procédez comme suit :
{: tsResolve}

  1. Sur la page Ajout d'une carte de crédit, remplissez toutes les zones requises qui se trouvent dans les sections relatives aux coordonnées, à l'adresse de contact et à l'adresse de facturation.
  2. Sélectionnez **I have read and agree to IBM's Terms and Conditions**, puis cliquez sur **Soumettre**. La section **Select a payment method** s'affiche.
  3. Entrez votre numéro de carte de crédit, la date d'expiration de votre carte et le code de sécurité qui se trouve sur votre carte. Cliquez sur **Soumettre**. 
