---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Journalisation dans Bluemix
{: #logging_bmx_ov}

Les fonctions de journalisation de {{site.data.keyword.Bluemix_notm}} sont intégrées à la plateforme et la collecte des données est activée automatiquement pour les ressources de cloud. Par défaut, {{site.data.keyword.Bluemix_notm}} collecte et affiche des journaux pour vos applications, vos contextes d'exécution d'application et vos contexte d'exécution de traitement dans lesquels ces applications s'exécutent. {:shortdesc}

Vous pouvez utiliser les fonctions de journalisation de {{site.data.keyword.Bluemix_notm}} pour comprendre le comportement de la plateforme cloud et les ressources qui s'exécutent sur cette dernière. Aucune instrumentation spéciale n'est requise pour collecter les journaux de sortie standard et d'erreur standard. Par exemple, vous pouvez utiliser des journaux pour fournir une analyse rétrospective relative à une application, détecter des problèmes dans votre service, identifier des vulnérabilités, dépanner vos déploiements d'application et le comportement d'exécution, détecter des problèmes dans l'infrastructure où vos applications s'exécutent, suivre votre application parmi les composants de la plateforme cloud et détecter des modèles que vous pouvez utiliser pour préempter des actions qui pourraient affecter votre accord sur les niveaux de service. 

Lorsque vous exécutez vos applications dans le cloud, il se peut que vous ne puissiez pas ouvrir une session SSH ou FTP dans l'infrastructure sur laquelle vos applications s'exécutent pour accéder aux journaux, par exemple, si votre application s'exécute dans Cloud Foundry. En revanche, vous pouvez exécuter votre application dans {{site.data.keyword.containershort}}, autre contexte d'exécution de traitement disponible dans {{site.data.keyword.Bluemix_notm}} et sur lequel vous pouvez ouvrir une session SSH pour accéder aux journaux. Indépendamment du contexte d'exécution de traitement, l'accès aux journaux est primordial et {{site.data.keyword.Bluemix_notm}} vous offre une expérience commune pour la visualisation et l'analyse des journaux dans votre plateforme cloud. 

{{site.data.keyword.Bluemix_notm}} enregistre les données de journal générées par la plateforme Cloud Foundry et par les applications Cloud Foundry. Ces journaux comportent les erreurs, les avertissements et les messages d'information qui sont générés pour votre application. Pour plus d'informations sur la journalisation dans Cloud Foundry, voir [Journalisation des applications Cloud Foundry dans Bluemix](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} enregistre les données de journal générées par {{site.data.keyword.containershort}}. Pour plus d'informations sur la journalisation dans {{site.data.keyword.containershort}}, voir [Journalisation dans {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


Grâce à la fonctionnalité de journalisation offerte par {{site.data.keyword.Bluemix_notm}}, vous pouvez :

* Visualiser vos ressources de cloud et connaître leurs niveaux de performances et savoir si elles fonctionnent correctement. 
* Définir des tendances destinées à vous aider à identifier les scénarios qui nécessitent une action de votre part.
* Définir des traces de données pour une application, par exemple, que vous pouvez utiliser pour le contrôle.
* Réduire le temps et l'effort qui sont requis pour identifier un problème dans une application et la résoudre.  
* Surveiller le déploiement de vos applications dans la plateforme cloud.
* Détecter qu'un service ou une application est arrêté ou en panne.
* Suivre l'exécution d'application et le flux de données. 
* Identifier des vulnérabilités sur votre application. 
* Détecter des problèmes dans l'infrastructure.
* Détecter des problèmes dans le contexte d'exécution d'application. 
