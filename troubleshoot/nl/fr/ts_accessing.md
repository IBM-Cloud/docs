---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Traitement des incidents liés à l'accès à {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Des problèmes d'ordre général relatifs à l'accès à {{site.data.keyword.Bluemix}} peuvent survenir par exemple lors de l'ouverture d'une session {{site.data.keyword.Bluemix_notm}} ou si un compte est bloqué à l'état en attente. Dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}

## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : mot de passe incorrect
{: #ts_logintobm}

Vous devez disposer d'un mot de passe valide associé à votre IBMid pour pouvoir vous connecter à la console {{site.data.keyword.Bluemix_notm}}.

Vous devez disposer d'un mot de passe valide associé à votre IBMid ou à votre ID SoftLayer pour pouvoir vous connecter via le [portail client](https://control.softlayer.com).

Lorsque vous tentez de vous connecter à {{site.data.keyword.Bluemix_notm}}, le message d'erreur suivant s'affiche :
{: tsSymptoms} 

`Le mot de passe que vous avez entré est incorrect.`

L'IBMid et le mot de passe que vous avez utilisés pour vous connecter à {{site.data.keyword.Bluemix_notm}} ne sont pas valides.
{: tsCauses} 
 
Utilisez l'une des solutions suivantes :
{: tsResolve}
 * Entrez le mot de passe correct. Pour vérifier si l'IBMid et le mot de passe sont valides, accédez à la page My IBM profile, cliquez sur **Log in** et entrez votre IBMid et votre mot de passe sur la page Log in.  
 * Si vous avez oublié votre mot de passe, cliquez sur **Forgot your password** pour le réinitialiser. Revenez ensuite à la [console Bluemix](https://console.{DomainName}) ou au [portail client](https://control.softlayer.com) et reconnectez-vous. 
 * Si vous avez oublié votre IBMid ou que les problèmes avec votre mot de passe persistent, prenez contact avec le service Worldwide IBM Registration Helpdesk pour obtenir de l'aide. 
 * Pour obtenir un IBMid et un mot de passe valides, accédez à la page My IBM profile, puis cliquez sur **Register**.

  
**Remarque :** Si vous êtes sur la page Sign in to IBM et que le processus de connexion est interrompu pour une raison quelconque (réinitialisation de votre mot de passe, par exemple), revenez à la [console Bluemix](https://console.{DomainName}) ou au [portail client](https://control.softlayer.com) et relancez le processus de connexion. 
 

## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : données d'identification incorrectes
{: #ts_login_invalid_credentials}

Lorsque vous vous connectez à l'aide de votre IBMid, le message suivant s'affiche :
{: tsSymptoms}

`Données d'identification incorrectes. Si vous possédez un IBMid associé à votre compte, connectez-vous ici` 

* Vous êtes passé à l'utilisation d'un IBMid, mais vous avez tenté de vous connecter via le [portail client](https://control.softlayer.com) à l'aide de votre nom d'utilisateur et de votre mot mot de passe SoftLayer précédents.
{: tsCauses}

* Vous avez tenté de vous connecter via le [portail client](https://control.softlayer.com), mais vous avez entré votre IBMid et le mot de passe correspondant dans les zones Username et Password.  

Cliquez sur **log in here** dans le message ou accédez à la section IBMid Account Login et cliquez sur **Log in with IBMid**.
{: tsResolve}

N'utilisez pas les zones **Username** et **Password** que vous avez utilisées avec votre ID SoftLayer précédent. 


## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : IBMid ou adresse électronique non reconnus
{: #ts_softlayer_username}

Lorsque vous vous connectez à la console {{site.data.keyword.Bluemix_notm}}, le message suivant s'affiche :
{: tsSymptoms} 

`Nous ne reconnaissons pas cet IBMid ou cette adresse électronique. `

Vous avez tenté de vous connecter à la console {{site.data.keyword.Bluemix_notm}} avec un IBMid qui n'est pas valide. Par exemple, vous n'avez pas entré une adresse électronique qualifiée complète pour l'IBMid ou vous avez tenté d'utiliser un nom d'utilisateur et un mot de passe SoftLayer.
{: tsCauses}
 
Vous devez disposer d'un IBMid et d'un mot de passe valides pour pouvoir vous connecter à {{site.data.keyword.Bluemix_notm}}.

 * Prenez soin d'entrer une adresse électronique qualifiée complète pour l'IBMid.
 {: tsResolve}
 * Si vous êtes un utilisateur SoftLayer disposant d'un ID SoftLayer, vous devez passer à l'authentification par IBMid dans le portail client dans chaque compte auquel vous avez accès pour pouvoir vous connecter via l'authentification par IBMid. Pour plus d'informations, voir [Passage à l'IBMid](/docs/admin/softlayerlink.html#ibmid_switch).


## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : l'IBMid n'est associé à aucun compte IBM Cloud
{: #ts_login_noswitch}

Lorsque vous vous connectez à l'aide de votre IBMid, le message suivant s'affiche :
{: tsSymptoms}

`Vous accédez à cette page car votre authentification a abouti. Toutefois, cet IBMid n'est associé à aucun compte Bluemix. Si vous pensez
que ce message ne s'affiche pas à bon escient, prenez contact avec votre propriétaire de compte ou votre utilisateur principal.`

Vous vous êtes connecté à partir du [portail client](https://control.softlayer.com) à l'aide d'un IBMid valide, mais vous n'êtes pas passé à l'authentification via IBMid dans SoftLayer.
{: tsCauses} 
 
Effectuez les vérifications suivantes :
{: tsResolve}
 * Prenez contact avec votre utilisateur principal ou votre administrateur de compte pour vérifier que vous pouvez passer à l'authentification via IBMid.

 * Prenez soin d'exécuter l'étape de passage à l'IBMid dans votre compte Softlayer. Voir [Passage à l'IBMid](/docs/admin/softlayerlink.html#ibmid_switch).
 * Prenez soin d'exécuter les actions décrites dans le courrier électronique **Associate your SoftLayer user with an IBMid**. Recherchez le courrier électronique dans votre boîte de réception et dans votre dossier de courrier indésirable. Pour que le courrier électronique vous soit de nouveau envoyé, par exemple, s'il a expiré, accédez à la page Edit User Profile dans le portail de contrôle et cliquez sur **Resend Email**. Vous pouvez aussi contacter le [support {{site.data.keyword.Bluemix_notm}} ![](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}.

**Remarque :** Si vous avez créé votre IBMid directement avec IBMid, deux courriers électroniques vous sont envoyés, l'un par le service d'enregistrement IBMid et l'autre par Softlayer. Prenez soin d'exécuter les actions décrites dans ces deux courriers électroniques. 

Selon la configuration de votre compte, certaines des options de connexion suivantes peuvent s'appliquer à votre cas : 
 * Les utilisateurs SoftLayer associés à un ID SoftLayer doivent se connecter via le [portail client](https://control.softlayer.com).
 * Les utilisateurs SoftLayer disposant d'un IBMid et possédant ou non un compte Bluemix lié peuvent se connecter via le [portail client](https://control.softlayer.com) afin d'ouvrir le portail client SoftLayer ou via la [console Bluemix](https://console.{DomainName}) afin d'ouvrir le tableau de bord Infrastructure.  


## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : l'IBMid n'est associé à aucun compte {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Lorsque vous vous connectez à {{site.data.keyword.Bluemix_notm}}, le message suivant s'affiche :
{: tsSymptoms} 
 
`Vous accédez à cette page car votre authentification a abouti. Toutefois, cet IBMid n'est associé à aucun compte {{site.data.keyword.Bluemix_notm}}.`

Vous vous êtes connecté à partir de la [console Bluemix](https://console.{DomainName}) à l'aide d'un IBMid valide, mais vous ne possédez pas encore de compte {{site.data.keyword.Bluemix_notm}}.
{: tsCauses} 

Pour créer un compte {{site.data.keyword.Bluemix_notm}}, suivez le processus d'inscription.
{: tsResolve}

Selon la configuration de votre compte, certaines des options de connexion suivantes peuvent s'appliquer à votre cas : 
 * Les utilisateurs Bluemix ne possédant pas de compte SoftLayer lié doivent se connecter via la console Bluemix.
 * Les utilisateurs Bluemix possédant un compte SoftLayer lié peuvent se connecter via la [console Bluemix](https://console.{DomainName}) ou le [portail client](https://control.softlayer.com).
 

## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : la console ne s'ouvre pas
{: #ts_login_stalls}

Lorsque vous vous connectez à l'aide de votre IBMid, un message indiquant que la connexion a abouti s'affiche, mais vous ne revenez pas à la [console Bluemix](https://console.{DomainName}) ou au [portail client](https://control.softlayer.com).
{: tsSymptoms}

Utilisez l'une des solutions suivantes :
{: tsResolve}
 * Fermez votre navigateur, effacez le contenu du cache et supprimez les cookies, puis essayez à nouveau de vous connecter.
 * Prenez soin de vous connecter à partir de la [console Bluemix](https://console.{DomainName}) ou du [portail client](https://control.softlayer.com) et non directement depuis le service d'authentification via IBMid. 
 
 
## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : échec de la connexion IBMid
{: #ts_login_ibmid}

Lorsque vous vous connectez à {{site.data.keyword.Bluemix_notm}}, l'authentification via IBMid n'aboutit pas.
{: tsSymptoms}

Il s'agit peut-être d'un problème lié au service d'authentification via IBMid.
{: tsCauses}

Vérifiez le statut du service sur le site [IBM BlueID ![](../icons/launch-glyph.svg "External link icon")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window}, puis renouvelez l'opération.
{: tsResolve}


## Impossible de se connecter à {{site.data.keyword.Bluemix_notm}} : compte en attente
{: #ts_accntpding}

Si votre compte est en attente, vous ne pouvez pas vous connecter à {{site.data.keyword.Bluemix_notm}}.
 
Après avoir procédé à votre enregistrement pour un compte d'essai {{site.data.keyword.Bluemix_notm}}, il est possible que vous ne puissiez pas vous connecter à {{site.data.keyword.Bluemix_notm}}. Le message suivant s'affiche :
{: tsSymptoms}

<code>Votre compte est en attente. La confirmation par courrier électronique peut prendre jusqu'à 24 heures ; vérifiez également votre dossier de courrier indésirable. Si vous ne recevez pas votre confirmation par courrier électronique, contactez le <a href="http://ibm.biz/bluemixsupport.com" target="_blank">support Bluemix</a>.</code>

Après avoir procédé à votre inscription pour un compte d'essai {{site.data.keyword.Bluemix_notm}}, vous recevez une confirmation par courrier électronique. Cliquez
sur le lien que contient ce courrier électronique pour compléter le processus d'enregistrement.
{: tsCauses} 

La confirmation par courrier électronique est envoyée à l'adresse de courrier électronique que vous avez indiquée. Vérifiez votre boîte de réception et votre dossier de courrier indésirable. Si vous ne recevez pas de confirmation par courrier électronique, prenez contact avec le [support {{site.data.keyword.Bluemix_notm}} ![](../icons/launch-glyph.svg "")](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}


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

Vous ne pouvez pas utiliser le basculement automatique entre les régions {{site.data.keyword.Bluemix_notm}}. Toutefois, vous pouvez utiliser un fournisseur DNS qui prend en charge le basculement entre plusieurs adresses IP comme solution de contournement.

Lorsqu'une région {{site.data.keyword.Bluemix_notm}} n'est plus disponible, les applications qui sont exécutées dans cette région ne sont plus
disponibles non plus, même si les mêmes applications s'exécutent dans une autre région {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} ne fournit pas encore le basculement automatique d'une région vers une autre.
{: tsCauses}
 
Vous pouvez utiliser un fournisseur DNS qui prend en charge le basculement intelligent entre plusieurs adresses IP et configurer manuellement vos paramètres DNS pour activer le basculement automatique entre des régions {{site.data.keyword.Bluemix_notm}}. NSONE, Akamai et Dyn sont des fournisseurs DNS qui proposent cette capacité.
{: tsResolve}

Lorsque vous configurez vos paramètres DNS, vous devez spécifier les adresses IP publiques des régions {{site.data.keyword.Bluemix_notm}} dans lesquelles vos applications s'exécutent. Pour obtenir l'adresse IP publique d'une région {{site.data.keyword.Bluemix_notm}}, utilisez la commande `nslookup`. Par exemple, vous pouvez entrer la commande suivante dans une fenêtre de ligne de commande :
```
nslookup stage1.mybluemix.net
```

## Impossible d'ajouter des utilisateurs à une organisation
{: #ts_adduser}

Vous pouvez inviter plusieurs utilisateurs dans la même organisation. Vous pouvez inviter des utilisateurs dans votre organisation uniquement si vous êtes propriétaire de compte ou si vous êtes à la fois responsable et membre de l'organisation.
 
Le lien **Inviter un nouvel utilisateur** n'apparaît pas dans votre section **Gérer les organisations**.
{: tsSymptoms}

Seuls les utilisateurs {{site.data.keyword.Bluemix_notm}} suivants peuvent inviter des utilisateurs dans une organisation :
{: tsCauses}
  * Le propriétaire de compte de l'organisation
  * Les responsables de l'organisation qui sont également membres, et non collaborateurs, de l'organisation
  
Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez être membre ou collaborateur d'une organisation.

<dl><dt>Collaborateur</dt>
<dd>Vous êtes collaborateur d'une organisation si vous possédez déjà un compte
{{site.data.keyword.Bluemix_notm}} et que quelqu'un vous invite dans l'organisation.</dd>
<dt>Membre</dt>
<dd>Vous êtes membre d'une organisation si vous ne possédez pas de compte {{site.data.keyword.Bluemix_notm}}, mais que quelqu'un vous invite dans l'organisation et que vous vous inscrivez à {{site.data.keyword.Bluemix_notm}} depuis l'invitation.</dd>
</dl>

Vous ne pouvez pas inviter d'utilisateurs dans votre organisation si vous êtes un collaborateur de l'organisation, même si vous avez été désigné comme responsable de l'organisation.

**Remarque :** tous les responsables de l'organisation, y compris ceux qui sont des collaborateurs d'une organisation, peuvent ajouter, modifier et supprimer des utilisateurs qui se trouvent déjà dans l'organisation.

Si vous ne pouvez pas inviter d'utilisateurs dans votre organisation et que vous avez besoin d'un autre rôle pour ce faire, prenez contact avec le responsable de l'organisation afin qu'il change votre rôle. Pour identifier le responsable de votre organisation, procédez comme suit :
{: tsResolve}

  1. Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}. Dans la barre de menu, cliquez sur l'élément de menu **Compte**, puis sur **Gérer les organisations**.
  2. Sélectionnez votre organisation et affichez les informations relatives au responsable dans l'onglet **Utilisateurs**.  
  
Si vous ne parvenez pas à inviter des utilisateurs car vous êtes collaborateur et non membre, vous devez supprimer votre compte {{site.data.keyword.Bluemix_notm}} précédent, puis être invité à rejoindre le compte en tant que membre de l'organisation. Pour supprimer votre compte précédent et rejoindre le compte en tant que membre, procédez comme suit : 

  1. Contactez le [support {{site.data.keyword.Bluemix_notm}} ![](../icons/launch-glyph.svg " ")](http://ibm.biz/bluemixsupport){: new_window} pour ouvrir un ticket de demande de service et demander la suppression de votre compte. Si vous voulez sauvegarder des données associées à votre ancien compte et les déplacer dans votre nouveau
compte, incluez ces informations dans votre courrier électronique. 
  2. Une fois votre compte supprimé, demandez à un utilisateur disposant du rôle de responsable de l'organisation de vous inviter dans l'organisation en
tant que responsable de l'organisation. Ensuite, inscrivez-vous à
{{site.data.keyword.Bluemix_notm}} à partir de l'invitation. 

## L'enregistrement d'utilisateurs par lots n'est pas pris en charge
{: #ts_batchregistration}

Lorsque vous enregistrez des utilisateurs pour {{site.data.keyword.Bluemix_notm}}, vous devez enregistrer chaque utilisateur individuellement.

{{site.data.keyword.Bluemix_notm}} ne permet pas d'enregistrer plusieurs utilisateurs simultanément.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} ne prend pas en charge l'enregistrement d'utilisateurs par lots. Pour enregistrer des utilisateurs pour {{site.data.keyword.Bluemix_notm}}, vous devez enregistrer chaque utilisateur individuellement.
{: tsCauses}
 
Pour enregistrer plusieurs utilisateurs pour {{site.data.keyword.Bluemix_notm}}, vous devez effectuer les opérations suivantes pour chaque utilisateur :
{: tsResolve}

  1. Cliquez sur **Inscription** dans la console {{site.data.keyword.Bluemix_notm}}.
  2. Suivez les étapes de l'assistant.
    

## La page {{site.data.keyword.Bluemix_notm}} ne peut pas être chargée
{: #ts_err}

Lorsque vous utilisez la console {{site.data.keyword.Bluemix_notm}}, il est possible que vous ne puissiez pas charger une page {{site.data.keyword.Bluemix_notm}}. A la place, un message d'erreur BXNUI0001E ou BXNUI0016E peut s'afficher.
 
L'un des messages d'erreur suivants peut s'afficher lorsque vous utilisez la console {{site.data.keyword.Bluemix_notm}} :
{: tsSymptoms}

`BXNUI0001E: La page n'a pas été chargée car Bluemix n'a pas détecté s'il existait une session.`

`BXNUI0016E: Les applications et les services n'ont pas été extraits car une page Bluemix n'a pas été chargée.`

Effectuez une ou plusieurs des actions suivantes :
{: tsResolve}

  * Actualisez ou redémarrez votre navigateur.
  * Déconnectez-vous de {{site.data.keyword.Bluemix_notm}}, puis reconnectez-vous.
  * Utilisez le mode de navigation privée de votre navigateur. 
  * Effacez les cookies et le cache du navigateur.
  * Utilisez un navigateur différent. Pour plus d'informations sur les versions des navigateurs qui sont prises en charge par {{site.data.keyword.Bluemix_notm}}, voir [Prérequis Bluemix](/docs/overview/whatisbluemix.html#prereqs).
  * Si vous avez installé l'interface de ligne de commande cf, entrez la commande `cf apps` pour déterminer si votre app est en cours d'exécution.
