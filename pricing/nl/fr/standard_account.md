---



copyright:

  years: 2016, 2017
lastupdated: "2017-05-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Compte standard bêta IBM {{site.data.keyword.Bluemix_notm}} 
{: #betaintro}

Le compte standard bêta {{site.data.keyword.Bluemix}} introduit
un nouveau compte gratuit, qui permet de travailler d'une nouvelle façon dans le
cloud {{site.data.keyword.Bluemix_notm}} public. Le compte standard
n'expire jamais, contrairement au compte d'essai {{site.data.keyword.Bluemix_notm}} de 30 jours. Vous pouvez continuer à
utiliser vos applications {{site.data.keyword.Bluemix_notm}}
sans vous soucier des restrictions de temps. 
{:shortdesc}

La participation au compte standard bêta s'effectue uniquement sur
invitation. Une fois que vous avez accepté l'invitation et que vous avez créé votre compte standard, vous pouvez inviter des amis et des collègues à
rejoindre ce compte bêta.  

## Présentation du compte {{site.data.keyword.Bluemix_notm}} standard
{: #standardaccount}

Vous vous demandez sans doute en quoi le compte standard diffère du
compte d'essai. Les tableaux suivants récapitulent les informations
essentielles liées au compte standard {{site.data.keyword.Bluemix_notm}}. 

|Quelles sont les nouveautés du compte standard ? |    
|-----------------|
| Le compte n'expire jamais. |
| Les applications Cloud Foundry peuvent accéder à 256 Mo de mémoire d'exécution instantanée et gratuite. |
| Vous pouvez accéder aux plans Lite gratuits pour Cloudant NoSQL DB et Internet of Things Platform, avec davantage de services à venir. |
| Vos applications passent en veille au bout de dix jours d'inactivité en termes de développement. |
| Vos instances de service sont supprimées au bout de 30 jours d'inactivité. |
{:caption="Tableau 1. Quelles sont les nouveautés du compte standard ?" caption-side="top"}

|Qu'est-ce qui ne change pas quand un compte d'essai est converti ? | 
|-----------------|
|Le compte est gratuit ; vous n'avez pas besoin de carte de crédit. |
|Les instances Lite de Cloudant NoSQL DB et d'Internet of Things Platform. Il est possible de transférer une instance Lite pour chacun de ces services vers votre nouveau compte. |
|Votre organisation, vos espaces et les paramètres d'accès des membres d'équipe associés restent les mêmes. Vous pouvez transférer une organisation vers votre nouveau compte. |
|Le niveau de support {{site.data.keyword.Bluemix_notm}} reste le même. |
{:caption="Tableau 2. Qu'est-ce qui ne change pas ?" caption-side="top"}

**Remarque :** si votre compte d'essai n'est pas converti, un message d'explication s'affiche. Votre compte d'essai comporte peut-être plusieurs organisations ou des applications qui ne peuvent pas être transférées. Effectuez l'action appropriée, puis faites une nouvelle tentative
de conversion.

Une fois inscrit à un compte standard, vous pouvez inviter des membres
d'équipe à collaborer dans votre organisation et vos espaces, afficher votre
utilisation, créer des espaces, mettre à jour votre profil de compte et gérer
votre organisation. Pour plus
d'informations, voir [Gestion de votre compte](/docs/admin/adminpublic.html#account).

## Plans Lite
{: #liteplans}
   
Les plans Lite, également disponibles dans un compte de type Paiement à
la carte, sont structurés sous forme de quota gratuit. Vous pouvez utiliser
vos projets gratuitement, sans risque de générer une facture par accident.
Le quota peut fonctionner pour une période spécifique, par exemple, un mois,
ou sur la base d'une utilisation unique. Voici quelques exemples de quotas de plans Lite :

<ul>
<li>Nombre maximal de périphériques enregistrés</li>
<li>Nombre maximal de liaisons d'application</li>
<li>Limite de stockage de données chiffrées, par exemple, 1 Go</li>
<li>Débit de mise à disposition</li>
</ul> 

Un compte standard vous permet d'utiliser n'importe quel élément du
catalogue {{site.data.keyword.Bluemix_notm}} doté d'un plan Lite. Les
plans Lite sont faciles à trouver. Par défaut, lorsque vous ouvrez le
catalogue, tous les services dotés d'un plan Lite sont affichés et identifiés par une balise Lite ![balise Lite](../icons/Lite.svg). Sélectionnez un service pour afficher les détails du quota du plan Lite associé.

## Qu'est-ce qui est disponible dans le compte standard ?
{: #whatsavailable}

Dans un compte standard, les applications Cloud Foundry peuvent accéder, au maximum, à 256 Mo de mémoire d'exécution instantanée. Si vous
dépassez votre quota alloué, vous pouvez arrêter certaines applications afin de
libérer de la mémoire d'exécution. 

Dans le compte standard bêta, les services suivants offrent un plan Lite :

<ul>
<li>Cloudant NoSQL DB</li>
<li>Internet of Things Platform</li>
</ul>

Nous étendrons cette liste, donc restez à l'écoute !

Quand vos limites de quota sont atteintes, votre application est arrêtée
ou votre service est désactivé. Si le plan Lite spécifie que le quota est
fourni sur une base mensuelle, l'utilisation des ressources est réinitialisée
le premier de chaque mois et vous pouvez alors réutiliser le service. Lorsque
vous approchez ou atteignez une limite de quota, vous recevez un courrier électronique de notification. 

Vous pouvez mettre à disposition 1 instance par plan Lite. 

**Remarque** : ces limitations s'appliquent uniquement au compte standard. Vous pouvez à tout moment procéder à une mise à niveau
vers un compte de facturation d'abonnement ou de type Paiement à la carte. Vous
ne payez que ce que vous utilisez au-delà des franchises. Pour plus d'informations sur les comptes Paiement à la carte et Abonnement,
voir [Types de compte](/docs/pricing/index.html#pay-accounts).

## Activité de développement
{: #devactivity}

Pour aider les utilisateurs de compte standard à mieux gérer leurs ressources, nous avons intégré diverses fonctionnalités efficaces basées sur l'activité de développement et l'utilisation :

 * Vos applications passent en veille après 10 jours d'inactivité en
termes de développement. Cela facilite l'utilisation d'une nouvelle
application, car vous évitez ainsi  d'atteindre la limite du quota de mémoire
de 256 Mo. Pour activer vos applications, commencez à les réutiliser dans la
ligne de commande Cloud Foundry ou dans la console {{site.data.keyword.Bluemix_notm}}. 
 
 Voici la liste de toutes les commandes qui permettent d'activer votre
application :
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **Remarque** : si votre application est déjà activée pour SSH, les commandes `cf enable-ssh` et `cf disable-ssh` ne permettent pas d'activer l'application. 

 * Vos services de plan Lite sont supprimés en l'absence d'activité pendant 30 jours. Il n'est ensuite plus nécessaire de supprimer les instances
inactives lorsque vous souhaitez créer une nouvelle instance. Actuellement,
seul le service Internet of Things Platform utilise cette fonctionnalité. 
 
 Conservez votre instance Lite Internet of Things Platform active en vous
connectant au tableau de bord de l'instance du service Internet of Things
Platform.
 
## Participation au compte standard bêta
{: #betainvitation}

Si vous êtes sélectionné pour participer à l'évaluation de la version bêta, une invitation est envoyée à l'adresse électronique associée à votre compte d'essai {{site.data.keyword.Bluemix_notm}}. Lorsque vous
recevez l'invitation, suivez les instructions indiquées dans le courrier
électronique pour vous enregistrer dans le compte standard. 

Vous souhaitez participer à l'offre du compte standard bêta ? Parlez-en à
vos amis et collègues. S'ils ont été invités à rejoindre ce compte bêta et qu'ils ont créé leur compte standard, ils peuvent vous inviter à leur tour. 
