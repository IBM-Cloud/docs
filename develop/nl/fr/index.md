---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

# Développement d'applications 
{: #develop-apps-IDS}

*Dernière mise à jour : 07 décembre 2015*  

Vous pouvez développer des applications dans un environnement de développement intégré (IDE) ou un éditeur de texte, ou avec {{site.data.keyword.jazzhub}}. 
{: shortdesc}

## Développement d'applications avec Bluemix DevOps Services
{: #dev_ops}

Vous pouvez utiliser {{site.data.keyword.jazzhub_short}} pour développer une application, en effectuer le suivi et la planifier dans le cloud, puis la déployer dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez passer du code source à une application opérationnelle en quelques minutes.  

{{site.data.keyword.jazzhub_short}} fournit deux services : {{site.data.keyword.trackplan}} et {{site.data.keyword.deliverypipeline}}. Le service {{site.data.keyword.trackplan}} est utilisé pour la planification agile. Le service {{site.data.keyword.deliverypipeline}} automatise les générations et les déploiements. Ces services se trouvent dans le catalogue {{site.data.keyword.Bluemix_notm}}. Pour en savoir plus sur leur utilisation, voir [Initiation à Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) et [Initiation à Delivery Pipeline](../services/DeliveryPipeline/index.html#getstartwithCD). 

{{site.data.keyword.jazzhub_short}} fournit également l'hébergement Git pour le contrôle des sources et un environnement de développement intégré Web dans lequel vous pouvez éditer, gérer et déployer votre code. Dans une application, vous activez l'hébergement Git en cliquant sur le lien **AJOUTER UN REFERENTIEL GIT**, qui se trouve dans le coin supérieur droit de la page Vue d'ensemble de l'application. Ensuite, vous pouvez éditer le code de votre application dans l'environnement de développement intégré Web en cliquant sur **Editer le code**. Depuis le shell de l'environnement de développement intégré Web, vous pouvez exécuter des commandes cf avec l'assistant de contenu. Par exemple, vous pouvez obtenir la liste de toutes les commandes Cloud Foundry en entrant la commande suivante :  
```
help cfo
```
{:pre}
