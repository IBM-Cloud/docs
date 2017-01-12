---

 

copyright:

  years: 2016
lastupdated: "2016-12-01"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Mise à niveau et unification des comptes de facturation {{site.data.keyword.Bluemix_notm}} et SoftLayer
{: #softlayerlink}

Si vous disposez d'un compte d'essai {{site.data.keyword.Bluemix_notm}} et voulez accéder au tableau de bord Infrastructure, vous devez
procéder à la mise à niveau vers un compte {{site.data.keyword.Bluemix_notm}} Paiement à la carte. Vous devez également effectuer une mise à niveau si vous voulez utiliser d'autres ressources payantes qui ne sont pas disponible dans un compte d'essai ou une fois votre compte d'essai arrivé à expiration. 

Vous pouvez unifier vos comptes de facturation {{site.data.keyword.Bluemix_notm}} et SoftLayer en les liant. Lorsque vous liez vos
comptes, vous êtes facturé via {{site.data.keyword.Bluemix_notm}} pour l'utilisation de ressources {{site.data.keyword.Bluemix_notm}} et
SoftLayer.

**Attention :** Un compte d'abonnement {{site.data.keyword.Bluemix_notm}} ne peut pas être lié à un compte SoftLayer. Pour
accéder au tableau de bord Infrastructure, vous devez créer un compte Paiement
à la carte, un second compte qui est automatiquement lié à un
compte SoftLayer. Vous recevez ensuite deux factures, une pour chaque compte {{site.data.keyword.Bluemix_notm}}. Même
si vos ressources d'infrastructure sont facturées dans un compte Paiement à la
carte distinct, elles peuvent être utilisées avec les applications et les
services de votre compte d'abonnement. Ainsi, si vous activez un service Watson
dans votre compte d'abonnement, vous pouvez copier les données d'identification
du service et les ajouter à votre application Bare Metal provenant de
votre compte Paiement à la carte. {:shortdesc}

## Mise à niveau vers un compte {{site.data.keyword.Bluemix_notm}} Paiement à la carte
{: #upgradetopayg}

Lorsque vous vous connectez à {{site.data.keyword.Bluemix_notm}} avec un compte d'essai, vous ne parvenez pas à accéder au tableau de bord
Infrastructure {{site.data.keyword.Bluemix_notm}}. Si vous voulez que vos applications utilisent les ressources d'infrastructure, vous devez
procéder à la mise à niveau vers un compte Paiement à la carte.

Pour mettre à niveau votre compte d'essai vers un compte {{site.data.keyword.Bluemix_notm}} Paiement à la carte, procédez comme suit :

 1. Cliquez sur **Compte** &gt; **Facturation**.
 2. Ensuite, cliquez sur **Ajouter une carte de crédit**.
 3. Entrez les détails de facturation requis. 
 4. Lisez et acceptez les dispositions relatives au compte Paiement à la carte. 
 5. Une fois que vous avez terminé, cliquez sur **Mise à niveau**. 
 
Une fois la mise à niveau vers un compte Paiement à la carte effectuée, les options **Infrastructure** sont
répertoriées dans le **catalogue** {{site.data.keyword.Bluemix_notm}}. Si vous utilisez plus que la franchise, vous recevrez
une facture {{site.data.keyword.Bluemix_notm}} mensuelle. Celle-ci est en dollars américains (USD) et détaille le prix des ressources. 

## Unification de vos comptes {{site.data.keyword.Bluemix_notm}} et SoftLayer
{: #unifyingaccounts}

Vous pouvez unifier vos comptes {{site.data.keyword.Bluemix_notm}} et SoftLayer afin d'utiliser les ressources combinées. Si vous liez
vos comptes {{site.data.keyword.Bluemix_notm}} et Softlayer, vous ne recevrez qu'une seule facture {{site.data.keyword.Bluemix_notm}}. Si vous possédez un compte {{site.data.keyword.Bluemix_notm}}, la facturation via {{site.data.keyword.Bluemix_notm}} pour des ressources
SoftLayer est appliquée lors du nouveau cycle de facturation qui démarre après la liaison des comptes.

**Important :** tous les comptes liés dans {{site.data.keyword.Bluemix_notm}} doivent être du type Paiement à la carte. Vous pouvez
en créer un nouveau ou utiliser un compte Paiement à la carte existant. Vous pouvez aussi lier un compte d'essai existant, mais celui-ci sera transformé en
compte Paiement à la carte. Les comptes d'abonnement {{site.data.keyword.Bluemix_notm}} ne peuvent pas être liés.  

Une fois vos comptes liés :

* Vous devez utiliser vos données d'identification IBMid pour accéder à votre compte SoftLayer et à votre compte
{{site.data.keyword.Bluemix_notm}}.
* Les remises SoftLayer existantes sont appliquées à tous les prix {{site.data.keyword.Bluemix_notm}}. 
* Vous recevez une facture en dollars américains (USD).
* Vous pouvez surveiller l'utilisation de vos ressources {{site.data.keyword.BluSoftlayer}} dans l'interface utilisateur
{{site.data.keyword.Bluemix_notm}}. 

**Attention :** la liaison des comptes est irréversible. 

Si vous disposez d'un compte SoftLayer et voulez lier des comptes SoftLayer et {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

 1. Depuis le {{site.data.keyword.slportal}}, cliquez sur **Link a {{site.data.keyword.Bluemix_notm}}** Account.
 2. Lisez et acceptez les dispositions pour la liaison de comptes SoftLayer et {{site.data.keyword.Bluemix_notm}}.
 3. A l'invite, indiquez l'adresse électronique associée à votre compte {{site.data.keyword.Bluemix_notm}}. Si vous ne disposez pas d'un compte
{{site.data.keyword.Bluemix_notm}}, indiquez l'adresse électronique que vous voulez utiliser, puis suivez les instructions pour être invité dans
{{site.data.keyword.Bluemix_notm}} et créer un compte.

Vous devez être défini comme utilisateur principal dans le compte SoftLayer pour lier des comptes.

Après avoir lié vos comptes, le lien **Accéder à {{site.data.keyword.Bluemix_notm}}** est disponible dans l'en-tête
global SoftLayer. En cliquant sur ce lien, vous accédez à la page de connexion de {{site.data.keyword.Bluemix_notm}}. De plus, le lien
**SoftLayer** est désormais disponible dans l'en-tête {{site.data.keyword.Bluemix_notm}}. En cliquant sur ce lien, vous accédez à la
page d'accueil du {{site.data.keyword.slportal}} dans une nouvelle fenêtre.

Les offres d'infrastructure {{site.data.keyword.Bluemix_notm}} sont connectées à un réseau à trois niveaux qui segmente le trafic public,
privé et de gestion. Les offres d'infrastructure sur un compte {{site.data.keyword.Bluemix_notm}} de client peuvent transférer les données dans une infrastructure de ce type sur le réseau privé gratuitement. Les offres d'infrastructure, telles que les serveurs Bare Metal, les serveurs virtuels et le stockage en cloud se connectent à d'autres
applications et services figurant dans le catalogue {{site.data.keyword.Bluemix_notm}}, comme des services Watson, des conteneurs ou des contextes
d'exécution, sur le réseau public. Le transfert de données entre ces deux types d'offre est mesuré et facturé en fonction des tarifs de bande
passante de réseau public
standard.

## Invitation de membres d'équipe SoftLayer dans {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

Vous pouvez inviter vos membres d'équipe SoftLayer à rejoindre {{site.data.keyword.Bluemix_notm}} lorsque vous liez les comptes
{{site.data.keyword.Bluemix_notm}} et SoftLayer. Vous pouvez également inviter plus tard des membres d'équipe SoftLayer depuis l'interface utilisateur de
{{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Depuis l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}, vous pouvez inviter en bloc tous les membres de votre compte
SoftLayer ou sélectionner des membres individuels. Lorsque vous invitez des membres de l'équipe, vous devez les affecter au rôle de
compte {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur les différents rôles dans
{{site.data.keyword.Bluemix_notm}}, voir
[Rôles utilisateur](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Vous devez être défini comme utilisateur principal dans le compte SoftLayer pour inviter des membres d'équipe dans le compte {{site.data.keyword.Bluemix_notm}}.

Pour inviter des membres d'équipe dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

 1. Cliquez sur **Compte** &gt; **Inviter des membres d'équipe**.
 2. Cliquez sur **Ajouter** pour vous authentifier dans votre compte SoftLayer et afficher la liste des membres d'équipe de votre
compte {{site.data.keyword.BluSoftlayer}}.
 3. Sélectionnez les membres de l'équipe à ajouter et cliquez sur **Envoyer**.
 
Le membre de l'équipe reçoit un courrier électronique incluant un lien **Join the organization**. Si le membre d'équipe ne dispose
pas d'un
IBMid, il est redirigé vers une page d'enregistrement. Il peut alors soumettre des informations de base et créer son compte
{{site.data.keyword.Bluemix_notm}}.

Pour plus d'informations sur l'invitation de membres d'équipe via l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}, voir
[Invitation de membres d'équipe](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## Passage à l'IBMid
{: #ibmid_switch}

Désormais, l'authentification dans SoftLayer utilise l'IBMid afin de fournir une connexion unique pour {{site.data.keyword.Bluemix_notm}}. Si
vous possédez un compte SoftLayer, vous pouvez passez à un IBMid. Un assistant de migration vous guidera tout au long de cette opération. 
{:shortdesc}

Si vous avez commencé le passage à l'IBMid, vous pouvez l'annuler tant que vous ne l'avez pas terminé. Toutefois, vous serez à nouveau invité à passer à l'IBMid à votre prochaine connexion.

Pour passer de votre nom d'utilisateur SoftLayer existant à un IBMid, procédez comme suit :

 1. Dans le {{site.data.keyword.slportal}}, accédez à la page Edit User Profile et cliquez sur **Switch to
IBMid**.
 2. Suivez les invites de l'assistant de migration afin de créer votre IBMid. Une fois l'IBMid créé, vous ne pouvez pas changer l'ID, qui est
une adresse électronique. Vous pouvez mettre à jour l'adresse électronique associée à votre profil, mais par défaut, cette valeur est la même que celle
que vous avez définie pour votre IBMid. Une fois l'assistant terminé, un courrier électronique vous est envoyé.
 3. Lorsque vous recevez le courrier électronique, suivez le lien ou copiez l'adresse URL dans un navigateur et entrez votre code
d'enregistrement. Le code est valable pendant sept jours et ne peut être utilisé qu'une fois.  Vous ne pouvez pas le réutiliser.
 Après avoir configuré le
lien utilisateur IBMid vers SoftLayer, vous ne pouvez vous connecter à votre compte qu'avec l'IBMid.  Dans la boîte de dialogue de connexion, vous devez
cliquer sur le bouton **Log in with IBMid** au lieu d'entrer votre nom d'utilisateur et votre mot de passe SoftLayer.
 
Si vous êtes un nouveau client, vous êtes invité à entrer une adresse électronique pour votre compte IBMid existant, ou à créer un compte IBMid,
lorsque vous passez au paiement de votre commande. 

### Mappage de plusieurs comptes SoftLayer à un IBMid
{: #map_multiple_accounts}

Vous pouvez associer un IBMid à plusieurs comptes SoftLayer en utilisant une adresse électronique IBMid existante lorsque vous configurez le
compte. Vous ne pouvez mapper qu'un seul utilisateur SoftLayer pour chaque compte à l'IBMid unique. L'IBMid doit être unique dans chaque compte SoftLayer. Toutefois,
un utilisateur disposant de l'accès à plusieurs comptes SoftLayer peut utiliser un IBMid afin d'accéder à plusieurs comptes SoftLayer.

Par exemple, un IBMid peut être mappé à un utilisateur principal dans les comptes A et B, et à un utilisateur supplémentaire dans les comptes C et D.
L'un des comptes mappés à cet IBMid est le compte par défaut.  En général, le compte par défaut est celui qui a été mappé en premier à l'IBMid. Toutefois,
vous pouvez changer le compte par défaut à l'aide d'une fonction de changement de compte dans le portail client.

Pour un utilisateur disposant d'un accès IBMid à plusieurs comptes pour lesquels l'authentification à deux facteurs est activée, un code de
vérification pour l'authentification à deux facteurs approprié par compte est requis lors de la connexion de compte et du changement de compte.

## Utilisation de services {{site.data.keyword.Bluemix_notm}} avec des actifs SoftLayer
{: #bluemix_services}

Vous pouvez utiliser sans difficulté des services {{site.data.keyword.Bluemix_notm}} publics reposant sur des API avec vos actifs
SoftLayer. Toutes les API sont
sécurisées et chiffrées de sorte que vos données sont protégées.
{:shortdesc}

Par exemple, souhaiteriez-vous ajouter des capacités cognitives de Watson à vos applications s'exécutant sur des serveurs sans système d'exploitation depuis
SoftLayer ? Vous pouvez ajouter un service tel que {{site.data.keyword.personalityinsightsshort}} pour mieux comprendre l'utilisateur de
votre application
en quatre étapes simples :

1. Recherchez le service dans le catalogue {{site.data.keyword.Bluemix_notm}}.
2. Mettez en place une instance du service en quelques clics.
3. Configurez le service pour son exécution avec le code existant en copiant les données d'identification au service et en les ajoutant à votre application.
4. Après la mise à jour de l'application, déployez sa nouvelle version dans votre infrastructure SoftLayer.

Vous pouvez dégager des enseignements *Insights and Cognitive* en appelant des API Watson
depuis vos applications dans SoftLayer pour les personnaliser davantage. Vous pouvez également utiliser les services *Data and Analytics* pour exploiter des analyses à hautes performances dans vos
applications. Vous pouvez aussi opter pour une approche DBaaS (database-as-a-service) où la gestion est laissée à {{site.data.keyword.Bluemix_notm}}.

Modernisez votre développement d'applications en utilisant des conteneurs avec des services tels que
{{site.data.keyword.activedeployshort}} et {{site.data.keyword.deliverypipeline}}. Vous pourrez ensuite utiliser le service
{{site.data.keyword.vpn_short}} pour communiquer avec SoftLayer et
connecter votre conteneur dans un réseau privé au réseau privé SoftLayer. Tous les frais d'utilisation des ressources de traitement et des services sont reflétés dans votre facture
{{site.data.keyword.Bluemix_notm}}. 

### Services {{site.data.keyword.Bluemix_notm}} reposant sur des API
Certains services {{site.data.keyword.Bluemix_notm}} ne peuvent pas être utilisés avec SoftLayer. Les services suivants peuvent être configurés pour
s'exécuter avec votre code d'application :
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**Remarque :** certains plans ne sont pas disponibles pour ces services. Seuls les plans activés pour les comptes Paiement à la
carte peuvent être utilisés avec des comptes liés. Toutefois,
vous pouvez utiliser n'importe quel plan pour l'un de ces services si vous disposez d'un compte {{site.data.keyword.Bluemix_notm}} séparé qui est facturé
à part.

## Facturation pour l'utilisation de {{site.data.keyword.Bluemix_notm}} lorsque les comptes sont liés
{: #bill_usage}

Une fois que vous avez lié vos comptes {{site.data.keyword.Bluemix_notm}} et SoftLayer, le prochain cycle de facturation sera imputé dans une
seule facture {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Votre cycle d'utilisation de {{site.data.keyword.Bluemix_notm}} est basé sur le mois calendaire et votre compte sera facturé chaque mois le jour de facturation établi pour votre contrat de crédit. Avec SoftLayer, votre cycle d'utilisation débute au moment où vous avez commencé à utiliser SoftLayer, et vous êtes donc facturé chaque mois le
même jour où vous avez ouvert votre compte SoftLayer. 

Lorsque vos comptes sont liés, votre utilisation de {{site.data.keyword.Bluemix_notm}} continue d'être mesurée pour le cycle du mois en
cours et vous
serez facturé pour cette utilisation sur une facture {{site.data.keyword.Bluemix_notm}}. A compter du premier jour du mois suivant, vos frais
{{site.data.keyword.Bluemix_notm}} et SoftLayer seront combinés sur votre facture {{site.data.keyword.Bluemix_notm}}.

Par exemple, si vous avez lié vos comptes le 16 avril, vous recevrez une facture Bluemix pour votre consommation en avril. Selon la date à
laquelle vous avez lié vos comptes, vous pouvez recevoir une facture distincte pour votre utilisation de SoftLayer. Votre utilisation en mai pour SoftLayer
et {{site.data.keyword.Bluemix_notm}} sera facturée via votre compte {{site.data.keyword.Bluemix_notm}}.

![Récapitulatif de la liaison de comptes Bluemix et SoftLayer](images/BluemixSoftLayerBill.svg)

Une fois vos factures liées, votre facture {{site.data.keyword.Bluemix_notm}} répertorie les prix de chaque ressource que vous avez
utilisée sous les en-têtes suivants :

* **Bare Metal Servers and Attached Services**
* **Virtual Servers and Attached Services**
* **Unattached Services**

Pour plus d'informations sur l'affichage de l'utilisation de {{site.data.keyword.Bluemix_notm}}, voir
[Affichage des détails de l'utilisation](https://console.ng.bluemix.net/docs/pricing/index.html#usage).

