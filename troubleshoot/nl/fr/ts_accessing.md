---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Traitement des incidents liés à l'accès à {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

Dernière mise à jour : 18 août 2016
{: .last-updated} 

Des problèmes d'ordre général liés à {{site.data.keyword.Bluemix}} peuvent survenir
: par exemple, un utilisateur ne parvient pas à établir une connexion dans
{{site.data.keyword.Bluemix_notm}},
un compte est bloqué à l'état en attente, etc. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples. 
{:shortdesc}

## Connexion à {{site.data.keyword.Bluemix_notm}} impossible
{: #ts_logintobm}

Vous devez disposer d'un IBMid et d'un mot de passe valides pour vous connecter à {{site.data.keyword.Bluemix_notm}}.


Lorsque vous tentez de vous connecter à {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche : 
{: tsSymptoms} 

`Le mot de passe que vous avez entré est incorrect.`


L'IBMid et le mot de passe que vous utilisez pour vous connecter à {{site.data.keyword.Bluemix_notm}} ne sont pas valides.
{: tsCauses} 
 

Pour obtenir un IBMid et un mot de passe valides, accédez à la page My IBM profile et procédez comme suit :
{: tsResolve}
  * Si vous disposez déjà d'un IBMid et que vous voulez vérifier si l'ID et le mot de passe sont valides, cliquez sur **Sign in** et entrez votre IBMid et votre mot de passe sur la page Sign in. Si vous avez oublié votre mot de passe, cliquez sur **Forgot your password** sur la page Sign in pour le réinitialiser. Si vous avez oublié votre IBMid ou que les problèmes avec votre mot de passe persistent, prenez contact avec le service Worldwide IBM
Registration Helpdesk pour obtenir de l'aide. 
  * Si vous ne disposez pas d'un IBMid, cliquez sur **Register** pour enregistrer un IBMid et un mot de passe. 
  
**Remarque :** pour les employés IBM, l'IBMid peut être différent de l'ID de connexion à l'intranet. 



<!-- begin STAGING ONLY --> 

## Problème d'accès à un site Web externe
{: #ts_bmlinkid}

Vous ne pouvez pas vous connecter à {{site.data.keyword.Bluemix_notm}} à l'aide de votre ID intranet IBM sauf si vous liez celui-ci à votre IBMid.


Après que vous avez sélectionné **Sign in with your intranet ID** sur la page Sign in de {{site.data.keyword.Bluemix_notm}}, il se peut que le message d'erreur suivant s'affiche :
{: tsSymptoms} 

`Problem Accessing External Website`



Ce problème survient lorsque vous vous connectez à {{site.data.keyword.Bluemix_notm}} à l'aide d'un ID intranet IBM qui n'est pas lié à un IBMid. Votre IBMid est l'ID que vous utilisez pour vous connecter à www.ibm.com.
{: tsCauses}


En tant qu'employé IBM, avant de pouvoir vous connecter à {{site.data.keyword.Bluemix_notm}} à l'aide de votre ID intranet IBM, vous devez lier celui-ci à votre IBMid externe. Pour lier les deux ID, procédez comme suit :
{: tsResolve} 

  1. Sur la page [Central Sign-on](https://w3-03.sso.ibm.com/tools/cso/index.jsp){: new_window}, cliquez sur **My Sign-ons**.
  2. Sur la page My Sign-ons, cliquez sur **Link IDs** et entrez votre IBMid et votre mot de passe sur la page Sign in de {{site.data.keyword.Bluemix_notm}}. Après cela, votre ID intranet et votre IBMid sont automatiquement liés.
  

<!-- end STAGING ONLY -->




## Des modifications n'ont pas été sauvegardées
{: #ts_unsaved_changes}


Lorsque vous naviguez dans la page des détails de l'application, vous ne pourrez peut-être pas effectuer d'action et vous serez invité à sauvegarder vos modifications pour pouvoir continuer. 


Lorsque vous essayez de vérifier votre appli ou vos services sur la page des détails de l'application, vous obtenez toujours le message d'erreur suivant :
{: tsSymptoms} 

`Des modifications n'ont pas été sauvegardées dans la page nom_appli. Sauvegardez ou annulez les modifications.`


Lorsque vous survolez avec la souris les zones **INSTANCES** ou **QUOTA DE MEMOIRE** dans le panneau du contexte d'exécution, les valeurs changent. Ce comportement est normal. Toutefois, le message d'erreur vous invite à sauvegarder les paramètres de mémoire ou d'instance avant de quitter la page. 
{: tsCauses}


Fermez la fenêtre de message, puis cliquez sur le bouton **REINITIALISER** de votre contexte d'exécution. 
{: tsResolve} 




    
    
## Le basculement automatique entre les régions {{site.data.keyword.Bluemix_notm}} n'est pas disponible
{: #ts_failover}

Vous ne pouvez pas utiliser le basculement automatique entre les régions
{{site.data.keyword.Bluemix_notm}}. Toutefois, vous pouvez utiliser un fournisseur DNS qui prend en charge
le basculement entre plusieurs adresses IP comme solution de contournement.
 

Lorsqu'une région {{site.data.keyword.Bluemix_notm}} n'est plus disponible, les applications qui sont exécutées dans cette région ne sont plus
disponibles non plus, même si les mêmes applications s'exécutent dans une autre région {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}}
ne fournit pas encore le basculement automatique d'une région à une autre.
{: tsCauses}

 
Vous pouvez utiliser un fournisseur DNS qui prend en charge le basculement intelligent entre plusieurs adresses IP et configurer manuellement vos
paramètres DNS pour activer le basculement automatique entre des régions {{site.data.keyword.Bluemix_notm}}. NSONE, Akamai et Dyn sont des fournisseurs DNS qui proposent cette capacité.
{: tsResolve}

Lorsque vous configurez vos paramètres DNS, vous devez spécifier les adresses IP publiques des régions {{site.data.keyword.Bluemix_notm}}
dans lesquelles vos applications s'exécutent. Pour obtenir l'adresse IP publique d'une région {{site.data.keyword.Bluemix_notm}}, utilisez la
commande `nslookup`. Par exemple, vous pouvez entrer la commande suivante dans une fenêtre de ligne de commande :
```
nslookup stage1.mybluemix.net
```



## Compte en attente
{: #ts_accntpding}

Si votre compte est en attente, vous ne pouvez pas vous connecter à {{site.data.keyword.Bluemix_notm}}.

 
Après avoir procédé à votre inscription pour un compte d'essai {{site.data.keyword.Bluemix_notm}}, il est possible que vous ne puissiez pas vous connecter à {{site.data.keyword.Bluemix_notm}} et que le message suivant s'affiche :
{: tsSymptoms}

<code>Votre
compte est en attente. La confirmation par courrier électronique peut prendre jusqu'à 24 heures ; vérifiez également votre dossier de courrier indésirable. Si vous ne recevez pas votre confirmation par courrier électronique, envoyez un message au
<a href="http://ibm.biz/bluemixsupport.com" target="_blank">support Bluemix</a>.</code>


Après avoir procédé à votre inscription pour un compte d'essai {{site.data.keyword.Bluemix_notm}}, vous recevez une confirmation par courrier électronique. Cliquez
sur le lien que contient ce courrier électronique pour compléter le processus d'enregistrement.
{: tsCauses} 

La confirmation par courrier électronique est envoyée à l'adresse de courrier électronique que vous avez indiquée. Vérifiez votre boîte de réception et votre dossier de courrier indésirable. Si vous ne recevez pas de confirmation par courrier électronique, prenez contact avec le
[support {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## Impossible d'ajouter des utilisateurs à une organisation
{: #ts_adduser}

Vous pouvez inviter plusieurs utilisateurs dans la même organisation. Vous pouvez inviter des utilisateurs dans votre organisation
uniquement si vous êtes propriétaire de compte ou si vous êtes à la fois responsable et membre de l'organisation.
 

Le lien **Inviter un nouvel
utilisateur** n'apparaît pas dans votre section **Gérer les organisations**. 
{: tsSymptoms}

 

Seuls les utilisateurs
{{site.data.keyword.Bluemix_notm}} suivants peuvent inviter des utilisateurs dans
une organisation :
{: tsCauses}
  * Le propriétaire de compte de l'organisation
  * Les responsables de l'organisation qui sont également membres, et non collaborateurs, de l'organisation
  
Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez être membre ou collaborateur d'une organisation.

<dl><dt>Collaborateur</dt>
<dd>Vous êtes collaborateur d'une organisation si vous possédez déjà un compte
{{site.data.keyword.Bluemix_notm}} et que quelqu'un vous invite dans l'organisation.</dd>
<dt>Membre</dt>
<dd>Vous êtes membre d'une organisation si vous ne possédez pas de compte
{{site.data.keyword.Bluemix_notm}}, mais que quelqu'un vous invite dans l'organisation et que
vous vous inscrivez à {{site.data.keyword.Bluemix_notm}} depuis l'invitation.</dd>
</dl>


Vous ne pouvez pas inviter d'utilisateurs dans votre organisation si vous êtes un collaborateur de l'organisation, même si vous avez
été désigné comme responsable de l'organisation.

**Remarque :** tous les responsables de l'organisation, y compris ceux qui sont des collaborateurs d'une organisation, peuvent
ajouter, modifier et supprimer des
utilisateurs qui se trouvent déjà dans l'organisation.

 

Si vous ne pouvez pas inviter d'utilisateurs dans votre organisation et que vous avez besoin d'un autre rôle pour ce faire, prenez contact
avec le responsable de l'organisation afin qu'il change votre rôle. Pour identifier le responsable de votre organisation, procédez comme suit :
{: tsResolve}

  1. Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône {{site.data.keyword.avatar}} ![icône Avatar](images/account_support.svg) dans la barre de menu, puis sélectionnez **Gérer les organisations**.
  2. Sélectionnez votre organisation et affichez les informations relatives au responsable dans l'onglet **Utilisateurs**.  
  
Si
vous ne parvenez pas à inviter des utilisateurs car vous êtes collaborateur et non membre, vous devez supprimer votre compte
{{site.data.keyword.Bluemix_notm}} précédent, puis être invité à rejoindre le compte en tant
que membre de l'organisation. Pour supprimer votre compte précédent et rejoindre le compte en tant que membre, procédez comme suit : 

  1. Contactez [{{site.data.keyword.Bluemix_notm}} Support](http://ibm.biz/bluemixsupport){: new_window} pour ouvrir un ticket de demande de service et demander la suppression de votre compte. Si vous voulez sauvegarder des données associées à votre ancien compte et les déplacer dans votre nouveau
compte, incluez ces informations dans votre courrier électronique. 
  2. Une fois votre compte supprimé, demandez à un utilisateur disposant du rôle de responsable de l'organisation de vous inviter dans l'organisation en
tant que responsable de l'organisation. Ensuite, inscrivez-vous à
{{site.data.keyword.Bluemix_notm}} à partir de l'invitation. 




## L'enregistrement d'utilisateurs par lots n'est pas pris en charge
{: #ts_batchregistration}

Lorsque
vous enregistrez des utilisateurs pour {{site.data.keyword.Bluemix_notm}}, vous devez
enregistrer chaque utilisateur individuellement.
 

{{site.data.keyword.Bluemix_notm}}
ne permet pas d'enregistrer plusieurs utilisateurs simultanément.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}}
ne prend pas en charge l'enregistrement d'utilisateurs par lots. Pour enregistrer des utilisateurs pour
{{site.data.keyword.Bluemix_notm}}, vous devez enregistrer chaque utilisateur
individuellement.
{: tsCauses}
 

Pour enregistrer plusieurs utilisateurs pour
{{site.data.keyword.Bluemix_notm}}, vous devez effectuer les opérations suivantes pour chaque
utilisateur :
{: tsResolve}

  1. Cliquez sur **S'INSCRIRE** dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.
  2. Suivez les étapes de l'assistant.

    

## La page {{site.data.keyword.Bluemix_notm}} ne peut pas être chargée
{: #ts_err}

Lorsque vous utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, il est possible que vous ne puissiez pas charger une page
{{site.data.keyword.Bluemix_notm}}. A la place, un message d'erreur BXNUI0001E ou BXNUI0016E peut s'afficher.
 

Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, un des messages d'erreur suivants peut s'afficher :
{: tsSymptoms}

`BXNUI0001E: La page n'a pas été chargée car Bluemix n'a pas détecté s'il existait une session.`


`BXNUI0016E: Les applications et les services n'ont pas été extraits car une page Bluemix n'a pas été chargée.`

 

Pour remédier au problème, effectuez une ou plusieurs des actions suivantes :
{: tsResolve}

  * Actualisez ou redémarrez votre navigateur.
  * Déconnectez-vous de {{site.data.keyword.Bluemix_notm}}, puis reconnectez-vous.
  * Utilisez le mode de navigation privée de votre navigateur. 
  * Effacez les cookies et le cache du navigateur.
  * Utilisez un navigateur différent. Pour des informations sur les versions des navigateurs qui sont prises en charge par
{{site.data.keyword.Bluemix_notm}}, voir [{{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Si vous avez installé l'interface de ligne de commande cf, entrez la commande `cf apps` pour déterminer si votre
application est en cours d'exécution.
  
  
  
  
  

